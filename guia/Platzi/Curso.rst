git config --global user.email "tu@email.com"
git config --global user.name "Tu Nombre"

Existen muchas otras configuraciones de Git que puedes encontrar ejecutando el comando git config --list (o solo git config para ver una explicación más detallada).

Si quieres ver los archivos ocultos de una carpeta puedes habilitar la opción de Vista > Mostrar u ocultar > Elementos ocultos (en Windows) o ejecutar el comando ls -a.

Comandos para iniciar tu repositorio con Git
git init: para inicializar el repositorio git y el staged
git add nombre_del_archivo.txt: enviar el archivo al staged
git status: ver el estado, si se requiere agregar al starget o si se requiere commit
git conf: para ver las posibles configuraciones
git conf --list: para ver la lista de configuraciones hechas
git conf --list --show-origin: para mostrar las configuraciones y sus rutas
git rm --cached nombre_del_archivo.txt: para eliminar el archivo del staged(ram)
git rm nombre_del_archivo.txt: para eliminar del repositorio
Si por algún motivo te equivocaste en el nombre o email que configuraste al principio, lo puedes modificar de la siguiente manera:
git config --global --replace-all user.name “Aquí va tu nombre modificado”
O si lo deseas eliminar y añadir uno nuevo
git config --global --unset-all user.name :Elimina el nombre del usuario
git config --global --add user.name “Aquí va tu nombre”


El comando git show nos muestra los cambios que han existido sobre un archivo y es muy útil para detectar cuándo se produjeron ciertos cambios, qué se rompió y cómo lo podemos solucionar. Pero podemos ser más detallados.

Si queremos ver la diferencia entre una versión y otra, no necesariamente todos los cambios desde la creación del archivo, podemos usar el comando git diff commitA commitB.

Recuerda que puedes obtener el ID de tus commits con el comando git log.

Comandos para analizar cambios en GIT
git init: inicializar el repositorio
git add nombre_de_archivo.extensión: agregar el archivo al repositorio
git commit -m “Mensaje”: Agregamos los cambios para el repositorio
git add: Agregar los cambios de la carpeta en la que nos encontramos agregar todo
git status: visualizar cambios
git log nombre_de_archivos.extensión: histórico de cambios con detalles
git push: envía a otro repositorio remoto lo que estamos haciendo
git pull: traer repositorio remoto
ls: listado de carpetas en donde me encuentro. Es decir, como emplear dir en windows.
pwd: ubicación actual
mkdir: make directory nueva carpeta
touch archivo.extensión: crear archivo vacío
cat archivo.extensión: muestra el contenido del archivo
history: historial de comandos utilizados durante esa sesión
rm archivo.extensión: Eliminación de archivo
comando --help: ayuda sobre el comando
git checkout: traer cambios realizados
git rm --cached archivo.extensión: se utiliza para devolver el archivo que se tiene en ram. Cuando escribimos git add, lo devuelve a estado natural mientras está en staging.
git config --list: muestra la lista de configuración de git
git config --list --show-origin: rutas de acceso a la configuración de git
git log archivo.extensión: muestra la historia del archivo


Qué es el staging y los repositorios? Ciclo básico de trabajo en Git
10/43

RECURSOS
MARCADORES
Para iniciar un repositorio, o sea, activar el sistema de control de versiones de Git en tu proyecto, solo debes ejecutar el comando git init.

Este comando se encargará de dos cosas: primero, crear una carpeta .git, donde se guardará toda la base de datos con cambios atómicos de nuestro proyecto; y segundo, crear un área que conocemos como Staging, que guardará temporalmente nuestros archivos (cuando ejecutemos un comando especial para eso) y nos permitirá, más adelante, guardar estos cambios en el repositorio (también con un comando especial).

Ciclo de vida o estados de los archivos en Git:

Cuando trabajamos con Git nuestros archivos pueden vivir y moverse entre 4 diferentes estados (cuando trabajamos con repositorios remotos pueden ser más estados, pero lo estudiaremos más adelante):

Archivos Tracked: son los archivos que viven dentro de Git, no tienen cambios pendientes y sus últimas actualizaciones han sido guardadas en el repositorio gracias a los comandos git add y git commit.
Archivos Staged: son archivos en Staging. Viven dentro de Git y hay registro de ellos porque han sido afectados por el comando git add, aunque no sus últimos cambios. Git ya sabe de la existencia de estos últimos cambios, pero todavía no han sido guardados definitivamente en el repositorio porque falta ejecutar el comando git commit.
Archivos Unstaged: entiéndelos como archivos “Tracked pero Unstaged”. Son archivos que viven dentro de Git pero no han sido afectados por el comando git add ni mucho menos por git commit. Git tiene un registro de estos archivos, pero está desactualizado, sus últimas versiones solo están guardadas en el disco duro.
Archivos Untracked: son archivos que NO viven dentro de Git, solo en el disco duro. Nunca han sido afectados por git add, así que Git no tiene registros de su existencia.
Recuerda que hay un caso muy raro donde los archivos tienen dos estados al mismo tiempo: staged y untracked. Esto pasa cuando guardas los cambios de un archivo en el área de Staging (con el comando git add), pero antes de hacer commit para guardar los cambios en el repositorio haces nuevos cambios que todavía no han sido guardados en el área de Staging (en realidad, todo sigue funcionando igual pero es un poco divertido).
Comandos para mover archivos entre los estados de Git:

git status: nos permite ver el estado de todos nuestros archivos y carpetas.
git add: nos ayuda a mover archivos del Untracked o Unstaged al estado Staged. Podemos usar git nombre-del-archivo-o-carpeta para añadir archivos y carpetas individuales o git add -A para mover todos los archivos de nuestro proyecto (tanto Untrackeds como unstageds).
git reset HEAD: nos ayuda a sacar archivos del estado Staged para devolverlos a su estado anterior. Si los archivos venían de Unstaged, vuelven allí. Y lo mismo se venían de Untracked.
git commit: nos ayuda a mover archivos de Unstaged a Tracked. Esta es una ocasión especial, los archivos han sido guardados o actualizados en el repositorio. Git nos pedirá que dejemos un mensaje para recordar los cambios que hicimos y podemos usar el argumento -m para escribirlo (git commit -m "mensaje").
git rm: este comando necesita alguno de los siguientes argumentos para poder ejecutarse correctamente:
- git rm --cached: Mueve los archivos que le indiquemos al estado Untracked.
- git rm --force: Elimina los archivos de Git y del disco duro. Git guarda el registro de la existencia de los archivos, por lo que podremos recuperarlos si es necesario (pero debemos usar comandos más avanzados).



¿Qué es branch (rama) y cómo funciona un Merge en Git?
11/43

RECURSOS
MARCADORES
Una rama o branch es una versión del código del proyecto sobre el que estás trabajando. Estas ramas ayudan a mantener el orden en el control de versiones y manipular el código de forma segura.

