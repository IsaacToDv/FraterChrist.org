# Arquitectura y viabilidad técnica

**Estado:** propuesta para revisión. No describe una aplicación ya implementada.

## 1. Criterios de diseño

1. **Empezar simple:** un monolito modular antes que microservicios.
2. **Privacidad en el servidor:** la interfaz no decide por sí sola quién puede leer contenido.
3. **Archivos separados de los datos relacionales:** PostgreSQL guarda metadatos; los binarios viven en almacenamiento de objetos.
4. **Calidad desde el comienzo:** pruebas para permisos y flujos críticos, análisis estático y CI.
5. **Decisiones reversibles:** no elegir proveedor de hosting, video en vivo o infraestructura de pago antes de validar necesidades y presupuesto.
6. **Evidencia antes de escalar:** medir rendimiento y costos antes de incorporar cachés, colas o servicios adicionales.

## 2. Stack recomendado para iniciar

| Capa | Elección | Motivo y condiciones |
|---|---|---|
| Lenguaje backend | Python 3.13 | Ecosistema amplio y adecuado para un proyecto colaborativo. Verificar el último parche compatible al crear el entorno. |
| Backend/API | Django 5.2 LTS + Django REST Framework 3.18.x | ORM, migraciones, autenticación, panel de administración y API en un stack conocido. La compatibilidad del DRF con Django 5.2 está documentada oficialmente. Fijar las versiones exactas al iniciar el ciclo técnico. |
| Base de datos | PostgreSQL 17 | Datos relacionales, restricciones e índices; rama mantenida y compatible con Django. Registrar la versión usada en desarrollo y pruebas. |
| Frontend | React + TypeScript + Vite | Separación clara de interfaz y API, tipos estáticos y ciclo de desarrollo rápido. Es una SPA inicial; la necesidad de SEO/SSR para publicaciones públicas debe validarse antes de cerrar su estructura. |
| API | REST versionada, contrato OpenAPI | Favorece una integración explícita entre frontend y backend y hace más comprensibles las contribuciones. Seleccionar la herramienta de esquema cuando se valide su compatibilidad con el stack. |
| Calidad backend | pytest-django y Ruff | Pruebas de lógica/permisos, formato y linting consistente. |
| Calidad frontend | TypeScript, ESLint, Vitest y pruebas de componentes | Comprobaciones de tipos, convenciones y pruebas del comportamiento esencial. |
| Automatización | GitHub Actions | Ejecutar comprobaciones en los pull requests; no publicar una versión que no pase las verificaciones. |
| Entorno local | Docker Compose | Reproducir servicios de desarrollo sin exigir una infraestructura compleja. No presupone que producción vaya a usar contenedores orquestados. |
| Medios | Disco privado local en desarrollo; almacenamiento de objetos en producción | No guardar imágenes/videos binarios en PostgreSQL ni exponer archivos privados mediante URLs públicas predecibles. El proveedor se decidirá por costo, controles de acceso y límites. |

### Compatibilidad y ciclo de soporte

La revisión de documentación oficial realizada el **25 de octubre de 2026** confirma que Django REST Framework 3.18.x admite Django 5.2 y que Django 5.2 es una rama LTS con soporte extendido previsto hasta abril de 2028. Esta combinación es una base conservadora para iniciar; se debe verificar el último parche antes de crear el entorno.

Django 6.2 LTS aparece en la hoja de ruta oficial para abril de 2027. Si la implementación comienza después de su publicación, comparar esa versión y su compatibilidad con DRF antes de fijar las dependencias. No actualizar por número de versión sin ejecutar la suite de pruebas.

