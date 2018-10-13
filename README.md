# MIGRAR
### MIGRAR DE REDHAT A UBUNTU/ CENTOS
Empezaremos con la migación comprobando la versión de RedHat que tenemos.
1. lo comprobamos con:
  ######  cat /etc/redhat-release
  la salida nos indica que version de RedHAt tenemos.
  
2.  lanzando el comando yum clean all para comprobar que no haya ningún paquete a media instalación, ni errores en alguna instalación previa de algún paquete.

3. Creamos una carpeta temporal en la cual descargaremos los paquetes necesarios para la migración.

  ######  mkdir –p /temp/centos

4. Procedemos a descargar los paquetes necesarios para la instalación de CentOS en el directorio temporal que hemos creado.

Una vez descargados todos los paquetes necesarios para la instalación, importaremos la clave GPG (GPG KEY) apropiada para la versión de CentOS que estemos usando con el comando:

    rpm –import RPM-GPG-KEY-CentOS-6

Ahora procederemos a eliminar los paquetes de RedHat con el commando:

    yum remove rhnlib abrt-plugin-bugzilla redhat-release-notes*

Y el siguiente comando:

    rpm –e –nodeps redhat-release-server-6Server redhat-indexhtml

Una vez eliminados los paquetes, procederemos a eliminar la subscripción a RedHat con los comandos:

    subscription-manager clean

y

    yum remove subscription-manager

Aquí ya habremos limpiado todos los paquetes de RedHat de nuestro servidor, ahora sólo queda instalar los paquetes de CentOS. Desde el mismo directorio temporal donde descargamos todos los paquetes de CentOS ejecutaremos el siguiente comando para instalar todos los paquetes.

    rmp -Uvh –force *.rpm

En el caso que nos de error de alguna dependencia, procedemos a instalarla manualmente. Por ejemplo, a mi en ésta migración me fallo Python. Lo instalé y pude instalar todos los paquetes satisfactoriamente.

Haremos un yum clean all de nuevo para haremos un yum upgrade para actualizar el sistema operativo.

Una vez actualizado todo, tendremos que reiniciar el servidor y comprobaremos que arranca correctamente con la versión de CentOS en lugar de RedHat.


