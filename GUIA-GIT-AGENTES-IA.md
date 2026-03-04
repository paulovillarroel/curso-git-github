# Guía Git y GitHub para Agentes de IA

> **Propósito:** Este archivo condensa todo el conocimiento del [curso de Git y GitHub](https://curso-git-github.com) en un formato optimizado para dar como contexto a agentes de IA (Claude Code, Gemini CLI, GitHub Copilot, etc.). Cópialo completo o por secciones según lo que necesites.

---

## 1. Comandos esenciales

### Configuración inicial (una sola vez por computadora)

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu@correo.com"
git config --global core.editor "code --wait"
git config --global init.defaultBranch main
```

### Flujo básico diario

```bash
git status                # Ver qué cambió (usar SIEMPRE antes y después de cada acción)
git add archivo.txt       # Preparar archivo específico
git add .                 # Preparar todos los cambios
git diff                  # Ver cambios antes de staging
git diff --staged         # Ver cambios ya en staging
git commit -m "mensaje"   # Guardar snapshot
git push                  # Subir a GitHub
git pull                  # Descargar y aplicar cambios de GitHub
```

### Repositorios

```bash
git init                            # Activar Git en carpeta actual
git clone <URL>                     # Descargar repositorio de GitHub
git remote add origin <URL>         # Conectar repo local con GitHub
git remote -v                       # Ver conexiones remotas
git push -u origin main             # Primera subida a GitHub
```

### Ramas

```bash
git branch                          # Listar ramas (actual marcada con *)
git switch -c feature/nombre        # Crear rama y moverse a ella
git switch nombre-rama              # Cambiar de rama
git merge nombre-rama               # Traer cambios de otra rama
git branch -d nombre-rama           # Borrar rama ya mergeada (seguro)
git branch -D nombre-rama           # Forzar borrado de rama no mergeada
git branch -m viejo nuevo           # Renombrar rama
git push origin --delete rama       # Borrar rama remota
```

### Historial

```bash
git log --oneline                   # Historial compacto
git log --oneline --graph           # Historial con visualización de ramas
git show <hash>:archivo.txt         # Ver archivo en un commit pasado
```

### Deshacer cambios (de más seguro a más peligroso)

```bash
git restore archivo.txt             # Descartar cambios no commiteados
git restore --staged archivo.txt    # Sacar del staging sin perder cambios
git restore .                       # Descartar TODOS los cambios no commiteados
git stash                           # Guardar cambios temporalmente
git stash pop                       # Recuperar cambios guardados
git revert <hash>                   # Deshacer commit creando uno nuevo (SEGURO, recomendado)
git reset --soft HEAD~1             # Deshacer commit, archivos quedan en staging
git reset --hard HEAD~1             # PELIGRO: borra commit y todos los cambios
```

### Emergencias

```bash
git merge --abort                   # Cancelar merge con conflictos
git clean -fd                       # Borrar archivos/carpetas no rastreados
git rm --cached archivo.txt         # Dejar de rastrear sin borrar el archivo
git restore --source=<hash> archivo # Recuperar versión antigua de un archivo
```

### GitHub CLI (`gh`)

```bash
gh auth login                                        # Autenticarse
gh repo create nombre --public --source=. --push     # Crear repo y subir
gh pr create --title "..." --body "..."              # Crear Pull Request
gh pr list                                           # Listar PRs abiertos
gh pr view                                           # Ver PR actual
gh pr merge --squash                                 # Mergear con squash
gh issue create --title "..."                        # Crear issue
gh repo view --web                                   # Abrir en navegador
```

### Avanzados

```bash
git fetch                           # Revisar cambios remotos sin aplicar
git rebase main                     # Reescribir historial sobre main (lineal)
git rebase --abort                  # Cancelar rebase
git pull --rebase origin main       # Actualizar rama con historial lineal
git push --force-with-lease         # Force push seguro (verifica que nadie más hizo push)
```

---

## 2. Flujo profesional: GitHub Flow

Este es el flujo estándar que usan equipos profesionales:

```
1. git switch main && git pull            ← Partir actualizado
2. git switch -c feature/mi-tarea         ← Crear rama con convención de nombre
3. (trabajar, git add, git commit)        ← Hacer cambios con commits atómicos
4. git push -u origin feature/mi-tarea    ← Subir rama a GitHub
5. gh pr create --title "..." --body "…"  ← Crear Pull Request
6. (revisión de código, ajustes)          ← El equipo revisa
7. gh pr merge --squash                   ← Aprobar y fusionar
8. git switch main && git pull            ← Actualizar local
9. git branch -d feature/mi-tarea         ← Limpieza
```

**Regla fundamental:** Main solo recibe código terminado y revisado via Pull Request.

---

## 3. Convenciones de equipo

### Nombres de ramas

Formato: `tipo/descripcion-corta` (kebab-case, sin mayúsculas, sin espacios)

| Prefijo | Uso | Ejemplo |
|---------|-----|---------|
| `feature/` | Nueva funcionalidad | `feature/filtro-busqueda` |
| `fix/` | Corrección de bug | `fix/login-error` |
| `hotfix/` | Corrección urgente en producción | `hotfix/crash-checkout` |
| `docs/` | Solo documentación | `docs/actualizar-readme` |
| `refactor/` | Reestructurar código sin cambiar comportamiento | `refactor/auth-module` |

### Conventional Commits

Formato del mensaje: `tipo: descripción en imperativo`

| Tipo | Cuándo usar | Ejemplo |
|------|------------|---------|
| `feat:` | Nueva funcionalidad | `feat: agregar filtro por región` |
| `fix:` | Corrección de bug | `fix: corregir validación de email` |
| `docs:` | Documentación | `docs: actualizar guía de instalación` |
| `refactor:` | Reestructurar código | `refactor: simplificar lógica de auth` |
| `chore:` | Mantenimiento/dependencias | `chore: actualizar dependencias` |

**Reglas del mensaje:**
- Imperativo: "Agregar", no "Agregado" ni "Agrega"
- Máximo 72 caracteres en la primera línea
- Sin punto final
- Responde: "¿qué hace este commit y por qué?"

### Estrategia de merge

**Squash merge** es la opción recomendada para equipos:
- Todos los commits de una rama se comprimen en uno solo al fusionar
- Main queda con un historial limpio: un commit = una tarea completada
- Configurar en GitHub: Settings → General → Pull Requests → solo "Squash merging"

---

## 4. Buenas prácticas

### Branch Protection (configurar en GitHub)

- Requerir Pull Request antes de merge a main
- Requerir al menos 1 aprobación
- Nadie puede hacer push directo a main (ni admins)

### Pull Requests efectivos

- Título corto y descriptivo
- Descripción: qué cambió, por qué, cómo probar
- PRs pequeños y frecuentes (más fácil de revisar)
- Usar PR template en `.github/pull_request_template.md`

### Prevención de conflictos

- Dividir trabajo por archivos/componentes
- Hacer `git pull` frecuentemente (al menos diario)
- Ramas pequeñas con PRs frecuentes
- Comunicar antes de hacer refactors grandes
- Nunca resolver conflictos sin entender ambas versiones

### Commits atómicos

- Un commit = un cambio lógico
- Si necesitas usar "y" en el mensaje, probablemente son dos commits

---

## 5. Anti-patrones: las 5 cosas que nunca hacer

| Anti-patrón | Por qué es malo | Qué hacer en su lugar |
|-------------|-----------------|----------------------|
| Commits gigantes (47 archivos) | Imposible de revisar, imposible de revertir parcialmente | Commits atómicos: un cambio lógico por commit |
| Trabajar directo en main | Rompe el flujo del equipo, sin revisión de código | Siempre crear rama: `git switch -c feature/tarea` |
| No hacer pull antes de crear rama | Crea conflictos innecesarios | `git switch main && git pull` antes de nueva rama |
| No limpiar ramas mergeadas | Repo se llena de basura | `git branch -d rama` después de merge |
| Force push a main | Destruye el historial del equipo | Solo force push a tus propias ramas, y usar `--force-with-lease` |

---

## 6. Resolución de errores comunes

### Error 1: Typo en nombre de rama

```bash
git branch -m nombre-mal nombre-bien          # Renombrar local
git push origin --delete nombre-mal           # Borrar remota vieja (si ya hiciste push)
git push -u origin nombre-bien                # Subir con nombre correcto
```

### Error 2: Push rechazado (rejected)

```bash
git pull origin main        # Traer cambios remotos primero
# Resolver conflictos si los hay
git push origin main        # Ahora sí funciona
```

### Error 3: Commits en main que debían ir a otra rama

```bash
git branch feature/mis-cambios   # Crear rama en el punto actual
git reset --keep HEAD~N          # Mover main N commits atrás (conserva archivos)
git switch feature/mis-cambios   # Cambiar a la rama correcta
```

### Error 4: Deshacer último commit (conservar archivos)

```bash
git reset --soft HEAD~1          # Archivos quedan en staging, listos para re-commit
```

### Error 5: Descartar cambios en un archivo

```bash
git restore archivo.txt                  # Si NO está en staging
git restore --staged archivo.txt         # Si YA está en staging (sacarlo primero)
git restore archivo.txt                  # Luego descartar
```

### Error 6: Descartar TODOS los cambios locales

```bash
git restore .            # Descartar cambios en archivos rastreados
git clean -fd            # Borrar archivos nuevos no rastreados
git pull                 # Sincronizar con remoto
```

### Error 7: Hice `git add` de un archivo que no debía

```bash
git restore --staged archivo-secreto.env                # Si NO fue commiteado
# Si YA fue commiteado:
git rm --cached archivo-secreto.env
echo "archivo-secreto.env" >> .gitignore
git add .gitignore && git commit -m "chore: ignorar archivo secreto"
```

### Error 8: Atrapado en Vim

```
Presionar: Esc → escribir :q! → Enter    (salir sin guardar)
Prevención: git config --global core.editor "code --wait"
```

### Error 9: Merge salió mal

```bash
git merge --abort               # Si el merge está en progreso
git revert -m 1 HEAD            # Si ya completaste el merge
```

### Error 10: Recuperar versión anterior de un archivo

```bash
git show HEAD~3:ruta/archivo.txt                  # Solo ver contenido
git restore --source=<hash> ruta/archivo.txt      # Recuperar esa versión
```

---

## 7. Rutinas diarias

### Al empezar a trabajar

```bash
git switch main && git pull       # Actualizar main
git switch -c feature/tarea-hoy   # Crear rama para la tarea del día
```

### Al terminar el día

```bash
git add . && git commit -m "feat: progreso en tarea-hoy"
git push -u origin feature/tarea-hoy     # Respaldo en GitHub
```

### Fin de semana / antes de ausencia

```bash
# Asegurar que todo está subido
git status                        # Verificar que no hay cambios sin commitear
git push                          # Subir todo a GitHub
# Crear PR si la tarea está lista para revisión
```

### Limpieza periódica

```bash
git switch main && git pull
git branch --merged main | grep -v main | xargs git branch -d   # Borrar ramas mergeadas
```

---

## 8. Reglas de seguridad

### Nunca commitear

- `.env` — variables de entorno y secrets
- Contraseñas, API keys, tokens
- `node_modules/`, `vendor/` — dependencias regenerables
- Archivos compilados (`dist/`, `build/`)

### .gitignore (crear al inicio del proyecto)

```gitignore
# Secretos
.env
*.secret

# Dependencias
node_modules/
vendor/

# Sistema operativo
.DS_Store
Thumbs.db

# Archivos temporales
*.log
*.tmp
dist/
build/
```

### Si commiteaste un secreto por error

```bash
git rm --cached archivo-con-secreto
echo "archivo-con-secreto" >> .gitignore
git add .gitignore && git commit -m "chore: remover archivo con secreto del tracking"
# IMPORTANTE: rota el secreto inmediatamente (cambiar contraseña/API key)
# El secreto sigue en el historial de Git
```

### Regla de oro del force push

- **Nunca** hacer force push a `main` o ramas compartidas
- Solo en tus propias ramas de feature
- Usar `--force-with-lease` en lugar de `--force`

---

## 9. Resolver conflictos de merge

### Paso a paso

```bash
# 1. Al hacer merge, Git avisa del conflicto
git merge otra-rama
# CONFLICT in archivo.txt

# 2. Abrir el archivo y buscar los marcadores:
<<<<<<< HEAD
tu versión (rama actual)
=======
la otra versión
>>>>>>> otra-rama

# 3. Editar: borrar los marcadores, dejar el contenido correcto

# 4. Marcar como resuelto
git add archivo.txt
git commit -m "fix: resolver conflicto en archivo.txt"
```

### Reglas al resolver conflictos

- Entender ambas versiones antes de elegir
- No aceptar automáticamente sin leer
- Si no entiendes un cambio, preguntar al autor
- Probar que el código funciona después de resolver

---

## 10. Tres áreas de Git

```
Working Directory    →    Staging Area    →    Repository
  (editas archivos)      (git add)           (git commit)
                          ↩ git restore       ↩ git reset --soft
                            --staged
```

- **Working Directory:** donde editas archivos normalmente
- **Staging Area:** preparas qué cambios incluir en el próximo commit
- **Repository:** historial permanente de snapshots (commits)

---

---

# Template de AGENTS.md para tu proyecto

> **Instrucciones:** Copia este template, renómbralo a `AGENTS.md` (o `CLAUDE.md` para Claude Code, `GEMINI.md` para Gemini CLI), y completa las secciones marcadas con `[COMPLETAR]`. Elimina las secciones que no apliquen a tu proyecto.

```markdown
# AGENTS.md

> Convenciones y reglas del proyecto para agentes de IA.
> Este archivo es documentación viva — actualízalo cuando el equipo adopte nuevas convenciones.

## Flujo de trabajo Git

- Nunca hacer commit directamente a main
- Crear ramas con formato: tipo/descripcion-corta
- Tipos permitidos: feature/, fix/, hotfix/, docs/, refactor/
- Todo cambio a main va via Pull Request
- Usar squash merge al fusionar PRs
- Borrar la rama después de merge

### Convención de commits

- Formato: Conventional Commits (feat:, fix:, docs:, refactor:, chore:)
- Idioma: [COMPLETAR: español/inglés]
- Tiempo verbal: imperativo ("Agregar", no "Agregado")
- Máximo 72 caracteres en primera línea
- Ejemplo: "feat: agregar validación de formulario de registro"

### Pull Requests

- Título descriptivo y corto
- Descripción: qué cambia, por qué, cómo probar
- Asignar al menos un reviewer
- No mergear sin aprobación

## Idioma y convenciones de código

- Idioma del código (variables, funciones): [COMPLETAR: inglés/español]
- Idioma de comentarios: [COMPLETAR]
- Idioma de documentación: [COMPLETAR]
- Naming convention: [COMPLETAR: camelCase, snake_case, PascalCase]
- Formato de archivos: [COMPLETAR: extensiones, estructura de nombres]

## Estructura del proyecto

[COMPLETAR: describir la estructura de carpetas relevante]

Ejemplo:
- src/ — código fuente
- src/components/ — componentes reutilizables
- src/pages/ — páginas/rutas
- tests/ — tests
- docs/ — documentación

## Testing y validación

- Comando para correr tests: [COMPLETAR: npm test, pytest, etc.]
- Correr tests antes de crear PR
- [COMPLETAR: cobertura mínima, tipos de tests requeridos]

## Restricciones y reglas de seguridad

- NUNCA commitear archivos .env, secrets, API keys o credenciales
- NUNCA hacer force push a main
- NUNCA resolver conflictos automáticamente sin entender ambas versiones
- NUNCA borrar ramas de otros sin confirmación
- [COMPLETAR: restricciones específicas del proyecto]

## Resolución de conflictos

- Al encontrar un conflicto de merge, explicar qué versiones hay
- No auto-resolver: mostrar ambas versiones y pedir confirmación
- Si es ambiguo, preguntar antes de elegir una versión
- Después de resolver, verificar que el código funciona

## Documentación

- Actualizar README si cambia la forma de instalar o usar el proyecto
- [COMPLETAR: herramientas de docs, formato, dónde se documentan las APIs]

## Dependencias

- [COMPLETAR: gestor de paquetes (npm, pip, cargo, etc.)]
- No agregar dependencias sin justificación
- [COMPLETAR: proceso para agregar nuevas dependencias]

## Entorno de desarrollo

- [COMPLETAR: versión de lenguaje/runtime requerida]
- [COMPLETAR: cómo levantar el proyecto localmente]
- [COMPLETAR: variables de entorno necesarias (sin valores)]
```

---

> **Nota:** Esta guía fue creada como material complementario del [Curso de Git y GitHub](https://paulovillarroel.github.io/curso-git-github/). Para aprender estos conceptos paso a paso, revisa el curso completo.