En otras palabras, un branch o rama en Git es una rama que proviene de otra. Imagina un árbol, que tiene una rama gruesa, y otra más fina, en la rama más gruesa tenemos los commits principales y en la rama fina tenemos otros commits que pueden ser de hotfix, devlopment entre otros.ㅤ

https://static.platzi.com/media/user_upload/ramas-branch-en-git-7e72b407-90cc-4b90-8de1-738b155764eb.jpg
Clases de branches o ramas en Git
Estas son las ramas base de un proyecto en Git:

1. Rama main (Master)
Por defecto, el proyecto se crea en una rama llamada Main (anteriormente conocida como Master). Cada vez que añades código y guardas los cambios, estás haciendo un commit, que es añadir el nuevo código a una rama. Esto genera nuevas versiones de esta rama o branch, hasta llegar a la versión actual de la rama Main.

2. Rama development
Cuando decides hacer experimentos, puedes generar ramas experimentales (usualmente llamadas development), que están basadas en alguna rama main, pero sobre las cuales puedes hacer cambios a tu gusto sin necesidad de afectar directamente al código principal.

3. Rama hotfix
En otros casos, si encuentras un bug o error de código en la rama Main (que afecta al proyecto en producción), tendrás que crear una nueva rama (que usualmente se llaman bug fixing o hot fix) para hacer los arreglos necesarios. Cuando los cambios estén listos, los tendrás que fusionar con la rama Main para que los cambios sean aplicados. Para esto, se usa un comando llamado Merge, que mezcla los cambios de la rama que originaste a la rama Main.

Todos los commits se aplican sobre una rama. Por defecto, siempre empezamos en la rama Main (pero puedes cambiarle el nombre si no te gusta) y generamos nuevas ramas, a partir de esta, para crear flujos de trabajo independientes.

Cómo crear un branch o rama en Git
El comando git branch permite crear una rama nueva. Si quieres empezar a trabajar en una nueva función, puedes crear una rama nueva a partir de la rama master con git branch new_branch. Una vez creada, puedes usar git checkout new_branch para cambiar a esa rama.

Recuerda que todas tus versiones salen de la rama principal o Master y de allí puedes tomar una versión específica para crear otra rama de versiones.

Cómo hacer merge
Producir una nueva rama se conoce como Checkout. Unir dos ramas lo conocemos como Merge.

Cuando haces merge de estas ramas con el código principal, su código se fusiona originando una nueva versión de la rama master (o main) que ya tiene todos los cambios que aplicaste en tus experimentos o arreglos de errores.

Podemos generar todas las ramas y commits que queramos. De hecho, podemos aprovechar el registro de cambios de Git para producir ramas, traer versiones viejas del código, arreglarlas y combinarlas de nuevo para mejorar el proyecto.

Solo ten en cuenta que combinar estas ramas (hacer “merge”) puede generar conflictos. Algunos archivos pueden ser diferentes en ambas ramas. Git es muy inteligente y puede intentar unir estos cambios automáticamente, pero no siempre funciona. En algunos casos, somos nosotros los que debemos resolver estos conflictos a mano.



Volver en el tiempo en nuestro repositorio utilizando reset y checkout
12/43

RECURSOS
MARCADORES
El comando git checkout + ID del commit nos permite viajar en el tiempo. Podemos volver a cualquier versión anterior de un archivo específico o incluso del proyecto entero. Esta también es la forma de crear ramas y movernos entre ellas.

También hay una forma de hacerlo un poco más “ruda”: usando el comando git reset. En este caso, no solo “volvemos en el tiempo”, sino que borramos los cambios que hicimos después de este commit.

Hay dos formas de usar git reset: con el argumento --hard, borrando toda la información que tengamos en el área de staging (y perdiendo todo para siempre). O, un poco más seguro, con el argumento --soft, que mantiene allí los archivos del área de staging para que podamos aplicar nuestros últimos cambios pero desde un commit anterior.

Cómo usar Git Reset
Para volver a commits previos, borrando los cambios realizados desde ese commit, podemos utilizar:

git reset --soft [SHA 1]: elimina los cambios hasta el staging area
git reset --mixed [SHA 1]: elimina los cambios hasta el working area
git reset --hard [SHA 1]: regresa hasta el commit del [SHA-1]
Donde el SHA-1 es el identificador del commit
Aporte creado por: Johan Mosquera


Git reset vs. Git rm
13/43

LECTURA

Git reset y git rm son comandos con utilidades muy diferentes, pero se pueden confundir muy fácilmente.

git rm
Este comando nos ayuda a eliminar archivos de Git sin eliminar su historial del sistema de versiones. Esto quiere decir que si necesitamos recuperar el archivo solo debemos “viajar en el tiempo” y recuperar el último commit antes de borrar el archivo en cuestión.

Recuerda que git rm no puede usarse así nomás. Debemos usar uno de los flags para indicarle a Git cómo eliminar los archivos que ya no necesitamos en la última versión del proyecto:

git rm --cached: Elimina los archivos de nuestro repositorio local y del área de staging, pero los mantiene en nuestro disco duro. Básicamente le dice a Git que deje de trackear el historial de cambios de estos archivos, por lo que pasaran a un estado untracked.
git rm --force: Elimina los archivos de Git y del disco duro. Git siempre guarda todo, por lo que podemos acceder al registro de la existencia de los archivos, de modo que podremos recuperarlos si es necesario (pero debemos usar comandos más avanzados).
git reset
Este comando nos ayuda a volver en el tiempo. Pero no como git checkout que nos deja ir, mirar, pasear y volver. Con git reset volvemos al pasado sin la posibilidad de volver al futuro. Borramos la historia y la debemos sobreescribir. No hay vuelta atrás.

Este comando es muy peligroso y debemos emplearlo solo en caso de emergencia. Recuerda que debemos usar alguna de estas dos opciones:

Hay dos formas de utilizar git reset: con el argumento --hard, borrando toda la información que tengamos en el área de staging (y perdiendo todo para siempre). O, un poco más seguro, con el argumento --soft, que mantiene allí los archivos del área de staging para que podamos aplicar nuestros últimos cambios pero desde un commit anterior.

git reset --soft: Borramos todo el historial y los registros de Git pero guardamos los cambios que tengamos en Staging, así podemos aplicar las últimas actualizaciones a un nuevo commit.
git reset --hard: Borra todo. Todo todito, absolutamente todo. Toda la información de los commits y del área de staging se borra del historial.
¡Pero todavía falta algo!

git reset HEAD: Este es el comando para sacar archivos del área de staging. No para borrarlos ni nada de eso, solo para que los últimos cambios de estos archivos no se envíen al último commit, a menos que cambiemos de opinión y los incluyamos de nuevo en staging con git add, por supuesto.
¿Por qué esto es importante?
Imagina el siguiente caso:

Hacemos cambios en los archivos de un proyecto para una nueva actualización. Todos los archivos con cambios se mueven al área de staging con el comando git add. Pero te das cuenta de que uno de esos archivos no está listo todavía. Actualizaste el archivo, pero ese cambio no debe ir en el próximo commit por ahora.

¿Qué podemos hacer?

