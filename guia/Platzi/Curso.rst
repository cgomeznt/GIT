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
