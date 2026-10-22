# Comandos de Git para el taller

**Del informe_final_v3_DEFINITIVO.pbix al control de versiones en Power BI con Git**

Todo lo que va entre `<>` es lo que tienes que sustituir. No se escriben los símbolos `<>`. Los comandos se ejecutan en la terminal de VS Code (Terminal \> New Terminal), dentro de la carpeta de tu proyecto. Cada comando tiene su botón equivalente en VS Code, que es la forma principal de trabajar en el taller.

## 1. Configuración inicial (una sola vez)

```         
git config --global user.name "<tu nombre>"
git config --global user.email "<tu correo de GitHub>"
git config --global init.defaultBranch main
```

Para comprobar lo que quedó guardado:

```         
git config --global --list
```

## 2. Empezar un repositorio

**Proyecto nuevo:** clonas un repositorio que creaste antes en GitHub.

```         
git clone <url-del-repositorio> <carpeta>
```

La `<url-del-repositorio>` es la del botón verde Code en GitHub, con la forma `https://github.com/<usuario>/<repositorio>.git`. La `<carpeta>` es opcional: si no la pones, usa el nombre del repositorio.

**Proyecto existente:** ya tienes la carpeta con tu .pbip y quieres convertirla en repositorio.

```         
git init
git add .
git commit -m "<mensaje>"
git branch -M main
git remote add origin <url-del-repositorio>
git push -u origin main
```

Antes de `git add .` ejecuta `git status` y comprueba que no vas a subir nada que no debas (datos, credenciales).

## 3. Mirar qué pasa

```         
git status
git diff
git diff <archivo>
git diff --staged
git log --oneline
git log --oneline -5
```

- `git status`: qué archivos cambiaron y cuáles están preparados.
- `git diff`: cambios que aún no has preparado. Con `<archivo>`, solo ese archivo.
- `git diff --staged`: cambios ya preparados, los que entrarán en el próximo commit.
- `git log --oneline`: historial resumido, una línea por commit. Con `-5`, los últimos cinco.

## 4. Guardar cambios

```         
git add <archivo>
git add <carpeta>/
git add .
git commit -m "<mensaje>"
```

- `git add <archivo>`: prepara un archivo, por ejemplo `Informe.SemanticModel/definition/tables/Ventas.tmdl`.
- `git add <carpeta>/`: prepara todo lo que hay dentro de esa carpeta.
- `git add .`: prepara todo lo que cambió desde donde estás. Úsalo solo después de revisar `git status`.
- `git commit -m "<mensaje>"`: guarda la foto con tu mensaje, entre comillas dobles. Ejemplo: `git commit -m "Añade la medida Margen"`.

## 5. Compartir con GitHub

```         
git push
git push -u origin <rama>
git pull
git pull origin <rama>
```

- `git push`: sube los commits de la rama actual a su remoto.
- `git push -u origin <rama>`: la primera vez que subes una rama nueva. `origin` es el nombre del remoto y `<rama>` es, por ejemplo, `main` o `mejora-portada`. El `-u` enlaza la rama, y después basta con `git push`.
- `git pull`: trae los cambios de GitHub a la rama actual.
- `git pull origin <rama>`: lo mismo, indicando de qué rama.

## 6. Ramas y fusión

```         
git switch <rama>
git switch -c <rama-nueva>
git merge <rama>
```

- `git switch <rama>`: cambia a una rama que ya existe.
- `git switch -c <rama-nueva>`: crea la rama y te cambia a ella.
- `git merge <rama>`: trae a la rama en la que estás los cambios de `<rama>`.

```         
git switch -c <rama-nueva>
# haces el cambio en Power BI Desktop, guardas
git add .
git commit -m "<mensaje>"
git push -u origin <rama-nueva>
git switch main
git merge <rama-nueva>
git push
```

Si ves `git checkout` en tutoriales, para cambiar de rama es la forma antigua de `git switch`.

## 7. Prompts de Claude equivalentes (opcional)

Si usas Claude Code en VS Code, estos prompts hacen lo mismo. Todos piden confirmación o piden explicar antes de ejecutar.

Arranque de sesión, pégalo al empezar:

```         
Antes de ejecutar nada, dime qué comando vas a usar y qué va a pasar. No uses push --force ni reset --hard, y no borres ramas. Espera mi confirmación.
```

Consultar, sin modificar nada:

```         
Ejecuta git status y explícame en lenguaje sencillo qué archivos han cambiado y cuáles están preparados para el commit. No modifiques nada.
```

```         
Ejecuta git diff y resume qué ha cambiado en el proyecto de Power BI: medidas, tablas o visuales. No modifiques nada.
```

```         
Muéstrame los últimos 5 commits con git log --oneline y explica en una frase qué hizo cada uno.
```

```         
Revisa si el .gitignore deja fuera los archivos locales de Power BI de la carpeta .pbi. Dime qué falta, pero no lo cambies.
```

Guardar y sincronizar:

```         
Prepara solo los cambios de la carpeta Informe.SemanticModel y propón un mensaje de commit en español, claro y de menos de 72 caracteres. Espera mi OK antes de hacer el commit.
```

```         
Sube la rama actual a GitHub con git push. Antes de ejecutarlo, dime a qué remoto y a qué rama va.
```

```         
Trae los cambios de GitHub con git pull. Si hay un conflicto, no lo resuelvas: dime qué archivos chocan.
```

Cambia el nombre de la carpeta o de la rama por el de tu proyecto.

## 8. Antes de cada push

- Haz `git status` y revisa qué archivos van a subir.
- No subas datos sensibles, credenciales ni cadenas de conexión con claves.
- Comprueba que `.pbi/cache.abf` y `.pbi/localSettings.json` quedan fuera (los excluye el .gitignore).
- Mira el diff de `visual.json` y de los marcadores: pueden contener valores de tus datos.
- Haz pull antes de empezar a trabajar y antes de subir.