Bueno, todos los cambios están en el área de Staging, incluido el archivo con los cambios que no están listos. Esto significa que debemos sacar ese archivo de Staging para poder hacer commit de todos los demás.

¡Al usar git rm lo que haremos será eliminar este archivo completamente de git! Todavía tendremos el historial de cambios de este archivo, con la eliminación del archivo como su última actualización. Recuerda que en este caso no buscábamos eliminar un archivo, solo dejarlo como estaba y actualizarlo después, no en este commit.

En cambio, si usamos git reset HEAD, lo único que haremos será mover estos cambios de Staging a Unstaged. Seguiremos teniendo los últimos cambios del archivo, el repositorio mantendrá el archivo (no con sus últimos cambios, pero sí con los últimos en los que hicimos commit) y no habremos perdido nada.

Conclusión: Lo mejor que puedes hacer para salvar tu puesto y evitar un incendio en tu trabajo es conocer muy bien la diferencia y los riesgos de todos los comandos de Git.

Aporte creado por: Juan David Castro


Flujo de trabajo básico con un repositorio remoto
14/43

RECURSOS
MARCADORES
Cuando empiezas a trabajar en un entorno local, el proyecto vive únicamente en tu computadora. Esto significa que no hay forma de que otros miembros del equipo trabajen en él.

Para solucionar esto, utilizamos los servidores remotos: un nuevo estado que deben seguir nuestros archivos para conectarse y trabajar con equipos de cualquier parte del mundo.

Estos servidores remotos pueden estar alojados en GitHub, GitLab, BitBucket, entre otros. Lo que van a hacer es guardar el mismo repositorio que tienes en tu computadora y darnos una URL con la que todos podremos acceder a los archivos del proyecto. Así, el equipo podrá descargarlos, hacer cambios y volverlos a enviar al servidor remoto para que otras personas vean los cambios, comparen sus versiones y creen nuevas propuestas para el proyecto.

Esto significa que debes aprender algunos nuevos comandos

Comandos para trabajo remoto con GIT
git clone url_del_servidor_remoto: Nos permite descargar los archivos de la última versión de la rama principal y todo el historial de cambios en la carpeta .git.
git push: Luego de hacer git add y git commit debemos ejecutar este comando para mandar los cambios al servidor remoto.
git fetch: Lo usamos para traer actualizaciones del servidor remoto y guardarlas en nuestro repositorio local (en caso de que hayan, por supuesto).
git merge: También usamos el comando git merge con servidores remotos. Lo necesitamos para combinar los últimos cambios del servidor remoto y nuestro directorio de trabajo.
git pull: Básicamente, git fetch y git merge al mismo tiempo.
Adicionalmente, tenemos otros comandos que nos sirven para trabajar en proyectos muy grandes:

git log --oneline:Te muestra el id commit y el título del commit.
git log --decorate: Te muestra donde se encuentra el head point en el log.
git log --stat: Explica el número de líneas que se cambiaron brevemente.
git log -p: Explica el número de líneas que se cambiaron y te muestra que se cambió en el contenido.
git shortlog: Indica que commits ha realizado un usuario, mostrando el usuario y el título de sus commits.
git log --graph --oneline --decorate y
git log --pretty=format:"%cn hizo un commit %h el dia %cd": Muestra mensajes personalizados de los commits.
git log -3: Limitamos el número de commits.
git log --after=“2018-1-2”
git log --after=“today” y
git log --after=“2018-1-2” --before=“today”: Commits para localizar por fechas.
git log --author=“Name Author”: Commits hechos por autor que cumplan exactamente con el nombre.
git log --grep=“INVIE”: Busca los commits que cumplan tal cual está escrito entre las comillas.
git log --grep=“INVIE” –i: Busca los commits que cumplan sin importar mayúsculas o minúsculas.
git log – index.html: Busca los commits en un archivo en específico.
git log -S “Por contenido”: Buscar los commits con el contenido dentro del archivo.
git log > log.txt: guardar los logs en un archivo txt
Aporte creado por: HellenBar



Introducción a las ramas o branches de Git
15/43

RECURSOS
MARCADORES
Las ramas (branches) son la forma de hacer cambios en nuestro proyecto sin afectar el flujo de trabajo de la rama principal. Esto porque queremos trabajar una parte muy específica de la aplicación o simplemente experimentar.

La cabecera o HEAD representan la rama y el commit de esa rama donde estamos trabajando. Por defecto, esta cabecera aparecerá en el último commit de nuestra rama principal. Pero podemos cambiarlo al crear una rama (git branch rama, git checkout -b rama) o movernos en el tiempo a cualquier otro commit de cualquier otra rama con los comandos (git reset id-commit, git checkout rama-o-id-commit).

Cómo funcionan las ramas en GIT
Las ramas son la manera de hacer cambios en nuestro proyecto sin afectar el flujo de trabajo de la rama principal. Esto porque queremos trabajar una parte muy específica de la aplicación o simplemente experimentar.

git branch -nombre de la rama-: Con este comando se genera una nueva rama.

git checkout -nombre de la rama-: Con este comando puedes saltar de una rama a otra.

git checkout -b rama: Genera una rama y nos mueve a ella automáticamente, Es decir, es la combinación de git brach y git checkout al mismo tiempo.

git reset id-commit: Nos lleva a cualquier commit no importa la rama, ya que identificamos el id del tag., eliminando el historial de los commit posteriores al tag seleccionado.

git checkout rama-o-id-commit: Nos lleva a cualquier commit sin borrar los commit posteriores al tag seleccionado.


.gitignore
.gitignore
*.txt
src/


(usa "git checkout -- <archivo>..." para descartar los cambios en el directorio de trabajo)

(usa "git reset HEAD <archivo>..." para sacar del área de stage)

git branch developer
git branch calidad
git checkout -b hotfix
Cambiado a nueva rama 'hotfix'
git checkout master
Cambiado a rama 'master'
git branch
  calidad
  developer
  hotfix
* master




Fusión de ramas con Git merge
16/43

RECURSOS
MARCADORES
El comando git merge nos permite crear un nuevo commit con la combinación de dos ramas o branches (la rama donde nos encontramos cuando ejecutamos el comando y la rama que indiquemos después del comando).

Cómo usar Git merge
En este ejemplo, vamos a crear un nuevo commit en la rama master combinando los cambios de una rama llamada cabecera:

git checkout master
git merge cabecera
Otra opción es crear un nuevo commit en la rama cabecera combinando los cambios de cualquier otra rama:

git checkout cabecera
git merge cualquier-otra-rama
Asombroso, ¿verdad? Es como si Git tuviera superpoderes para saber qué cambios queremos conservar de una rama y qué otros de la otra. El problema es que no siempre puede adivinar, sobre todo en algunos casos donde dos ramas tienen actualizaciones diferentes en ciertas líneas en los archivos. Esto lo conocemos como un conflicto.

Recuerda que al ejecutar el comando git checkout para cambiar de rama o commit puedes perder el trabajo que no hayas guardado. Guarda siempre tus cambios antes de hacer git checkout.

