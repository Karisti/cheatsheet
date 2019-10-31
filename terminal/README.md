# Terminal & Command Line<!-- omit in toc -->

## Index<!-- omit in toc -->
- [Comandos Básicos](#comandos-básicos)
- [Vim](#Vim)
- [Shortcuts](#Shortcuts)
- [Diferencias entre la estructura de archivos de Windows Mac o Linux](#diferencias-entre-la-estructura-de-archivos-de-windows-mac-o-linux)


## Comandos Básicos
- `pwd` nos muestra la ruta de carpetas en la que te encuentras ahora mismo.
- `mkdir` ns permite crear carpetas (por ejemplo, mkdir Carpeta-Importante).
- `touch` nos permite crear archivos (por ejemplo, touch archivo.txt).
- `rm` nos permite borrar un archivo o carpeta (por ejemplo, rm archivo.txt). Mucho cuidado con este comando, puedes borrar todo tu disco duro.
  - `rm -rf` borra todo recursivamente y sin preguntar. No usarlo sin indicar un nombre.
- `cat` ver el contenido de un archivo (por ejemplo, cat nombre-archivo.txt).
- `[comando] > [loquesea.txt]` copia lo que devuelve el comando donde indiquemos.
- `ls` nos permite ver los archivos de la carpeta donde estamos ahora mismo. Podemos usar uno o más argumentos para ver más información sobre estos archivos (los argumentos pueden ser -- + el nombre del argumento o - + una sola letra o shortcut por cada argumento).
  - `ls -a` mostrar todos los archivos, incluso los ocultos.
  - `ls -l` ver todos los archivos como una lista.
  - `ls -al` ver todos los archivos (también los ocultos) como una lista.
- `cd` nos permite navegar entre carpetas.
  - `cd ` ir a la ruta principal
  - `cd o cd ~` ir a la ruta de tu usuario
  - `cd carpeta/subcarpeta` navegar a una ruta dentro de la carpeta donde estamos ahora mismo.
  - `cd ..` regresar una carpeta hacia atrás.
  - `cd .` si quieres referirte al directorio en el que te encuentras ahora mismo
- `history` ver los últimos comandos que ejecutamos y un número especial con el que podemos repetir su ejecución.
- `! + número` ejecutar algún comando con el número que nos muestra el comando history (por ejemplo, !72).
- `clear` o `cls` para limpiar la terminal. También podemos usar los atajos de teclado **Ctrl + L o Command + L**.
- `--help` podemos descubrir todos los argumentos de un comando con el argumento --help (por ejemplo, cat --help).
- `alias [name]= "[command 1]; [command 2]; [command 3]; .....  [command n]"` para crear un comando personal con el nombre [name]

<div align="right">
  <small><a href="#terminal--command-line">🡡 Vuelta al Index</a></small>
</div>


## Vim
- `vim nombre` abrir archivo con editor en linea de comandos.
* `{i}` **Insert mode**. You can just type like normal text editor.
* `{ESC}` **Command mode**. Where you give commands to the editor to get things done.
  - `x` delete the unwanted character.
  - `u` to undo the last the command and `U` to undo the whole line.
  - `CTRL-R` to redo.
  - `A` to append text at the end.
  - `:wq` to save and exit.
  - `:q!` to trash all changes.
  - `dw` move the cursor to the beginning of the word to delete that word.
  - `2w` to move the cursor two words forward.
  - `3e` to move the cursor to the end of the third word forward.
  - `0` to move to the start of the line.
  - `d2w` which deletes 2 words .. number can be changed for deleting the number of consecutive words like d3w.
  - `dd` to delete the line and 2dd to delete to line .number can be changed for deleting the number of consecutive words.

<div align="right">
  <small><a href="#terminal--command-line">🡡 Vuelta al Index</a></small>
</div>


## Shortcuts
- **Tab**: Autocompletado. Presiona la tecla Tab para que la terminal nos muestre todas las posibles carpetas o comandos que podemos ejecutar.
- **Arriba**: Si presionas la tecla Arriba puedes ver el último comando ejecutado.

<div align="right">
  <small><a href="#terminal--command-line">🡡 Vuelta al Index</a></small>
</div>


## Diferencias entre la estructura de archivos de Windows Mac o Linux
- La ruta principal en Windows es C:\, en UNIX es solo /.
- Windows no hace diferencia entre mayúsculas y minúsculas pero UNIX sí.
- GitBash usa la ruta /c para dirigirse a C:\ (o /d para dirigirse a D:\) en Windows. Por lo tanto, la ruta del usuario con el que estás trabajando es /c/Users/Nombre de tu usuario

<div align="right">
  <small><a href="#terminal--command-line">🡡 Vuelta al Index</a></small>
</div>


