# Instalación de GCC y CLion en macOS

Para el uso de **GCC** en **macOS** es necesario un contenedor Linux creado con Docker.
De esta forma podremos utilizar GCC como si estuviéramos utilizando Linux.
Para ello necesitamos:

- Instalar **Docker Desktop**
- Descargar una **imagen de Ubuntu** para usar GCC
- **Configurar CLion** para que en cada ejecución utilice esa imagen descargada

## Instalación de Docker Desktop

Para instalar Docker Desktop ir al sitio oficial de
<a href="https://www.docker.com/products/docker-desktop/">Docker Desktop</a>
y presionar **Download for Mac**

<img src="clion-mac-1.png" alt="CLion Mac 1" width="600"/>

<tip>Revisar que está realizando la descarga para la arquitectura correcta 
(Elegir Apple Chip para los ordenadores con procesadores M1 o superior)</tip>

Abrir el **Docker.dmg** y arrastrar la aplicación Docker a la carpeta de Aplicaciones.
Abrir la carpeta Aplicaciones y luego abrir Docker.
Seguir los pasos necesarios para la instalación.

<img src="clion-mac-1A.png" alt="CLion Mac 1A" width="600"/>

## Descarga de la imagen de Ubuntu

<warning>
A continuación se detalla el proceso de descarga de una imagen que posee los utilitarios necesarios para utilizar GCC
y CLion. <br />
<strong>En caso de querer utilizar otro IDE o editor de texto NO es necesario continuar con este tutorial</strong>.
</warning>

Una vez instalado Docker, crearemos un archivo de texto llamado `Dockerfile` (sin extensión)
que contiene los comandos para descargar e instalar sobre una imagen de Ubuntu la versión estable más reciente
de **GCC** y demás utilitarios necesarios por **CLion**. Copiar el siguiente contenido en el archivo:

<code-block lang="docker">
<![CDATA[
FROM gcc:15

ENV DEBIAN_FRONTEND="noninteractive"

RUN apt-get update && apt-get install -y --no-install-recommends \
gdb \
cmake \
ninja-build \
make \
tzdata \
&& rm -rf /var/lib/apt/lists/*
]]>
</code-block>

Con la aplicación Docker en ejecución abrir la **Terminal** de macOS y navegar al directorio donde se encuentra el
archivo
<code>Dockerfile</code>. Ejecutar el siguiente comando:

<code-block>
docker build -t pi:15 -f Dockerfile .
</code-block>

Una vez terminado ya cuenta con la imagen de Ubuntu descargada.

## Registro y Licencia de CLion

<snippet id="clion-registro-snippet">

**CLion** ofrece una licencia **"Free for non-commercial use"**.

</snippet>

## Instalación de CLion usando ToolBox App

<snippet id="clion-toolbox-snippet">

Para instalar **CLion** recomendamos utilizar **Toolbox App**.

Puede consultar el siguiente tutorial:

<a href="https://www.jetbrains.com/help/clion/installation-guide.html#toolbox">Install using the Toolbox App</a>.

</snippet>

## Configuración de CLion

Una vez finalizada la instalación, abrir **CLion** y presionar el botón
<shortcut>New Project</shortcut>

En la barra izquierda seleccionar
<shortcut>C Executable</shortcut>

En
<shortcut>Location</shortcut> 
indicar el path donde estará ubicado el proyecto. 
En este ejemplo será `/Users/fmeola/pi`

Y en **Language standard** seleccionar
<shortcut>C23</shortcut>

Para crear el proyecto presionar
<shortcut>Create</shortcut>

<img src="clion-mac-2.png" alt="CLion Mac 2" width="600"/>

**CLion** se compone de una ventana con varias secciones. La sección
<shortcut>Project</shortcut>
de la izquierda cuenta con el árbol de archivos del proyecto. Encontrará dos archivos relevantes:
- `main.c` El punto de entrada de la aplicación
- `CMakeLists.txt` El archivo de configuración para crear los ejecutables (los parámetros del gcc, archivos fuentes, flags, nombres de los ejecutables, etc.).

Presionando el botón del engranaje de la parte superior derecha se abrirá un menú contextual. Clickear en
<shortcut>Settings</shortcut>. Allí elegir 
<shortcut>Build, Execution, Deployment</shortcut>
<shortcut>Toolchains</shortcut> 

<img src="clion-mac-3.png" alt="CLion Mac 3" width="200"/>

<img src="clion-mac-4.png" alt="CLion Mac 4" width="600"/>

En
<shortcut>Toolchains</shortcut>
presionar el botón
<shortcut>+</shortcut>
y luego seleccionar
<shortcut>Docker</shortcut>

<img src="clion-mac-5.png" alt="CLion Mac 5" width="200"/>

En el campo **Image** asegurarse de elegir
<code>pi:15</code>. Debería ver algo así:

<img src="clion-mac-6.png" alt="CLion Mac 6" width="600"/>

Presionar
<shortcut>Apply</shortcut> para guardar los cambios.

Ahora ir a la sección
<shortcut>CMake</shortcut> del menú izquierdo de 
<shortcut>Build, Execution, Deployment</shortcut>. 
Asegurarse de contar con al menos un profile que tenga en el campo **Toolchain**
el ítem **Docker** creado en el paso anterior. 
Asegurarse que el **Build type** del perfil sea **Debug**. 
De haber realizado un cambio presionar 
<shortcut>Apply</shortcut>.

<tip>En caso de ya contar con un Profile asegurarse que el que utiliza
la Toolchain Docker recién configurada esté primero en la lista.
</tip>

<img src="clion-mac-6a.png" alt="CLion Mac 6A" width="600"/>

Siguiendo en la misma ventana, ahora en el menú izquierdo bajo la misma sección
<shortcut>Build, Execution, Deployment</shortcut>
ir a
<shortcut>Dynamic Analysis Tools</shortcut> 
y luego a
<shortcut>Sanitizers</shortcut>

Allí destildar la opción
<shortcut>Use visual representation for Sanitizer's output</shortcut>
y presionar
<shortcut>OK</shortcut> para guardar los cambios y cerrar la ventana.

<img src="clion-mac-7.png" alt="CLion Mac 7" width="600"/>

De vuelta en el proyecto editar el archivo `CMakeLists.txt` para que se vea así (donde `pi` es el nombre
del proyecto que definió más arriba)

<code-block lang="cmake">
 <![CDATA[
cmake_minimum_required(VERSION 3.31)
project(pi C)

set(CMAKE_C_FLAGS "-Wall -Wextra -pedantic -std=c23 -lm -g -fsanitize=address")

add_executable(pi main.c)
]]>
</code-block>

En la sección
<shortcut>CMake</shortcut>
presionar el botón de 
<shortcut>Reload CMake Project</shortcut>

<img src="clion-mac-8.png" alt="CLion Mac 8" width="600"/>

Luego abrir el archivo `main.c` y presionar el botón de Play que aparece en el renglón de `int main`.
En el menú contextual elegir la primera opción de
<shortcut>Run</shortcut>

<img src="clion-mac-9.png" alt="CLion Mac 9" width="600"/>

El programa se ejecutará y podrá ver la correspondiente salida en la sección de
<shortcut>Run</shortcut>

<img src="clion-mac-10.png" alt="CLion Mac 10" width="600"/>

<note id="success-gcc-clion">
    <p>
        Listo! Ya cuenta con GCC y CLion funcionando correctamente.
    </p>
</note>

<tip>Para más información consultar
<a href="https://www.jetbrains.com/help/clion/clion-toolchains-in-docker.html#sample-dockerfile">
Docker toolchain</a>
</tip>