Comandos básicos de GitHub
git init: crear un repositorio.
git add: agregar un archivo a staging.
git commit -m “mensaje”: guardar el archivo en git con un mensaje.
git branch: crear una nueva rama.
git checkout: moverse entre ramas.
git push: mandar cambios a un servidor remoto.
git fetch: traer actualizaciones del servidor remoto y guardarlas en nuestro repositorio local.
git merge: tiene dos usos. Uno es la fusión de ramas, funcionando como un commit en la rama actual, trayendo la rama indicada. Su otro uso es guardar los cambios de un servidor remoto en nuestro directorio.
git pull: fetch y merge al mismo tiempo.
Comandos para corrección en GitHub
git checkout “codigo de version” “nombre del archivo”: volver a la última versión de la que se ha hecho commit.
git reset: vuelve al pasado sin posibilidad de volver al futuro, se debe usar con especificaciones.
git reset --soft: vuelve a la versión en el repositorio, pero guarda los cambios en staging. Así, podemos aplicar actualizaciones a un nuevo commit.
git reset --hard: todo vuelve a su versión anterior
git reset HEAD: saca los cambios de staging, pero no los borra. Es lo opuesto a git add.
git rm: elimina los archivos, pero no su historial. Si queremos recuperar algo, solo hay que regresar. se utiliza así:
git rm --cached elimina los archivos en staging pero los mantiene en el disco duro.
git rm --force elimina los archivos de git y del disco duro.
Comandos para revisión y comparación en GitHub
git status: estado de archivos en el repositorio.
git log: historia entera del archivo.
git log --stat: cambios específicos en el archivo a partir de un commit.
git show: cambios históricos y específicos hechos en un archivo.
git diff “codigo de version 1” “codigo de version 2”: comparar cambios entre versiones.
git diff: comparar directorio con staging.
Aporte creado por: Pedro Alejandro Silva.

(usa "git merge --abort" para abortar la fusion)

git branch -d nombre_rama

Si aún así queremos eliminar esa rama, se puede forzar el borrado de la siguiente manera:

$ git branch -D nombre-rama

En el caso de querer eliminar una rama del repositorio remoto, la sintaxis será la siguiente:

$ git push origin :nombre-rama

NOTA: MERGE en la rama master el programador edita la linea 10 del archivo index.html, en la rama calidad otro programador edita la linea 21 del archivo index.html. en ambas ramas se hace el commit. Luego nos paramos en la rama master y hacemos un merge de la rama calidad y se va fusionar bien.
En el archivo index.html tendremos las modificaciones tanto de la linea 10 como de la linea 21
cuando hagamos un git log, veremos el ultimo hash de la rama calidad, luego el ultimo hash de la rama master y por ultimo el hash del merge

Si en ambas ramas ubieran editado la misma linea del archivo index.html, ahí si vamos a tener un conflicto al momento de hacer el merge


Resolución de conflictos al hacer un merge
17/43

RECURSOS
MARCADORES
Git nunca borra nada, a menos que nosotros se lo indiquemos. Cuando usamos los comandos git merge o git checkout estamos cambiando de rama o creando un nuevo commit, no borrando ramas ni commits (recuerda que puedes borrar commits con git reset y ramas con git branch -d).

Git es muy inteligente y puede resolver algunos conflictos automáticamente: cambios, nuevas líneas, entre otros. Pero algunas veces no sabe cómo resolver estas diferencias, por ejemplo, cuando dos ramas diferentes hacen cambios distintos a una misma línea.

Esto lo conocemos como conflicto y lo podemos resolver manualmente. Solo debemos hacer el merge, ir a nuestro editor de código y elegir si queremos quedarnos con alguna de estas dos versiones o algo diferente. Algunos editores de código como Visual Studio Code nos ayudan a resolver estos conflictos sin necesidad de borrar o escribir líneas de texto, basta con hacer clic en un botón y guardar el archivo.

Recuerda que siempre debemos crear un nuevo commit para aplicar los cambios del merge. Si Git puede resolver el conflicto, hará commit automáticamente. Pero, en caso de no pueda resolverlo, debemos solucionarlo y hacer el commit.

Los archivos con conflictos por el comando git merge entran en un nuevo estado que conocemos como Unmerged. Funcionan muy parecido a los archivos en estado Unstaged, algo así como un estado intermedio entre Untracked y Unstaged. Solo debemos ejecutar git add para pasarlos al área de staging y git commit para aplicar los cambios en el repositorio.

Cómo revertir un merge
Si nos hemos equivocado y queremos cancelar el merge, debemos usar el siguiente comando:

git merge --abort
Conflictos en repositorios remotos
Al trabajar con otras personas, es necesario utilizar un repositorio remoto.
­
-Para copiar el repositorio remoto al directorio de trabajo local, se utiliza el comando git clone <url>, y para enviar cambios al repositorio remoto se utiliza git push.
-Para actualizar el repositorio local se hace uso del comando git fetch, luego se debe fusionar los datos traídos con los locales usando git merge.

Para traer los datos y fusionarlos a la vez, en un solo comando, se usa git pull.
­- Para crear commits rápidamente, fusionando git add y git commit -m "", usamos git commit -am "".
­- Para generar nuevas ramas, hay que posicionarse sobre la rama que se desea copiar y utilizar el comando git branch <nombre>.
Para saltar entre ramas, se usa el comando git checkout <branch>
­- Una vez realizado los cambios en la rama, estas deben fusionarse con git merge.
El merge ocurre en la rama en la que se está posicionado. Por lo tanto, la rama a fusionar se transforma en la principal.
Los merges también son commits.
Los merges pueden generar conflictos, esto aborta la acción y pide que soluciones el problema manualmente, aceptando o rechazando los cambios que vienen.
Aporte creado por: José Tuzinkievicz, Lottie






Cambios en GitHub: de master a main
18/43

LECTURA

El escritor Argentino Julio Cortázar afirma que las palabras tienen color y peso. Por otro lado, los sinónimos existen por definición, pero no expresan lo mismo. Feo no es lo mismo que desagradable, ni aromático es lo mismo que oloroso.

Por lo anterior podemos afirmar que los sinónimos no expresan lo mismo, no tienen el mismo “color” ni el mismo “peso”.

Sí, esta lectura es parte del curso profesional de Git & GitHub. Quédate conmigo.

Desde el 1 de octubre de 2020 GitHub cambió el nombre de la rama principal: ya no es “master” -como aprenderás en el curso- sino main.

Este derivado de una profunda reflexión ocasionada por el movimiento #BlackLivesMatter.

La industria de la tecnología lleva muchos años usando términos como master, slave, blacklist o whitelist y esperamos pronto puedan ir desapareciendo.

Y sí, las palabras importan.

Por lo que de aquí en adelante cada vez que escuches a Freddy mencionar “master” debes saber que hace referencia a “main”

Puedes leer un poco más aquí: Cambios en GitHub: de master a main

git branch -M main

