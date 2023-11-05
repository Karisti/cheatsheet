# Git & Github<!-- omit in toc -->

## Index<!-- omit in toc -->
- [Comandos Git](#comandos-básicos)
  - [Comandos Básicos](#flujos-de-trabajo)
  - [Múltiples Branches](#múltiples-branches)
  - [Repositorios Remotos (Github)](#repositorios-remotos-github)
- [Configurar Git](#configurar-git)
- [Estados de los archivos en Git](#estados-de-los-archivos-en-git)
- [Utilidades](#utilidades)


## Comandos Git

### Comandos Básicos

* `git init` inicia un repositorio en la carpeta actual.
  * `git init [nombre]` crea la carpeta [nombre] e inicia el repositorio.
* `git add [archivo]` nos ayuda a mover archivos del **Untracked o Unstaged al estado Staging**.
  * `git add .` agrega todos los archivos del working directory al staging area. `git add -A` hace lo mismo.
  * `git add -n [archivo]` simula el agregado de un [archivo].  
* `git commit` guarda los cambios **del Staging al Repositorio** Cada commit es como una nueva versión.
  * `git commit -m "mensaje"` le añade el mensaje directamente.
  * `git commit -am "mensaje"` hace el add también junto con el commit.
  * `git commit --amend` añade el último cambio al anterior commit. Si se escribe un mensaje este sobreescribe el anterior.  
* `git status` nos permite ver el estado de todos nuestros archivos y carpetas.
  * `untracked files` son archivos que están en nuestro Working Directory, lo que aparezca en rojo es lo que se ha modificado y hay que pasarlo al Staging.
  * `changes to be comitted` son los archivos que se encuentran en el staging area. Aparecen en verde.
* `git show` nos muestra todos los cambios hechos en un archivo, lineas codigos, quien lo hizo...
* `git log` nos permite ver la historia completa de commits.
  *  `--stat` estadisticas de los cambios realizados.
  * `--oneline` resumido.
  * `--graph` ver las ramificaciones.
  * `-S "[palabra]"`muestra todas las veces que se ha usado la palabra [palabra] en los commits.
  * `-[numero]` ver los ultimos [numero] commits.
* `gitk` ver historia con interfaz.
* `git checkout [ID del commit]` nos olver a cualquier versión anterior de un archivo específico o incluso del proyecto entero. Esta también es la forma de crear ramas y movernos entre ellas.
* `git clean` de alguna de estas formas:
  * `git clean --dry-run` para ver qué archivos vamos a borrar.
  * `git clean -f` para borrar todos los archivos listados (que no son carpetas, las carpetas hay que borrarlas a mano).
* `git rm` este comando necesita alguno de los siguientes argumentos para poder ejecutarse correctamente:
  * `git rm --cached [archivo]` mueve los archivos que le indiquemos al estado Untracked.
  * `git rm -force` elimina los archivos de Git y del disco duro. Git guarda el registro de la existencia de los archivos, por lo que podremos recuperarlos si es necesario (pero debemos usar comandos más avanzados).
* `git reset HEAD` saca los archivos del estado Staged para devolverlos a su estado anterior. Si los archivos venían de Unstaged, vuelven allí. Y lo mismo se venían de Untracked.
* `git tag` agrega tag.
  * `git tag -a [tag] -m ["comentario"]` agrega el tag con un comentario al ultimo commit.
  * `git tag -l` lista los tags.
  * `git push origin --tags` publicar un tag en el repositorio remoto.
  * `git tag [tag] [sha1 del commit]` agrega un tag a un commit en partcular.
  * `git tag -d [tag]` y `git push origin :refs/tags/nombre-del-tag` elimina el tag.
  * `git tag -f -a [nuevo tag] [sha1 del commit]` renombra el tag del commit pero deja el anterior tag.
* `git diff` diferencias entre el directorio actual y lo que tengo en staging.
  * `git diff [sha1-1] [sha1-2]` diferencia entre la version 1 vs la version 2.
* `git reflog` muestra una lista de toda la historia de commits, cada uno con su hash y HEAD.
* `git reset`
  * `--soft [sha1]` borra todos los commits posteriores a [sha1], pero lo que está en staging se mantiene en staging.
  * `--hard [sha1]` borra todos los commits posteriores a [sha1], desaparece todo lo hecho hasta ese punto.
  * `--mixed [sha1]` borrar todos los commits posteriores a [sha1]. Los archivos que salen del repositorio son pasados al working directory.
* `git grep [palabra]` buscará en todo el proyecto los archivos en donde está la palabra [palabra].
  * `git grep -n [palabra]` nos dirá en qué línea está lo que estamos buscando.
  * `git grep -c [palabra]` nos dirá cuántas veces se repite esa palabra y en qué archivo. *Hay que usar comillas si tiene caracteres como < o >, por ejemplo, `git grep -c "<p>"`.
* `git shortlog` para ver cuantos commits ha hecho cada uno del equipo.
  * `-sn` solo muestra las personas que han hecho commits.
  * `--all` cuenta todos los commits, incluso los que fueron borrados.
   `--no-merges` no contará los merges.
* `git config --global alias.[nombre-comando] "[comando]"` crea el comando [nombre-comando] que ejecutará [comando] de aquí en adelante. Ejemplo: *git config --global alias.stats "shortlog -sn --all --no-merges"*
* `git blame [archivo]` veremos quién hizo cada cosa.
  * `git blame [archivo] -L[NUM1],[NUM2]` veremos quién hizo cada cosa entre las lineas [NUM1] y [NUM2]. *Ejemp: git blame py/test.py -L35,58* `-c` añade más formato.
* `git [comando] --help` abre la documentación de [comando].



Si se desea eliminar el repositorio, solo hay que eliminar la carpeta oculta .git

<div align="right">
  <small><a href="#git--github">🡡 Vuelta al Index</a></small>
</div>

### Múltiples branches

* `git branch` para saber las ramas que tenemos y en cual estamos.
  * `git branch [nombre]` crear la rama [nombre].
  * `-l` lista las ramas.
  * `-d [nombre]` elimina el branch [nombre]. Esto solo funciona si el branch no tiene ningún commit.
  * `-D [nombre]` fuerza la eliminación de un branch sin importar si tiene commits.
  * `-m [nombre inicial] [nuevo nombre] ` renombra el branch [nombre inicial] por [nuevo nombre].
  * `-r` ver las ramas remotas.
  * `-a` ver TODAS las ramas. En rojo -> remotas, en blanco -> locales, asterisco -> rama en la que estás actual.
* `git checkout [brach]` moverse al branch [branch].
  * `git chechout [sha1]` ir al momento del tiempo de ese commit.
  * `-b [nombre]` crea un branch y se mueva al mismo.
  * `-- [archivo]` descarta todos los cambios del archivo.
* `git merge [branch]` fusiona el branch [branch] con el branch actual.
* `git rebase [branch]` recoger todos los cambios confirmados en una rama y ponerlos sobre otra. *Primero se hace rebase a la rama que voy a eliminar de la historia, y luego a la rama principal. Sino habrá conflictos.* **No usarlo, borra todo rastro de la rama.**
* `git stash` guardar temporalmente sin hacer commit. Es un limbo como el staging area. Te permite cambiar de branch para comprobar cosas sin tener que hacer commit.
  * `list` ver la lista de los stash.
  * `pop` volver al stash que he guardado.
  * `branch [nombre-rama]` guardar en una nueva rama [nombre-rama] lo que habíamos guardado temporalmente en stash.
  * `drop stash@{numero}` elimina el stash.
  * `apply stash@{numero}` aplica el stash.
* `git cherry pick [IDCommit]` mover el commit viejo [IDCommit] de otro branch al branch actual.

<div align="right">
  <small><a href="#git--github">🡡 Vuelta al Index</a></small>
</div>

### Submódulos

* `git submodule add <PATH_REMOTO> <NOMBRE_CARPETA>` añadir submódulo.
* `git clone --recursive <PATH_REMOTO> <NOMBRE_CARPETA>` hacer clone bajando submódulos.
* `git pull --recurse-submodules` hacer pull bajando submódulos.
* `git rm <NOMBRE>` borrar submódulo.
* `git submodule update --remote` actualizará el submódulo al HEAD del remoto.
 
<div align="right">
  <small><a href="#git--github">🡡 Vuelta al Index</a></small>
</div>

### Repositorios Remotos (Github)

* `git clone [URL]` nos permite descargar los archivos de la última versión de la rama principal y todo el historial de cambios en la carpeta .git.
* `git remote add origin [URL]` conecta un repositorio remoto con uno local. Por defecto el nombre es **origin**.
  * `git remote -v` lista las conexiones remotas.
  * `git remote remove [nombre]` remueve una conexión remota.
  * `git remote set-url origin url-ssh-del-repositorio-en-github` para conectar con SSH.
* `git push origin master` luego de hacer git add y git commit debemos ejecutar este comando para mandar los cambios al servidor remoto.
  * `--all origin` push a todos los branch y tags.
  * `--tags` enviar los tags.
* `git pull origin [branch]` básicamente, git fetch y git merge al mismo tiempo.
* `git fetch [nombre] [branch]` trae las actualizaciones del repositorio remoto.
* `git merge [origin/master] --allow-unrelated-histories` hace un merge de la ultima version con el repositorio local.
* `fork` hace una copia de un repositorio externo a nuestra cuenta.
* `ssh-keygen -t rsa -b 4096 -C "correo@ejemploc.com"` crea una llave ssh. El correo debe de ser el mismo que se encuentra en Github.

<div align="right">
  <small><a href="#git--github">🡡 Vuelta al Index</a></small>
</div>


## Configurar Git
- `git config`
  - `--global user.email user@example.com` cambiar email.
  - `--global user.name "Sergio Minei"` cambiar nombre.
  - `--global color.ui true` colorear el output del terminal de Git.
  - `--global core.editor ["editor --wait"]` configurar el editor de texto de git.
  - `--list` ver la lista de configuraciones.
  - `--list --show-origin` ver donde están guardadas las configuraciones.

<div align="right">
  <small><a href="#git--github">🡡 Vuelta al Index</a></small>
</div>


## Estados de los archivos en Git
Cuando trabajamos con Git, nuestros archivos pueden vivir y moverse entre 4 diferentes estados:
- **Archivos Tracked**: Son los archivos que viven dentro de Git, no tienen cambios pendientes y sus últimas actualizaciones han sido guardadas en el repositorio gracias a los comandos git add y git commit.
- **Archivos Staged**: Son archivos en Staging. Viven dentro de Git y hay registro de ellos porque han sido afectados por el comando git add, aunque no sus últimos cambios. Git ya sabe de la existencia de estos últimos cambios pero todavía no han sido guardados definitivamente en el repositorio porque falta ejecutar el comando git commit.
- **Archivos Unstaged**: Entiendelos como archivos “Tracked pero Unstaged”. Son archivos que viven dentro de Git pero no han sido afectados por el comando git add ni mucho menos por git commit. Git tiene un registro de estos archivos pero está desactualizado, sus últimas versiones solo están guardadas en el disco duro.
- **Archivos Untracked**: Son archivos que NO viven dentro de Git, solo en el disco duro. Nunca han sido afectados por git add, así que Git no tiene registros de su existencia.

<div align="right">
  <small><a href="#git--github">🡡 Vuelta al Index</a></small>
</div>


## Utilidades
- https://pandao.github.io/editor.md/en.html
- https://learngitbranching.js.org/
- [Readme template](https://gist.github.com/PurpleBooth/109311bb0361f32d87a2)

<div align="right">
  <small><a href="#git--github">🡡 Vuelta al Index</a></small>
</div>


