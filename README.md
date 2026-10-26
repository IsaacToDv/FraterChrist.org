<h1 align="center">FraterChrist.org</h1>

<p align="center">
  <strong>Una comunidad cristiana abierta, construida con fe, respeto y colaboración.</strong><br>
  Un espacio digital para compartir, aprender, servir y crear herramientas que edifiquen a la comunidad.
</p>

<p align="center">
  <a href="LICENSE"><img alt="Licencia GPL-3.0" src="https://img.shields.io/badge/licencia-GPL--3.0-6F42C1?style=flat-square&logo=gnu&logoColor=white"></a>
  <img alt="Etapa del proyecto" src="https://img.shields.io/badge/etapa-dise%C3%B1o%20y%20validaci%C3%B3n-8B72BE?style=flat-square">
  <img alt="Colaboración abierta" src="https://img.shields.io/badge/contribuciones-bienvenidas-2E8B57?style=flat-square&logo=github">
</p>

<p align="center"><em>«Id por todo el mundo y predicad el evangelio a toda criatura» — Marcos 16:15</em></p>

<p align="center">
  <a href="#visión">Visión</a> ·
  <a href="#primer-objetivo">Primer objetivo</a> ·
  <a href="docs/ROADMAP.md">Roadmap</a> ·
  <a href="docs/ARCHITECTURE.md">Arquitectura y stack</a> ·
  <a href="#comunidad">Comunidad</a> ·
  <a href="CONTRIBUTING.md">Contribuir</a>
</p>

---

## Visión

FraterChrist.org es el **repositorio abierto de la iniciativa comunitaria** FraterChrist. La meta es construir por etapas una plataforma cristiana en la que las personas puedan compartir publicaciones, conversar con respeto, estudiar la Biblia, organizar espacios de oración y participar en experiencias de aprendizaje.

La comunidad y el software se construirán de forma colaborativa. Las decisiones técnicas priorizarán **seguridad, privacidad, accesibilidad, mantenibilidad y costos sostenibles**, evitando complejidad que todavía no resuelva una necesidad real.

> **Estado actual:** estamos en diseño y validación. Este repositorio aún no contiene una aplicación funcional. El stack y el roadmap son propuestas iniciales que se revisarán antes de implementar cada etapa.

### Primer objetivo

Comenzar con una base pequeña que pueda probarse, revisarse y ampliarse sin rehacer la arquitectura:

- Cuentas y autenticación.
- Feed cronológico con publicaciones de texto y respuestas.
- Controles de visibilidad aplicados desde el backend.
- Herramientas iniciales para reportar contenido y moderar la comunidad.
- Interfaz web adaptable y accesible.

Las **imágenes** se incorporarán después de definir y probar el manejo seguro de archivos. La carga de **video** y las experiencias en tiempo real se evaluarán en etapas posteriores por sus requisitos de almacenamiento, procesamiento, moderación y costo.

## Stack propuesto

<p align="center">
  <a href="https://www.python.org/"><img alt="Python" src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white"></a>
  <a href="https://www.djangoproject.com/"><img alt="Django" src="https://img.shields.io/badge/Django-092E20?style=flat-square&logo=django&logoColor=white"></a>
  <a href="https://www.django-rest-framework.org/"><img alt="Django REST Framework" src="https://img.shields.io/badge/Django%20REST%20Framework-A30000?style=flat-square&logo=django&logoColor=white"></a>
  <a href="https://www.postgresql.org/"><img alt="PostgreSQL" src="https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white"></a>
  <a href="https://react.dev/"><img alt="React" src="https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB"></a>
  <a href="https://www.typescriptlang.org/"><img alt="TypeScript" src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white"></a>
  <a href="https://vite.dev/"><img alt="Vite" src="https://img.shields.io/badge/Vite-646CFF?style=flat-square&logo=vite&logoColor=white"></a>
</p>

