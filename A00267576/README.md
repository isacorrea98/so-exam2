### Examen 2
**Universidad ICESI**  
**Curso:** Sistemas Operativos  
**Docente:** Daniel Barragán C.  
**Tema:** Namespaces, CGroups, LXC  
**Correo:** daniel.barragan@correo.icesi.edu.co  
  
**Estudiante:** Óscar Daniel Molano Torres  
**Código:** A00267576  
**Correo:** oscar.molano@correo.icesi.edu.co  

### Objetivos
* Comprender los fundamentos que dan origen a las tecnologías de contenedores virtuales
* Conocer y emplear funcionalidades del sistema operativo para asignar recursos a procesos
* Conocer y emplear capacidades de CentOS7 para la virtualización

### Prerrequisitos
* Virtualbox o WMWare
* Máquina virtual con sistema operativo CentOS7

### Descripción
El segundo parcial del curso sistemas operativos trata sobre el manejo de namespaces, cgroups y virtualización por medio de LXC/LXD

### Actividades
1. Incluir nombre, código (5%)
2. Ortografía y redacción cuando sea necesario (5%)
3. Realice una prueba de concepto empleando systemd y el recurso de control CPUQuota teniendo en cuenta los requerimientos que se describen a cotinuación. Incluya evidencias del funcionamiento de lo solicitado (30%):
 * Las pruebas se realizaran sobre un solo núcleo de la CPU  
   
 ![][1]  
   
 Podemos observar que la máquina virtual fue configurada para solo procesar con un solo nucleo de la máquina.  
 
 * Se deben ejecutar dos procesos  
 
 Se crearon dos scripts como se muestran a continuación:  
   
 test1.sh  
 ![][2]  
   
 test2.sh  
 ![][3]  
   
 Posteriormente se procedió a crear, habilitar e inicializar servicios que corriran estos scripts .sh:  
   
 proceso1.service  
 ![][4]  
   
 proceso2.service  
 ![][5]  
 
 * Cada proceso debe poder acceder solo al 50% de la CPU  
   
 Para esto se ejecutó el comando *systemctl set-property proceso1.services CPUQuota=50%* como se muestra a continuación:  
     
 CPUQuota=50% para el proceso1.services  
 ![][6]  
   
 CPUQuota=50% para el proceso2.services  
 ![][7]  
 
 * Cuando uno de los procesos se cancela, el que continua ejecutándose no debe acceder a mas del 50% de la CPU  
   
 Finalmente, se detuvo el proceso1.service y se pudo observar que el proceso2.service no accedia a más que el 50% de la CPU gracias a la configuración preivia:  
   
 ![][8]  
   
4.  Realice una prueba de concepto empleando systemd y el recurso de control CPUShares teniendo en cuenta los requerimientos que se describen a continuación. Incluya evidencias del funcionamiento de lo solicitado (30%):
 * Las pruebas se realizaran sobre un solo núcleo de la CPU  
   
 Para este punto se dejó la configuración de los nucleos de la maquina virtual de la misma manera que el punto anterior.  
   
 * Se deben ejecutar dos procesos  
   
 Se utilizaron los procesos proceso1.service y proceso2.service del punto anterior, elimiando la configuración de CPUQuota.  
   
 * Uno de los procesos tendrá el 25% de la CPU mientras que el otro tendrá el 75% de la CPU  
   
 Para esto se ejecutó el comando *systemctl set-property proceso1.services CPUShares=7680* y *systemctl set-property proceso12.services CPUShares=2560* como se muestra a continuación:  
   
 ![][9]  
   
 ![][10]  
   
 En las imagenes también podemos observar que ambos procesos están siendo ejecutados bajo las restriciones de CPUShares.  
 
 * Cuando uno de los procesos se cancela, el que continua ejecutándose debe poder llegar al 100% de la CPU  
   
 Para lograr esto se creó un script que fue capaz de reconfigurar el proceso2.service ya que se decidió que el proceso1.service era el proceso que se detendría. Adicionalmente este script era ejecutado automaticamente después de ejecutar la acción stop, por medio del parámetro *ExceStop* que se activa cuando reconoce la ejecución de este comando.  
 
 Script  
 ![][11]  
   
 Configuración ExceStop  
 ![][12]  
 
5. Por medio de las evidencias obtenidas en los puntos anteriores y de fuentes de consulta en Internet, elabore las definiciones para los grupos de control CPUQuota y CPUShares, además concluya acerca de cuando es preferible usar un recurso de control sobre otro (20%)
6. El informe debe ser entregado en formato pdf a través del moodle y el informe en formato README.md debe ser subido a un repositorio de github. El repositorio de github debe ser un fork de https://github.com/ICESI-Training/so-exam2 y para la entrega deberá hacer un Pull Request (PR) respetando la estructura definida. El código fuente y la url de github deben incluirse en el informe (10%)  

### Referencias
https://github.com/ICESI/so-containers

[1]: imagenes/nucleo.jpg  
[2]: imagenes/test1sh.JPG  
[3]: imagenes/test2sh.JPG  
[4]: imagenes/proceso1running.JPG  
[5]: imagenes/proceso2running.JPG  
[6]: imagenes/proceso1CPUQuota.JPG  
[7]: imagenes/proceso2CPUQuota.JPG  
[8]: imagenes/stopproceso1.JPG  
[9]: imagenes/proceso1CPUShares.JPG  
[10]: imagenes/proceso2CPUShares.JPG  
[11]: imagenes/pararproceso1.JPG  
[12]: imagenes/pararproceso11.JPG  