Sabemos que git branch nos ayuda a crear una nueva rama dentro de nuestro repositorio y -M nos ayudará a mover todo el historial que tengamos (en caso de que los haya) en master a la nueva rama que estamos creando que se llama main


Uso de GitHub
19/43

RECURSOS
MARCADORES
GitHub es una plataforma que nos permite guardar repositorios de Git que podemos usar como servidores remotos y ejecutar algunos comandos de forma visual e interactiva (sin necesidad de la consola de comandos).

Luego de crear nuestra cuenta, podemos crear o importar repositorios, crear organizaciones y proyectos de trabajo, descubrir repositorios de otras personas, contribuir a esos proyectos, dar estrellas y muchas otras cosas.

El README.md es el archivo que veremos por defecto al entrar a un repositorio. Es una muy buena práctica configurarlo para describir el proyecto, los requerimientos y las instrucciones que debemos seguir para contribuir correctamente.

Para clonar un repositorio desde GitHub (o cualquier otro servidor remoto) debemos copiar la URL (por ahora, usando HTTPS) y ejecutar el comando git clone + la URL que acabamos de copiar. Esto descargará la versión de nuestro proyecto que se encuentra en GitHub.

Sin embargo, esto solo funciona para las personas que quieren empezar a contribuir en el proyecto.

Cómo conectar un repositorio de Github a nuestro documento local
Si queremos conectar el repositorio de GitHub con nuestro repositorio local, que creamos usando el comando git init, debemos ejecutar las siguientes instrucciones:

Guardar la URL del repositorio de GitHub con el nombre de origin
git remote add origin URL
Verificar que la URL se haya guardado correctamente:
git remote
git remote -v
Traer la versión del repositorio remoto y hacer merge para crear un commit con los archivos de ambas partes. Podemos usar git fetch y git merge o solo git pull con el flag --allow-unrelated-histories:
git pull origin master --allow-unrelated-histories
Por último, ahora sí podemos hacer git push para guardar los cambios de nuestro repositorio local en GitHub:
git push origin master
Archivos de la clase












Cómo funcionan las llaves públicas y privadas
20/43

RECURSOS
MARCADORES
Las llaves públicas y privadas, conocidas también como cifrado asimétrico de un solo camino, sirven para mandar mensajes privados entre varios nodos con la lógica de que firmas tu mensaje con una llave pública vinculada con una llave privada que puede leer el mensaje.

Las llaves públicas y privadas nos ayudan a cifrar y descifrar nuestros archivos de forma que los podamos compartir sin correr el riesgo de que sean interceptados por personas con malas intenciones.

Cómo funciona un mensaje cifrado con llaves públicas y privadas
Ambas personas deben crear su llave pública y privada.
Ambas personas pueden compartir su llave pública a las otras partes (recuerda que esta llave es pública, no hay problema si la “interceptan”).
La persona que quiere compartir un mensaje puede usar la llave pública de la otra persona para cifrar los archivos y asegurarse que solo puedan ser descifrados con la llave privada de la persona con la que queremos compartir el mensaje.
El mensaje está cifrado y puede ser enviado a la otra persona sin problemas en caso de que los archivos sean interceptados.
La persona a la que enviamos el mensaje cifrado puede emplear su llave privada para descifrar el mensaje y ver los archivos.
Nota: puedes compartir tu llave pública, pero nunca tu llave privada.

Aporte creado por: David Behar





Configura tus llaves SSH en local
21/43

RECURSOS
MARCADORES
En este ejemplo, aprenderemos cómo configurar nuestras llaves SSH en local.

Cómo generar tus llaves SSH
1. Generar tus llaves SSH**
Recuerda que es muy buena idea proteger tu llave privada con una contraseña.

ssh-keygen -t rsa -b 4096 -C "tu@email.com"
2. Terminar de configurar nuestro sistema.
En Windows y Linux:

Encender el “servidor” de llaves SSH de tu computadora:
eval $(ssh-agent -s)
Añadir tu llave SSH a este “servidor”:
ssh-add ruta-donde-guardaste-tu-llave-privada
En Mac:

Encender el “servidor” de llaves SSH de tu computadora:
eval "$(ssh-agent -s)"
Si usas una versión de OSX superior a Mac Sierra (v10.12), debes crear o modificar un archivo “config” en la carpeta de tu usuario con el siguiente contenido (ten cuidado con las mayúsculas):
Host *

AddKeysToAgent yes
UseKeychain yes
IdentityFile ruta-donde-guardaste-tu-llave-privada
Añadir tu llave SSH al “servidor” de llaves SSH de tu computadora (en caso de error puedes ejecutar este mismo comando pero sin el argumento -K):
ssh-add -K ruta-donde-guardaste-tu-llave-privada
Aporte creado por: Juan Luis Rojas



Conexión a GitHub con SSH
22/43

RECURSOS
MARCADORES
La creación de las SSH es necesario solo una vez por cada computadora. Aquí conocerás cómo conectar a GitHub usando SSH.

Luego de crear nuestras llaves SSH podemos entregarle la llave pública a GitHub para comunicarnos de forma segura y sin necesidad de escribir nuestro usuario y contraseña todo el tiempo.

Para esto debes entrar a la Configuración de Llaves SSH en GitHub, crear una nueva llave con el nombre que le quieras dar y el contenido de la llave pública de tu computadora.

Ahora podemos actualizar la URL que guardamos en nuestro repositorio remoto, solo que, en vez de guardar la URL con HTTPS, vamos a usar la URL con SSH:

ssh
git remote set-url origin url-ssh-del-repositorio-en-github
Comandos para copiar la llave SSH:
-Mac:

pbcopy < ~/.ssh/id_rsa.pub
Windows (Git Bash):
clip < ~/.ssh/id_rsa.pub
Linux (Ubuntu):
cat ~/.ssh/id_rsa.pub
Aporte de: Juan Luis Rojas




Tags y versiones en Git y GitHub
23/43

RECURSOS
MARCADORES
Los tags o etiquetas nos permiten asignar versiones a los commits con cambios más importantes o significativos de nuestro proyecto.

Comandos para trabajar con etiquetas:
Crear un nuevo tag y asignarlo a un commit: git tag -a nombre-del-tag id-del-commit.
Borrar un tag en el repositorio local: git tag -d nombre-del-tag.
Listar los tags de nuestro repositorio local: git tag o git show-ref --tags.
Publicar un tag en el repositorio remoto: git push origin --tags.
Borrar un tag del repositorio remoto: git tag -d nombre-del-tag y git push origin :refs/tags/nombre-del-tag.
Para generar un comando complejo con varios comandos de una forma optimizada, utilizamos conjuntos de sentencias conocidas como alias.

Cómo aregar un alias solo para git
Para un proyecto:
git config alias.arbolito "log --all --graph --decorate --oneline"
Global:
git config --global alias.arbolito "log --all --graph --decorate --oneline"
Para correrlo:
git arbolito
Aporte creado por: Jorge Sarabia



Manejo de ramas en GitHub
24/43

