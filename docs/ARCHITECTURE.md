# Arquitectura y viabilidad técnica

**Estado:** propuesta técnica para revisión. La aplicación todavía no está implementada y el proveedor de LiveKit sigue por decidir.

## 1. Enfoque

- Empezar con un monolito modular, no microservicios.
- Mantener la lógica de producto y los permisos en el backend de FraterChrist.
- Usar LiveKit para la infraestructura de audio/video en tiempo real, sin reinventar transporte WebRTC.
- Construir en React las interfaces que hacen que cada sala tenga un propósito distinto.
- Persistir en PostgreSQL el contenido y estado que deba sobrevivir a una sesión.
- No añadir infraestructura de alto costo antes de validar uso, seguridad y presupuesto.

## 2. Stack propuesto

| Capa | Tecnología | Responsabilidad |
|---|---|---|
| Backend/API | Python, Django y Django REST Framework | Autenticación, publicaciones, permisos, mesas, salas y reglas de negocio. |
| Base de datos | PostgreSQL | Cuentas, publicaciones, relaciones, membresías, peticiones y estado persistente. |
| Frontend | React y TypeScript | Feed, perfiles, mesas y experiencias temáticas. |
| SDK de navegador | livekit-client | Conectar el navegador a una sala, administrar participantes y publicar/recibir audio y video. |
| Componentes React | @livekit/components-react y estilos opcionales @livekit/components-styles | Primitivas para conexión/estado de sala y controles reutilizables; el diseño visual final seguirá siendo propio. |
| SDK del servidor | livekit-api para Python | Generar tokens de acceso y utilizar las APIs de salas/participantes desde el backend. |
| Servicio de medios | LiveKit Cloud o servidor LiveKit autohospedado | Señalización, conexión de participantes y transporte de medios en tiempo real. La opción final requiere comparar costo y operación. |
| Calidad | Pruebas backend/frontend, linting y GitHub Actions | Detectar errores, validar permisos y revisar cambios. |
| Entorno local | Docker Compose si ayuda a reproducir el entorno | Levantar los servicios de desarrollo con instrucciones repetibles. |

