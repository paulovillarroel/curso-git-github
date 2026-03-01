# Curso de Git y GitHub

Curso interactivo para principiantes que cubre desde la configuración inicial hasta flujos de trabajo colaborativos profesionales con GitHub.

**[Ir al curso](https://paulovillarroel.github.io/curso-git-github/)**

## Contenido

El curso está organizado en 10 módulos progresivos agrupados en 3 niveles, más secciones de práctica y referencia.

### Básico

| # | Módulo | Descripción |
|---|--------|-------------|
| 01 | Prerequisitos de terminal | `pwd`, `ls`, `cd`, `mkdir`, `touch`, `echo`, `cat` |
| 02 | Configuración inicial | Qué es Git, instalación, `git config` |
| 03 | Ciclo de vida local | `git init`, `status`, `add`, `diff`, `commit`, `log`, `.gitignore` |
| 04 | GitHub (la nube) | `remote`, `push`, `pull`, `clone`, `fork`, autenticación |

### Intermedio

| # | Módulo | Descripción |
|---|--------|-------------|
| 05 | Viajes en el tiempo | `git switch --detach`, `revert`, `reset --soft`, `reset --hard` |
| 06 | Ramas (universos paralelos) | `git branch`, `switch -c`, `merge`, conflictos, `branch -d` |
| 07 | Flujo profesional | GitHub Flow, Pull Requests, code review, merge en GitHub |

### Avanzado

| # | Módulo | Descripción |
|---|--------|-------------|
| 08 | Técnicas avanzadas | `rebase`, `pull --rebase`, `stash`, limpieza de ramas |
| 09 | Agentes IA (bonus) | Claude Code, Gemini CLI, GitHub Copilot CLI como asistentes de Git |
| 10 | Git para equipos | Branch protection, PR templates, `AGENTS.md`, anti-patrones |

### Práctica y referencia

- **Rutinas diarias** — Hábitos para mantener repositorios sanos
- **Errores comunes** — Soluciones paso a paso a los 10 errores más frecuentes
- **Ejercicios integradores** — 5 ejercicios que combinan todos los conceptos
- **Cheatsheet** — Referencia rápida de todos los comandos

## Características

- Tono conversacional con analogías y metáforas para cada concepto
- Instrucciones para **WSL (Windows)** y **macOS**
- Bloques de código con syntax highlighting (Expressive Code)
- Progreso por módulo con persistencia en localStorage
- Dark mode
- Responsive (sidebar en desktop, drawer en mobile)
- Widget flotante de "siguiente sección"

## Tech stack

- [Astro](https://astro.build/) — Framework de sitio estático
- [Tailwind CSS v4](https://tailwindcss.com/) — Estilos
- [MDX](https://mdxjs.com/) — Contenido con componentes
- [Expressive Code](https://expressive-code.com/) — Bloques de código
- [canvas-confetti](https://github.com/catdad/canvas-confetti) — Celebración al completar módulos

## Desarrollo local

```bash
# Clonar el repositorio
git clone https://github.com/paulovillarroel/curso-git-github.git
cd curso-git-github

# Instalar dependencias
npm install

# Iniciar servidor de desarrollo
npm run dev

# Build de producción
npm run build
```

## Parte de Hazla con Datos

Este curso es un recurso complementario de [Hazla con Datos](https://hazlacondatos.com/), una comunidad enfocada en programación y ciencia de datos en salud.

Otros recursos relacionados:
- [Curso de Terminal y Bash](https://paulovillarroel.github.io/curso-terminal-bash/) — Prerequisito recomendado

## Licencia

MIT
