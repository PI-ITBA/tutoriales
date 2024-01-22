# Uso de CLion con Pampero

Con los siguientes pasos podrá configurar **CLion** para que utilice el **GCC de Pampero**. 
Cada vez que se genere un ejecutable los archivos fuentes presentes en el ordenador local se cargarán a un directorio
de su usuario de Pampero, por lo tanto es necesaria la conexión a internet para esta modalidad.

<warning>Si no cuenta con CLion instalado consulte primero las secciones

- Registro y Licencia
- Instalación de CLion usando ToolBox App

del tutorial de **Instalación de GCC y Clion** de su sistema operativo.

Puede omitir las referencias a configurar una Toolchain ya que eso se cubre
en este tutorial
</warning>

## Toolchain Remote Host

Presionando el botón del engranaje de la parte superior derecha se abrirá un menú contextual. Clickear en
<shortcut>Settings</shortcut>. Allí elegir 
<shortcut>Build, Execution, Deployment</shortcut>
<shortcut>Toolchains</shortcut> 

Presionar el botón 
<shortcut>+</shortcut>
y luego en
<shortcut>Remote Host</shortcut>.
En la línea de **Credentials** presionar el ícono del engranaje. 
En la ventana **SSH Configurations** que se abrió hacer click en 
<shortcut>+</shortcut> 
y completar con sus credenciales de Pampero. Por ejemplo:

<img src="clion-pampero-1.png" alt="CLion Pampero 1" width="600"/>

Antes de guardar los cambios presionar 
<shortcut>Test Connection</shortcut>
Debería obtener el siguiente mensaje.

<img src="clion-pampero-2.png" alt="CLion Pampero 2" width="300"/>

Presionar 
<shortcut>OK</shortcut> para cerrar el mensaje y presionar 
<shortcut>OK</shortcut>
para volver a la ventana anterior.

Asegurarse que los valores sean `Bundled` y `Detected`
y que no se mencionan errores.
Presionar 
<shortcut>Apply</shortcut>.

<img src="clion-pampero-3.png" alt="CLion Pampero 3" width="600"/>

## CMake Profile

Ahora ir a la sección
<shortcut>CMake</shortcut> del menú izquierdo de 
<shortcut>Build, Execution, Deployment</shortcut>. En el campo **Toolchain**
elegir del menú desplegable el ítem **Remote Host** creado en el paso anterior. 
Asegurarse que el **Build type** del perfil sea **Debug**. 
A este Profile de CMake le daremos el nombre de Pampero. Luego presionar 
<shortcut>Apply</shortcut>.

<img src="clion-pampero-4.png" alt="CLion Pampero 4" width="600"/>

<tip>
Puede tener varios perfiles de CMake, por ejemplo uno que utilice la Toolchain local (el GCC instalado
localmente) y otro que utilice la Toolchain Remote Host (el GCC de Pampero). 

Por ejemplo llamamos Docker
a un Profile además del Profile de nombre Pampero mencionado más arriba
<img src="clion-pampero-5.png" alt="CLion Pampero 5" width="600"/>
</tip>

## Deployment

Ahora ir a la sección
<shortcut>Deployment</shortcut> del menú izquierdo de 
<shortcut>Build, Execution, Deployment</shortcut>.
Estando en la solapa **Connection** presionar el botón
<shortcut>Autodetect</shortcut>
del campo **Root Path**.
Debería ver un path válido de Pampero.

<img src="clion-pampero-6.png" alt="CLion Pampero 6" width="600"/>

Ahora en la solapa **Mappings** revisar el campo **Deployment path**. 
Este es el directorio de Pampero donde serán copiados nuestros archivos fuentes y donde también serán generados los ejecutables.
Puede dejar el autogenerado o cambiarlo por un path identificable como 
<code>pi/clion</code>

<tip>
El path completo que utilizará CLion es la concatenación del 
<b>Root Path</b>
con
<b>Deployment path</b>. 

Es por eso que en <b>Deployment Path</b> sólo debe indicar el path desde su home.
</tip>

Por último presionar 
<shortcut>OK</shortcut>

## Primer uso

Esperar a que CLion complete unas **Background Tasks** que consisten en indexar todos los archivos de encabezados 
presentes en la biblioteca estándar instalada en Pampero.

A partir de ahora, al ejecutar un main se cargarán los archivos necesarios a Pampero y se utilizará el GCC de Pampero
para la creación del ejecutable.

<img src="clion-pampero-7.png" alt="CLion Pampero 7" width="600"/>

Puede consultar los archivos que fueron cargados a Pampero desde la sección 
<shortcut>File Transfer</shortcut>
Por ejemplo puede ver los mensajes:

<code-block lang="plain text">
[05/04/2021 12:09] Upload file '/Users/fmeola/CLionProjects/pi/CMakeLists.txt' to '/afs/it.itba.edu.ar/home/fmeola/pi/clion/CMakeLists.txt'
[05/04/2021 12:09] Upload file '/Users/fmeola/CLionProjects/pi/main.c' to '/afs/it.itba.edu.ar/home/fmeola/pi/clion/main.c'
[05/04/2021 12:09] Upload to Remote Host (1d...) completed in 4 sec, 538 ms: 1 item excluded, 33 files transferred (51.9 kbit/s)
</code-block>

<tip>
En caso de contar con dos o más perfiles de CMake puede cambiarlo desde la esquina superior izquierda.
Aparecerá el nombre del Profile de CMake actual y presionando aparecerá un menú contextual para elegir otro.
De esta forma puede intercambiar rápidamente entre usar el GCC local o el de Pampero.

<img src="clion-pampero-8.png" alt="CLion Pampero 8" width="600"/>
</tip>

<note>
    <p>
        Listo! Ya cuenta con CLion funcionando correctamente con Pampero.
    </p>
</note>
