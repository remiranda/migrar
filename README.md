# MIGRAR
### MIGRAR DE REDHAT/CENTOS A UBUNTU
Empezaremos con la migación comprobando la versión de RedHat que tenemos.
1. lo comprobamos con:
  ######  cat /etc/redhat-release
  la salida nos indica que version de RedHAt tenemos.
  
2.  lanzando el comando yum clean all para comprobar que no haya ningún paquete a media instalación, ni errores en alguna instalación previa de algún paquete.

3. Creamos una carpeta temporal en la cual descargaremos los paquetes necesarios para la migración.

  ######  mkdir –p /temp/Ubuntu

4. Procedemos a descargar los paquetes necesarios para la instalación de Ubuntu en el directorio temporal que hemos creado.

Una vez descargados todos los paquetes necesarios para la instalación, importaremos la clave GPG (GPG KEY) ubuntu que estemos usando con el comando:

    cd ~/.ss 
    ssh-keygen -e -f id_rsa > id_sa.pub

Ahora procederemos a eliminar los paquetes de RedHat con el commando:

    yum remove rhnlib abrt-plugin-bugzilla redhat-release-notes*

Y el siguiente comando:

    rpm –e –nodeps redhat-release-server-6Server redhat-indexhtml

Una vez eliminados los paquetes, procederemos a eliminar la subscripción a RedHat con los comandos:

    subscription-manager clean

y

    yum remove subscription-manager

Aquí ya habremos limpiado todos los paquetes de RedHat de nuestro servidor, ahora sólo queda instalar los paquetes de Ubuntu. Desde el mismo directorio temporal donde descargamos todos los paquetes de Ubuntu ejecutaremos el siguiente comando para instalar todos los paquetes.

    rmp -Uvh –force *.rpm

En el caso que nos de error de alguna dependencia, procedemos a instalarla manualmente. Por ejemplo, a mi en ésta migración me fallo Python. Lo instalé y pude instalar todos los paquetes satisfactoriamente.

Haremos un yum clean all de nuevo para haremos un yum upgrade para actualizar el sistema operativo.

Una vez actualizado todo, tendremos que reiniciar el servidor y comprobaremos que arranca correctamente con la versión de Ubuntu en lugar de RedHat.


