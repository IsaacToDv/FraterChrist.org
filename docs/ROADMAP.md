# Roadmap de FraterChrist.org

El orden representa la prioridad del producto, no fechas garantizadas. Cada etapa debe terminar en entregables verificables y pruebas acordes al riesgo.

**Estado actual:** diseño y planificación. La aplicación todavía no está implementada.

## Ciclo 0 — Definir el MVP

- Confirmar los flujos principales del feed.
- Definir autenticación, privacidad, reportes y moderación.
- Revisar qué contenido necesita ser público e indexable.
- Definir límites de archivos y requisitos de almacenamiento.
- Documentar las decisiones abiertas del stack y convertir el trabajo acordado en Issues.

**Salida:** alcance y criterios de aceptación revisables, riesgos identificados y siguiente paso claro para cada decisión pendiente.

## Ciclo 1 — Base técnica

- Preparar la estructura backend/frontend y configuración por entorno.
- Configurar PostgreSQL y documentar el inicio local.
- Añadir pruebas automatizadas, linting y GitHub Actions.
- Documentar ramas, pull requests y gestión de secretos.

**Salida:** una persona colaboradora puede levantar el entorno y ejecutar las comprobaciones básicas siguiendo la documentación.

## Ciclo 2 — Feed: hilos, fotos y videos

- Feed cronológico con paginación.
- Publicaciones de texto y respuestas.
- Carga de fotos/videos con límites, validación y almacenamiento privado.
- Visibilidad comprobada en el backend.
- Reportes y herramientas iniciales de moderación.

**Salida:** las operaciones respetan los permisos, los archivos inválidos se rechazan y los flujos críticos cuentan con pruebas.

## Ciclo 3 — Perfil

- Definir campos y opciones de privacidad.
- Mostrar publicaciones respetando los permisos del feed.
- Probar acceso y edición de perfil.

**Salida:** los datos privados no quedan accesibles mediante consultas directas a la API.

## Ciclo 4 — Mesas

### Mesa de oración
- Diseñar la hoja de peticiones y su ciclo de vida.
- Definir visibilidad, edición, borrado y audiencia de cada petición.

### Mesa de estudio bíblico
- Diseñar el espacio para pasajes, reflexiones y aportes de los participantes.
- Definir cómo organizar y moderar las contribuciones.

**Salida:** las reglas de privacidad y moderación quedan documentadas y probadas antes de abrir mesas comunitarias.

## Ciclo 5 — Prototipo LiveKit

Antes de implementar las salas completas, validar la integración de audio/video con un prototipo pequeño.

- Integrar en React los paquetes livekit-client y @livekit/components-react.
- Crear en Django un endpoint autenticado para emitir tokens de LiveKit con permisos limitados.
- Usar livekit-api desde el backend cuando sea necesario gestionar las salas.
- Probar dos o más participantes, entrada autorizada, micrófono/cámara, desconexión y reconexión.
- Comparar LiveKit Cloud con autohospedado en costo, operación, privacidad y límites.

**Salida:** dos participantes pueden conectarse con credenciales emitidas por el backend; no se expone el secreto; los permisos y los costos aproximados están documentados.

## Ciclo 6 — Salas temáticas

Reutilizar la capa común de conexión LiveKit y desarrollar las experiencias de FraterChrist por separado.

### Juego bíblico
- Herramientas para crear partidas educativas y responder preguntas.
- Validación de respuestas, reglas, permisos del anfitrión y resultados desde el backend.
- Evaluar canales de datos LiveKit solo para eventos en tiempo real que lo necesiten.

### Oración
- Interfaz minimalista.
- Controles y estado de micrófono claros para el modo silencio.
- Hoja de peticiones con privacidad explícita y acciones de moderación.

### Sala libre
- Videollamada y pizarra compartida.
- Definir sincronización, permisos de edición e historial persistente.
- Evaluar canales de datos para eventos efímeros y backend para datos que deban conservarse.

**Salida:** cada modalidad tiene pruebas de permisos, controles comprensibles, mecanismos de reporte y una definición clara de qué datos se guardan.

## Cierre de etapa

- Cumplir criterios de aceptación de las Issues.
- Añadir pruebas para los riesgos relevantes.
- Revisar mediante pull request.
- Actualizar la documentación para reflejar lo que realmente funciona.
- Registrar limitaciones conocidas y costos operativos.

No se deben desplegar salas abiertas hasta probar la integración, los permisos, la moderación y la operación de LiveKit.
