# Guía de instalación previa al taller

**Del informe_final_v3_DEFINITIVO.pbix al control de versiones en Power BI con Git**

Para que el taller arranque sin perder tiempo en instalaciones, necesitas tener todo esto listo antes. Calcula unos 30 minutos y hazlo con calma, no el mismo día. Si algo falla, escríbeme con una captura de pantalla antes del taller y lo resolvemos.

## Antes de empezar

El taller está preparado para **Windows**, porque Power BI Desktop solo funciona en Windows. Si trabajas con Mac o Linux, necesitas una máquina virtual con Windows, y conviene que lo resuelvas cuanto antes.

Necesitas permisos para instalar programas en tu computadora. Si usas un equipo de empresa con instalaciones restringidas, pide permiso a tu área de sistemas con tiempo.

## Paso 1. Crear tu cuenta de GitHub

1.  Entra en <https://github.com> y crea una cuenta gratuita.
2.  Confirma tu correo electrónico (te llega un mensaje con un código o enlace).
3.  Anota tu nombre de usuario y el correo con el que te registraste. Los vas a usar en el paso 3.

## Paso 2. Instalar Git

1.  Descarga Git para Windows desde <https://git-scm.com/download/win>
2.  Ejecuta el instalador y deja todas las opciones por defecto (pulsa "Next" hasta el final).
3.  Cuando termine, abre el menú de inicio, busca "Git Bash" o "Símbolo del sistema" y comprueba la instalación escribiendo:

```         
git --version
```

Debe mostrarte un número de versión. Si dice que no reconoce el comando, reinicia el ordenador y vuelve a probar.

## Paso 3. Configurar tu identidad en Git

Git necesita saber quién firma tus cambios. En la misma terminal (Git Bash) escribe estas dos líneas, sustituyendo por tus datos (el correo debe ser el de tu cuenta de GitHub):

```         
git config --global user.name "Tu Nombre"
git config --global user.email "tu_correo@ejemplo.com"
```

## Paso 4. Instalar Visual Studio Code

1.  Descárgalo desde <https://code.visualstudio.com>
2.  Instálalo con las opciones por defecto.
3.  Ábrelo y comprueba que tienes una versión reciente (menú Ayuda \> Acerca de). Si te aparece un aviso de actualización, acéptalo.

## Paso 5 (opcional). Asistente de IA en VS Code

En una parte del taller veremos cómo usar un asistente de IA para ayudarte con Git. **Es opcional**: todo el taller se puede seguir sin él, y cada ejercicio tiene su versión manual.

Si quieres probarlo y ya tienes acceso a algún asistente, puedes instalarlo ahora desde el panel de Extensiones de VS Code (`Ctrl + Mayús + X`). Un ejemplo es la extensión oficial de Claude Code, que requiere una suscripción de pago de Claude (o una cuenta de Claude Console) y una versión reciente de VS Code. Si ya usas otro asistente integrado en VS Code, también te sirve.

## Lista de comprobación final

Antes del taller, confirma que puedes marcar todo esto:

- [ ] Tengo cuenta de GitHub con el correo confirmado
- [ ] `git --version` me muestra una versión
- [ ] Configuré mi nombre y correo en Git
- [ ] VS Code está instalado y actualizado
- [ ] Opcional: Extensión de Claude Code en VSC u otro asistente de IA.
