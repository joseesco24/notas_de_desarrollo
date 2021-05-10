# Notas De Kubernetes

- [Introducción](#introducción)
- [Contenedores En Kubernetes](#contenedores-en-kubernetes)
- [Arquitectura De Kubernetes](#arquitectura-de-kubernetes)
  - [Componentes De Los Nodos Maestro En Kubernetes](#componentes-de-los-nodos-maestro-en-kubernetes)
  - [Componentes De Los Nodos Esclavo En Kubernetes](#componentes-de-los-nodos-esclavo-en-kubernetes)
- [Sistemas Declarativos E Imperativos En Kubernetes](#sistemas-declarativos-e-imperativos-en-kubernetes)
- [Redes En Kubernetes](#redes-en-kubernetes)

<br>

## Introducción

<p align="center">
<img src="imagenes/notas_de_kubernetes/arquitectura_basica_kubernetes.svg" width="100%" height="auto"/>
</p>

[kubernetes](https://kubernetes.io/es/docs/concepts/overview/what-is-kubernetes/) es la plataforma de orquestación de contenedores más popular actualmente en el desarrollo profesional, esto en gran parte es gracias a que kubernetes apunta a ser una plataforma declarativa donde no se indique paso a paso todo lo que debe hacer la infraestructura si no que apunta a que se indique el estado deseado de esta y kubernetes se encarga de llegar a ese estado deseado, lo que hace más fácil la administración de la infraestructura, kubernetes además pertenece al [cncf](https://www.cncf.io/), lo que le da un enorme respaldo como plataforma de orquestación de contenedores, el principal trabajo de kubernetes es desplegar y gestionar contenedores en un cluster basándose en pods, algunas de las principales ventajas de utilizar kubernetes como plataforma para desplegar aplicaciones contenerizadas son:

- al ejecutar varias réplicas del mismo contenedor garantiza que todas las réplicas están funcionando.
- provee un balanceador de carga interno y externo para todos los servicios, por lo que no hace falta instalar balanceadores de carga o servicios de proxy inverso.
- permite definir varios mecanismos para hacer restauraciones y despliegues de un servicio.
- permite definir políticas de auto scaling.
- permite manejar muy en detalle los trabajos programados.
- permite definir políticas de roles.

en kubernetes un pod es una agrupación de contenedores que se ejecutan en el mismo host y que además comparten un namespace o interfaz de red, por lo que todos los contenedores dentro de un pod tienen la misma ip, gracias a esto todos los contenedores que están dentro de un pod se ven unos a otros como procesos ejecutándose dentro del mismo sistema, además en un pod pueden haber varios tipos de contenedores, lo que permite tener en un pod varios tipos de aplicaciones que necesariamente deben trabajar juntas.
cuando se escala algo en kubernetes no se agregan más contenedores, se agregan más pods.

<br>

## Contenedores En Kubernetes

los contenedores en kubernetes o en cualquier otra plataforma que use contenedores son entidades que no están definidas dentro del sistema operativo como las máquinas virtuales, los contendores son abstracciones puramente lógicas, que son el resultado de combinar varias tecnologías potenciando unas con otras para generar ambientes de ejecución aislados equivalentes a los de una máquina virtual, sin ser máquinas virtuales con sistemas operativos aislados, de hecho todos los contenedores comparten un mismo sistema operativo. las tres principales tecnologías que hacen posibles los contenedores en kubernetes y en la mayoría de las plataformas que usan contenedores son:

- **cgroups:** también llamados control groups son los encargados de que un proceso tenga aislados sus recursos, principalmente memoria, disco, red y cpu, gracias a los cgroups se puede indicar al kernel de linux con precisión qué recursos que puede usar un contenedor.
- **chroot:** permite llamar al contenedor como un proceso aislado cambiando su directorio raíz, gracias a chroot un contenedor tiene acceso a su directorio de trabajo sin tener acceso a los demás directorios del sistema de archivos del host.
- **namespaces:** permite aislar el contenedor en un sandbox de tal modo que el contenedor no pueda ver otros recursos del sistema operativo o de los demás contenedores, los namespaces además se dividen en varios tipos, pero los más importantes son:

  - **mount namespace:** permite que un proceso tenga una visibilidad reducida de los directorio de trabajo.
  - **networking namespace:** permite que cada contenedor tenga sus recursos de red separados y que los recursos de un contenedor no interfiera con los de los demás contenedores.
  - **process id namespace:** permite que los procesos secundarios se aniden en el proceso principal establecido al iniciar el contenedor, de tal modo que al finalizar el proceso principal se finalice la ejecución del contenedor.

<br>

## Arquitectura De Kubernetes

la arquitectura de kubernetes se basa en dos tipos de nodos, al igual que la mayoría de los sistemas de cómputo distribuido los nodos se dividen en maestro y esclavo, los maestros, que son designados usando el algoritmo [**raft**](https://www.freecodecamp.org/news/in-search-of-an-understandable-consensus-algorithm-a-summary-4bc294c97e0d/) son los encargados de administrar todos los recursos del cluster y de la asignacion de las tareas, mientras que los esclavos se encargan de ejecutar todas las tareas que les son asignadas por los maestros, kubernetes permite tener maestros redundantes ademas de poder utilizar mas de un maestro al tiempo, de tal modo que si un maestro falla por alguna razon este puede ser reemplazado casi de inmediato, ademas, en caso de que no se pueda reemplazar y el cluster no disponga de nodos maestro que lo reemplacen los demas componentes del cluster seguiran funcionando, simplemente el cluster no se podra administrar hasta que no se asigne un nuevo nodo maestro que lo controle.
kubernetes para comunicarse con los nodos maestro utiliza una api, todas las acciones de administración tiene que pasar por esta api para llegar a los nodos maestro, además del api kubernetes da una interfaz de usuario y un cli, ambos utilizan el api para comunicarse con los nodos maestro, pero también se pueden enviar las instrucciones de administración directamente al api.

<br>

### Componentes De Los Nodos Maestro En Kubernetes

- **etcd:** key value store que permite que el cluster esté altamente disponible.
- **servidor api:** el servidor api es a donde llegan todas las conexiones internas y externas del cluster, como los agentes de kubernetes, el cli, el dashboard y demás. cuando un nodo maestro falla solo se pierde el api que se usa para conectarse a ese nodo.
- **scheduler:** se encarga de ubicar los pods en los diferentes nodos, asignar las tareas y administrar los flujos de trabajo, revisando siempre las restricciones y los recursos disponibles de cada nodo.
- **controller manager:** es un proceso que está en un ciclo de reconciliación constante buscando llegar al estado deseado del cluster con base al modelo declarativo con el que se le dan instrucciones a kubernetes, los control manager además pueden ser de varios tipos, algunos de los más usados son:

  - **deployment manager**
  - **replica manager**
  - **service manager**

<br>

### Componentes De Los Nodos Esclavo En Kubernetes

- **kubelet:** los kubelet son agentes de kubernetes que se conectan con el scheduler y solicitan recursos (pods o contenedores) para ejecutar. además los kubelet monitorean los pods constantemente para saber si se están ejecutando correctamente, monitorea también los recursos disponibles y comunica constantemente al scheduler el estado de los recursos y las tareas.
- **kube-proxy:** se encarga de balancear el tráfico que se mueve entre los contenedores o servicios.

<br>

## Sistemas Declarativos E Imperativos En Kubernetes

en kubernetes todo se crea a través de una especificación en un archivo yml o manifest, estos archivos pueden variar segun la configuracion de kubernetes, la cual puede ser declarativa o imperativa, en el modo declarativo la especificación entregada a kubernetes indica el estado deseado del cluster y kubernetes trata de converger al estado deseado que le fue proporcionado, cuando kubernetes está configurado en modo declarativo constantemente revisa los cambios en el sistema y si algo falla calcula la diferencia entre el estado deseado, el estado actual y trata de que el estado actual converja hacia el estado deseado, por lo que al usar una configuración declarativa es totalmente necesario que el estado deseado pueda ser computado y comparado con el actual. cuando la configuración es imperativa los archivos de configuración se componen de una serie de pasos que kubernetes sigue ciegamente, su principal desventaja respecto a los sistemas declarativos es que al no proveer un contexto en caso de fallo del sistema debe iniciar desde cero su ejecución.

<br>

## Redes En Kubernetes

las redes en todos los clusters son fundamentales, ya que es mediante una red que se comunican todos los nodos del cluster, las redes en un cluster de kubernetes deben obedecer las siguientes reglas para que el cluster funcione correctamente.

- todos los nodos en un cluster de kubernetes se configuran bajo el mismo segmento de red, esto para que todos los pod, servicios y máquinas del cluster se puedan comunicar fácilmente unos con otros.
- los nodos del cluster deben conectarse entre sí sin usar nat, por lo que cada nodo debe tener una dirección ip asignada.
- los pods del cluster, al igual que los nodos, deben conectarse entre sí sin usar nat, por lo que cada nodo debe tener una dirección ip asignada.
- en kubernetes los pods a nivel de red en el modelo [**osi**](https://www.networkworld.com/article/3239677/the-osi-model-explained-and-how-to-easily-remember-its-7-layers.html) trabajan en capa 3 y los servicios en capa 4, por lo que es lo mas adecuado configurar segmentos de red diferentes para los servicios y para los pods, esto para evitar posibles colisiones entre el trafico de unos y otros.

observaciones adicionales sobre las redes en kubernetes.

- kubertenets utiliza un cni (container network interface) para cambiar las reglas de enrutamiento y así lograr que incluso cuando se usan segmentos de red diferentes para servicios y pueda haber comunicación entre ellos.
- kube-proxy es el componente de kubernetes que permite realizar conexiones entre pods y contenedores usando iptables para enrutar las conexiones de un componente con otro.

<br>
