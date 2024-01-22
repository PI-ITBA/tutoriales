# Instalación de GCC y CLion en Linux

## Uso de apt-get

Para instalar la versión estable más reciente de **GCC** y demás utilitarios necesarios por **CLion** ejecute los siguientes comandos:

<code-block lang="console">
sudo apt-get update
</code-block>

<code-block lang="console">
sudo apt-get install -y build-essential gcc g++ gdb clang make ninja-build cmake autoconf automake libtool valgrind locales-all dos2unix rsync tar python2 python2-dev
</code-block>

Al finalizar la instalación verificar que al invocar a

<code-block lang="console">
gcc --version
</code-block>

se obtiene una salida similar a la siguiente:

<code-block lang="plain text">
gcc (Ubuntu 11.4.0-1ubuntu1~22.04) 11.4.0
Copyright (C) 2021 Free Software Foundation, Inc.
This is free software; see the source for copying conditions. There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
</code-block>

## Registro y Licencia

**CLion** requiere una licencia. Los alumnos pueden registrarse en 
<a href="https://www.jetbrains.com/shop/eform/students">**Productos JetBrains para el aprendizaje**</a>
con su mail **@itba.edu.ar** y así obtener una **licencia gratuita** para utilizar CLion y demás aplicaciones
de JetBrains de forma gratuita.

## Instalación de CLion usando ToolBox App

Para instalar **CLion** recomendamos utilizar **Toolbox App**.

Puede consultar el siguiente tutorial:

<a href="https://www.jetbrains.com/help/clion/installation-guide.html#toolbox">Install using the Toolbox App</a>.

## Configuración de CLion

Una vez finalizada la instalación, abrir **CLion** y presionar el botón 
<shortcut>New Project</shortcut>

En la barra izquierda seleccionar 
<shortcut>C Executable</shortcut>

En 
<shortcut>Location</shortcut> 
indicar el path donde estará ubicado el proyecto. 
En este ejemplo será `/home/fmeola/pi`

Y en **Language standard** seleccionar 
<shortcut>C99</shortcut>

Para crear el proyecto presionar 
<shortcut>Create</shortcut>

<img src="clion-linux-1.png" alt="CLion Linux 1" width="600"/>

Aparecerá un diálogo 
<shortcut>Open Project Wizard</shortcut>
donde debe asegurarse que los valores sean `Bundled` y `Detected` 
y que no se mencionan errores.
Presionar
<shortcut>OK</shortcut>

<img src="clion-linux-2.png" alt="CLion Linux 2" width="600"/>

<tip>
Si no aparece el diálogo anterior puede consultarlo desde
<shortcut>Settings</shortcut>
<shortcut>Build, Execution, Deployment</shortcut>
<shortcut>Toolchains</shortcut>
</tip>

**CLion** se compone de una ventana con varias secciones. La sección 
<shortcut>Project</shortcut>
de la izquierda cuenta con el árbol de archivos del proyecto. Encontrará dos archivos relevantes:
- `main.c` El punto de entrada de la aplicación
- `CMakeLists.txt` El archivo de configuración para crear los ejecutables (los parámetros del gcc, archivos fuentes, flags, nombres de los ejecutables, etc.).

Presionando el botón del engranaje de la parte superior derecha se abrirá un menú contextual. Clickear en
<shortcut>Settings</shortcut>. Allí elegir
<shortcut>Build, Execution, Deployment</shortcut>
<shortcut>Dynamic Analysis Tools</shortcut> 
y por último
<shortcut>Sanitizers</shortcut>

Allí destildar la opción 
<shortcut>Use visual representation for Sanitizer's output</shortcut>
y presionar
<shortcut>OK</shortcut>

<img src="clion-linux-3.png" alt="CLion Linux 3" width="600"/>

De vuelta en el proyecto editar el archivo `CMakeLists.txt` para que se vea así (donde `pi` es el nombre
del proyecto que definió más arriba)

<code-block lang="cmake">
<![CDATA[
cmake_minimum_required(VERSION 3.27)
project(pi C)

set(CMAKE_C_FLAGS "-Wall -pedantic -std=c99 -lm -g -fsanitize=address")

add_executable(pi main.c)
]]>
</code-block>

En la sección 
<shortcut>CMake</shortcut>
presionar el botón de 
<shortcut>Reload CMake Project</shortcut>

<img src="clion-linux-4.png" alt="CLion Linux 4" width="600"/>

Luego abrir el archivo `main.c` y presionar el botón de Play que aparece en el renglón de `int main`. 
En el menú contextual elegir la primera opción de 
<shortcut>Run</shortcut>

<img src="clion-linux-5.png" alt="CLion Linux 5" width="600"/>

El programa se ejecutará y podrá ver la correspondiente salida en la sección de
<shortcut>Run</shortcut>

<img src="clion-linux-6.png" alt="CLion Linux 6" width="600"/>

<note>
    <p>
        Listo! Ya cuenta con GCC y CLion funcionando correctamente.
    </p>
</note>