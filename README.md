# Configuración inicial de entorno de trabajo en Windows 11

Con este repositorio pretendo tener una guía para poder configurar un entorno de Windows desde cero, con las herramientas que suelo utilizar para esta plataforma. Quizá este trabajo le sirva a alguien más.

## Instalando y configurando Oh My Posh

Para comenzar a configurar el nuevo entorno de trabajo necesito tener la [Windows Terminal](https://apps.microsoft.com/detail/9N0DX20HK701?hl=en-us&gl=MX&ocid=pdpshare). Ahora, como estoy trabajando en Windows 11 usaremos el [PowerShell](https://apps.microsoft.com/detail/9MZ1SNWT0N5D?hl=en-us&gl=MX&ocid=pdpshare).  
Como pasos adicionales, para poder trabajar con repositorios (como este) necesitaré descargar dos herramientas más, [Visual Studio Code](https://code.visualstudio.com/) y [Git](https://git-scm.com/).

- Dentro de la **Windows Terminal** ve a `Settings > Startup` y en la opción `Default Profile`, selecciona **PowerShell**. Después en `Default terminal application` selecciona **Windows Terminal** y clic en el botón `Save`.

Se puede cambiar los colores de la terminal, esto es totalmente opcional.

- En `Settings > Color schemes`. Ahí se puede elegir alguno de los temas que vienen por defecto.
- También se puede buscar algún tema o crear uno por cuenta propia. En esta ocasión usaré alguno de la página [**Windows Terminal Themes**](https://windowsterminalthemes.dev/)
- Clic en `Open JSON file`
- Ve a `"schemes":[]`
- Dentro de los corchetes `[ ]` escribe el Color Scheme
- Gardas los cambios

Ahora en `Settings > Appearance` activa la opción "Use acrylic material in the tab row"

Lo siguiente es instalar un *Prompt theme* que será [**Oh My Posh**](https://ohmyposh.dev/)

- Dentro de la terminal ejecuta:

~~~pwsh
 winget install JanDeDobbeleer.OhMyPosh --source winget
~~~

- Ahora ejecuta:

~~~pwsh
oh-my-posh font install
~~~

- Puedes seleccionar cualquiera, la documentación recomienda utilizar **Meslo**
- Ahora ve a `Settings > Defaults > Appearance` en **Font face** debajo de **Text** selecciona la fuente que elegiste antes
- Clic en `Save`

Ahora configuraremos *Oh My Posh*. Consulta la [documentación](https://ohmyposh.dev/docs/installation/prompt) para más información

1. Ejecuta:

~~~pwsh
notepad $PROFILE
~~~

2. Si lo anterior te da error, ejecuta:

~~~pwsh
New-Item -Path $PROFILE -Type File -Force
~~~

3. vuelve a ejecutar el paso 1
4. Dentro del **$PROFILE** agrega:

~~~pwsh
oh-my-posh init pwsh | Invoke-Expression
~~~

6. Ahora ejecuta:

~~~pwsh
. $PROFILE
~~~

Con esto hecho, la terminal ya se verá diferente. Podemos elegir el tema que usará la terminal, puedes ver los [temas aquí](https://ohmyposh.dev/docs/themes). Yo usaré el tema ***space***

- Agrega `--config 'space'` al $PROFILE, debe verse así:

~~~pwsh
oh-my-posh init pwsh --config 'space' | Invoke-Expression
~~~

## Terminal Icons

Ahora, agregaré íconos a la terminal, para eso utilizaré el módulo [**Terminal-Icons**](https://github.com/devblackops/Terminal-Icons)

- Ejecuta:

~~~pwsh
Install-Module -Name Terminal-Icons -Repository PSGallery
~~~

- Te preguntará si estas seguro de instalar los módulos, escribe la opción `A` y enter
- Ahora, dentro de el archivo **$PROFILE**, hay que agregar la línea:

~~~pwsh
Import-Module -Name Terminal-Icons
~~~

## PSReadLine

Ahora cambiaré el comportamiento de un módulo que ya viene integrado en la nueva PowerShell [PSReadLine](https://learn.microsoft.com/es-es/powershell/module/psreadline/?view=powershell-7.5)

- Agrega al archivo $PROFILE:

~~~pwsh
Set-PSReadLineOption -PredictionViewStyle ListView
~~~
