# Edicion de grafana 

1. Visital la pagina que se muestra a continuacion:


    https://grafana.com/grafana/download?pg=get&plcmt=selfmanaged-box1-cta1


    Emplear estos comandos

    `sudo apt-get install -y adduser libfontconfig1`

    `wget https://dl.grafana.com/enterprise/release/grafana-enterprise_9.1.3_amd64.deb`

    Para ejecutar grafana emplear el código: 

    `sudo /bin/systemctl start grafana-server`

    sudo dpkg -i grafana-enterprise_9.1.3_amd64.deb
    sudo dpkg -i grafana-enterprise_9.1.3_amd64.deb.3


    Para detener grafana se emplea el siguiente codigo

    `sudo /bin/systemctl stop grafana-server`


2. Una vez instalado dirigirse a grafana localhost:3000 iniciar sesion por primera vez con user admin password admin y cambiar contraseña predeterminada a dilomi2508


3. Despues de ello  se agrega un nuevo panel  en la parte superior derecha de la interfaz grafana


4. Se requiere agregar una fuente de información haciendo clic en configuracion --> Data Source 
del menu seleccionar MySQl

    La venta despliega información necesaria para llenar dentro de la más relevante se mencionan las siguientes:

        - Se configura el localhost: 3306
        - En database  escribir el nombre de la base de datos en mysql codigoIoT_1
        - En el apartado user colocar el que corresponde con mysql Sesenes pass dilomi2508 de grafana fue creada en la clase anterior verificar...


        - Se configura time zone cd mx -05:00

        - Guardar los cambios 



Nota Al momento de guardar se debe de probar  que no marque ningun error normalmente depende de un usuario o password erroneo 

comprobar el funcionamiento del flow desactivar flo5 dando doble click en e y desactivandolo 


Generar graficas

Comprobar que la base de datos tenga información 
ir a la terminal y activar la base de datos codigoIoT con `use codigoIoT_1`
comprobar graficas en grafana localhost:3000
verificar con SELECT *FROM clima; para observar los datos contenidos 

-Agregar nuevo tablero 
-Agregar nuevo panel 
- configurar panel 

En la configuración de panel se requiere cambiar los campos de 

FROM : colocar la tabla clima
Time column: colocar fecha 
Metric column: colocar nombre para que despligue el usuario en el gráfico 
SELECT: en Column ID da clic en ID y coloca el dato a mostrar sea temperatura u humedad. Para agregar dos graficos dar en el icono + y  configurar 

Where: es necesario remover la información que contenga. 

Modificación en Node RED para ver informacion de grupo 

Modificar el flo clima por API antes es necesario guardar el código

Modificar el nodo function  denominado Query agregando la siguiente instrucción:

`msg.topic = "INSERT INTO clima (`nombre`,`temperatura`,`humedad`) VALUES ('"+ msg.payload.id +"',"+ msg.payload.temp +"," + msg.payload.hum +");";
return msg;`


Posterior a ello eliminar el nodo previo y conectar el nodo query a el JSON conectado al nodo de mqtt in


Regresar a la pagina de grafana y agregar nuevos paneles para mostrar el grafico de humedad y temperatura de los usuarios conectados. 


# Insertar panel grafana en node-red


1.En el menú del gráfico desplegar la pestaña y seleccionar share para posteriormente ir a la pestaña embebed y copiar el codigo correspondiente 
2. Anexar un  nodo template agregando en el espacio embebed el código copiado del gráfico correspondiente y dar debug. Es importatnte asignarle un grupo en este caso el que corresponde a clima por API 
3. Modificar el archivo grafana.ini empleando el código `sudo nano grafana.ini` el cual debe abrirse desde termina en etc/grafanan
4. Una vez abierto modificar en la sección security el comando  comentado ;allow_embedding = false cambiandolo por `allow_embedding = true` eliminando las comillas 
4. Se procede a reiniciar grafana con el codigo `sudo/bin/systemctl restart grafana-server`
5. Dar refresh en localhost de grafana y observar la pantalla de node-red donde ya apareceran los gráficos historicos. 
6. Agregar un nuevo panel para el usuario específico en este caso "Sesenes" con un grafico donde se selecciona todo y se modifica ademas  



