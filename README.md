CC2 - Proyecto #2 - Process Scheduler
Proyecto: Process Scheduler
Tema:Pilas, Colas, Herencia y Threads
Fecha de Entrega: 4 de noviembre, 2015
Grupo: Individual o en Parejas
Calificacion personal:Nosotros le indicaremos
ATENCION: Todos los proyectos consumen tiempo, asi que trate de empezar lo mas pronto que pueda. Recuerde que el proyecto es individual entre grupos , es decir que no puede trabajar junto a otros compaeros de otro grupo. No puede compartir codigo con ningun otro estudiante. Si se encuentra codigo compartido o soluciones iguales, se tomara como copia y se le evaluara con -100.
Process Scheduling

Para este proyecto ustedes implementaran una simulacion de un Calendarizador de Procesos tal y como lo hacen los procesadores para atender a todos los procesos que solicitan de su servicio. La multiprogramacion permite que varios procesos utilicen varios recursos del sistema simultaneamente. Esto incrementa el uso de cada recurso (por ejemplo: un proceso utiliza el CPU mientras otro utiliza el disco, los dos recursos estan siendo utilizados). Cuando se disenia un sistema como este, la dificultad se presenta cuando hay mas de un proceso compitiendo por el mismo recurso. Es entonces donde se debe aplicar un algoritmo que decida cual de los procesos recibira el servicio primero.

Generalmente, los procesos son todos diferentes, y se diferencian por el tiempo que requieren el servicio, y/o alguna prioridad. Existen politicas de calendarizacion que toman en cuenta estas caracteristicas para decidir que proceso es el que debe ser atendido primero. A continuacion le explicaremos algunas de las politicas para process scheduling :
First-Come First-Served (FCFS): El proceso que llega de primero, es el primero en ser atendido.
Last-Come First-Served (LCFS): El proceso que llega de ultimo es atendido primero.
Priority Policy (PP): El proceso que tiene mayor prioridad es el que se atiende de primero.
Round-Robin (RR): Se define una unidad de tiempo fija llamada quantum. Cada proceso se atiende esa unidad de tiempo, en una forma FCFS, y si no alcanza ese tiempo para concluir el requerimiento del proceso, el proceso pasa a la cola a esperar su turno otra vez. Entonces, el tiempo que requiere el proceso, es dividido en quanta (plural de quantum) y eso seria el total de veces que tendria que hacer cola. Cuando su tiempo requerido acaba, sale de la cola definitivamente.
Su proyecto
En general:
ÀQue es lo que tiene que hacer en su proyecto? Implementar la simulacion de el funcionamiento de un Calendarizador de Procesos. Su calendarizador debe implemetar simulacion para las cuatro politicas descritas anteriormente:

First Come First Served
Last Come First Served
Round Robin
Priority Policy
Random (elije procesos a atender en forma aleatoria en la cola)
utilizando solo una cola de atencion y un procesador
Especificaciones:
La politica en que se manejaran los procesos sera escogida por el usuario al momento de ejecutar el programa. Por cada ejecucion solo se podra correr la simulacion de una politica a la vez (Mas adelante se mostrara como elije el usuario dicha politica). Ya escogida la politica, su programa debe empezar la simulacion de ingreso y atencion de procesos.

Cada proceso debe guardar un numero de id (codigo) y un tiempo de servicio en segundos o milisegundos (como le funcione a ud mejor). Este tiempo esta definido dependiendo el tipo de proceso que sea. En este proyecto manejaremos cuatro tipos de proceso: Aritmetico, de Input/Output, condicional e iterativo. Los tiempos seran definidos al momento de mandar a ejecutar el programa, y seran fijos para todos los procesos del mismo tipo. Ejemplo: Todos los procesos Aritmeticos duran 400 milisegundos, todos los de input/ouput duran 200 milisegundos, y asi sucesivamente.

Los procesos deben ser generados en forma aleatoria, y en tiempos aleatorios. El id de los procesos debe ir incrementando (no es aleatorio) con cada proceso, es decir que el primer proceso tendra id = 1, el segundo id = 2, etc. Su tipo sera aleatorio, es decir que se eligira de forma aleatorea que tipo de proceso es (aritmetico, input/output. etc...). El numero correlativo es compartido entre todos los tipos de proceso, es decir que no hay contadores separados para cada tipo.

Los procesos generados aleatoriamente se posicionaran en una "cola" de servicios, esta "cola" debe ser implementada segun la politica que se haya escogido. Para el caso de Priority Policy solamente, los procesos se iran metiendo en la cola correspondiente a su prioridad. La prioridad de un proceso se debe elegir aleatoriamente al momento de crearse y debe estar entre 1 y 100.

