# WSL - Windows

WSL (Windows Subsystem for Linux) es una capa de compatibilidad para correr aplicaciones de Linux en Windows.

<tip>

- <a href="https://learn.microsoft.com/es-es/windows/wsl/about">¿Qué es WSL?</a>

- <a href="https://learn.microsoft.com/es-es/windows/wsl/compare-versions">Comparación de WSL 1 y WSL 2</a>

</tip>

Lo principal a entender es que WSL es **otro sistema operativo** que corre **dentro de Windows**. Lo que significa que
tiene otro filesystem, otro conjunto de programas, y librerías, por ende, los cambios realizados en uno no afectan al
otro.

## Pasaje de archivos entre Windows y WSL

Se pueden acceder a los archivos de Windows desde WSL y viceversa.

### Via Windows Explorer (interfaz gráfica)

Para acceder a los archivos de WSL desde Windows se debe acceder a la carpeta `\\\\wsl$` desde el explorador de archivos
de Windows.

<img src="wsl-3.png" alt="Acceso a WSL desde Windows" width="600"/>

<img src="wsl-4.png" alt="Acceso a WSL desde Windows" width="600"/>

Luego presionar enter y se abrirá una ventana con las distintas distribuciones de Linux instaladas.

<img src="wsl-5.png" alt="Distribuciones de Linux en WSL" width="600"/>

Los resultados **varían** según la distribución de Linux que se tenga instalada. En este caso se tiene instalada la
distribución de **Ubuntu** versión **20.04**. Y allí es donde vamos a acceder. _Ignorar las demás carpetas._

El nombre dentro de la carpeta `home` es el nombre de usuario que se creó al instalar la distribución de Linux. En este
caso es `octavio`. Accediendo a dicha carpeta se puede ver el filesystem de la distribución de Linux.

<img src="wsl-6.png" alt="Acceso al filesystem de Ubuntu" width="600"/>

En mi caso dispongo de varias carpetas creadas. Para una mejor organización recomiendo crear una carpeta dedicada a la
materia, yo utilicé `PI`.

<img src="wsl-7.png" alt="Acceso al filesystem de Ubuntu" width="600"/>

Luego abriendo otra ventana con el explorador de archivos de Windows se pueden pasar archivos de Windows a WSL y viceversa
mediante `copiar` y `pegar` o directamente `arrastrar y soltar`.

### Via terminal WSL

<tip>
La terminal de WSL se puede acceder al buscar <strong>wsl</strong> en el menú de inicio de Windows.
</tip>

Los archivos de Windows **dentro de WSL** se encuentran en la carpeta `/mnt/c/` (siendo `c` la letra de la unidad de
disco). Puede que dicha
letra difiera en cada sistema, por lo que se puede verificar accediendo directamente al explorador de archivos de
Windows y luego
clickear en `Este Equipo` o `This PC`.

<img src="wsl-1.png" alt="WSL 1" width="600"/>

Una vez dentro de la terminal de WSL se puede acceder
a los archivos de Windows
mediante el comando `cd`:

```bash
cd /mnt/c/
```

<img src="wsl-2.png" alt="WSL Terminal list Windows files" width="600"/>

Luego podemos mover archivos de Windows a WSL o viceversa mediante el comando `cp` o `mv`.