| Capa | Propuesta inicial |
|---|---|
| Backend y API | Python, Django y Django REST Framework |
| Datos | PostgreSQL |
| Interfaz | React, TypeScript y Vite |
| Calidad | Pruebas automatizadas, linting y CI con GitHub Actions |
| Desarrollo local | Docker Compose cuando se establezca la estructura del proyecto |
| Archivos | Almacenamiento privado en desarrollo; proveedor compatible con objetos en producción, por decidir |

Las insignias indican la **dirección propuesta**, no tecnologías ya implementadas. La justificación y los puntos que todavía deben verificarse están en [Arquitectura y stack](docs/ARCHITECTURE.md).

## Roadmap por ciclos

Cada etapa tendrá un objetivo concreto y criterios de salida verificables. No avanzaremos una fase solo por calendario.

| Ciclo | Objetivo | Estado |
|---|---|---|
| 0. Descubrimiento | Alcance, usuarios, privacidad, seguridad y decisiones pendientes | En curso |
| 1. Base técnica | Estructura, entorno local, estándares y comprobaciones automáticas | Pendiente |
| 2. Cuentas y permisos | Autenticación y autorización en el servidor | Pendiente |
| 3. Feed y comunidad | Publicaciones, respuestas, visibilidad y reportes | Pendiente |
| 4. Imágenes | Carga validada, almacenamiento y permisos de acceso | Pendiente |
| 5. Experiencia web | Accesibilidad, adaptación móvil y pruebas de flujos | Pendiente |
| 6. Beta responsable | Despliegue, respaldos, monitoreo y preparación comunitaria | Pendiente |

Consulta el detalle, las entregas y los criterios de aceptación en el [roadmap completo](docs/ROADMAP.md). Perfiles avanzados, video, mesas de oración/estudio, salas en tiempo real, pizarras y juegos bíblicos son **líneas futuras**, no compromisos del primer MVP.

## Arquitectura y decisiones

El punto de partida será un **monolito modular**: una API backend, una base de datos relacional y una interfaz web. No se proponen microservicios, colas, servidores de video ni infraestructura distribuida hasta que una necesidad comprobada los justifique.

- [Arquitectura, stack y riesgos](docs/ARCHITECTURE.md)
- [Roadmap y ciclos de entrega](docs/ROADMAP.md)
- [Guía para contribuir](CONTRIBUTING.md)
- [Código de conducta](CODE_OF_CONDUCT.md)
- [Reporte de seguridad](SECURITY.md)

Las decisiones importantes se documentarán antes de cerrar la etapa correspondiente. En especial: autenticación, indexación de páginas públicas, almacenamiento de medios y futuras funciones en tiempo real.

## Comunidad

La comunidad es parte del producto. Mantendremos espacios para coordinar, aprender, resolver dudas y proponer mejoras. **Los siguientes enlaces son marcadores de posición y aún no son invitaciones activas.**

- [WhatsApp — añadir enlace de invitación](https://chat.whatsapp.com/REEMPLAZAR_CON_INVITACION)
- [Discord — añadir enlace de invitación](https://discord.gg/REEMPLAZAR_CODIGO)
- [Proponer una mejora o reportar un problema](https://github.com/IsaacToDv/FraterChrist.org/issues)

Antes de participar, lee el [Código de conducta](CODE_OF_CONDUCT.md). Se aceptan propuestas técnicas y comunitarias respetuosas; las ideas se evaluarán por su utilidad, viabilidad, seguridad y adecuación al alcance.

## Cómo colaborar

1. Revisa el [roadmap](docs/ROADMAP.md) y las [Issues abiertas](https://github.com/IsaacToDv/FraterChrist.org/issues).
2. Para un cambio grande, conversa primero sobre el problema y el alcance mediante una Issue.
3. Envía una propuesta acotada con contexto, criterios de aceptación y pruebas cuando corresponda.
4. Consulta [CONTRIBUTING.md](CONTRIBUTING.md) para el flujo de trabajo.

FraterChrist.org utiliza la licencia **GNU GPL v3.0**. Revisa [LICENSE](LICENSE) antes de contribuir.

---

<p align="center"><sub>Construido paso a paso, con responsabilidad, humildad y colaboración.</sub></p>