Al mismo tiempo que llegan los procesos a la "cola" el "procesador" debe irlos atendiendo, otra vez, dependiendo de la politica que se haya escogido. Cada proceso tiene su tiempo de servicio, y eso es lo que se debe tardar el "procesador" en atenderlos. Como esto es solo una simulacion, el procesador solo tiene que "esperar" los milisegundos que el proceso tardaria en ser atendido, en vez de atenderlo en realidad. Es decir :
Si un proceso n tiene tiempo de 1000 milisegundos entonces su procesador deberia ejecutar un:
  		Thread.sleep(1000);
para tardarse exactamente lo que el proceso debe tardarse. La simulacion de la atencion al proceso es simplemente pausar el programa procesador por el tiempo que el proceso tenga asociado, no hay que hacer nada mas.
Despues de ser atendido, el proceso se elimina de la "cola" y se atiende el siguiente proceso. En el caso Priority Policy la atencion de procesos es por prioridad, la prioridad esta definida por los tipos de proceso: Se atenderan primero los de input/output, despues los aritmeticos, despues los condicionales y despues los iterativos.
Definicion de sus clases:
Las clases que se le proveen para este proyecto estan aqui: scheduler.zip, cuya documentacion puede encontrar aqui(se puede ver desde index.html).
Para la definicion de sus clases debe cumplir con lo siguiente:

En este proyecto SE DEBE utilizar herencia, clases abstractas e interfaces.
Debe definir cuatro tipos de proceso: ArithmeticProcess, IOProcess, ConditionalProcess, y LoopProcess. Se le provee una clase abstracta SimpleProcess para que todos sus tipos de procesos hereden de ella (TIENE que heredar de ella). Las clases que usted defina para esto deben pertenecer al paquete llamado scheduler.processing. Recuerde que los procesos ademas de su id, guardan un tiempo de procesamiento y este es IGUAL para todos los procesos que sean del mismo tipo. El tiempo de cada proceso es definido como argumento a la hora de iniciar la ejecucion del programa.
Tome en cuenta que para la politica Round Robin, el proceso deberia tener dos tiempos, el tiempo total de procesamiento (que dependera del tipo de proceso) y el tiempo que le falta para terminar de ser procesado.
Cada una de las clases que representen una politica deben heredar de la clase abstracta Policy e implementar la interfaz Enqueable incluidas en las clases proveidas para el proyecto. Todas estas deben pertenecer al paquete llamado policies, el cual es subpaquete del paquete scheduler.scheduling. Y las clases que las utilicen deben importar este paquete.
Las clases que defina (que no sean politicas o tipos de proceso), deben pertenecer al paquete scheduler, no estar metidas en un subpaquete de el. Ejemplo: procesador y generador de procesos.
DEBE utilizar pilas y colas para guardar los procesos. NO puede utilizar arreglos o ArrayList.
Las clases como estructuras de datos que se le permiten utilizar son: ConcurrentLinkedQueue como cola, Stack como pila y LinkedList como lista encadenada, proveidas en Java. La estructura de LinkedList solo puede ser utilizada en una politica, no mas. NO puede utilizar estructuras de datos hechas por usted.
NO puede utilizar Menus para la ejecucion de politicas.
La clase principal: ProcessScheduler no debe pertenecer a ningun paquete.
TODAS sus clases deben ir comentariadas de la siguiente forma:
En la primera linea debe llevar siempre el nombre del archivo
			/* Proceso.java */
En la parte de arriba deben llevar nombre del implementador, seccion y carnet
			/**
			 ** Hecho por: Juan Perez
			 ** Carnet: 14007891
			 ** Seccion: A
			**/	
Despues debe llevar una breve descripcion de para que sirve la clase.
Cada uno de los metodos debe llevar un comentario antes de la declaracion en donde diga como se llama el metodo, que parametros recibe y que devuelve al final y para que sirve.
Presentacion:
Recuerde que usted debe seguir TODAS las especificaciones del proyecto para que no se le bajen puntos en su calificacion total del mismo. He aqui entonces las especificaciones para su presentacion:
Su programa se debe poder mandar a ejecutar de las siguientes formas (note que es desde la consola de comandos):
	
	java ProcessScheduler -politica(en minusculas) rango_tiempo_ingreso arith io cond loop                   
