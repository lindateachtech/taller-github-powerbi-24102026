# Comandos de Git para el taller

**Del informe_final_v3_DEFINITIVO.pbix al control de versiones en Power BI con Git**

Todo lo que va entre `<>` es lo que tienes que sustituir. No se escriben los símbolos `<>`. Los comandos se ejecutan en la terminal de VS Code (Terminal \> New Terminal), dentro de la carpeta de tu proyecto. Cada comando tiene su botón equivalente en VS Code, que es la forma principal de trabajar en el taller.

Si al pegar un comando en la terminal ves caracteres raros como [200\~, escríbelo a mano o pégalo con clic derecho.

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

El correo debe ser el de tu cuenta de GitHub. Si omites este paso, el primer commit te dará un error diciendo que Git no sabe quién eres.

### Camino 1. Local primero: ya tengo un proyecto de Power BI

1.  En Power BI Desktop, abre tu informe y guárdalo como proyecto (.pbip) dentro de una carpeta corta, por ejemplo `C:\taller-git\<proyecto>`, fuera de OneDrive.
2.  En VS Code, abre esa carpeta (Archivo \> Abrir carpeta) y abre la terminal.
3.  Crea el archivo `.gitignore` en la raíz del proyecto, al mismo nivel que el archivo `.pbip`, con estas dos líneas. Hazlo antes de preparar nada.

```         
**/.pbi/localSettings.json
**/.pbi/cache.abf
```

4.  Convierte la carpeta en un repositorio y mira qué archivos va a ver Git. Comprueba que `cache.abf` y `localSettings.json` no aparecen en la lista.

```         
git init
git status
```

5.  Prepara los archivos y haz el primer commit.

```         
git add .
git commit -m "<mensaje>"
```

6.  En GitHub, crea un repositorio nuevo sin marcar ninguna opción: ni README, ni .gitignore, ni licencia. Que sea público y que su nombre no tenga espacios ni tildes. Copia la URL HTTPS, que tiene la forma `https://github.com/<usuario>/<repositorio>.git`.
7.  Conéctalo y sube el proyecto.

```         
git branch -M main
git remote add origin <url-del-repositorio>
git push -u origin main
```

8.  Actualiza la página del repositorio en GitHub y comprueba que está tu proyecto.

### Camino 2. GitHub primero: clono un repositorio

1.  En GitHub, crea el repositorio, público y con un README (o copia la URL de uno que ya exista).
2.  En VS Code: Ctrl+Mayús+P, Git: Clone, pega la URL y elige la carpeta donde quieres el proyecto. Con comando:

```         
git clone <url-del-repositorio> <carpeta>
```

La `<carpeta>` es opcional: si no la pones, usa el nombre del repositorio.

## 2. Mirar qué pasa

```         
git status
git diff
git diff <archivo>
git diff --staged
git log --oneline
git log --oneline -5
git branch -vv
```

- `git status`: qué archivos cambiaron y cuáles están preparados.
- `git diff`: cambios que aún no has preparado. Con `<archivo>`, solo ese archivo.
- `git diff --staged`: cambios ya preparados, los que entrarán en el próximo commit.
- `git log --oneline`: historial resumido, una línea por commit. Con `-5`, los últimos cinco.
- `git branch -vv`: tus ramas y a qué rama remota está enlazada cada una.

En el panel de Control de código fuente de VS Code, las letras junto a cada archivo indican su estado: `U` es un archivo nuevo sin seguimiento, `M` es modificado y `D` es eliminado.

## 3. Guardar cambios

```         
git add <archivo>
git add <carpeta>/
git add .
git commit -m "<mensaje>"
```

- `git add <archivo>`: prepara un archivo, por ejemplo `<proyecto>.SemanticModel/definition/tables/Ventas.tmdl`.
- `git add <carpeta>/`: prepara todo lo que hay dentro de esa carpeta.
- `git add .`: prepara todo lo que cambió desde donde estás. Úsalo solo después de revisar `git status`.
- `git commit -m "<mensaje>"`: guarda la foto con tu mensaje, entre comillas dobles. Ejemplo: `git commit -m "Cambia la medida del gráfico circular"`.

## 4. Compartir con GitHub

```         
git push
git push -u origin <rama>
git pull
git pull origin <rama>
```

- `git push`: sube los commits de la rama actual a su remoto.
- `git push -u origin <rama>`: la primera vez que subes una rama nueva. `origin` es el nombre del remoto y `<rama>` es, por ejemplo, `main` o `mejora-grafico`. El `-u` enlaza la rama, y después basta con `git push`.
- `git pull`: trae los cambios de GitHub a la rama actual.
- `git pull origin <rama>`: lo mismo, indicando de qué rama.

## 5. Ramas, pull request y fusión

Crea la rama antes de abrir el informe en Power BI Desktop, o cierra el proyecto en Desktop antes de cambiar de rama.

```         
git switch <rama>
git switch -c <rama-nueva>
git merge <rama>
```

- `git switch <rama>`: cambia a una rama que ya existe.
- `git switch -c <rama-nueva>`: crea la rama y te cambia a ella.
- `git merge <rama>`: trae a la rama en la que estás los cambios de `<rama>`. Se puede fusionar cualquier rama con cualquier otra, no solo con `main`.

Receta de la práctica 3, con pull request:

```         
git switch main
git pull
git switch -c <rama-nueva>
# haces el cambio en Power BI Desktop y guardas
git add .
git commit -m "<mensaje>"
git push -u origin <rama-nueva>
```

Después, en GitHub:

1.  Actualiza la página del repositorio. Si la rama tiene commits propios, aparece un aviso para crear el pull request. Si no aparece, usa la pestaña Pull requests \> New pull request y elige tu rama.
2.  Revisa los cambios y crea el pull request.
3.  Quien administra el repositorio lo revisa y pulsa Merge pull request. En tu propio repositorio, eres tú. Y de vuelta en VS Code:

```         
git switch main
git pull
```

Alternativa sin pull request, fusionando en local:

```         
git switch main
git merge <rama-nueva>
git push
```

Para borrar una rama que ya no necesitas (solo en tu computadora):

```         
git branch -d <rama>
```

Con `-d`, Git solo la borra si sus cambios ya están fusionados. No se puede borrar la rama en la que estás.

## 6. Si algo sale mal

**Se coló un archivo local en el commit (`cache.abf` o `localSettings.json`).** Comprueba qué archivos sigue Git con `git ls-files`. Si aparece alguno de esos, deja de seguirlo sin borrarlo de tu disco:

```         
git rm --cached "<carpeta>.Report/.pbi/localSettings.json"
git rm --cached "<carpeta>.SemanticModel/.pbi/cache.abf"
git rm --cached "<carpeta>.SemanticModel/.pbi/localSettings.json"
git add .gitignore
git commit -m "Deja de versionar archivos locales de Power BI"
git push
```

Añadir un `.gitignore` después del primer `git add` no saca los archivos que Git ya sigue. Por eso el `.gitignore` va antes.

**El primer commit da un error de que Git no sabe quién eres.** Haz la configuración de la sección 1.

**El push se rechaza o habla de historiales distintos.** El repositorio de GitHub se creó con README, `.gitignore` o licencia. Bórralo en GitHub, vuelve a crearlo vacío y repite el paso 7 del camino 1.

**No aparece el aviso para crear el pull request.** La rama no tiene commits propios (en el push aparece `Total 0 (delta 0)`). Haz el cambio, guarda, haz commit y `git push` de nuevo.

**El botón de commit está apagado.** No hay cambios pendientes. Modifica algo en Power BI, guarda, y el archivo aparecerá en la lista de cambios.

**El push se queda cargando.** Mira si hay una ventana de inicio de sesión de GitHub escondida detrás de VS Code o en el navegador. También puedes cancelar y escribir `git push` en la terminal para ver el mensaje.

## 7. Prompts para Claude Code (opcional)

Si usas la extensión Claude Code en VS Code, estos prompts hacen lo mismo que los comandos. Todos piden confirmación o piden explicar antes de ejecutar.

Consultar, sin modificar nada:

```         
Dime el estado del repositorio y explícame en lenguaje sencillo qué archivos han cambiado. No modifiques nada.
```

```         
Resume qué ha cambiado en el proyecto: medidas, tablas o visuales. No modifiques nada.
```

```         
Muéstrame los últimos 5 commits y explica en una frase qué hizo cada uno.
```

Guardar y sincronizar:

```         
Prepara todos los cambios, dime un mensaje de commit en español de menos de 72 caracteres. Espera mi OK antes de hacer el commit.
```

```         
Sube la rama actual a GitHub con git push. Antes de ejecutarlo, dime a qué remoto y a qué rama va.
```

```         
Trae los cambios de GitHub con git pull. Si hay un conflicto, no lo resuelvas: dime qué archivos chocan.
```

Ramas:

```         
Crea una rama llamada <rama> desde main y cámbiame a ella. Dime los comandos antes de ejecutarlos.
```

Cambia el nombre de la rama por el de tu proyecto.

## 8. Antes de cada push

- Haz `git status` y revisa qué archivos van a subir.
- Comprueba que `cache.abf` y `localSettings.json` no aparecen en la lista.
- No subas datos sensibles, credenciales, tokens ni cadenas de conexión con claves.
- Mira el diff de `visual.json` y de los marcadores: pueden contener valores de tus datos.
- Haz pull antes de empezar a trabajar y antes de subir.