Fuentes oficiales:
- [Versiones y soporte de Django](https://www.djangoproject.com/download/)
- [Compatibilidad y notas de Django REST Framework](https://www.django-rest-framework.org/community/release-notes/)
- [Política de versiones de PostgreSQL](https://www.postgresql.org/support/versioning/)
- [Guía oficial de Vite](https://vite.dev/guide/)
- [React: construir una app desde cero](https://react.dev/learn/build-a-react-app-from-scratch)

## 3. Arquitectura lógica

~~~mermaid
flowchart LR
    Browser[Browser] --> Web[React + TypeScript]
    Web -->|HTTPS / JSON| API[Django REST Framework]
    API --> Accounts[Accounts]
    API --> Feed[Feed and replies]
    API --> Moderation[Reports and moderation]
    API --> Media[Media access control]
    Accounts --> DB[(PostgreSQL)]
    Feed --> DB
    Moderation --> DB
    Media --> DB
    Media --> Store[(Private object storage)]
~~~

Los módulos son límites de código dentro de una aplicación, no servicios independientes. Al inicio pueden compartir el mismo despliegue backend y la misma base de datos.

## 4. Decisiones técnicas

### Autenticación y sesiones

**Propuesta inicial:** usar autenticación basada en sesión/cookies de Django, protección CSRF y cookies HttpOnly/Secure en producción. Preferir servir frontend y API bajo el mismo origen mediante proxy o rutas como /api, para reducir complejidad de CORS y cookies de terceros. No almacenar tokens de sesión en localStorage.

Esta decisión se confirmará mediante un prototipo que cubra inicio/cierre de sesión, CSRF, cookies, despliegue local y permisos. Si el proyecto incorpora clientes móviles u otras integraciones, evaluar la estrategia entonces.

### Publicaciones y permisos

- La API debe comprobar permisos en cada operación de lectura, creación, modificación y borrado.
- Los niveles de visibilidad iniciales propuestos son public, members y private.
- Las respuestas deben heredar la política de la publicación raíz; una ruta alternativa no debe permitir saltarse esa regla.
- Incluir reportes y herramientas básicas de moderación antes de una beta comunitaria abierta.

### Imágenes y videos

La subida de archivos es una superficie de riesgo. Antes de habilitar imágenes, documentar límites de tamaño, tipos permitidos, comprobación del contenido real (no confiar solo en la cabecera Content-Type), nombres generados por la aplicación, permisos de lectura y ubicación no ejecutable/aislada. Aplicar los límites tanto en la aplicación como en el proxy o servidor web.

- Primero: imágenes con límites y acceso validado.
- Después: video, si la comunidad lo necesita y se puede operar de forma responsable.
- Antes de video: validar cuotas, consumo de ancho de banda, almacenamiento, eliminación, moderación y necesidad de miniaturas/transcodificación.

Referencia: [OWASP File Upload Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/File_Upload_Cheat_Sheet.html) y [seguridad de Django](https://docs.djangoproject.com/en/5.2/topics/security/).

### Funciones en tiempo real

Chat, voz, videollamadas, pizarras y salas compartidas quedan fuera del primer MVP. Antes de construirlas, preparar una decisión de arquitectura que compare soluciones gestionadas frente a WebRTC, señalización, TURN, moderación, escalabilidad y costos. No añadir Redis, Celery ni microservicios solo por anticipación.

### Indexación y páginas públicas

Vite entrega una SPA como punto de partida, pero puede no resolver por sí solo todas las necesidades de SEO y vistas previas para publicaciones públicas. En el ciclo de descubrimiento se debe decidir si el contenido público necesita indexación por buscadores y tarjetas enriquecidas al compartir. Si es requisito del producto, comparar renderizado del lado del servidor o generación estática antes de desarrollar la navegación completa.

## 5. No añadir por defecto

No formar parte de la base inicial salvo que una necesidad real lo requiera:

- Microservicios o Kubernetes.
- Redis y colas de tareas.
- Recomendaciones algorítmicas.
- Almacenamiento o transcodificación de video propia.
- Analítica invasiva o seguimiento innecesario.
- Servicios de pago sin evaluar primero opciones gratuitas/abiertas, privacidad y costos de salida.

## 6. Decisiones pendientes antes de implementar

1. ¿Qué páginas y publicaciones serán visibles sin sesión y necesitan indexación?
2. ¿Qué datos mínimos requiere el registro y qué política de conservación/eliminación se aplicará?
3. ¿Qué reglas de convivencia, reporte, apelación y moderación necesita la primera beta?
4. ¿Qué límites iniciales tendrán las imágenes y qué proveedor de almacenamiento permite cubrirlos sin costo sorpresa?
5. ¿Dónde se desplegará la primera beta y cómo se harán respaldos y restauraciones?
6. ¿Qué requisitos legales y de privacidad corresponden a los territorios y edades de las personas usuarias?

Cada decisión importante se anotará en un registro breve: contexto, opciones, decisión, consecuencias y fecha. Resolver estas preguntas por etapas evita presentar una propuesta como arquitectura ya validada en producción.
