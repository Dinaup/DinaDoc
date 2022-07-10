




# Introducción
A nivel de IT. Dinaup no es más que un gestor de datos. Un software con una interfaz amigable que fácilita a las empresas el proceso de (Agregar / Editr / Eliminar / Compartir) los datos. \
Los datos están guardados en una base de datos PostgreSQL.

Hemos desarrollado 2 aplicaciones (.exe) principales.
1. **DinaupS.exe**: Este ejecutable es Dinaup Servidor. Un servicio de Windows. El que conecta a PostrgreSQL. No tiene interfaz, se ejecutando en segundo plano.
1. **Dinaup.exe**: Este ejecutable es el Terminal de Dinaup. Un software con interfaz amigable desde el cual se administran los datos de la empresa. Este ejecutable, por motivos de seguridad y optimización conecta por TCP / IP a `Dinaup Servidor`
1. **Tadmin.exe**: Esta aplicacion es una pequeña herramienta utilizada para poder iniciar, detener el Dinaup Servidor.


# Dinaup Servidor

![](/imagenes/Captura_DinaupServidor.PNG)

El servidor debe ejecutarse en un ordenador con SAI o en la nube. Debe tener accesible el puerto (defecto `19263`).

Se encuentra en `c:\Dinaup\Dinaups.exe`

Cuando se inicia el servidor extrae las dependencias y crea la base de datos automáticamente si es necesario.\
La base de datos PostgreSQL está en `c\Dinaup\SQL64\data`

Si desea iniciar el servicio puede utilizar  `c:\Dinaup\TAdmin.exe`


> **Note** 
> Este ejecutable únicamente está en el servidor

# Dinaup Terminal

![](/imagenes/Captura_DinaupTerminal.PNG)

> **Note** 
> Este ejecutable únicamente está tanto en el servidor, como en el ordenador de los empleados.




 