En la bandera -politica debe ir -fcfs para FIRST COME FIRST SERVED, -lcfs para LAST COME FIRST SERVED, -rr para ROUND ROBIN, -pp para PRIORITY POLICY y -rand para RANDOM POLICY
Con respecto a los tiempos: rango_tiempo_ingreso es el rango de tiempos dentro del cual se elije aleatoriamente el tiempo en el que se va a ingresar un nuevo proceso; arith es el tiempo que duran los procesos aritmeticos; io es el tiempo que duran los procesos input/ouput; cond es el tiempo que duran los procesos condicionales; y loop es el tiempo que duran los procesos iterativos. Para la politica Round Robin, hay que agregar un tiempo adicional quantum.

	java ProcessScheduler -fcfs rango_tiempo_ingreso arith io cond loop  o
	java ProcessScheduler -lcfs rango_tiempo_ingreso arith io cond loop  o
	java ProcessScheduler -rr   rango_tiempo_ingreso arith io cond loop  quantum  o
	java ProcessScheduler -pp   rango_tiempo_ingreso arith io cond loop  o
	java ProcessScheduler -rand   rango_tiempo_ingreso arith io cond loop            
	
	Ejemplos:
			java ProcessScheduler -fcfs  1.5-3  2 1 2.5 3     
				
			Significa que su Process Scheduler debe utilizar la politica FIRST COME FIRST SERVED,
			utilizando para la simulacion 1 programa procesador,
			Tiempo de entrada de procesos debe estar entre 1.5 segundos y 3 segundos
			El tiempo de procesos aritmeticos es 2 segundos
                         El tiempo de procesos input/output es 1 segundo
                         El tiempo de procesos condicionales es 2.5 segundos
                         El tiempo de procesos iterativos es 3 segundos
				
			java ProcessScheduler -rr  1-2.5  1.5 1 3 4  0.5
			politica: Round Robin
			tiempo de entrada entre 1 y 2.5 segundos
			El tiempo de procesos aritmeticos es 1.5 segundos
                         El tiempo de procesos input/output es 1 segundo
                         El tiempo de procesos condicionales es 3 segundos
                         El tiempo de procesos iterativos es 4 segundos
			y un quantum de 0.5 segundos.
			
Ya escogida la politica, el process Scheduler debe empezar el simulador e imprimir los datos correspondientes en la pantalla.
Al correr la simulacion, su programa debe desplegar en pantalla la siguiente informacion:
La cola de procesos: representando cada proceso con su numero, su tiempo de atencion y su tipo: A si es aritmetico, IO si es de input/output, C si es condicional y L si es iterativo.
Todos los datos de el proceso o procesos que estan siendo atendidos en el momento
la politica que se esta utilizando
El numero de procesos ya atendidos hasta el momento.
Cada vez que se de una accion: Ingreso de proceso a la cola(s), se termino de atender un proceso y se empieza a atender otro, se debe desplegar en pantalla toda la informacion: cola, procesos, etc.
La informacion debe ser ordenada y legible.

Su programa terminara si oprimimos la tecla q. (Puede ser q y ENTER). Y puede detenerse en cualquier momento de la ejecucion. Al detenerse debe imprimir en la pantalla la informacion de: cuantos procesos se atendieron, cuantos procesos quedaron en cola (sin atenderse), el tiempo promedio de atencion por proceso (por procesador) y la politica utilizada. Para el caso de round-robin entre los procesos atendidos solo se tomara en cuenta los procesos que se terminaron de atender por completo.
Estas son todas las especificaciones que necesita para realizar el proyecto, si en caso tiene alguna duda sobre especificaciones SOLO puede preguntarle a la catedratica del curso. Asi nos evitaremos ambiguedades.
Entrega de su solucion

Todo su proyecto debe estar en un directorio llamado pj2, en el cual debe incluir los directorios ya hechos de los paquetes (con los paquetes ya compilados). Completado su directorio, debe agregarlo a un archivo pj2-GrupoN.zip y subirlo al GES.

No puede entregar su proyecto tarde

Para poder obtener su numero de grupo debe mandar un correo a su catedratico (andreaq@galileo.edu, alilemus@galileo.edu, mrm_31@galileo.edu o marito.h@galileo.edu) indicando quienes seran sus integrantes del grupo o si lo hara individual. Debe incluir su seccion. Este correo debe llegar a mas tardar un dia ANTES de la entrega del proyecto, despues de eso ya no se crearan grupos.

Puntos Extra

Para poder implementar los puntos extra, deberia haber terminado el proyecto completo, NO se meta a hacer puntos extra antes de terminarlo.

Ninguna politica adicional , se le tomara en cuenta, asi que ni lo haga.
Puede implementar su proyecto en forma grafica. (Applets o JFrames)
Puede implementar la documentacion de java para sus clases, que se pueda generar con javadoc (formato API)
Cualquier cosa adicional(que no sea otra politica) que implemente por su propia cuenta y se considere para puntos extra.
EXITOS Y MUCHA SUERTE!
andreaq@galileo.edu, alilemus@galileo.edu, mrm_31@galileo.edu, marito.h@galileo.edu