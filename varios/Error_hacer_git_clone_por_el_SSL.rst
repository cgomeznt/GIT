
Error al hacer git clone por el certificado
==============================================

Esto paso en un Windows con Mobaxterm, al tratar de clonar un repositorio de github::

	git clone https://github.com/cgomeznt/CentOS.git
	Cloning into 'CentOS'...
	fatal: unable to access 'https://github.com/cgomeznt/CentOS.git/': error setting certificate verify locations:
	  CAfile: ./ca-bundle.crt
	  CApath: none

Para corregir, le indicamos a Git que no verifique el SSL::

	git config --system http.sslverify false
	
Luego podemos continuar::

	git clone https://github.com/cgomeznt/CentOS.git
	Cloning into 'CentOS'...
	remote: Enumerating objects: 229, done.
	remote: Total 229 (delta 0), reused 0 (delta 0), pack-reused 229
	Receiving objects: 100% (229/229), 1.24 MiB | 90.00 KiB/s, done.
	Resolving deltas: 100% (87/87), done.
	Checking connectivity... done.