RECURSOS
MARCADORES
Si no te funciona el comando gitk es posible no lo tengas instalado por defecto.
Para instalar gitk debemos ejecutar los siguientes comandos:
sudo apt-get update
sudo apt-get install gitk

Las ramas nos permiten hacer cambios a nuestros archivos sin modificar la versión principal (master). Puedes trabajar con ramas que nunca envías a GitHub, así como pueden haber ramas importantes en GitHub que nunca usas en el repositorio local. Lo crucial es que aprendas a manejarlas para trabajar profesionalmente.

Si, estando en otra rama, modificamos los archivos y hacemos commit, tanto el historial(git log) como los archivos serán afectados. La ventaja que tiene usar ramas es que las modificaciones solo afectarán a esa rama en particular. Si luego de “guardar” los archivos(usando commit) nos movemos a otra rama (git checkout otraRama) veremos como las modificaciones de la rama pasada no aparecen en la otraRama.

Comandos para manejo de ramas en GitHub
Crear una rama:
git branch branchName
Movernos a otra rama:
git checkout branchName
Crear una rama en el repositorio local:
git branch nombre-de-la-rama o git checkout -b nombre-de-la-rama.
Publicar una rama local al repositorio remoto:
git push origin nombre-de-la-rama.
Recuerda que podemos ver gráficamente nuestro entorno y flujo de trabajo local con Git utilizando el comando gitk. Gitk fue el primer visor gráfico que se desarrolló para ver de manera gráfica el historial de un repositorio de Git.

Repasa: Qué es branch.

Aporte creado por: Brayan Mamani



Configurar múltiples colaboradores en un repositorio de GitHub
25/43

RECURSOS
MARCADORES
Por defecto, cualquier persona puede clonar o descargar tu proyecto desde GitHub, pero no pueden crear commits, ni ramas. Esto quiere decir que pueden copiar tu proyecto pero no colaborar con él. Existen varias formas de solucionar esto para poder aceptar contribuciones. Una de ellas es añadir a cada persona de nuestro equipo como colaborador de nuestro repositorio.

Cómo agregar colaboradores en Github
Solo debemos entrar a la configuración de colaboradores de nuestro proyecto. Se encuentra en:
Repositorio > Settings > Collaborators
Ahí, debemos añadir el email o username de los nuevos colaboradores.

collaborator.png
Si, como colaborador, agregaste erróneamente el mensaje del commit, lo puedes cambiar de la siguiente manera:

Hacer un commit con el nuevo mensaje que queremos, esto nos abre el editor de texto de la terminal:
git commit —amend
Corregimos el mensaje
Traer el repositorio remoto
git pull origin master
Ejecutar el cambio
git push --set-upstream origin master
Aporte creado por: Andrés Zambrano


Flujo de trabajo profesional: Haciendo merge de ramas de desarrollo a master
26/43

RECURSOS
MARCADORES
Para poder desarrollar software de manera óptima y ordenada, necesitamos tener un flujo de trabajo profesional, que nos permita trabajar en conjunto sin interrumpir el trabajo de otros desarrolladores. Una buena práctica de flujo de trabajo sería la siguiente:

Crear ramas
Asignar una rama a cada programador
El programador baja el repositorio con git pull origin master
El programador cambia de rama
El programador trabaja en esa rama y hace commits
El programador sube su trabajo con git push origin #nombre_rama
El encargado de organizar el proyecto baja, revisa y unifica todos los cambios
Aporte creado por: Alejandro Dubon.



Flujo de trabajo profesional con Pull requests
27/43

RECURSOS
MARCADORES
En un entorno profesional normalmente se bloquea la rama master, y para enviar código a dicha rama pasa por un code review y luego de su aprobación se unen códigos con los llamados merge request.

Para realizar pruebas enviamos el código a servidores que normalmente los llamamos staging develop (servidores de pruebas) luego de que se realizan las pruebas pertinentes tanto de código como de la aplicación estos pasan al servidor de producción con el ya antes mencionado merge request.

Los PR (pull requests) son la base de la colaboración a proyectos Open Source, si tienen pensando colaborar en alguno es muy importante entender esto y ver cómo se hace en las próximas clases. Por lo general es forkear el proyecto, implementar el cambio en una nueva rama, hacer el PR y esperar que los administradores del proyecto hagan el merge o pidan algún cambio en el código o commits que hiciste.

Proceso de un pull request para trabajo en producción:
Un pull request es un estado intermedio antes de enviar el merge.
El pull request permite que otros miembros del equipo revisen el código y así aprobar el merge a la rama.
Permite a las personas que no forman el equipo, trabajar y colaborar con una rama.
La persona que tiene la responsabilidad de aceptar los pull request y hacer los merge tienen un perfil especial y son llamados DevOps





Utilizando Pull Requests en GitHub
28/43

RECURSOS
MARCADORES
Pull request es una funcionalidad de Github (en Gitlab llamada merge request y en Bitbucket push request), en la que un colaborador pide que revisen sus cambios antes de hacer merge a una rama, normalmente master (ahora conocida como main).

Al hacer un pull request, se genera una conversación que pueden seguir los demás usuarios del repositorio, así como autorizar y rechazar los cambios.

Cómo se realiza un pull request
Se trabaja en una rama paralela los cambios que se desean git checkout -b <rama>.
Se hace un commit a la rama git commit -am '<Comentario>'.
Se suben al remoto los cambios git push origin <rama>.
En GitHub se hace el pull request comparando la rama master con la rama del fix.
Uno, o varios colaboradores revisan que el código sea correcto y dan feedback (en el chat del pull request).
El colaborador hace los cambios que desea en la rama y lo vuelve a subir al remoto (automáticamente jala la historia de los cambios que se hagan en la rama, en remoto).
Se aceptan los cambios en GitHub.
Se hace merge a master desde GitHub.
Importante: Cuando se modifica una rama, también se modifica el pull request.

Aporte creado por: David Behar




Creando un Fork, contribuyendo a un repositorio
29/43

RECURSOS
MARCADORES
Los forks o bifurcaciones son una característica única de GitHub en la que se crea una copia exacta del estado actual de un repositorio directamente en GitHub. Este repositorio podrá servir como otro origen y se podrá clonar (como cualquier otro repositorio). En pocas palabras, lo podremos utilizar como un nuevo repositorio git cualquiera

Un fork es como una bifurcación del repositorio completo. Comparte una historia en común con el original, pero de repente se bifurca y pueden aparecer varios cambios, ya que ambos proyectos podrán ser modificados en paralelo y para estar al día un colaborador tendrá que estar actualizando su fork con la información del original.

Al hacer un fork de un poryecto en GitHub, te conviertes en dueñ@ del repositorio fork, puedes trabajar en este con todos los permisos, pero es un repositorio completamente diferente que el original, teniendo solamente alguna historia en común (como crédito al creado o creadora original).

Los forks son importantes porque es la manera en la que funciona el open source, ya que, una persona puede no ser colaborador de un proyecto, pero puede contribuír al mismo, haciendo mejor software que pueda ser utilizado por cualquiera.

