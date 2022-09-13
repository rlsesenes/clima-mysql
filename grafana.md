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






