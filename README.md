> # :copyright: https://github.com/viktoriiaStasiuk/CRUD_JSP
> **Proyecto bifurcado**
>
> ## MYSQL
> - Usuario: root
> - Contraseña: (sin contraseña)
> - Base de datos: **reservaHoteles**
>
> ## DESPLIEGUE EN UBUNTU 
>
> ### Instalación de software
> ```console
> sudo  apt  install  git  mysql-client  mysql-server  tomcat8  tomcat8-admin 
> ``` 
> ### Descarga de código fuente
> ```console
> git  clone  https://github.com/iesvelez-daw/JSP_CRUD_hoteles.git  &&  cd  JSP_CRUD_hoteles
> ```
>
> ### Introducción de datos
> ```console
> sudo su  # (Introducidos nuestra contraseña, para obtener acceso como root)
> 
> # Cambiamos el plugin de autenticación de auth_socket a mysql_native_password. 
> # Es necesario para que la aplicación conecte correctamente al servidor MySQL.
> echo "ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY ''" | mysql -u root
>
> echo "drop database if exists reservaHoteles; create database reservaHoteles" | mysql -u root
> cat reservahoteles.sql | mysql -u root -D reservaHoteles
> ```
> ### Despliegue en Tomcat 8
> ```console
> sudo su  # (Introducidos nuestra contraseña, para obtener acceso como root)
> 
> cp  mysql-connector-java-5.1.21.jar  /var/lib/tomcat8/lib
> cp  -r  ReservaHoteles  /var/lib/tomcat8/webapps/hoteles
> ```
>
> ### Ejecutar aplicación
>
> Abrimos en el navegador la URL http://localhost:8080/hoteles
>

# CRUD Reserva de hoteles
Trabajo compartido entre las asignaturas de programación y base de datos donde se realizará un CRUD (create, read, update and delete) en JSP y MySql
## Descripción

Temática CRUD: reservas de hoteles.

Lo primero que tiene que hacer el administrador para que la aplicación funcione es añadir un cliente, si no hay clientes no se pueden hacer reservas, una vez añadido el cliente se podrá hacer la reserva de cualquier hotel.
Los clientes se pueden añadir, modificar y dar de baja.
Las reservas solo se pueden añadir y cancelar, no se pueden modificar.

## Explicación de la APP con capturas de pantalla

### [index.jsp](https://github.com/luciaflores25/CRUD_JSP/blob/master/ReservaHoteles/index.jsp)
El index es la página principal, donde se puede elegir entre: añadir un cliente, ver un listado de clientes, añadir una reserva y ver un listado de reservas. </br>
<img src="img/index.PNG">

### [nuevoCliente.jsp](https://github.com/luciaflores25/CRUD_JSP/blob/master/ReservaHoteles/nuevoCliente.jsp) 
Al pulsar en el icono de añadir un cliente aparece el siguiente formulario donde hay que escribir los siguientes campos (El código de cada cliente se va auto incrementando, por lo que no hay que ponerlo): nombre del cliente, apellidos, DNI y email. </br>
<img src="img/nuevoCliente.PNG">

### [grabaCliente.jsp](https://github.com/luciaflores25/CRUD_JSP/blob/master/ReservaHoteles/grabaCliente.jsp) 
Esta página aparece cuando se pulsa el botón añadir y el cliente se ha añadido correctamente sin ningún fallo. Al pulsar el botón "Dar de alta otro cliente" te llevará de nuevo al formulario de nuevoCliente.jsp En el caso de pulsar aceptar te llevará al listado de todos los clientes. </br>
<img src="img/grabaCliente.PNG">

### [listadoCliente.jsp](https://github.com/luciaflores25/CRUD_JSP/blob/master/ReservaHoteles/listadoCliente.jsp) 
Desde esta página se puede ver el listado de los clientes y el código del cliente, que hará falta posteriormente para hacer una reserva. </br>
<img src="img/listadoCliente.PNG">

