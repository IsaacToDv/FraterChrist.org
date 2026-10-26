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
  <a href="#producto-por-etapas">Producto</a> ·
  <a href="#stack-propuesto">Stack</a> ·
  <a href="#cómo-funcionarán-las-salas">Salas y LiveKit</a> ·
  <a href="docs/ROADMAP.md">Roadmap</a> ·
  <a href="CONTRIBUTING.md">Colaborar</a>
</p>

---

> **Estado:** diseño y planificación del MVP. La aplicación todavía no está implementada; las etapas y tecnologías descritas aquí son propuestas de trabajo.

## La idea

FraterChrist busca reunir publicaciones, oración, estudio bíblico y experiencias de aprendizaje en un mismo espacio. El producto se desarrollará por etapas para probar lo esencial antes de asumir la complejidad de las funciones comunitarias en tiempo real.

## Producto por etapas

### 01 — Feed · primera entrega

La primera versión se centrará en un feed cronológico con:

- **Hilos:** publicaciones de texto y respuestas.
- **Fotos:** publicaciones con imágenes.
- **Videos:** publicaciones audiovisuales.

La base incluirá cuentas, permisos de visibilidad y herramientas iniciales de reporte y moderación. Las cargas de archivos tendrán límites y controles de acceso; los detalles se validarán durante el diseño del MVP.

### 02 — Perfil

Una página para cada persona y acceso a sus publicaciones. Antes de implementarla se definirán los campos, la privacidad y qué información será visible para otros usuarios.

### 03 — Mesas

Espacios para reunirse alrededor de una actividad:

- **Oración:** compartir peticiones y acompañarse en oración.
- **Estudio bíblico:** estudiar pasajes, compartir reflexiones y aprender en comunidad.

### 04 — Salas temáticas

Salas con videollamada e interfaces adaptadas al propósito de la reunión.

| Sala | Experiencia prevista |
|---|---|
| **Juego bíblico** | Crear y participar en juegos educativos basados en la Biblia, con una experiencia de autoría inspirada en herramientas como Educaplay. |
| **Oración** | Diseño minimalista, modo silencio y hoja para registrar peticiones de oración. |
| **Sala libre** | Videollamada y pizarra compartida para explicar ideas o colaborar. |

Las salas se construirán después de las primeras etapas. LiveKit facilitará la comunicación de audio y video en tiempo real; las interfaces temáticas y sus herramientas serán funcionalidades propias de FraterChrist.

## Stack propuesto

<p align="center">
  <a href="https://www.python.org/"><img alt="Python" src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white"></a>
  <a href="https://www.djangoproject.com/"><img alt="Django REST Framework" src="https://img.shields.io/badge/Django%20REST%20Framework-A30000?style=flat-square&logo=django&logoColor=white"></a>
  <a href="https://www.postgresql.org/"><img alt="PostgreSQL" src="https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white"></a>
  <a href="https://react.dev/"><img alt="React" src="https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB"></a>
  <a href="https://www.typescriptlang.org/"><img alt="TypeScript" src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white"></a>
  <a href="https://livekit.io/"><img alt="LiveKit" src="https://img.shields.io/badge/LiveKit-Realtime%20Rooms-6B4EFF?style=flat-square&logo=webrtc&logoColor=white"></a>
</p>

| Capa | Tecnología propuesta | Responsabilidad |
|---|---|---|
| Backend y API | Python, Django y Django REST Framework | Cuentas, publicaciones, permisos, mesas y reglas de producto. |
| Datos | PostgreSQL | Usuarios, contenido, permisos, metadatos y estado persistente de las salas. |
| Interfaz | React y TypeScript | Feed, perfiles y diseños de cada tipo de sala. |
| Audio/video en tiempo real | LiveKit: SDK de cliente JS, componentes React y servidor LiveKit Cloud o autohospedado por decidir | Conexión de participantes, publicación de micrófono/cámara y transporte de medios. |
| Integración de servidor | Paquete Python livekit-api | Emisión de tokens con permisos limitados y gestión de salas cuando sea necesario. |
| Calidad y colaboración | Pruebas automatizadas, GitHub Actions y pull requests | Detectar regresiones y revisar los cambios antes de integrarlos. |

La propuesta empieza con un **monolito modular**. El servicio de LiveKit se encargaría del transporte de audio/video; Django seguiría siendo responsable de las cuentas, los permisos y la lógica de FraterChrist. La elección entre LiveKit Cloud y una instancia autohospedada se evaluará por costo, mantenimiento y necesidades de privacidad.

## Cómo funcionarán las salas

1. Una persona solicita entrar a una sala desde la interfaz de FraterChrist.
2. Django comprueba su sesión y sus permisos para esa sala.
3. El backend genera un token de acceso de LiveKit limitado a la identidad, sala y capacidades permitidas. El secreto de LiveKit nunca se envía al navegador.
4. La interfaz React conecta el SDK a LiveKit para la comunicación de audio/video.
5. La aplicación muestra la interfaz correspondiente: juego bíblico, oración o sala libre.

**LiveKit no construye por sí solo las herramientas temáticas.** FraterChrist implementará el creador y estado de los juegos bíblicos, la hoja de peticiones, la experiencia de modo silencio y la pizarra. Si se necesitan acciones en tiempo real, podrán evaluarse los canales de datos de LiveKit; los datos que deban conservarse se validarán y guardarán a través del backend.

Documentación: [SDK para React](https://docs.livekit.io/transport/sdk-platforms/react/), [SDK de navegador](https://github.com/livekit/client-sdk-js), [tokens y permisos](https://docs.livekit.io/frontends/reference/tokens-grants/) y [API de servidor para Python](https://docs.livekit.io/reference/python/livekit/api/).

## Empezar a colaborar

El repositorio está en fase de planificación. Revisa primero el alcance y el [roadmap](docs/ROADMAP.md) antes de implementar funciones.

**Clonar el repositorio**

~~~
git clone https://github.com/IsaacToDv/FraterChrist.org.git
cd FraterChrist.org
~~~

**O hacer un fork**

1. Pulsa **Fork** en GitHub.
2. Clona tu fork:

~~~
git clone https://github.com/TU-USUARIO/FraterChrist.org.git
cd FraterChrist.org
~~~

3. Revisa las [guías de contribución](CONTRIBUTING.md) y las [Issues](https://github.com/IsaacToDv/FraterChrist.org/issues).

## Documentación

- [Roadmap por etapas y criterios de aceptación](docs/ROADMAP.md)
- [Arquitectura, LiveKit y decisiones técnicas](docs/ARCHITECTURE.md)
- [Guía de contribución](CONTRIBUTING.md)
- [Código de conducta](CODE_OF_CONDUCT.md)
- [Reporte de vulnerabilidades](SECURITY.md)

## Comunidad

Los enlaces de WhatsApp y Discord de la parte superior son marcadores de posición. Se sustituirán por invitaciones oficiales cuando los espacios estén listos.

FraterChrist.org utiliza la licencia [GNU GPL v3.0](LICENSE).

<p align="center"><sub>Construyamos con propósito, responsabilidad y espíritu de servicio.</sub></p>