Cómo se hace un fork remoto desde consola en GitHub
Al hacer un fork, GitHub sabe que se hizo el fork del proyecto, por lo que se le permite al colaborador hacer pull request desde su repositorio propio.

Cuando trabajas en un proyecto que existe en diferentes repositorios remotos (normalmente a causa de un fork), es muy probable que desees poder trabajar con ambos repositorios. Para esto, puedes generar un remoto adicional desde consola.

git remote add <nombre_del_remoto> <url_del_remoto> 
git remote upstream https://github.com/freddier/hyperblog
Al crear un remoto adicional, podremos hacer pull desde el nuevo origen. En caso de tener permisos, podremos hacer fetch y push.

git pull <remoto> <rama>
git pull upstream master
Este pull nos traerá los cambios del remoto, por lo que se estará al día en el proyecto. El flujo de trabajo cambia, en adelante se estará trabajando haciendo pull desde el upstream y push al origin para pasar a hacer pull request.

git pull upstream master
git push origin master
Aporte creado por: David Behar




Haciendo deployment a un servidor
30/43

RECURSOS
MARCADORES
Deploy es el proceso que permite enviar al servidor uno o varios archivos. Este servidor puede ser de prueba, desarrollo o producción.

En el siguiente ejemplo veremos cómo se realiza el deployment de un documento en un servidor web básico.

Pasos para hacer deployment en un servidor web:
Entrar a la capeta de los archivos del servidor.
Copiar link en clone, elegir entre HTTPS o SSH del repositorio a contribuir.
-En la carpeta deseada se clona el repositorio:
git clone url
Deploy:
Realizar cambios y commit en GitHub.
Traer al Repositorio local las actualizacion para el servidor en la capeta de los archivos del servidor.
git pull ramaRemota main
Nota: Siempre se debe proteger el archivo .git. Dependiendo del software para el servidor web, existen diferentes maneras. La conexión entre GitHub y el servidor se puede realizar mediante: Travis (pago) o Jenkis (Open source).

Aporte creado por: Brayan Mamani, chedl





Hazme un pull request
31/43

RECURSOS
MARCADORES
Aviso importante del Team Platzi

¡Muchas gracias por tu participación en este reto! Hasta agosto de 2020 hemos procesado 1.269 pull requests en el repositorio del curso. Ahora hemos decidido cerrar este experimento, por lo que no seguiremos aprobando nuevos PRs. ¡Pero no te desanimes! Aún así te animamos a completar y enviar tu solución a este desafío para poner en práctica todo lo que has aprendido.

Queremos que uses las habilidades ya aprendidas para aplicarlas en esta clase. Haz un fork de el repositorio de GitHub y realiza las tareas que te indicaremos en esta clase. Ojo, debes seguir las reglas e instrucciones que se dieron en el video.

Regla a seguir:

Dentro del ID “post” luego de “suscribete y dale like” agrega otra línea o párrafo con tu nombre o tu nombre de usuario en Platzi.
¡Suerte! Y #NuncaParesDeAprender




Ignorar archivos en el repositorio con .gitignore
32/43

RECURSOS
MARCADORES
No todos los archivos que agregas a un proyecto deberían ir a un repositorio. Por ejemplo, cuando tienes un archivo donde están tus contraseñas que comúnmente tienen la extensión .env o cuando te estás conectando a una base de datos; son archivos que nadie debe ver.

Por diversas razones, no todos los archivos que agregas a un proyecto deberían guardarse en un repositorio. Esto es porque hay archivos que no todo el mundo debería de ver, y hay archivos que al estar en el repositorio ralentizan el proceso de desarrollo (por ejemplo: los binary large objects, blob, que tardan en descargarse).

Para que no se suban estos archivos no deseados se puede crear un archivo con el nombre .gitignore en la raíz del repositorio con las reglas para los archivos que no se deberían subir: Aquí puedes ver la sintaxis de los .gitignore.

Las razones principales para tomar la decisión de no agregar un archivo a un repositorio son:

Es un archivo con contraseñas (normalmente con la extensión .env)
Es un blob (binary large object, objeto binario grande), mismos que son difíciles de gestionar en git.
Son archivos que se generan corriendo comandos, por ejemplo la carpeta node_modules, que genera npm al correr el comando npm install
Aporte creado por: David Behar.



Readme.md es una excelente práctica
33/43

RECURSOS
MARCADORES
README.md es el lugar donde se explica de qué trata el proyecto, cómo utilizarlo y demás información que se considere que se deba conocer cualquier persona que vaya a trabajar de alguna forma con el proyecto.
.
Los archivos README son escritos en un lenguaje llamado markdown, por eso la extensión .md, mismo que es un estándar de escritura en diversos sitios (como Platzi, Wikipedia y el mismo GitHub). Aquí puedes ver las reglas de markdown.

Los README.md pueden estar en todas las carpetas, pero el más importante es el que se encuentra en la raíz. Este documento ayuda a que los colaboradores sepan información relevante del proyecto, módulo o sección. Puedes crear cualquier archivo con la extensión .md pero solo los README.md los mostrará por defecto GitHub.

Aporte creado por: David Behar.




Tu sitio web público con GitHub Pages
34/43

RECURSOS
MARCADORES
GitHub tiene un servicio de hosting gratis llamado GitHub Pages. Con él, puedes tener un repositorio alojado en GitHub y hacer que el contenido se muestre en la web en tiempo real.

Este es un sitio para nuestros proyectos donde lo único que tenemos que hacer es tener un repositorio alojado. En la página, podemos seguir las instrucciones para crear este repositorio

Pasos para subir un repositorio a GitHub Pages
Debemos tomar la llave SSH y hacer un git clone #SSHexample en mi computador local (Home).
Luego, accederemos a la carpeta nueva que aparece en nuestra máquina local.
Creamos un nuevo archivo que se llame index.html
Guardamos los cambios, hacemos un git pull y seguido de esto un git push a master.
Vamos a las opciones de settings de este repositorio y, en la parte de abajo, en la columna Github Pages, configuramos el source o fuente para que traiga la rama master
Guardamos los cambios.
Después de esto, podremos ver nuestro trabajo en la web como si tuviéramos nuestro propio servidor.

Aporte creado por: Jhon Bangera.




Git Rebase: reorganizando el trabajo realizado
35/43

RECURSOS
MARCADORES
Rebase es el proceso de mover o combinar una secuencia de confirmaciones en una nueva confirmación base. La reorganización es muy útil y se visualiza fácilmente en el contexto de un flujo de trabajo de ramas de funciones. El proceso general se puede visualizar de la siguiente manera.

rebase1.png
Para hacer un rebase en la rama feature de la rama master, correrías los siguientes comandos:

git checkout feature
git rebase master
Esto trasplanta la rama feature desde su locación actual hacia la punta de la rama master:

rebase2.png
Ahora, falta fusionar la rama feature con la rama master