### [modificaCliente.jsp](https://github.com/luciaflores25/CRUD_JSP/blob/master/ReservaHoteles/modificaCliente.jsp) 
Desde la página del listado aparece el botón modificar que si se pulsa aparece el mismo formulario de nuevoCliente, pero relleno con los datos del cliente que hayamos seleccionado, en la siguiente imagen se muestra un ejemplo </br>
<img src="img/modificaCliente.PNG">

### [errorDNI.jsp](https://github.com/luciaflores25/CRUD_JSP/blob/master/ReservaHoteles/errorDNI.jsp) 
En el caso de que se pulse el botón añadir (formulario de nuevoCliente) o modificar (formulario modificaCliente) y haya registrado un cliente con el mismo DNI que se ha introducido, aparecerá la siguiente página de error, con el botón de intentar de nuevo que te vuelve a redireccionar a la pag de nuevoCliente.jsp </br>
<img src="img/errorDNI.PNG">

### [grabaClienteModificado.jsp](https://github.com/luciaflores25/CRUD_JSP/blob/master/ReservaHoteles/grabaClienteModificado.jsp) 
Esta página aparece cuando se pulsa el botón modificar y el cliente se ha modificado correctamente sin ningún fallo. Al pulsar aceptar te llevará al listado de todos los clientes para visualizar que se ha añadido correctamente, y al pulsar hacer otra modificación te llevará también al listado por si se desea hacer otra modificación. </br>
<img src="img/grabaClienteModificado.PNG">

### [confirmacionBorradoCliente.jsp](https://github.com/luciaflores25/CRUD_JSP/blob/master/ReservaHoteles/confirmacionBorradoCliente.jsp) 
Desde la página del listado de todos los clientes también se pueden dar de baja pulsando en "Borrar", donde aparecerá la siguiente confirmación. </br>
<img src="img/confirmacionBorradoCliente.PNG">

Para hacer una reserva volvemos al index.jsp

### [nuevaReserva.jsp](https://github.com/luciaflores25/CRUD_JSP/blob/master/ReservaHoteles/nuevaReserva.jsp) 
Desde el index al pulsar en el icono de añadir una reserva aparece el siguiente formulario donde hay que escribir los siguientes campos (El código de cada reserva se va auto incrementando, por lo que no hay que ponerlo): país del hotel, nombre del hotel y código cliente. </br> Para este formulario hay que recordar el código del cliente, de donde se extraen los datos del cliente al que corresponde el código introducido para mostrarlo en el listado de las reservas. </br>
<img src="img/nuevaReserva.PNG">

### [listadoReservas.jsp](https://github.com/luciaflores25/CRUD_JSP/blob/master/ReservaHoteles/listadoReservas.jsp) 
Si la reserva se añade correctamente aparecerá lo que se ve en la siguiente captura, un listado de todas las reservas con su correspondiente botón de cancelar. </br>
<img src="img/listadoReservas.PNG">

### [errorCliente.jsp](https://github.com/luciaflores25/CRUD_JSP/blob/master/ReservaHoteles/errorCliente.jsp) 
Si al añadir una nueva reserva, introducimos el código de un cliente que no está dado de alta, aparecerá un error como en el de la siguiente captura. </br>
<img src="img/errorCliente.PNG">

### [grabaReserva.jsp](https://github.com/luciaflores25/CRUD_JSP/blob/master/ReservaHoteles/grabaReserva.jsp) 
Esta página aparece cuando se pulsa el botón añadir y la reserva se ha añadido correctamente sin ningún fallo. Al pulsar el botón "Hacer otra reserva" te llevará de nuevo al formulario de nuevaReserva.jsp En el caso de pulsar aceptar te llevará al listado de todas las reservas. </br>
<img src="img/grabaReserva.PNG">

### [confirmacionBorrado.jsp](https://github.com/luciaflores25/CRUD_JSP/blob/master/ReservaHoteles/confirmacionBorrado.jsp) 
Al pulsar en el botón cancelar que aparece en el listado de las reservas, aparecerá una página de confirmación como se ve en la captura </br>
<img src="img/confirmacionBorrado.PNG">
