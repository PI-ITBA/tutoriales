# Instalación de GCC y CLion en Linux

## Uso de apt-get

<tip>
Para este tutorial se utilizó Ubuntu 25.10 Questing
</tip>

<snippet id="apt-get-snippet">

Para instalar la versión estable más reciente de **GCC** y demás utilitarios necesarios por **CLion** ejecute los siguientes comandos:

<code-block lang="console">
sudo apt-get update
</code-block>

<code-block lang="console">
sudo apt install -y build-essential gdb cmake ninja-build tzdata
</code-block>

Al finalizar la instalación verificar que al invocar a

<code-block lang="console">
gcc --version
</code-block>

se obtiene una salida similar a la siguiente:

<code-block lang="plain text">
gcc (Ubuntu 15.2.0-4ubuntu4) 15.2.0
Copyright (C) 2025 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
</code-block>

</snippet>

## Registro y Licencia de CLion

<warning>
A continuación se detalla el proceso de registro y licencia de <strong>CLion</strong>, el mismo
NO está vinculado a la instalación de <strong>GCC</strong>. <br />
<strong>En caso de querer utilizar otro IDE o editor de texto NO es necesario continuar con este tutorial</strong>.
</warning>

<include from="gcc-macos.md" element-id="clion-registro-snippet"/>

## Instalación de CLion usando ToolBox App

<include from="gcc-macos.md" element-id="clion-toolbox-snippet"/>

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
<shortcut>C23</shortcut>

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

<img src="clion-linux-4.png" alt="CLion Linux 4" width="600"/>

Luego abrir el archivo `main.c` y presionar el botón de Play que aparece en el renglón de `int main`. 
En el menú contextual elegir la primera opción de 
<shortcut>Run</shortcut>

<img src="clion-linux-5.png" alt="CLion Linux 5" width="600"/>

El programa se ejecutará y podrá ver la correspondiente salida en la sección de
<shortcut>Run</shortcut>

<img src="clion-linux-6.png" alt="CLion Linux 6" width="600"/>

<include from="gcc-macos.md" element-id="success-gcc-clion"/>
