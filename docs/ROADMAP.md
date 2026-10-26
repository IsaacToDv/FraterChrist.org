# Roadmap de FraterChrist.org

El producto se desarrollará en etapas. El orden expresa prioridades, no fechas garantizadas. Cada etapa debe cerrar con un resultado comprobable y una revisión de seguridad, calidad y alcance.

**Estado actual:** planificación y validación del MVP. La aplicación todavía no está implementada.

## Ciclo 0 — Definir el MVP

**Objetivo:** confirmar el alcance de la primera entrega y las decisiones que afectan a la arquitectura.

- Definir los flujos principales del feed: crear, leer, responder, editar y eliminar publicaciones.
- Definir autenticación y niveles de visibilidad.
- Establecer reglas iniciales de reporte y moderación.
- Decidir si las publicaciones públicas deben indexarse en buscadores.
- Definir límites iniciales para imágenes y videos, almacenamiento y costos.
- Registrar decisiones técnicas y convertir el trabajo validado en Issues pequeñas.

**Criterios de salida**
- El alcance del MVP y las funciones fuera de alcance están documentados.
- Los flujos y permisos principales pueden revisarse antes de implementar.
- Los riesgos abiertos tienen un siguiente paso concreto.

## Ciclo 1 — Base técnica

**Objetivo:** dejar un entorno reproducible y listo para contribuciones.

- Preparar la estructura backend/frontend y configuración por variables de entorno.
- Configurar PostgreSQL y documentar el arranque local.
- Incorporar pruebas, linting y comprobaciones automáticas con GitHub Actions.
- Definir convenciones de ramas, pull requests, dependencias y manejo de secretos.

**Criterios de salida**
- Una persona nueva puede seguir las instrucciones para iniciar el proyecto.
- Las comprobaciones automatizadas se ejecutan en los pull requests.
- No hacen falta credenciales personales para ejecutar las pruebas básicas.

## Ciclo 2 — Feed: hilos, fotos y videos

**Objetivo:** construir la primera experiencia comunitaria.

- Feed cronológico con paginación.
- Publicaciones de texto y respuestas.
- Publicaciones con fotos y videos, sujetas a la validación del manejo de archivos.
- Permisos comprobados en el backend.
- Reporte de contenido y acciones básicas de moderación.
- Pruebas de acceso, visibilidad, paginación y archivos.

**Criterios de salida**
- Las personas solo pueden acceder al contenido que sus permisos permiten.
- Las publicaciones y respuestas respetan las reglas de visibilidad.
- Las cargas inválidas o demasiado grandes se rechazan.
- Los flujos esenciales tienen pruebas automatizadas.

## Ciclo 3 — Perfil

**Objetivo:** permitir que cada persona tenga una presencia reconocible en la comunidad.

- Definir campos y opciones de privacidad.
- Mostrar publicaciones del perfil respetando los permisos del feed.
- Añadir pruebas para acceso, edición y visibilidad.

**Criterios de salida**
- La información privada no se expone por consultas directas a la API.
- La interfaz comunica con claridad qué información es pública.

## Ciclo 4 — Mesas de oración y estudio bíblico

**Objetivo:** añadir espacios organizados por propósito comunitario.

- Definir cómo se crean, encuentran y moderan las mesas.
- Mesa de oración con peticiones y controles de privacidad adecuados.
- Mesa de estudio bíblico con contenido organizado para estudiar y compartir reflexiones.
- Validar las reglas de participación, reporte y visibilidad antes de abrir espacios públicos.

**Criterios de salida**
- Las reglas de acceso y moderación están documentadas y probadas.
- Las personas comprenden quién puede ver sus aportes.

## Ciclo 5 — Salas temáticas y comunicación en tiempo real

**Objetivo:** evaluar e implementar salas de videollamada cuya interfaz se adapte a la actividad.

**Tipos de sala previstos**
- **Juego bíblico:** interfaz para crear y jugar actividades educativas basadas en la Biblia.
- **Oración:** interfaz minimalista, modo silencio y hoja de peticiones.
- **Sala libre:** videollamada y pizarra colaborativa.

Antes de implementar se debe comparar una solución de videollamada gestionada con una arquitectura propia basada en WebRTC, considerando señalización, TURN, moderación, privacidad, accesibilidad, límites y costo. La pizarra y el sistema de juegos tendrán criterios de alcance separados.

**Criterios de salida**
- La opción elegida tiene un costo y unos límites operativos conocidos.
- Los permisos de sala, controles de participantes y mecanismos de reporte están definidos.
- La experiencia básica se prueba con una cantidad limitada de participantes antes de ampliar su disponibilidad.

## Condiciones para cerrar una etapa

- Cumple los criterios de aceptación de sus Issues.
- Incluye pruebas acordes al riesgo.
- La documentación refleja el comportamiento real.
- Se revisa mediante pull request.
- Las limitaciones conocidas quedan registradas.

Las etapas pueden dividirse en entregas menores. No se deben comenzar funciones posteriores solo porque estén descritas aquí: primero se valida la etapa actual y se revisa la retroalimentación.
