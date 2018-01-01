Configure GIT sobre HTTP
++++++++++++++++++++++++

Configuracion Base
+++++++++++++++++++

La configuracion mas basica para permitir la lectura a los anonimos al repositorio GIT es utilizando el script git-http-backend que viene de la versions 1.6.6 y superior.

pero antes de comenzar debemos modificar el httpd.conf para que evitar el error de forbbiden. Comentamso las siguientes lineas::

	# vi /etc/httpd/conf/httpd.conf 
	# <Directory />
	#    Options FollowSymLinks
	#     AllowOverride None
	# </Directory>

Debemos modificar la configuracion de Apache para que utilice el script git-http-backend. Cambiamos el Virtual Host.::

	# vi git.conf
	<VirtualHost *:80>
	    ServerName git.gitserver
	    DocumentRoot /opt/repos
	    <Directory /opt/repos/>
		# Order allow,deny
		# allow from all
		Allow from All
		Options +ExecCGI
		AllowOverride All
	    </Directory>
	SetEnv GIT_PROJECT_ROOT /opt/repos
	SetEnv GIT_HTTP_EXPORT_ALL
	ScriptAlias /git/ /usr/libexec/git-core/git-http-backend/
	</VirtualHost>

En este punto ya un usuario anonimo desde el cliente podra ser capaz de clonar un proyecto.::

	$ git clone http://git.gitserver/git/Cursos.git
	Cloning into 'Cursos'...
	remote: Counting objects: 3, done.
	remote: Total 3 (delta 0), reused 0 (delta 0)
	Unpacking objects: 100% (3/3), done.

Anonimo pueda escribir
++++++++++++++++++++++

Esto no debe ser considerado en produccion.::

	$ /opt/repos/Cursos.git
	$ git config http.receivepack true

Probamos desde el cliente.::

	$ git log
	commit 8148e4b15ec71978672469559ee6185743c385de
	Author: Carlos Gómez G <cgomeznt@gmail.com>
	Date:   Sun Dec 31 21:58:50 2017 -0400

	    First Commit
	$ echo "Agregamos esto" >> README.txt 
	$ git status
	On branch master
	Your branch is up-to-date with 'origin/master'.
	Changes not staged for commit:
	  (use "git add <file>..." to update what will be committed)
	  (use "git checkout -- <file>..." to discard changes in working directory)

		modified:   README.txt

	no changes added to commit (use "git add" and/or "git commit -a")
	$ git add *
	$ git status
	On branch master
	Your branch is up-to-date with 'origin/master'.
	Changes to be committed:
	  (use "git reset HEAD <file>..." to unstage)

		modified:   README.txt
	$ git commit -m "Realizando el teste de Anonimo"
	[master b060ea9] Realizando el teste de Anonimo
	 1 file changed, 1 insertion(+)
	$ git status
	On branch master
	Your branch is ahead of 'origin/master' by 1 commit.
	  (use "git push" to publish your local commits)
	nothing to commit, working tree clean
	$ git remote -v
	origin	http://git.gitserver/git/Cursos.git (fetch)
	origin	http://git.gitserver/git/Cursos.git (push)
	$ git branch -a
	* master
	  remotes/origin/HEAD -> origin/master
	  remotes/origin/master
	$ git push origin master
	Counting objects: 3, done.
	Writing objects: 100% (3/3), 294 bytes | 0 bytes/s, done.
	Total 3 (delta 0), reused 0 (delta 0)
	To http://git.gitserver/git/Acsel-e.git
	   8148e4b..b060ea9  master -> master

Acceso con Autenticacion
+++++++++++++++++++++++++

Una manera simple de hacerlo es con la ayuda de apache.

En el servidor agregamos esto a la configuracion del virtualhost:
<Location /git>
  AuthType Basic
  AuthName "Private Git Access"
  AuthUserFile "/etc/git-auth-file"
  Require valid-user
</Location>::

	# vi git.conf
	<VirtualHost *:80>
	    ServerName git.gitserver
	    DocumentRoot /opt/repos
	    <Directory /opt/repos/>
		# Order allow,deny
		# allow from all
		Allow from All
		Options +ExecCGI
		AllowOverride All
	    </Directory>
	SetEnv GIT_PROJECT_ROOT /opt/repos
	SetEnv GIT_HTTP_EXPORT_ALL
	ScriptAlias /git/ /usr/libexec/git-core/git-http-backend/

	<Location /git>
	  AuthType Basic
	  AuthName "Private Git Access"
	  AuthUserFile "/etc/git-auth-file"
	  Require valid-user
	</Location>

	</VirtualHost>

Creamos el archivo donde se gurdaran los usuarios y las claves.::

	$ touch /etc/git-auth-file

Con la ayuda de **htpasswd ** creamos el usuario y le colocamos la clave.::

	# htpasswd /etc/git-auth-file cgomez
	New password: 
	Re-type new password: 
	Adding password for user cgomez

Nos vamos al cliente y realizamos la verificacion.::

	$ echo "Agregamos esto para validar la autenticacion" >> README.txt 
	$ git add README.txt 
	$ git commit -m "Se modifico para validar la autenticacion"
	[master 9158e1f] Se modifico para validar la autenticacion
	 1 file changed, 1 insertion(+)
	$ git push origin master
	Username for 'http://git.gitserver': cgomez
	Password for 'http://cgomez@git.gitserver': 
	Counting objects: 3, done.
	Delta compression using up to 4 threads.
	Compressing objects: 100% (2/2), done.
	Writing objects: 100% (3/3), 336 bytes | 0 bytes/s, done.
	Total 3 (delta 0), reused 0 (delta 0)
	To http://git.gitserver/git/Cursos.git
	   b060ea9..9158e1f  master -> master

