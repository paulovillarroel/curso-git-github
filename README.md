# Curso de Git y GitHub

Curso interactivo para principiantes que cubre desde la configuración inicial hasta flujos de trabajo colaborativos profesionales con GitHub.

**[Ver el curso en vivo](https://paulovillarroel.github.io/curso-git-github/)**

## Contenido

El curso está organizado en 8 módulos progresivos, una sección de errores comunes, ejercicios integradores y un cheatsheet de referencia rápida.

### Fundamentos

| # | Módulo | Descripción |
|---|--------|-------------|
| 01 | Supervivencia en Terminal | `pwd`, `ls`, `cd`, `mkdir`, `touch`, `echo`, `cat` |
| 02 | Configuración inicial | Qué es Git, instalación, `git config` |
| 03 | Ciclo de vida local | `git init`, `status`, `add`, `diff`, `commit`, `log`, `.gitignore` |
| 04 | Viajes en el tiempo | `git switch --detach`, `revert`, `reset --soft`, `reset --hard` |
| 05 | Ramas (universos paralelos) | `git branch`, `switch -c`, `merge`, conflictos, `branch -d` |
| 06 | GitHub (la nube) | `remote`, `push`, `pull`, `clone`, `fork`, autenticación |

### Avanzado

| # | Módulo | Descripción |
|---|--------|-------------|
| 07 | Flujo profesional | GitHub Flow, Pull Requests, code review, merge en GitHub |
| 08 | GitHub CLI y agentes IA | `gh` CLI, Claude Code, Gemini CLI, GitHub Copilot CLI |

### Práctica y referencia

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
