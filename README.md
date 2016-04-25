# Create service in linux/Creación de servicio en linux

* Create script/Creamos un script
```sh
$ vim /etc/init.d/myscript
```
* We add the following lines of code to the script/Agregamos las siguientes lineas de codigo al script
```sh
#!/bin/sh
#We indicate the path of our script or script to run/Indicamos la ruta de nuestro script o scripts a ejecutar
path=/home/myuser/myexample    

#Indicate the scripts to run/Indicamos los scripts a ejecutar
startup=$path/bin/start.sh       
shutdown=$path/bin/stop.sh

#We create functions (start, stop, restart) for flow execution of our scripts indicated/Creamos funciones(start, stop, restart) para flujo de ejecucion de nuestros scripts indicados
start() {
  echo -n $"Starting service: "
  $startup
  RETVAL=$?
  echo 
}
stop() {
  echo -n $"Stopping service: "
  $shutdown
  RETVAL=$?
  echo
}
restart() {
  stop
  sleep 10
  start
}

#Our script will have a parameter which will compare with the functionalities of start, stop and restart, if that message options are of a different send.
#Nuestro script tendra un parametro el cual compararemos con las funcionalidades de start, stop y restart, en caso que se de una distinta mandaremos mensaje de las opciones.
case "$1" in
start)
  start
  ;;
stop)
  stop
  ;;
restart)
  restart
  ;;
*)
  echo $"Options: $0 {start|stop|restart}"
  exit 1
esac

#End/Terminamos
exit 0
```

#We give execute permissions to our script/Daremos permisos de ejecucion a nuestro script
```sh
$ sudo chmod ug+x /etc/init.d/myscript
```

#Now we can run our script made service/Ahora podemos ejecutar nuestro script hecho servicio
```sh
$ sudo service myscript start
$ sudo service myscript stop
$ sudo service myscript restart
```

#We can add functionality to our service to start when you start the operating system/Podemos agregar funcionalidad a nuestro servicio para que inicie cuando inicia el sistema operativo
```sh
$ sudo update-rc.d myscript defaults
```



