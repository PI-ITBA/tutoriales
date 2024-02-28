# Instalación y uso de VS Code con GCC

VS Code es un editor de código fuente desarrollado por Microsoft para Windows, Linux y macOS. Permite añadir extensiones
para
ampliar su funcionalidad, como por ejemplo, la edición y autocompletado de código en C/C++.

## Instalación de VS Code

Para instalar **VS Code** acceder a su <a href="https://code.visualstudio.com/#alt-downloads" target="_blank">sitio
oficial</a> y descargar el instalador para su sistema operativo.

## Uso de VS Code con GCC

El uso de **VS Code** con **GCC** es idéntico entre los distintos sistemas operativos. Solamente debemos tener
instalado **GCC** en el sistema operativo (ver primeras secciones):

- <a href="gcc-macos.md">Instalación de GCC en **macOS**</a>

- <a href="gcc-linux.md">Instalación de GCC en **Linux**</a>

- <a href="gcc-windows.md">Instalación de GCC en **Windows**</a>

## Uso de VS Code en diferentes sistemas operativos

El uso de **VS Code** es idéntico entre los distintos sistemas operativos, no debiera haber complicaciones. Las únicas
excepciones a esta regla son **Windows sin WSL** y **macOS con procesadores M1 en adelante**, donde el flag `-fsanitize=address`
no detecta leaks de memoria.

### macOS con procesadores M1 en adelante

<a href="vs-code-docker.md">Debemos utilizar **Docker** para compilar y ejecutar el código.</a>

### Windows sin WSL

<a href="wsl.md">Instalar **WSL** en Windows.</a>

## Extensiones recomendadas

**VS Code** permite extender su funcionalidad mediante la instalación de extensiones.
Las mismas se pueden acceder mediante:

1. El ícono de la barra lateral <img src="vscode-terminal-2.png" alt="Extensiones de VS Code" width="100%"/>
2. El menú `View` -> `Extensions`.
3. El atajo `Ctrl + Shift + X`.

Algunas extensiones recomendadas son:

- **C/C++**: Permite la edición de código en
  C/C++. <a href="https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools" target="_blank">Link</a>
- **Prettier**: Formatea el código de forma
  automática. <a href="https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode" target="_blank">
  Link</a>