git checkout master
git rebase feature
# No reorganices el historial público
Nunca debes reorganizar las confirmaciones una vez que se hayan enviado a un repositorio público. La reorganización sustituiría las confirmaciones antiguas por las nuevas y parecería que esa parte del historial de tu proyecto se hubiera desvanecido de repente.

El comando rebase es **_una mala práctica, sobre todo en repositorios remotos. Se debe evitar su uso, pero para efectos de práctica te lo vamos a mostrar, para que hagas tus propios experimentos. Con rebase puedes recoger todos los cambios confirmados en una rama y ponerlos sobre otra.

# Cambiamos a la rama que queremos traer los cambios
git checkout experiment
# Aplicamos rebase para traer los cambios de la rama que queremos 
git rebase master
Aporte creado por: Carlos Eduardo Diaz




Git Stash: Guardar cambios en memoria y recuperarlos después
36/43

RECURSOS
MARCADORES
El stashed nos sirve para guardar cambios para después, Es una lista de estados que nos guarda algunos cambios que hicimos en Staging para poder cambiar de rama sin perder el trabajo que todavía no guardamos en un commit

Ésto es especialmente útil porque hay veces que no se permite cambiar de rama, ésto porque tenemos cambios sin guardar, no siempre es un cambio lo suficientemente bueno como para hacer un commit, pero no queremos perder ese código en el que estuvimos trabajando.

El stashed nos permite cambiar de ramas, hacer cambios, trabajar en otras cosas y, más adelante, retomar el trabajo con los archivos que teníamos en Staging, pero que podemos recuperar, ya que los guardamos en el Stash.

git stash
El comando git stash guarda el trabajo actual del Staging en una lista diseñada para ser temporal llamada Stash, para que pueda ser recuperado en el futuro.

Para agregar los cambios al stash se utiliza el comando:

git stash

Podemos poner un mensaje en el stash, para asi diferenciarlos en git stash list por si tenemos varios elementos en el stash. Ésto con:

git stash save "mensaje identificador del elemento del stashed"

Obtener elelmentos del stash
El stashed se comporta como una Stack de datos comportándose de manera tipo LIFO (del inglés Last In, First Out, «último en entrar, primero en salir»), así podemos acceder al método pop.

El método pop recuperará y sacará de la lista el último estado del stashed y lo insertará en el staging area, por lo que es importante saber en qué branch te encuentras para poder recuperarlo, ya que el stash será agnóstico a la rama o estado en el que te encuentres. Siempre recuperará los cambios que hiciste en el lugar que lo llamas.

Para recuperar los últimos cambios desde el stash a tu staging area utiliza el comando:

git stash pop

Para aplicar los cambios de un stash específico y eliminarlo del stash:

git stash pop stash@{<num_stash>}

Para retomar los cambios de una posición específica del Stash puedes utilizar el comando:

git stash apply stash@{<num_stash>}

Donde el <num_stash> lo obtienes desden el git stash list

Listado de elementos en el stash
Para ver la lista de cambios guardados en Stash y así poder recuperarlos o hacer algo con ellos podemos utilizar el comando:

git stash list

Retomar los cambios de una posición específica del Stash || Aplica los cambios de un stash específico

Crear una rama con el stash
Para crear una rama y aplicar el stash más reciente podemos utilizar el comando

git stash branch <nombre_de_la_rama>

Si deseas crear una rama y aplicar un stash específico (obtenido desde git stash list) puedes utilizar el comando:

git stash branch nombre_de_rama stash@{<num_stash>}

Al utilizar estos comandos crearás una rama con el nombre <nombre_de_la_rama>, te pasarás a ella y tendrás el stash especificado en tu staging area.

Eliminar elementos del stash
Para eliminar los cambios más recientes dentro del stash (el elemento 0), podemos utilizar el comando:

git stash drop

Pero si, en cambio, conoces el índice del stash que quieres borrar (mediante git stash list) puedes utilizar el comando:

git stash drop stash@{<num_stash>}

Donde el <num_stash> es el índice del cambio guardado.

Si, en cambio, deseas eliminar todos los elementos del stash, puedes utilizar:

git stash clear

Consideraciones:
El cambio más reciente (al crear un stash) SIEMPRE recibe el valor 0 y los que estaban antes aumentan su valor.
Al crear un stash tomará los archivos que han sido modificados y eliminados. Para que tome un archivo creado es necesario agregarlo al Staging Area con git add [nombre_archivo] con la intención de que git tenga un seguimiento de ese archivo, o también utilizando el comando git stash -u (que guardará en el stash los archivos que no estén en el staging).
Al aplicar un stash este no se elimina, es buena práctica eliminarlo.
Aporte creado por: David Behar.




Git Clean: limpiar tu proyecto de archivos no deseados
37/43

RECURSOS
MARCADORES
Mientras estamos trabajando en un repositorio podemos añadir archivos a él, que realmente no forma parte de nuestro directorio de trabajo, archivos que no se deberían de agregar al repositorio remoto.

El comando clean actúa en archivos sin seguimiento, este tipo de archivos son aquellos que se encuentran en el directorio de trabajo, pero que aún no se han añadido al índice de seguimiento de repositorio con el comando add.

$ git clean

La ejecución del comando predeterminado puede producir un error. La configuración global de Git obliga a usar la opción force con el comando para que sea efectivo. Se trata de un importante mecanismo de seguridad ya que este comando no se puede deshacer.

Revisar que archivos no tienen seguimiento.
$ git clean --dry-run

Eliminar los archivos listados de no seguimiento.
$ git clean -f
Git clean tiene muchísimas opciones adicionales, que puedes explorar al ver su documentación oficial.

Aporte creado por: Alex Camacho.




Git cherry-pick: traer commits viejos al head de un branch
38/43

RECURSOS
MARCADORES
Git Cherry-pick es un comando que permite tomar uno o varios commits de otra rama sin tener que hacer un merge completo. Así, gracias a cherry-pick, podríamos aplicar los commits relacionados con nuestra funcionalidad en la rama master sin necesidad de hacer un merge.

Para demostrar cómo utilizar git cherry-pick, supongamos que tenemos un repositorio con el siguiente estado de rama:

a -b - c - d   Master
         \
           e - f - g Feature

El uso de git cherry-pick es sencillo y se puede ejecutar de la siguiente manera:

git checkoutmaster
En este ejemplo, commitSha es una referencia de confirmación. Puedes encontrar una referencia de confirmación utilizando el comando git log. En este caso, imaginemos que queremos utilizar la confirmación ‘f’ en la rama master. Para ello, primero debemos asegurarnos de que estamos trabajando con esa rama master.

git cherry-pick f

Una vez ejecutado, el historial de Git se verá así:

a -b - c - d - f   Master
         \
           e - f - g Feature

La confirmación f se ha sido introducido con éxito en la rama de funcionalidad

Atención
Cherry-pick es una mala práctica porque significa que estamos reconstruyendo la historia, usa cherry-pick con sabiduría. Si no sabes lo que estás haciendo, mejor evita emplear este comando.

Aporte creado por: Carlos Eduardo Diaz.






