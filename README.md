# Windows 11 - Configuración de entorno de desarrollo JavaScript

> [!NOTE]
> Esta es la configuración que estoy utilizando a la fecha 12 / 17 / 2025 para trabajar con JavaScript

Con este repositorio pretendo tener una guía para poder configurar un entorno de desarrollo para Windows 11 desde cero, con las herramientas que suelo utilizar para esta plataforma. Quizá este trabajo pueda ayudar a otras personas y no solo a mi. La intención principal es no tener que volver a buscar toda esta información por separado y hacer más rápido este proceso.

- [Windows 11 - Configuración de entorno de desarrollo JavaScript](#windows-11---configuración-de-entorno-de-desarrollo-javascript)
  - [Herramientas necesarias](#herramientas-necesarias)
  - [Configuración de la Windows Terminal](#configuración-de-la-windows-terminal)
    - [Comportamiento](#comportamiento)
    - [Apariencia](#apariencia)
    - [Agregar Color Schemes](#agregar-color-schemes)
  - [Oh My Posh](#oh-my-posh)
  - [Terminal Icons](#terminal-icons)
  - [PSReadLine](#psreadline)
  - [Entorno de desarrollo con JavaScript](#entorno-de-desarrollo-con-javascript)
    - [fnm - Fast Node Manager](#fnm---fast-node-manager)
    - [Utilización](#utilización)
  - [Configurar Git](#configurar-git)
    - [Configuración de identidad](#configuración-de-identidad)
    - [Alias](#alias)
    - [Generando una nueva clave SSH y agregándola al ssh-agent](#generando-una-nueva-clave-ssh-y-agregándola-al-ssh-agent)
  - [Temas](#temas)

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

- Te preguntará si estas seguro de instalar los módulos, escribe la opción `A` y enter
- Ahora, dentro de el archivo _...profile.ps1_, hay que agregar la línea:

```pwsh
Import-Module -Name Terminal-Icons
```

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

- Inicia el agente SSH

```bash
eval "$(ssh-agent -s)"
```

- Agrega tu clave privada al agente:

```bash
ssh-add ~/.ssh/id_ed25519
```

**Paso 3**: Agregar clave pública a GitHub

- Retrieve your public key:

```bash
cat ~/.ssh/id_ed25519.pub
```

- Copia la salida y agrégala a tu cuenta de GitHub en Configuración > SSH y claves GPG.

**Paso 4**: Probar la conexión

```bash
ssh -T git@github.com
```

- Si tienes éxito, verás un mensaje como: ¡Hola `<username>`! Te has autenticado con éxito.

---

## Temas

```json
"schemes":
    [
        {
          "name": "Monokai Vivid",
          "background": "#121212",
          "black": "#121212",
          "blue": "#0443FF",
          "brightBlack": "#838383",
          "brightBlue": "#0443FF",
          "brightCyan": "#51CEFF",
          "brightGreen": "#B1E05F",
          "brightPurple": "#F200F6",
          "brightRed": "#F6669D",
          "brightWhite": "#FFFFFF",
          "brightYellow": "#FFF26D",
          "cursorColor": "#FB0007",
          "cyan": "#01B6ED",
          "foreground": "#F9F9F9",
          "green": "#98E123",
          "purple": "#F800F8",
          "red": "#FA2934",
          "selectionBackground": "#FFFFFF",
          "white": "#FFFFFF",
          "yellow": "#FFF30A"
        },
        {
          "name": "Oceanic-Next",
          "background": "#121B21",
          "black": "#121C21",
          "blue": "#5486C0",
          "brightBlack": "#52606B",
          "brightBlue": "#5486C0",
          "brightCyan": "#50A5A4",
          "brightGreen": "#89BD82",
          "brightPurple": "#B77EB8",
          "brightRed": "#E44754",
          "brightWhite": "#FFFFFF",
          "brightYellow": "#F7BD51",
          "cursorColor": "#B3B8C3",
          "cyan": "#50A5A4",
          "foreground": "#B3B8C3",
          "green": "#89BD82",
          "purple": "#B77EB8",
          "red": "#E44754",
          "selectionBackground": "#3E4953",
          "white": "#FFFFFF",
          "yellow": "#F7BD51"
        },
        {
          "name": "TokyoNight",
          "background": "#16161E",
          "black": "#363B54",
          "blue": "#7AA2F7",
          "brightBlack": "#363B54",
          "brightBlue": "#7AA2F7",
          "brightCyan": "#7DCFFF",
          "brightGreen": "#41A6B5",
          "brightPurple": "#BB9AF7",
          "brightRed": "#F7768E",
          "brightWhite": "#ACB0D0",
          "brightYellow": "#E0AF68",
          "cursorColor": "#FFFFFF",
          "cyan": "#7DCFFF",
          "foreground": "#787C99",
          "green": "#41A6B5",
          "purple": "#BB9AF7",
          "red": "#F7768E",
          "selectionBackground": "#FFFFFF",
          "white": "#787C99",
          "yellow": "#E0AF68"
        },
        {
          "name": "Tomorrow Night",
          "background": "#1D1F21",
          "black": "#000000",
          "blue": "#81A2BE",
          "brightBlack": "#000000",
          "brightBlue": "#81A2BE",
          "brightCyan": "#8ABEB7",
          "brightGreen": "#B5BD68",
          "brightPurple": "#B294BB",
          "brightRed": "#CC6666",
          "brightWhite": "#FFFFFF",
          "brightYellow": "#F0C674",
          "cursorColor": "#C5C8C6",
          "cyan": "#8ABEB7",
          "foreground": "#C5C8C6",
          "green": "#B5BD68",
          "purple": "#B294BB",
          "red": "#CC6666",
          "selectionBackground": "#373B41",
          "white": "#FFFFFF",
          "yellow": "#F0C674"
        },
        {
          "name": "tokyonight",
          "background": "#1A1B26",
          "black": "#15161E",
          "blue": "#7AA2F7",
          "brightBlack": "#414868",
          "brightBlue": "#7AA2F7",
          "brightCyan": "#7DCFFF",
          "brightGreen": "#9ECE6A",
          "brightPurple": "#BB9AF7",
          "brightRed": "#F7768E",
          "brightWhite": "#C0CAF5",
          "brightYellow": "#E0AF68",
          "cursorColor": "#C0CAF5",
          "cyan": "#7DCFFF",
          "foreground": "#C0CAF5",
          "green": "#9ECE6A",
          "purple": "#BB9AF7",
          "red": "#F7768E",
          "selectionBackground": "#33467C",
          "white": "#A9B1D6",
          "yellow": "#E0AF68"
        }
    ],
```
