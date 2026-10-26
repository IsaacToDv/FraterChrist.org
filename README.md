<h1 align="center">FraterChrist.org</h1>

<p align="center">
  <strong>Pensada para la Comunión, Edificación y la gran Comisión, esto es FraterChrist.</strong><br>
  Un proyecto de red social open source para Hilos (Comunión), Mesas (Edificación) y Salas colaborativas (Comisión).
</p>

<p align="center">
  <a href="#comunidad"><img alt="WhatsApp" src="https://img.shields.io/badge/WhatsApp-Comunidad-25D366?style=for-the-badge&logo=whatsapp&logoColor=white"></a>
  <a href="#comunidad"><img alt="Discord" src="https://img.shields.io/badge/Discord-Comunidad-5865F2?style=for-the-badge&logo=discord&logoColor=white"></a>
  <a href="LICENSE"><img alt="Licencia GPL-3.0" src="https://img.shields.io/badge/Licencia-GPL--3.0-6F42C1?style=for-the-badge&logo=gnu&logoColor=white"></a>
</p>

<p align="center">
  <a href="#el-producto">El producto</a> ·
  <a href="#cómo-se-conecta">Arquitectura</a> ·
  <a href="#participa">Participa</a> ·
  <a href="docs/ROADMAP.md">Roadmap</a>
</p>

---

> **Estado actual:** diseño y planificación. El desarrollo comenzará por el feed.

## ¿Qué es FraterChrist?

Una red social donde hermanos en cristo en todo el mundo puedan publicar contenido a través de hilos, tener perfiles temáticos, reunirse para orar o estudiar la Biblia y participar en salas colaborativas donde podrán recrearse, jugar en grupo, colaborar juntos.

## El producto

El desarrollo se plantea como un recorrido: primero el feed; después, los espacios personales y comunitarios.

~~~mermaid
flowchart TD
    Feed["**Feed · primera etapa**<br/>Hilos · Fotos · Videos"]
    Profile["Perfil"]
    Tables["Mesas<br/>Oración · Estudio bíblico"]
    Rooms["Salas temáticas<br/>Juegos bíblicos · Peliculas · Temas libres"]

    Feed --> Profile --> Tables --> Rooms
~~~

Las salas tendrán una experiencia propia según la actividad:

- **Juego bíblico:** crear y jugar actividades educativas inspiradas en herramientas como Educaplay.
- **Oración:** interfaz minimalista, modo silencio y hoja de peticiones.
- **Sala libre:** videollamada y pizarra compartida.

## Cómo se conecta

~~~mermaid
flowchart LR
    People["Comunidad"] --> Web["Web<br/>React + TypeScript"]
    Web <-->|"HTTPS / JSON"| API["Backend y permisos<br/>Django REST Framework"]
    API <--> DB[("PostgreSQL")]
    API -->|"Token de acceso limitado"| Web
    Web <-->|"Audio y video"| LK["LiveKit"]
    Web --> UI["Interfaz temática<br/>Juego · Oración · Pizarra"]
    UI --> API
~~~

**LiveKit** se encargará de la conexión de audio y video en tiempo real. FraterChrist controlará quién puede entrar a cada sala y desarrollará sus herramientas específicas: los juegos, las peticiones de oración y la pizarra. El stack sigue siendo una propuesta que se validará antes de implementar cada etapa.

<p align="center">
  <a href="https://www.python.org/"><img alt="Python" src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white"></a>
  <a href="https://www.djangoproject.com/"><img alt="Django REST Framework" src="https://img.shields.io/badge/Django%20REST%20Framework-A30000?style=flat-square&logo=django&logoColor=white"></a>
  <a href="https://www.postgresql.org/"><img alt="PostgreSQL" src="https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white"></a>
  <a href="https://react.dev/"><img alt="React" src="https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB"></a>
  <a href="https://www.typescriptlang.org/"><img alt="TypeScript" src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white"></a>
  <a href="https://livekit.io/"><img alt="LiveKit" src="https://img.shields.io/badge/LiveKit-Audio%20%2F%20Video-6B4EFF?style=flat-square&logo=webrtc&logoColor=white"></a>
</p>

## Participa

<details>
<summary><strong>Solo quiero conocer el proyecto</strong></summary>

Consulta el [roadmap](docs/ROADMAP.md) para ver lo que se piensa construir y el orden propuesto.
Nota. Las funciones futuras son ideas de producto.
</details>

<details>
<summary><strong>Quiero colaborar con código o documentación</strong></summary>

Clona el repositorio:

~~~bash
git clone https://github.com/IsaacToDv/FraterChrist.org.git
cd FraterChrist.org
~~~

O haz un **Fork** desde GitHub y clona tu copia:

~~~bash
git clone https://github.com/TU-USUARIO/FraterChrist.org.git
cd FraterChrist.org
~~~

Antes de hacer cambios, revisa las [Issues](https://github.com/IsaacToDv/FraterChrist.org/issues) y la [guía para contribuir](CONTRIBUTING.md). Como el proyecto está en etapa temprana, también son valiosas las aportaciones de diseño, accesibilidad, documentación y revisión de requisitos.
</details>

<details>
<summary><strong>Quiero seguir el progreso o proponer una idea</strong></summary>

- [Ver Issues y propuestas](https://github.com/IsaacToDv/FraterChrist.org/issues)
- [Consultar el roadmap](docs/ROADMAP.md)
- [Leer la arquitectura propuesta](docs/ARCHITECTURE.md)
</details>

## Comunidad

Los botones de WhatsApp y Discord de la parte superior enlazan a este apartado por ahora. **Las invitaciones oficiales están pendientes de añadir.**

Para que la colaboración sea respetuosa y segura, consulta el [Código de conducta](CODE_OF_CONDUCT.md). Las vulnerabilidades deben comunicarse siguiendo [SECURITY.md](SECURITY.md), no en una Issue pública.

---

<p align="center"><sub>Colosenses 3:17</sub></p>
