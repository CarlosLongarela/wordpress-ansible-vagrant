[![Build Status](https://travis-ci.org/CarlosLongarela/LWP.svg?branch=master)](https://travis-ci.org/CarlosLongarela/LWP)
[![Percentage of issues still open](http://isitmaintained.com/badge/open/CarlosLongarela/LWP.svg)](http://isitmaintained.com/project/CarlosLongarela/LWP "Percentage of issues still open")
[![Average time to resolve an issue](http://isitmaintained.com/badge/resolution/CarlosLongarela/LWP.svg)](http://isitmaintained.com/project/CarlosLongarela/LWP "Average time to resolve an issue")



      ______       ___       __   ________
      ___  /       __ |     / /   ___  __ \
      __  /        __ | /| / /    __  /_/ /
      _  /___      __ |/ |/ /     _  ____/
      /_____/      ____/|__/      /_/



      Lord         Word           Press

      Lord of WordPress. One WordPress to rule them all.

      v: "0.0.1a"
      By: Carlos Longarela"

      Docs:       https://github.com/CarlosLongarela/LWP/wiki

# EN DESARROLLO - AÚN NO LISTA PARA PRODUCCIÓN

# LWP (Lord of WordPress)

LWP: Proyecto para el desarrollo de plugins y temas de WordPress con un entorno Ubuntu Xenial y Nginx, MariaDB y PHP 7.1 realizando el aprovisionamiento desde Ansible en la máquina virtual Vagrant (con VirtualBox).

## Tabla de Contenidos

- [Resumen](#resumen)
  - [WordPress](#wordpress)
  - [Vagrant](#vagrant)
  - [Ansible](#ansible)
  - [ngrok](#ngrok)
- [Instalación](#instalación)
- [Uso Básico](#uso-básico)
  - [Back Office](#back-office)
  - [MySQL](#mysql)
  - [PHPmyAdmin](#phpmyadmin)
  - [XDebug](#xdebug)
  - [Vagrant](#vagrant)
- [Desarrollo](#development)
  - [Módulos](#module)
  - [Temas](#theme)
  - [Acceder a servidor local](#acceder-a-servidor-local)

## Resumen

### WordPress

[WordPress](https://wordpress.org/) WordPress es un sistema de gestión de contenidos o CMS (por sus siglas en inglés, Content Management System) enfocado a la creación de cualquier tipo de sitio web. Originalmente alcanzó una gran relevancia usado para la creación de blogs, para convertirse con el tiempo en una de las principales herramientas para la creación de páginas web comerciales. Ha sido desarrollado en el lenguaje PHP para entornos que ejecuten MySQL y Apache, bajo licencia GPL y es software libre. [Wikipedia](https://es.wikipedia.org/wiki/WordPress)

El entorno de desarrollo incluye WordPress en su última versión

### Vagrant

[Vagrant](https://www.vagrantup.com/) Vagrant es una herramienta para la creación y configuración de entornos de desarrollo virtualizados.

Originalmente se desarrolló para VirtualBox y sistemas de configuración tales como Chef, Salt y Puppet. Sin embargo desde la versión 1.1 Vagrant es capaz de trabajar con múltiples proveedores, como VMware, Amazon EC2, LXC, DigitalOcean, etc. Aunque Vagrant se ha desarrollado en Ruby se puede usar en multitud de proyectos escritos en otros lenguajes, tales como PHP, Python, Java, C# y JavaScript. [Wikipedia](https://es.wikipedia.org/wiki/Vagrant_(software))

La máquina virtual está basada en Ubuntu 16.04 LTS (Xenial Xerus).

### Ansible

[Ansible](https://www.ansible.com/), es una herramienta de aprovisionamiento para sistemas Linux, Unix, y Window, que realiza tareas administrativas como instalar paquetes, configurar servicios, añadir bases de datos y usuarios, etc. desde un terminal y sin instalar nada en el servidor (sólo requiere acceso por SSH).

No es necesario tener instalado Ansible ne nuestro sistema ya que se ejecuta desde la propia virtual al utilizar `ansible_local`.

### ngrok

[ngrok](https://ngrok.com/) es una herramienta y servicio que permite realizar tuneling de las peticiones desde Intenert a la máquina local aunque esté detrás de una NAT o firewall. Esto es útil en multitud de casos, como por ejemplo si queremos mostrar a un cliente el actual estado de desarrollo pero aún no hemos hecho *deploy* del código a un sitio web accesible desde Internet.

## Instalación

Primero, tenemos que asegurarnos que tenemos [VirtualBox](https://www.virtualbox.org/wiki/Downloads) y
[Vagrant](https://www.vagrantup.com/downloads.html) instalados.

Después abrimos el terminal y `cd` en el directorio que contiene este README:

```shell
$ cd RUTA-AL-PROYECTO
```

Ahora sólo necesitamos levantar Vagrant y se instalará y configurará todo:

```shell
$ vagrant up
```

## Uso Básico

### Panel de control WordPress

Se puede acceder al panel de control del WordPress la siguiente url:

- [lwp.test/wp-admin](http://lwp.test/wp-admin)

Para autenticarse en el panel de control utilizaremos las siguientes credenciales:

- Usuario: lwp
- Clave: lwp

### MariaDB

Se puede acceder a la base de datos MariaDB con las siguientes credenciales _(en construcción)_:

- Host: localhost
- Puerto: 3366
- Usuario: root
- Clave: lwp

### PHPmyAdmin

Se puede acceder al PHPmyAdmin desde la siguiente url:

- [lwp.test/phpmyadmin](http://lwp.test/phpmyadmin)
- Usuario: lwp
- Contraseña: lwp

### XDebug

XDebug _(en construcción)_.

Para configurar XDebug necesitamos:

- fijar la ruta raíz del proyecto remoto a  `/home/webs/stable.wordpress.test/public`
- fijar la ruta raíz del proyecto local al workspace actual

Ahora nos conectamos a XDebug en el puerto 9000

Nota: Las configuraciones de XDebug se pueden asignar en el php.ini del rol _php7_.

### Vagrant

Vagrant está [muy bien documentada](https://www.vagrantup.com/docs/) pero aquí están algunos comandos:

- `vagrant up` - inicia la máquina virtual y la aprovisiona
- `vagrant suspend` - pone la máquina virtual _a dormir_ y con `vagrant resume` la devolvemos a su estado anterior
- `vagrant halt` - realiza un apagado ordenado de la máquina virtual
- `vagrant reload` - realiza un reinicio de la máquina virtual
- `vagrant ssh` - se conecta a la máquina virtual por ssh

Usuario ssh: ubuntu

## Desarrollo


Para el desarrollo tanto de plugins como de temas de WordPress, tenemos compartido el directorio raíz de la web de WordPress, por lo que podemos editar con nuestras herramientas favoritas de desarrollo desde `./www/public` en nuestra máquina local.

- **Temas** en `./www/public/themes`
- **Plugins** en `./www/public/plugins`

### Acceder a servidor local

_(en construcción)_

No es necesario subir el código a un website accesible desde Internet continuamente para obtener feedback del clientes.
ngrok crea una URL pública segura (https://yourapp.ngrok.io) al servidor local en tu máquina.

Para exponer el servidor local, necesitamos realizar los siguientes pasos:

```
$ vagrant ssh
$ cd /var/www
$ ./ngrok http 80
```

Ahora sólo necesitamos copiar la URL pública y enviársela al cliente.

PRECAUCIÓN: Se necesita cambiar la URL del sitio web de WordPress a la URL pública de ngrok, sino WordPress te redirigirá a localhost.
