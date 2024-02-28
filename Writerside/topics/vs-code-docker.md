# Uso de VS Code con Docker

Para utilizar **VS Code** con **Docker** debemos:

- Instalar **Docker** en el sistema operativo.
- Descargar una **imagen de Ubuntu** para usar GCC.
- Configurar **VS Code** para que en cada ejecución utilice esa imagen descargada.

## Instalación de Docker Desktop

Para instalar Docker Desktop ir al sitio oficial de
<a href="https://www.docker.com/products/docker-desktop/">Docker Desktop</a>
y presionar la opción correspondiente a su sistema operativo. En caso de dudas, revisar la sección de
instalación para cada sistema operativo:

- <a href="gcc-macos.md" anchor="instalaci-n-de-docker-desktop">Instalación de Docker en **macOS**.</a>
- <a href="https://docs.docker.com/desktop/install/linux-install/" target="_blank">Instalación de Docker en **Linux**.</a>
- Instalación de Docker en **Windows**: Clickear `Download for Windows`.

## Descarga de la imagen de Ubuntu

No es necesario descargar la imagen de Ubuntu, ya que con **VS Code** y **Docker** podemos descargarla automáticamente
mediante el uso de una extensión.

## Configuración de VS Code

Instalar las siguientes extensiones en **VS Code**:

- **Docker**: Permite la administración de contenedores **Docker**.

<img src="docker-vs-code-1.png" alt="Docker Extension" width="600" />

- **Remote Development**: Permite el desarrollo remoto en **VS Code**.

<img src="docker-vs-code-2.png" alt="Remote Development Extension" width="600" />

- **Dev Containers**: Permite el desarrollo de aplicaciones en contenedores **Docker**.

<img src="docker-vs-code-3.png" alt="Dev Containers Extension" width="600" />


Ahora debemos iniciar el **Docker Daemon**, para ello simplemente abrir **Docker Desktop**.

Luego debemos abrir la carpeta que deseemos en **VS Code** y clickear `Ctrl` + `Shift` + `P`, o en su defecto acceder
directamente via la barra superior, como se indica en la siguiente imagen

<img src="docker-vs-code-4.png" alt="Comandos" width="600" />

y escribir `dev containers open folder` para luego seleccionar la opción `Dev Containers: Open Folder in Container`.

<img src="docker-vs-code-5.png" alt="Open folder" width="600" />

En mi caso la carpeta en cuestión se llama `PI-WINDOWS` y tiene un archivo llamado `test.txt`.

Seleccionar la primer opción

<img src="docker-vs-code-6.png" alt="Archivo de configuración" width="600" />

Seleccionar la primer opción nuevamente

<img src="docker-vs-code-7.png" alt="Template" width="600" />

Buscar `c++` y seleccionar la opción `C++`

<img src="docker-vs-code-8.png" alt="C++" width="600" />

Vamos a usar como base una imagen de **Ubuntu** con **GCC**. En mi caso elegí la opción `ubuntu-22.04` pero se puede
elegir cualquier otra

<img src="docker-vs-code-9.png" alt="Imagen base" width="600" />

Seleccionar la opción `none (default)` para la versión de **CMake**, aunque se puede elegir cualquier otra

<img src="docker-vs-code-10.png" alt="CMake version" width="600" />

Por último, no queremos añadir más configuraciones, por lo que seleccionamos la opción `OK`

<img src="docker-vs-code-11.png" alt="Configuraciones extra" width="600" />

Finalmente, **VS Code** se conectará a **Docker** y abrirá la carpeta en el contenedor en cuestión, quedando
nuestro setup de la siguiente forma

<img src="docker-vs-code-12.png" alt="Conectado a contenedor Docker" width="600" />

<note>
Ahora podemos utilizar <strong>VS Code</strong> para programar, crear archivos y carpetas, y estos se van a guardar en el contenedor,
así como ejecutar el código en el mismo.
</note>

<warning>
<strong>Siempre que se desee utilizar VS Code con Docker se debe abrir la aplicación Docker Desktop previamente.</strong>
</warning>

<tip>
La próxima vez que abramos <strong>VS Code</strong> en la misma carpeta, se conectará automáticamente al contenedor. Es decir, no es necesario
realizar este proceso nuevamente.
</tip>

<warning>
Para conectarse nuevamente a un contenedor, simplemente abrir la carpeta en uno mediante el comando <code>dev containers open folder</code>.
Para desconectarse, clickear el ícono azul de la esquina inferior izquierda y seleccionar <code>Close Remote Connection</code>.
</warning>