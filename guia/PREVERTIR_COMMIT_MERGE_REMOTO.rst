¿Cómo revertir un merge que se hizo un push al remoto?
=======================================================================

Para revertir los commit incorrectos o para restablecer la rama remota al HEAD/estado correcto.

Nota:No para una branch compartida.

Verificar el branch en el repositorio local::

	git checkout your_branch_name
	
copie el hash del commit correcto (es decir, el hash del commit inmediatamente antes de la commit incorrecto) ::

	git log 
	git log -n5
	
debería mostrar algo como esto y debemos copiar el commit correcto::

	commit 7cd42475d6f95f5896b6f02e902efab0b70e8038 "Merge branch 'wrong-commit' into 'your_branch_name'"
	commit f9a734f8f44b0b37ccea769b9a2fd774c0f0c012 "this is a wrong commit" 
	commit 3779ab50e72908da92d2cfcd72256d7a09f446ba "this is the correct commit"

Reset la rama con el hash del commit correcto copiado en el paso anterior (ultimo hash bueno conocido)::

	git reset <commit-hash> 
	
Ejemplo::

	git reset 3779ab50e72908da92d2cfcd72256d7a09f446ba
	
ejecute el **git status** para mostrar todos los cambios que formaron parte del commit incorrecto.

simplemente ejecute **git reset --hard** para revertir todos esos cambios::

	git reset --hard


Forzar su branch local a la remota y observe que su historial de confirmaciones está limpio como estaba antes de contaminarse::

	git push -f origin your_branch_name
	
	
Si al ejecutar el comando anterior les genera el siguiente error::

	 ! [remote rejected] master -> master (pre-receive hook declined)
	error: failed to push some refs to 'http://wiki.credicard.com.ve/kb/unix.git'

	
En el Gitlab debera hacer lo siguiente::


Abir project > Settings > Repository luego ir a "Protected branches", buscar "master" branch dentro de la lista y hacer click en  "Unprotect" y luego hacer el paso anterior::

	git push -f origin your_branch_name

Luego que pueda ejecutar el comando anterior con exito, debe nuevamente colocar en "protect" del repositorio.


Si realizo un merge y no se ha realizado el commit
====================================================

Simplemente es ejecutar::

	git merge --abort
	
	
Borrar branch (ramas) local y/o remota
=========================================

Borrar branch local::

	git branch -d localBranchName

Borrar branch remoto::

	git push origin --delete remoteBranchName
	
Esto corrige el problem en local, no quieres hacer merge, solo que se traiga el remoto
==================================================================================
::

	git fetch origin master
	git reset --hard FETCH_HEAD
	git clean -df

Resumen de git fetch
=========================

En resumen, git fetch es un comando principal que se usa para descargar contenidos desde un repositorio remoto. 
git fetch se usa en combinación con git remote, git branch, git checkout y git reset para actualizar un repositorio local al estado de un remoto. 
El comando git fetch es una pieza fundamental de los flujos de trabajo colaborativos de git. git fetch presenta un comportamiento similar a git pull, 
aunque git fetch se puede considerar una versión más segura y menos destructiva::

	git fetch origin master
	
	
	
	
https://stackoverflow.com/questions/3528245/whats-the-difference-between-git-reset-mixed-soft-and-hard
