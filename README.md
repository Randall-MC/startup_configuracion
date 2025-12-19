# Windows 11 - Configuración de entorno de desarrollo JavaScript

> [!NOTE]
> Esta es la configuración que estoy utilizando a la fecha 12 / 17 / 2025 para trabajar con JavaScript

Con este repositorio pretendo tener una guía para poder configurar un entorno de desarrollo para Windows 11 desde cero, con las herramientas que suelo utilizar para esta plataforma. Quizá este trabajo pueda ayudar a otras personas y no solo a mi. La intención principal es no tener que volver a buscar toda esta información por separado y hacer más rápido este proceso.

---

## Índice

- [Windows 11 - Configuración de entorno de desarrollo JavaScript](#windows-11---configuración-de-entorno-de-desarrollo-javascript)
  - [Índice](#índice)
  - [Herramientas necesarias](#herramientas-necesarias)
  - [Configuración de la Windows Terminal](#configuración-de-la-windows-terminal)
    - [Comportamiento](#comportamiento)
    - [Apariencia](#apariencia)
    - [Agregar Color Schemes](#agregar-color-schemes)
  - [Oh My Posh](#oh-my-posh)
  - [Terminal Icons](#terminal-icons)
  - [Fastfetch](#fastfetch)
  - [PSReadLine](#psreadline)
  - [Entorno de desarrollo con JavaScript](#entorno-de-desarrollo-con-javascript)
    - [fnm - Fast Node Manager](#fnm---fast-node-manager)
    - [Utilización](#utilización)
  - [Configurar Git](#configurar-git)
    - [Configuración de identidad](#configuración-de-identidad)
    - [Alias](#alias)
    - [Generando una nueva clave SSH y agregándola al ssh-agent](#generando-una-nueva-clave-ssh-y-agregándola-al-ssh-agent)
      - [Recursos](#recursos)

---

## Herramientas necesarias

> [!IMPORTANT]
> Antes de comenzar, necesitas instalar

- [**Windows Terminal**](https://apps.microsoft.com/detail/9N0DX20HK701?hl=en-us&gl=MX&ocid=pdpshare)
- [**PowerShell**](https://apps.microsoft.com/detail/9MZ1SNWT0N5D?hl=en-us&gl=MX&ocid=pdpshare)
- [Visual Studio Code](https://code.visualstudio.com/)
- [Git](https://git-scm.com/)

## Configuración de la Windows Terminal

En una ventana de la terminal, en la parte superior haz clic en el símbolo `∨` a lado de `+` y después seleccionas **Configuración** o puedes presionar la combinación de teclas `Ctrl + ,` se desplegará un menú, ahí:

### Comportamiento

- En la pestaña **Inicio**
- En **Perfil predeterminado**
- Selecciona **PowerShell**
- En **Aplicación de terminal predeterminada**
- Selecciona **Terminal Windows**
- Clic en el botón **Guardar**

### Apariencia

- Presiona la combinación de teclas `Ctrl + ,`
- Clic en la pestaña **Apariencia**
- Activa la opción **Usar material acrílico en la fila de tabulación**
- Ahora, clic en la pestaña **Valores predeterminados**
- En **Apariencia**
- En la sección **Cursor**
- Clic en **Forma del cursor**
- Selecciona el que más te guste
- Clic en el desplegable `∨` **Color del cursor**
- Selecciona el que más te guste
- Ahora en la sección **Transparencia**
- Modifica la opción **Opacidad del fondo** entre un 80% y 90%
- Activa la opción **Habilitar material acrílico**
- Clic en el botón **Guardar**

### Agregar Color Schemes

Yo voy a usar algunas _combinaciones de colores_ de la página [**Windows Terminal Themes**](https://windowsterminalthemes.dev/), seleccionas un tema, lo copias y después lo agregas dentro del archivo `settings.json`.

- Presiona `Ctrl + ,`
- Clic en el botón `⚙️ Abrir archivo JSON`
- Busca `"schemes": []`
- Dentro de `[]` pega la combinación de colores que hayas copiado
- Y guardas los cambios

Para usar cualquier combinación de colores agregada en el archivo JSON

- Presiona la combinación de teclas `Ctrl + ,`
- Ahora, clic en la pestaña **Valores predeterminados**
- En **Apariencia**
- En la opción **Combinación de colores**
- Selecciona la combinación de colores
- Clic en el botón **Guardar**

---

## Oh My Posh

Lo siguiente es instalar un _Prompt theme_, que será [**Oh My Posh**](https://ohmyposh.dev/). Dentro de la terminal ejecuta:

```pwsh
 winget install JanDeDobbeleer.OhMyPosh --source winget
```

Para que los íconos se muestren correctamente se necesita instalar alguna fuente que tenga soporte estos, en la [documentación de Oh-My-Posh](https://ohmyposh.dev/docs/installation/prompt) se recomienda utilizar **Meslo**. Ejecuta

```pwsh
oh-my-posh font install
```

- Selecciona una fuente
- Presiona la combinación de teclas `Ctrl + ,`
- Clic en la pestaña **Valores predeterminados**
- En **Apariencia**
- En **Font face**
- Selecciona la fuente que elegiste antes
- Clic en el botón **Guardar**

Ahora configuraremos _Oh My Posh_. Consulta la [documentación](https://ohmyposh.dev/docs/installation/prompt) para más información

- Ejecuta:

```pwsh
notepad $PROFILE
```

> [!CAUTION]
> Si al ejecutar el comando anterior te da un error, entonces ejecuta:

```pwsh
New-Item -Path $PROFILE -Type File -Force
```

Para que _Oh my posh_ se ejecute cada vez que usamos la terminal, agrega la siguiente línea dentro del archivo _...profile.ps1_

```pwsh
oh-my-posh init pwsh | Invoke-Expression
```

- En la terminal ejecuta

```pwsh
. $PROFILE
```

Con esto hecho, la terminal ya se verá diferente. Podemos elegir el tema que usará la terminal, puedes ver los [temas aquí](https://ohmyposh.dev/docs/themes). Yo usaré el tema **_space_**

```pwsh
oh-my-posh init pwsh --config 'space' | Invoke-Expression
```

---

## Terminal Icons

Ahora, agregaré íconos a la terminal, para eso utilizaré el módulo [**Terminal-Icons**](https://github.com/devblackops/Terminal-Icons)

- Ejecuta:

```pwsh
Install-Module -Name Terminal-Icons -Repository PSGallery
```

- Te preguntará si estas seguro de instalar los módulos, escribe la opción `Y` y enter
- Ahora, dentro de el archivo _...profile.ps1_, hay que agregar la línea:

```pwsh
Import-Module -Name Terminal-Icons
```

---

## Fastfetch

Fastfetch es una herramienta para obtener información del sistema (como recursos cpu, memoria) y mostrarla visualmente de manera atractiva.

- Instalación

```pwsh
winget install fastfetch
```

> [!WARNING]
> Reemplaza "_usuario_" por tu usuario 😒

- Navega hacia `C:\Users\usuario`
- Crea una nueva carpeta con el nombre `.config`
- Clic derecho sobre `.config`
- Click en **Mostrar Más opciones**
- Clic en **Propiedades**
- Activa la opción **Oculto** ⏹️
- Clic en el botón **Aplicar**
- Clic en el botón **Aceptar**

Dentro de la carpeta `.config`

- Crea una nueva carpeta con el nombre `fastfetch`
- Copia los archivos `ascii.txt` y `config.jsonc` [(los encuentras aquí)](./fastfetch)
- Dentro del archivo `config.jsonc`
- Reemplaza `%USERPROFILE%` por tu nombre de usuario

Agrega lo siguiente dentro del archivo _...profile.ps1_

```bash
# Minimal profile: UTF‑8 + Oh My Posh (if installed) + Fastfetch with explicit config path
try {
    [Console]::InputEncoding  = [System.Text.Encoding]::UTF8
    [Console]::OutputEncoding = [System.Text.Encoding]::UTF8
    $OutputEncoding = [System.Text.UTF8Encoding]::new($false)
    chcp 65001 > $null
} catch {}

Clear-Host

# Force Fastfetch to use YOUR config every time (bypass path confusion)
if (Get-Command fastfetch -ErrorAction SilentlyContinue) {
    fastfetch -c "C:/Users/%USERPROFILE%/.config/fastfetch/config.jsonc"
}
```

Reemplaza `%USERPROFILE%` por tu nombre de usuario

---

## PSReadLine

> [!TIP]
> Esto es opcional

Ahora cambiaré el comportamiento de un módulo que ya viene integrado en la nueva PowerShell [PSReadLine](https://learn.microsoft.com/es-es/powershell/module/psreadline/?view=powershell-7.5)

- Agrega al archivo _...profile.ps1_:

```pwsh
Set-PSReadLineOption -PredictionViewStyle ListView
```

---

## Entorno de desarrollo con JavaScript

### fnm - Fast Node Manager

Para poder instalar [**fnm**](https://github.com/Schniz/fnm) ejecuta el siguiente comando

```pwsh
winget install Schniz.fnm
```

Después agrega la siguiente línea al archivo de tu perfil (_profile_)

```pwsh
fnm env --use-on-cd --shell powershell | Out-String | Invoke-Expression
```

### Utilización

Para más información sobre cómo utilizar **fnm**, [haz clic aquí](https://github.com/Schniz/fnm).  
Por ejemplo, para instalar la última versión _LTS_

```pwsh
fnm install --lts
```

Para comprobar que se ha instalado _node_

```pwsh
node --version
```

---

## Configurar Git

> [!WARNING]
> Esta configuración puede variar según cada persona

### Configuración de identidad

```bash
git config --global user.name "tu nombre"

git config --global user.email "tucorreo@ejemplo.com"
```

### Alias

Estos alias los utilizo mucho y los obtuve del curso de [**GIT+GitHub: Todo un sistema de control de versiones de cero**](https://www.udemy.com/course/git-github/) impartido por el grande _Fernando Herrera_. Estos se encuentran en [GitHub Gist](https://gist.github.com/Klerith/0acf18bbece7923bcac55edb71b03c2b), creo que toda esta información es pública así que no debería tener problemas por esto, pero si en su defecto existe algún error, por favor háganlo saber tan pronto sea posible.

```bash
git config --global alias.lg "log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all"

git config --global alias.s "status -sb"
```

### Generando una nueva clave SSH y agregándola al ssh-agent

Para más información, puedes consultar la [documentación oficial de GitHub](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

**Paso 1**: Generar una llave SSH

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

**Paso 2**: Agregar la clave al agente SSH

- En una nueva ventana de laterminal con permisos de administrador (Solo para este paso), inicia el agente SSH

```bash
# start the ssh-agent in the background
Get-Service -Name ssh-agent | Set-Service -StartupType Manual
Start-Service ssh-agent
```

- En una ventana de la terminal sin permisos de administrador, agrega tu clave privada al agente:

```bash
ssh-add ~/.ssh/id_ed25519
```

**Paso 3**: Agregar clave pública a GitHub

- Copia tu clave pública:

```bash
cat ~/.ssh/id_ed25519.pub | clip
```

- Ahora agrégala a tu cuenta de GitHub en **Configuración** > **SSH** y **claves SSH**.

**Paso 4**: Probar la conexión

```bash
ssh -T git@github.com
```

- Si tienes éxito, verás un mensaje como: ¡Hola `<username>`! Te has autenticado con éxito.

---

#### Recursos

Tomé ideas de algunos vídeos para poder realizar este trabajo. También claro de la documentación oficial de los recursos que menciono, los cuales dejé enlaces para esos recursos.

[Cómo configurar tu terminal para que sea asombrosa en Windows 11](https://www.youtube.com/watch?v=6SGIFVJ5Izs) - HolaMundo

[Your terminal is boring… Fix it!](https://www.youtube.com/watch?v=z3NpVq-y6jU) - SleepyCatHey
