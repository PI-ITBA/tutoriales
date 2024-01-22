# Uso de CMakeLists.txt

## Múltiples ejecutables con múltiples fuentes

Dentro de un proyecto se pueden generar múltiples ejecutables. 
Por ejemplo para la siguiente estructura de archivos:

<img src="cmake.png" alt="CMake" width="300"/>

el siguiente archivo 
<code>CMakeLists.txt</code>
genera cuatro ejecutables distintos que utilizan distintos archivos fuentes ubicados
en distintas partes del directorio del proyecto:

<code-block lang="cmake">
<![CDATA[

cmake_minimum_required(VERSION 3.16)
project(pi C)

set(CMAKE_C_FLAGS "-Wall -pedantic -std=c99 -lm -g -fsanitize=address")

add_executable(pi main.c)
# Para un ejecutable amigos a partir del main de amigos.c
add_executable(amigos amigos.c)
# Para un ejecutable primo a partir del main de primo.c que utiliza la biblioteca de getnum
add_executable(primo primo.c lib/getnum.c)
# Para un ejecutable generala a partir del main de generala.c que utiliza la biblioteca de números aleatorios
add_executable(generala generala.c lib/random.c)

]]>
</code-block>
