USO DEL PROYECTO

1) PARA CREAR UN CONTENEDOR QUE USA LA APLICACIÓN DE CALCULADORA:
  docker run -d  -p 8081:8080 -e PBA=Servidor_8081 -v /home/jesusv/curso-dgp/vertx-sample:/vertx-sample kebblar/jdk18-utf8-debug-maven java -jar /vertx-sample/target/sample-1.0-SNAPSHOT-fat.jar


2) Se crean contenedores para los puertos 8081, 8082 y 8083.


3) EL PROYECTO
     La calculadora se creó de tal forma que se tienen cuatro servicios que son SUMA, RESTA, MULTIPLICACIÓN y DIVISIÓN

3) PARA PROBAR LOS SERVICIOS EN UN PUERTO:
     http://localhost:8081/api/suma?primerNum=30&segundoNum=10
     http://localhost:8081/api/resta?primerNum=30&segundoNum=10
     http://localhost:8081/api/multiplica?primerNum=30&segundoNum=10
     http://localhost:8081/api/divide?primerNum=30&segundoNum=10


4) PARA PROBAR CON EL BALANCEADOR DE CARGA
 
   a) Se configura el archivo "haproxy" para habilitar el servicio de balanceo, para lo cual se descomenta la línea "CONFIG=...", Y
      se agrega al finalla linea ENABLED=1.
 
   b) En el archivo haproxy.cfg se agregan las lineas para dar de alta el servicio y se agregan además al final seis líneas de código como se
      indica a continuación:
  
        // se agregan las lineas para dar de alta el backend y el frontend, para que el servicio se de por algún puerto, como puede ser el
          9090.

	// Se agregan las lineas de los servidores donde están los servicios REST.
	http://localhost:8081
	http://localhost:8082
	http://localhost:8083
	http://localhost:8084
	http://localhost:8085
	http://localhost:8086
   
    c) Se arranca el servicio haproxy con el comando
      sudo service haproxy start


    d) Finalmente, el balanceador de carga se prueba de la siguiente manera:
       http://localhost:9090/api/suma?primerNum=30&segundoNum=10
    
   
