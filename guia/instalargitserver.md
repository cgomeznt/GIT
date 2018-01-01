Instalar un servidor GIT
==========================

Primero que todo el link oficial de GIT https://git-scm.com/book/es/v1/Git-en-un-servidor-Los-Protocolos

Crear Servidor Git por ssh
++++++++++++++++++++++++++++

Instalar y configurar servidor Git con SSH en Centos.
Git es un software de control de versiones diseñado por **Linus Torvalds**, pensando en la eficiencia y la confiabilidad del mantenimiento de versiones de aplicaciones cuando estas tienen un gran número de archivos de código fuente. Al principio, Git se pensó como un motor de bajo nivel sobre el cual otros pudieran escribir la interfaz de usuario o front end como Cogito o StGIT. Sin embargo, Git se ha convertido desde entonces en un sistema de control de versiones con funcionalidad plena. Hay algunos proyectos de mucha relevancia que ya usan Git, en particular, el grupo de programación del núcleo Linux.


En el Servidor
++++++++++++++++

Vamos a crear dos repositorios.::

	# yum install git
	# mkdir /opt/repos
	# useradd usergit
	# passwd usergit
	# chown -R usergit. /opt/repos/
	# cd /opt/repos/
	# su usergit
	$ mkdir Training.git
	$ mkdir Cursos.git
	$ cd Training.git/
	$ git --bare init 
	$ ls
	branches  config  description  HEAD  hooks  info  objects  refs  testing
	$ cd ../Cursos.git/
	$ git --bare init 
	$ ls
	branches  config  description  HEAD  hooks  info  objects  refs  testing

En el Cliente
++++++++++++++

Esta es una forma.::

	$ cd /opt/local
	$ git clone usergit@192.168.56.20:/opt/repos/Training.git
	Cloning into 'Training.git'...
	usergit@192.168.56.20's password: 
	warning: You appear to have cloned an empty repository.
	$ echo "Esta es la primera version" >> README.txt
	$ git status
	On branch master

	Initial commit

	Untracked files:
	  (use "git add <file>..." to include in what will be committed)

		README.txt

	nothing added to commit but untracked files present (use "git add" to track)
	$ git status
	On branch master

	Initial commit

	Changes to be committed:
	  (use "git rm --cached <file>..." to unstage)

		new file:   README.txt

	$ git commit -m "First Commit"
	[master (root-commit) 8148e4b] First Commit
	 1 file changed, 1 insertion(+)
	 create mode 100644 README.txt
	$ git status
	On branch master
	Your branch is based on 'origin/master', but the upstream is gone.
	  (use "git branch --unset-upstream" to fixup)
	nothing to commit, working tree clean
	$ git remote -v
	origin	usergit@192.168.56.20:/opt/repos/Acsel-e.git (fetch)
	origin	usergit@192.168.56.20:/opt/repos/Acsel-e.git (push)
	$ git push origin master
	usergit@192.168.56.20's password: 
	Counting objects: 3, done.
	Writing objects: 100% (3/3), 232 bytes | 0 bytes/s, done.
	Total 3 (delta 0), reused 0 (delta 0)
	To 192.168.56.20:/opt/repos/Acsel-e.git
	 * [new branch]      master -> master
	$ git log
	commit 8148e4b15ec71978672469559ee6185743c385de
	Author: Carlos Gómez G <cgomeznt@gmail.com>
	Date:   Sun Dec 31 21:58:50 2017 -0400

	    First Commit


Esta es la otra forma.::

	$ cd /opt/local
	$ mkdir Cursos
	$ cd Cursos/
	$ git init
	Initialized empty Git repository in /tmp/consis/Cursos/.git/
	$ git remote add origin usergit@192.168.56.20/opt/repos/Cursos.git
	$ git remote -v
	origin	usergit@192.168.56.20/opt/repos/Cursos.git (fetch)
	origin	usergit@192.168.56.20/opt/repos/Cursos.git (push)
	$ git pull origin master
	usergit@192.168.56.20's password: 
	remote: Counting objects: 3, done.
	remote: Total 3 (delta 0), reused 0 (delta 0)
	Unpacking objects: 100% (3/3), done.
	From 192.168.56.20:/opt/repos/Acsel-e
	 * branch            master     -> FETCH_HEAD
	 * [new branch]      master     -> origin/master
	$ ls
	README.txt
	$ git log
	commit 8148e4b15ec71978672469559ee6185743c385de
	Author: Carlos Gómez G <cgomeznt@gmail.com>
	Date:   Sun Dec 31 21:58:50 2017 -0400

	    First Commit







