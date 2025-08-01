# Instalación de GCC y CLion en Windows

Para el uso de **GCC** en **Windows** es necesario una imagen de Linux a través de 
**Windows Subsystem for Linux (WSL)**.
De esta forma podremos utilizar GCC como si estuviéramos utilizando Linux.
Para ello necesitamos:

- Instalar **Windows Subsystem for Linux (WSL)**
- Instalar una **imagen de Ubuntu** para WSL
- **Configurar CLion** para que en cada ejecución utilice esa imagen descargada

<warning>Para el funcionamiento de WSL es necesario que en la PC estén habilitadas las
caracterísiticas de virtualización.

Puede ser que necesite activar la funcionalidad de virtualización desde el BIOS.
</warning>

## Instalación de WSL

Instalar WSL desde la tienda:
<a href="https://apps.microsoft.com/detail/9P9TQF7MRM4R?hl=es-AR">**WSL en Microsoft Store**</a>

<img src="clion-win-1.PNG" alt="CLion Win 1" width="600"/>

La instalación requerirá los permisos de administrador.

Luego abrir la **Terminal** de Windows y ejecutar el siguiente comando

<code-block lang="console">
wsl --status
</code-block>

Debería obtener una salida como la siguiente:

<code-block>
Default Version: 2
</code-block>

<tip>Para más información sobre <b>WSL</b> consultar
<a href="https://learn.microsoft.com/es-mx/windows/wsl/install">
Instalación de Linux en Windows con WSL</a>
</tip>

## Instalación de Ubuntu

Instalar Ubuntu desde la tienda:
<a href="https://apps.microsoft.com/detail/9PDXGNCFSCZV?hl=es-ar">**Ubuntu en Microsoft Store**</a>

<img src="clion-win-2.PNG" alt="CLion Win 2" width="600"/>

Finalizada la instalación abrir la aplicación **Ubuntu**.

## Solución de errores

Pueden surgir errores al ejecutar **WSL**, y para solucionarlos recomendamos seguir los siguientes pasos:

1. Verificar que está activada la funcionalidad de virtualización en el BIOS (el acceso al BIOS varía según el
   fabricante de la PC).
2. Verificar que estén activadas las funcionalidades de virtualización y WSL en Windows. Para ello abrir el **Panel de
   Control**, luego **Programas** y **Características** y finalmente **Activar o desactivar las características de
   Windows**. Otra
   forma de acceder a esta ventana es presionando la tecla de Windows y escribiendo **Características** o **Features**,
   dependiendo del idioma del sistema operativo.

   <img src="clion-win-13.PNG" alt="Open Windows Features" width="600"/>

   Asegurarse de que esté tildada la opción **Plataforma de máquina virtual** y **Subsistema de Windows para Linux**. En
   caso de tener el sistema operativo en inglés, las opciones son **Virtual Machine Platform** y **Windows Subsystem for
   Linux**.

   <img src="clion-win-14.PNG" alt="Toggle Windows Features" width="600"/>

   Finalmente, reiniciar la PC.
3. Si el error persiste, abrir **PowerShell** como administrador y ejecutar el siguiente comando:

   <code-block lang="console">
   dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
   </code-block>

   Luego reiniciar la PC.

<warning>
En caso de que el error persista, consultar la documentación oficial de Microsoft buscando el error específico y enviar
una consulta vía mail a la cátedra adjuntando el error en cuestión.
</warning>

### Creación de usuario

Luego de abrir la aplicación Ubuntu y esperar unos instantes verá que la terminal le solicita **crear un usuario**.

Complete un usuario, contraseña y luego repita la contraseña ingresada.

<img src="clion-win-3.PNG" alt="CLion Win 3" width="600"/>

### Uso de apt-get en la consola de Ubuntu

<include from="gcc-linux.md" element-id="apt-get-snippet"/>

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
En este ejemplo será `C:\Users\fmeola\pi`

Y en **Language standard** seleccionar
<shortcut>C23</shortcut>

Para crear el proyecto presionar
<shortcut>Create</shortcut>

<img src="clion-win-4.PNG" alt="CLion Win 4" width="600"/>

**CLion** se compone de una ventana con varias secciones. La sección
<shortcut>Project</shortcut>
de la izquierda cuenta con el árbol de archivos del proyecto. Encontrará dos archivos relevantes:
- `main.c` El punto de entrada de la aplicación
- `CMakeLists.txt` El archivo de configuración para crear los ejecutables (los parámetros del gcc, archivos fuentes, flags, nombres de los ejecutables, etc.).

Presionando el botón del engranaje de la parte superior derecha se abrirá un menú contextual. Clickear en
<shortcut>Settings</shortcut>. Allí elegir 
<shortcut>Build, Execution, Deployment</shortcut>
<shortcut>Toolchains</shortcut> 

<img src="clion-win-5.PNG" alt="CLion Win 5" width="600"/>

En
<shortcut>Toolchains</shortcut>
presionar el botón
<shortcut>+</shortcut>
y luego seleccionar
<shortcut>WSL</shortcut>

<img src="clion-win-6.PNG" alt="CLion Win 6" width="200"/>

En el campo **Toolset** asegurarse de elegir
<code>Ubuntu</code>. Debería ver algo así:

<img src="clion-win-7.PNG" alt="CLion Win 7" width="600"/>

Presionar
<shortcut>Apply</shortcut> para guardar los cambios.

Ahora ir a la sección
<shortcut>CMake</shortcut> del menú izquierdo de 
<shortcut>Build, Execution, Deployment</shortcut>. 
Asegurarse de contar con al menos un profile que tenga en el campo **Toolchain**
el ítem **WSL** creado en el paso anterior. 
Asegurarse que el **Build type** del perfil sea **Debug**. 
De haber realizado un cambio presionar 
<shortcut>Apply</shortcut>.

<tip>En caso de ya contar con un Profile asegurarse que el que utiliza
la Toolchain WSL recién configurada esté 
<b>primero en la lista</b>.

<img src="clion-win-8.PNG" alt="CLion Win 8" width="600"/>

</tip>

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

<img src="clion-win-9.PNG" alt="CLion Win 9" width="600"/>

De vuelta en el proyecto editar el archivo `CMakeLists.txt` para que se vea así (donde `pi` es el nombre
del proyecto que definió más arriba)

<code-block lang="cmake">
 <![CDATA[
cmake_minimum_required(VERSION 3.25)
project(pi C)

set(CMAKE_C_FLAGS "-Wall -pedantic -std=c23 -lm -g -fsanitize=address")

add_executable(pi main.c)
]]>
</code-block>

En la sección
<shortcut>CMake</shortcut>
presionar el botón de 
<shortcut>Reload CMake Project</shortcut>

<img src="clion-win-10.PNG" alt="CLion Win 10" width="600"/>

Luego abrir el archivo `main.c` y presionar el botón de Play que aparece en el renglón de `int main`.
En el menú contextual elegir la primera opción de
<shortcut>Run</shortcut>

<img src="clion-win-11.PNG" alt="CLion Win 11" width="600"/>

El programa se ejecutará y podrá ver la correspondiente salida en la sección de
<shortcut>Run</shortcut>

<img src="clion-win-12.PNG" alt="CLion Win 12" width="600"/>

<include from="gcc-macos.md" element-id="success-gcc-clion"/>

<tip>Para más información sobre <b>WSL en CLion</b> consultar
<a href="https://www.jetbrains.com/help/clion/how-to-use-wsl-development-environment-in-product.html#wsl-tooclhain">
WSL2</a>
</tip>
