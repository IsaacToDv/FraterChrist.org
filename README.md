<h1 align="center">FraterChrist.org</h1>

<p align="center">
  <strong>Fe, comunidad y creación colaborativa.</strong><br>
  Una plataforma cristiana abierta para compartir, aprender y construir juntos.
</p>

<p align="center">
  <a href="https://chat.whatsapp.com/REEMPLAZAR_CON_INVITACION"><img alt="Comunidad en WhatsApp" src="https://img.shields.io/badge/WhatsApp-Comunidad-25D366?style=for-the-badge&logo=whatsapp&logoColor=white"></a>
  <a href="https://discord.gg/REEMPLAZAR_CODIGO"><img alt="Comunidad en Discord" src="https://img.shields.io/badge/Discord-Comunidad-5865F2?style=for-the-badge&logo=discord&logoColor=white"></a>
  <a href="LICENSE"><img alt="Licencia GPL-3.0" src="https://img.shields.io/badge/Licencia-GPL--3.0-6F42C1?style=for-the-badge&logo=gnu&logoColor=white"></a>
</p>

<p align="center">
  <a href="#visión">Visión</a> ·
  <a href="#producto-por-etapas">Producto</a> ·
  <a href="docs/ROADMAP.md">Roadmap</a> ·
  <a href="docs/ARCHITECTURE.md">Arquitectura</a> ·
  <a href="CONTRIBUTING.md">Colaborar</a>
</p>

---

> **Estado:** diseño y planificación del MVP. La aplicación todavía no está implementada. El alcance y el stack se validarán por etapas.

## Visión

FraterChrist busca crear un espacio digital donde la comunidad pueda compartir contenido, crecer en la fe y reunirse en experiencias centradas en la oración, el estudio bíblico y el aprendizaje. El proyecto es abierto: producto, diseño y código podrán mejorar con la colaboración de la comunidad.

## Producto por etapas

### 01 · Feed — primera entrega

El primer objetivo es un feed cronológico donde las personas puedan compartir:

- **Hilos:** publicaciones de texto y respuestas.
- **Fotos:** publicaciones con imágenes.
- **Videos:** publicaciones audiovisuales.

La prioridad es construir una experiencia útil y segura, con autenticación, permisos de visibilidad y herramientas básicas de reporte y moderación. Las fotos y los videos se habilitarán con límites y controles de archivos; su alcance exacto se validará durante el MVP.

### 02 · Perfil

Perfiles para presentar a cada persona dentro de la comunidad y acceder a sus publicaciones. Los campos, la visibilidad y las opciones de privacidad se definirán antes de implementar esta etapa.

### 03 · Mesas

Espacios de encuentro enfocados en dos propósitos:

- **Mesa de oración:** compartir peticiones y acompañarse en oración.
- **Mesa de estudio bíblico:** estudiar pasajes, compartir reflexiones y aprender en comunidad.

### 04 · Salas temáticas

Salas con videollamada y una interfaz que se adapta a la actividad. La experiencia se diseñará por módulos, evitando desarrollar una herramienta distinta desde cero para cada temática.

| Tipo de sala | Experiencia prevista |
|---|---|
| **Juego bíblico** | Entorno para crear y participar en juegos educativos basados en la Biblia, con una experiencia de creación inspirada en herramientas como Educaplay. |
| **Oración** | Interfaz minimalista, modo silencio y una hoja para escribir peticiones de oración. |
| **Sala libre** | Videollamada y pizarra compartida para conversar, explicar ideas o colaborar libremente. |

Las salas son una etapa posterior: antes de implementarlas se evaluarán las opciones de videollamada, privacidad, moderación, accesibilidad y costo operativo.

## Stack propuesto

<p align="center">
  <img alt="Python" src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white">
  <img alt="Django REST Framework" src="https://img.shields.io/badge/Django%20REST%20Framework-A30000?style=flat-square&logo=django&logoColor=white">
  <img alt="PostgreSQL" src="https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white">
  <img alt="React" src="https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB">
  <img alt="TypeScript" src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white">
</p>

| Capa | Propuesta inicial |
|---|---|
| Backend y API | Python, Django y Django REST Framework |
| Base de datos | PostgreSQL |
| Interfaz web | React y TypeScript |
| Calidad | Pruebas automatizadas y GitHub Actions |
| Entorno de desarrollo | Docker Compose, si aporta una configuración reproducible |

La propuesta parte de un **monolito modular** para reducir complejidad y facilitar las contribuciones. No se incorporarán microservicios ni infraestructura de tiempo real hasta que una etapa los necesite. Consulta [Arquitectura y decisiones pendientes](docs/ARCHITECTURE.md).

## Empezar a colaborar

Puedes explorar el proyecto, proponer mejoras o preparar tu entorno local. Como aún está en fase de planificación, revisa primero el alcance antes de empezar a implementar funcionalidades.

**Opción A — Clonar el repositorio**

\`\`\`bash
git clone https://github.com/IsaacToDv/FraterChrist.org.git
cd FraterChrist.org
\`\`\`

**Opción B — Hacer un fork**

1. Abre el repositorio en GitHub y pulsa **Fork**.
2. Clona tu fork:

\`\`\`bash
git clone https://github.com/TU-USUARIO/FraterChrist.org.git
cd FraterChrist.org
\`\`\`

3. Consulta las [guías de contribución](CONTRIBUTING.md) y las [Issues](https://github.com/IsaacToDv/FraterChrist.org/issues) antes de proponer cambios.

## Documentación

- [Roadmap por ciclos y criterios de aceptación](docs/ROADMAP.md)
- [Arquitectura, stack y riesgos técnicos](docs/ARCHITECTURE.md)
- [Guía de contribución](CONTRIBUTING.md)
- [Código de conducta](CODE_OF_CONDUCT.md)
- [Reporte de vulnerabilidades](SECURITY.md)

## Comunidad

Los enlaces de WhatsApp y Discord en la parte superior son **marcadores de posición**. Se activarán cuando se creen los espacios oficiales.

FraterChrist.org se publica bajo la licencia [GNU GPL v3.0](LICENSE).

<p align="center"><sub>Construyamos con propósito, responsabilidad y espíritu de servicio.</sub></p>
