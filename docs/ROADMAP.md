# Roadmap de FraterChrist.org

El proyecto avanzará mediante **ciclos de entrega pequeños**. Cada ciclo debe terminar en un resultado revisable y tener criterios explícitos de aceptación. Las etapas futuras pueden cambiar según pruebas, retroalimentación y capacidad de la comunidad.

**Estado:** Ciclo 0 — descubrimiento y validación. La aplicación aún no está implementada.

## Ciclo 0 — Descubrimiento y acuerdos

**Objetivo:** entender para quién se construye el producto y definir límites razonables antes de elegir detalles irreversibles.

**Entregables**
- Visión del producto, tipos de usuario y principales recorridos.
- Alcance del primer MVP y lista visible de ideas futuras.
- Requisitos no funcionales iniciales: privacidad, accesibilidad, seguridad y costos.
- Reglas iniciales de convivencia, reporte y moderación.
- Decisiones registradas sobre autenticación, contenido público/SEO, almacenamiento de medios y licencia.
- Issues iniciales creadas con contexto y criterios de aceptación.

**Criterios de salida**
- El equipo puede explicar qué problema resuelve el MVP y qué queda fuera.
- Los flujos de publicación, visibilidad, denuncia y moderación están descritos.
- Los riesgos abiertos tienen un siguiente paso verificable.

## Ciclo 1 — Base técnica y experiencia de contribución

**Objetivo:** preparar un entorno repetible antes de añadir funcionalidades.

**Entregables**
- Estructura de backend y frontend, con configuración por variables de entorno.
- PostgreSQL disponible para desarrollo mediante una guía de instalación o Docker Compose.
- Dependencias fijadas en versiones compatibles y con instrucciones de actualización.
- Comprobaciones automáticas para pruebas, linting y tipos en GitHub Actions.
- Convenciones de ramas, commits, pull requests, manejo de secretos y revisión de código.

**Criterios de salida**
- Una persona nueva puede seguir la documentación para iniciar el entorno.
- Las comprobaciones automáticas se ejecutan en pull requests y fallan al detectar errores.
- No se requieren credenciales personales ni secretos reales para ejecutar las pruebas básicas.

## Ciclo 2 — Cuentas y autorización

**Objetivo:** establecer la identidad y las reglas de acceso antes del contenido comunitario.

**Entregables**
- Modelo de usuario definido antes de la primera migración.
- Registro, inicio y cierre de sesión.
- Protección CSRF, cookies seguras en producción y límites contra abuso del endpoint de acceso.
- Pruebas de acceso anónimo, usuario autenticado, propietario y otros usuarios.

**Criterios de salida**
- Los datos de autenticación no exponen contraseñas ni secretos.
- Los permisos se validan en el backend y están cubiertos por pruebas.
- Las configuraciones sensibles se suministran por entorno y no se guardan en Git.

## Ciclo 3 — Feed y herramientas básicas de comunidad

**Objetivo:** tener una experiencia mínima útil, no solo una API de demostración.

**Entregables**
- Feed cronológico con paginación.
- Publicaciones de texto y respuestas directas.
- Visibilidad pública, para miembros autenticados y privada.
- Edición/borrado según permisos.
- Reporte de contenido y acciones mínimas de moderación.
- Pruebas para privacidad, paginación, relaciones y reglas de acceso.

**Criterios de salida**
- Un visitante no puede leer contenido restringido aunque consulte la API directamente.
- Las respuestas y acciones respetan los permisos de su publicación raíz.
- Los flujos esenciales tienen pruebas automáticas.

## Ciclo 4 — Imágenes y acceso a archivos

**Objetivo:** añadir imágenes sin convertir el almacenamiento en un riesgo o un costo inesperado.

**Entregables**
- Límites configurables de tamaño y formatos aceptados.
- Validación del tipo real, nombres de archivo generados y almacenamiento privado.
- Permisos verificados al servir cada archivo.
- Procedimiento de eliminación de archivos, pruebas de entradas inválidas y documentación de límites.
- Decisión documentada sobre almacenamiento local y proveedor de producción.

**Criterios de salida**
- Archivos inválidos o demasiado grandes se rechazan.
- Una URL o identificador directo no permite acceder a medios privados.
- Los límites se aplican en la aplicación y en la capa de servidor/proxy.

**Fuera del ciclo:** video público, transcodificación y distribución por CDN.

## Ciclo 5 — Interfaz web y accesibilidad

**Objetivo:** conectar los flujos completos y hacerlos utilizables en diferentes tamaños de pantalla.

**Entregables**
- Formularios y vistas del feed conectados a la API.
- Estados de carga, error, vacío y sesión expirada.
- Navegación por teclado, etiquetas accesibles, contraste y diseño adaptable.
- Pruebas de los recorridos principales desde la interfaz.
- Resolución del punto de SEO/metadata para las páginas públicas antes de cerrar la estructura del frontend.

**Criterios de salida**
- Los usuarios pueden completar los flujos sin depender de llamadas manuales a la API.
- Errores y restricciones se explican de forma comprensible.
- Se verifica la navegación esencial por teclado y en una vista móvil.

## Ciclo 6 — Beta, operación y preparación de comunidad

**Objetivo:** probar con una comunidad limitada antes de una apertura más amplia.

**Entregables**
- Despliegue inicial con HTTPS y configuración segura.
- Respaldos y una prueba documentada de restauración.
- Registros útiles para diagnosticar errores sin almacenar datos privados innecesarios.
- Proceso de reportes, moderación, soporte y comunicación de incidencias.
- Revisión de privacidad, licencias, dependencias vulnerables y límites operativos.

**Criterios de salida**
- La restauración de respaldo está probada.
- Existe una forma clara de reportar problemas y responder a contenido dañino.
- El equipo conoce los límites de la beta y cómo detener una función si falla.

## Ciclos futuros — solo después de validar necesidad

Estas funcionalidades requerirán una propuesta acotada, revisión de costo/seguridad y criterios de aceptación propios:

1. Perfiles y preferencias de usuario.
2. Video en publicaciones, con almacenamiento y tratamiento de archivos definidos.
3. Mesas de oración y estudio bíblico.
4. Salas de voz/video, previa evaluación de WebRTC o proveedor especializado.
5. Pizarras colaborativas y juegos bíblicos educativos.
6. Notificaciones y otras herramientas comunitarias.

No se establece un orden definitivo para todas las funciones futuras; la comunidad podrá priorizarlas mediante Issues y discusiones.

## Cómo se considera terminado un ciclo

- El cambio responde a una necesidad descrita.
- Cumple los criterios de aceptación de su Issue.
- Incluye pruebas acordes con el riesgo.
- La documentación refleja el comportamiento real.
- Se revisa mediante pull request antes de integrarse.
- Las limitaciones conocidas quedan escritas; no se declara lista una función que solo está diseñada.
