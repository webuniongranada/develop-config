# vagrant-dev-rails-box

Archivos para inicializar un entorno virtual de desarrollo basado en Rails.

# Primeros pasos

Necesitaremos [Vagrant](https://www.vagrantup.com/downloads.html), [VirtualBox](https://www.virtualbox.org/wiki/Downloads) y [Git](https://git-scm.com/downloads) instalados en nuestros equipos y funcionando en nuestros equipos.

# Configuración de GIT

Para cofigurar Git os dejo un enlace de [primeros pasos git](https://git-scm.com/book/es/v1/Empezando-Configurando-Git-por-primera-vez).

Una vez configurado Git clonaremos este repositorio.

`git clone https://github.com/webuniongranada/develop-config.git`

Esto nos generará una carpeta con el mismo nombre del respositorio, *develop-config*. Podéis renombrar la carepeta aunque yo me seguire refiriendo a ella con ese mismo nombre.

# Inicializando Vagrant

Ahora que tenemos el repositorio clonado es momento de lanzar Vagrant, para ello entramos en la carpeta *develop-config* y dentro de ella ejecutamos el siguiente comando:

`vagrant up`

Con este sencillo comando empezará la magia. El servidor empezara a instalar una distro linux, la base de datos, rails... una vez finalizada la instalación entraremos en la maquina que acabomos de crear.

`vagrant ssh`

Ahora estaremos dentro de la maquina virtual que acabamos de lanzar.

Para salir se escribe `exit`

# WebUnionGranada

Ya tenemos todo lo necesario para poder lanzar el servidor de WUG pero ahora nos hace falta el proyecto en sí.

Para ello dentro de la carpeta donde tenemos el vagrant montado (*develop-config*) vamos a generar una nueva carpeta llamada `apps` y dentro de ella clonaremos el [proyecto de WUG](https://github.com/webuniongranada/webuniongranada).

`git clone https://github.com/webuniongranada/webuniongranada.git`

Ahora debería de existir una carpeta llamada `webuniongranada`. Esta no la podréis renombrar. Volvemos a entrar en `vagrant` y ahora escribiremos `cd /vagrant/wug/apps/webuniongranada` para localizarnos dentro de la carpeta del proyecto.

Acto seguido ejecutaremos el siguiente comando `bundle install` que nos realizara la instalación de las gemas necesarias para el proyecto.

Al finalizar y si todo ha ido correcto ejecutaremos `bundle exec thin start -p 8000` para poder lanzar el servidor. Si todo ha ido bien nos dará un mensaje parecido a este

`Listening on 0.0.0.0:8000, CTRL+C to stop`

Bien todo funciona!!! El problema es que no podemos verlo en ningún sitio. Nos falta un último paso. Tenemos que configurar el archivos hosts de nuestro sistema operativo para que sepa donde tiene que resolver la URL del servidor que le especificaremos.

Tendremos que añadir esta linea. La linea es para decir que cuando pongamos wug.dev o webuniongranada.dev en el navegador, ambos redirigiran al servidor montado en vagrant.

`192.168.70.10 wug.dev webuniongranada.dev`

En windows este archivo se encuentra en `Windows\System32\drivers\etc\hosts` y en linux/mac `/etc/hosts`