Paquetes y documentación oficiales:
- [LiveKit JavaScript/TypeScript SDK](https://github.com/livekit/client-sdk-js)
- [LiveKit React quickstart](https://docs.livekit.io/transport/sdk-platforms/react/)
- [Paquete Python livekit-api](https://docs.livekit.io/reference/python/livekit/api/)
- [APIs de salas](https://docs.livekit.io/reference/other/roomservice-api/)
- [Tokens y permisos](https://docs.livekit.io/frontends/reference/tokens-grants/)

Las dependencias exactas se fijarán en el ciclo de implementación después de revisar versiones estables y compatibilidad entre paquetes. Esta tabla describe una propuesta, no paquetes ya instalados.

## 3. Vista general de componentes

~~~mermaid
flowchart TB
    User[Usuario] --> UI[Interfaz React + TypeScript]
    UI -->|HTTPS / JSON| API[Django REST Framework]
    API --> Auth[Cuenta y permisos]
    API --> Feed[Feed y publicaciones]
    API --> Groups[Mesas y salas FraterChrist]
    Auth --> DB[(PostgreSQL)]
    Feed --> DB
    Groups --> DB
    API -->|Token restringido| UI
    API -->|livekit-api: tokens y Room Service| LK[LiveKit Cloud o servidor propio]
    UI <-->|livekit-client: audio / video / eventos en tiempo real| LK
    UI --> Themes[UI temática de la sala]
    Themes --> Game[Juego bíblico]
    Themes --> Prayer[Petición de oración / modo silencio]
    Themes --> Board[Pizarra libre]
    Game --> API
    Prayer --> API
    Board --> API
~~~

LiveKit y FraterChrist tienen responsabilidades diferentes:

- **LiveKit** transporta audio/video, gestiona la conexión de participantes y expone APIs para administrar salas.
- **Django** decide quién puede crear, encontrar y entrar a una sala y qué acciones tiene permitidas.
- **React** implementa la interfaz, la navegación y el diseño específico para cada modalidad.
- **PostgreSQL** conserva las entidades y los datos que deban seguir existiendo al terminar la llamada.

## 4. Flujo de entrada a una sala

1. El usuario elige una sala y el tipo de experiencia.
2. El cliente envía una solicitud autenticada al backend.
3. Django verifica que la sala exista, que el usuario pueda entrar y qué capacidades se le conceden.
4. El backend genera un token de acceso LiveKit firmado en el servidor, con identidad opaca y permisos limitados a la sala adecuada.
5. El cliente recibe únicamente la URL del servidor LiveKit y el token individual, y conecta el SDK.
6. React presenta los controles y módulos de la sala; al salir, la app limpia el estado local y registra las acciones de producto necesarias.

El secreto de la API de LiveKit y cualquier credencial de servidor deben permanecer en variables de entorno protegidas del backend. No se deben incluir en el bundle del frontend, documentación pública, logs ni repositorio.

LiveKit registra los nombres/identidades de salas y participantes en logs/telemetría. Usar identificadores internos no sensibles —por ejemplo, UUIDs—, no correos, nombres reales ni otra información personal. La API de FraterChrist debe comprobar los permisos antes de entregar un token; ocultar un botón en React no es autorización.

## 5. Salas temáticas: qué aporta cada capa

### Base compartida

Todas las modalidades reutilizarán el flujo de acceso a la sala, el estado de la conexión, la lista de participantes, los controles de micrófono/cámara, la salida y los mecanismos de reporte. LiveKit ofrece la conectividad y componentes de base; FraterChrist decide el producto y el aspecto visual.

### Juego bíblico

La interfaz propia permitirá crear y participar en actividades educativas. FraterChrist tendrá que definir el modelo de juego, preguntas, respuestas, validación, puntajes y permisos de anfitrión. LiveKit podrá transportar audio/video y, si el prototipo lo justifica, eventos de baja latencia mediante sus canales de datos. Las respuestas y resultados oficiales deben ser validados por el backend, no aceptados ciegamente desde el navegador.

### Oración

La vista será deliberadamente minimalista. El modo silencio se implementará como una experiencia clara de controles de micrófono y estado de participación; no debe fingir que una persona está silenciada cuando su pista de audio sigue publicada. La hoja de peticiones y sus reglas de visibilidad serán funciones de FraterChrist respaldadas por el backend y la base de datos.

Las peticiones de oración pueden incluir información sensible. Antes de habilitarlas se deben decidir visibilidad por defecto, audiencia, edición, borrado, conservación y reporte.

### Sala libre y pizarra

LiveKit facilitará la videollamada. La pizarra será una funcionalidad separada de la interfaz: habrá que decidir cómo sincronizar trazos, cómo autorizarlos y si se guardarán para continuar luego. Los eventos efímeros pueden probarse con canales de datos de LiveKit; para historial persistente, el backend deberá validar y guardar el estado.

## 6. Decisiones a validar antes de implementar salas

1. **LiveKit Cloud frente a self-hosting.** Comparar límites, costo estimado, región, mantenimiento, actualizaciones y necesidad de observabilidad antes de una beta.
2. **Prototipo técnico.** Conectar dos navegadores con token emitido por Django, comprobar permisos, micrófono/cámara, reconexión y salida.
3. **Permisos y moderación.** Definir anfitrión, entrada, expulsión, bloqueo, reportes y tratamiento de participantes desconectados.
4. **Datos y privacidad.** Definir qué se guarda de las mesas, juegos, peticiones y pizarras, quién lo puede ver y cuánto tiempo se conserva.
5. **Costo y abuso.** Establecer duración, tamaño máximo de salas, límites de creación y controles contra uso automatizado.
6. **Accesibilidad.** Probar teclado, subtítulos cuando proceda, controles visibles y alternativas para personas que no puedan usar cámara o micrófono.

No se deben publicar salas comunitarias abiertas antes de validar estos requisitos.

## 7. Seguridad de archivos y publicaciones

El feed de fotos/videos requiere límites de tamaño, validación del contenido real (no confiar solo en la cabecera Content-Type), nombres generados por la aplicación, almacenamiento privado y comprobaciones de acceso en servidor. Los binarios no se guardarán en PostgreSQL; la base conservará sus referencias y metadatos.

Referencia: [OWASP File Upload Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/File_Upload_Cheat_Sheet.html).

## 8. Complejidad que no se añade todavía

No incorporar microservicios, Kubernetes, Redis, colas, infraestructura de video propia, transcodificación ni una plataforma de juegos independiente por anticipado. LiveKit se evaluará como un servicio separado de medios; el resto de la aplicación se mantendrá modular hasta que el uso y las mediciones justifiquen crecer.

## 9. Criterio de viabilidad

La arquitectura se considerará suficientemente validada para la siguiente etapa cuando exista un prototipo pequeño que conecte dos participantes, emita tokens desde el backend, aplique permisos de entrada, y documente costo aproximado y operación de LiveKit Cloud o de la alternativa autohospedada. Después se podrá construir la interfaz temática sobre esa base.
