# Uso de VS Code y WSL

Para acceder al filesystem de WSL mediante VS Code hay dos formas de hacerlo.

<include from="wsl.md" element-id="wsl-install-warning" />

## Acceso a WSL remoto

Para empezar debemos instalar dos extensiones:

- **Remote Explorer**

<img src="wsl-vs-code-1.png" alt="Remote Explorer extension" width="600" />

- **Remote Development**

<img src="wsl-vs-code-2.png" alt="Remote Development extension" width="600" />

Luego debemos acceder al filesystem de WSL utilizando las extensiones previamente mencionadas.
Para ello clickeamos el nuevo ícono de la barra lateral:

<img src="wsl-vs-code-3.png" alt="Remote Explorer icon" width="300" />

Continuando, abrir el menu desplegable y seleccionar la opción que mencione a `WSL`, en mi caso `WSL Targets`.
_Ignorar las otras opciones_.

<img src="wsl-vs-code-4.png" alt="Remote Explorer WSL Target" width="600" />

<tip>
En caso que no aparezca el menú desplegable, verificar que dentro de la lista inferior aparezca una distribución (es decir una opción) con la palabra <strong>Ubuntu</strong>. 

Puede que aparezcan otras opciones dependiendo de la distribución instalada.
</tip>

Ahora, buscar la distribución a la que queremos conectarnos y clickear el ícono de la flecha.

<img src="wsl-vs-code-5.png" alt="Remote Explorer WSL connection" width="300" />

<tip>
Prestar atención a los popups de la esquina inferior derecha. Si indican algo acerca de instalar un addon de WSL, hacerlo.
</tip>

<warning>
Si no aparece la distribución de Linux a la que queremos conectarnos, verificar que esté instalada.

Para instalar una distribución de Linux en WSL (Ubuntu en particular), clickear <a href="gcc-windows.md" anchor="instalaci-n-de-ubuntu">acá</a>.
</warning>

Lo único que nos falta hacer es abrir la carpeta que deseemos. En mi caso creé una previamente llamada `PI` para una
mejor organización.

<tip>
<a href="wsl.md#via-windows-explorer-interfaz-gr-fica">Cómo crear carpetas dentro de WSL desde Windows.</a>
</tip>

<img src="wsl-vs-code-6.png" alt="Remote Explorer WSL folder" width="600" />

<img src="wsl-vs-code-7.png" alt="Remote Explorer WSL folder" width="600" />

<tip>
Puede ser que aparezca un popup solicitando permisos para continuar. Aceptar.
<img src="wsl-vs-code-9.png" alt="Trust the Authors popup" width="600" />
</tip>

Por último, mi setup de VS Code conectado a WSL quedó así:

<img src="wsl-vs-code-8.png" alt="Remote Explorer WSL VS Code setup" width="600" />

Ahora podemos utilizar VS Code para programar, crear archivos y carpetas, y estos se van a guardar en WSL, entre otras
tantas funcionalidades.

<tip>
<a href="https://github.com/RehanSaeed/Bash-Cheat-Sheet">Cheat sheet de comandos Bash.</a>
</tip>

<note>
Esta es la forma recomendada de acceder al filesystem de WSL via VS Code.
</note>

## Acceso a WSL desde Windows

La otra opción consiste en abrir la carpeta del filesystem de WSL buscándola directamente en el explorador de archivos
de VS Code dentro del path `\\\\wsl$`, y trabajar allí como si fuera una carpeta más. Es decir, no conectarnos
remotamente
a WSL, sino directamente abrir carpetas de dicho filesystem.

<warning>
Esta no es la forma recomendada.
</warning>
