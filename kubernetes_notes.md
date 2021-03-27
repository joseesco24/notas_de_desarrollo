# Kubernetes - K8s

[Kubernetes](https://kubernetes.io/es/docs/concepts/overview/what-is-kubernetes/) es la plataforma de orquestación de contenedores mas popular actualmente, esto en parte es gracias a que Kubernetes apunta a ser una plataforma declarativo donde no se indique paso a paso todo lo que debe hacer la infraestructura si no que apunta a que se indique el estado deseado del cluster y Kubernetes se encarga de llegar a ese estado deseado, ademas kubernetes pertenece al [**CNCF**](https://www.cncf.io/), lo que le da un enorme respaldo a esta plataforma, el principal trabajo de Kubernetes es desplegar y gestionar contenedores en un cluster basándose en pods, algunas de las principales ventajas de utilizar Kubernetes como plataforma para desplegar aplicaciones contenerizadas son:

- Al ejecutar varias réplicas Kubernetes garantiza que todas las réplicas están funcionando.
- Provee un balanceador de carga interno y externo para todos los servicios, por lo que no hace falta instalar balanceadores de carga o servicios de inverted proxy.
- Permite definir varios mecanismos para hacer restauraciones y despliegues de un servicio.
- Tiene políticas de scaling automáticas.
- Permite manejar muy en detalle los trabajos programados.
- Permite dar políticas de roles.

Un pod es una agrupación de contenedores que se ejecutan en la misma máquina anfitrión y que además comparten un namespace o interfaz de red, por lo que todos los contenedores dentro de un pod tienen la misma IP, gracias a esto todos los contenedores que están dentro de un pod se ven unos a otros como procesos ejecutándose dentro del mismo sistema, además en un pod pueden haber varios tipos de contenedores, lo que permite tener en un pod varios tipos de aplicaciones que necesariamente deben trabajar juntas.
Cuando se escala algo en Kubernetes no se agregan más contenedores, lo que se escala son los pods.

## Apuntes de contenedores

Los contenedores no son entidades definidas dentro del sistema operativo como las máquinas virtuales, los contendores son una abstracción puramente lógica, que es el resultado de utilizar varias tecnologías trabajando en conjunto potenciando unas con otras para generar ambientes de ejecución aislados equivalentes a los de una máquina virtual sin ser máquinas virtuales con sistemas operativos aislados, de hecho todos los contenedores comparten un mismo sistema operativo, las tres principales tecnologías que hacen posibles los contenedores son:

- **cgroups:** También llamados control groups son los encargados de que un proceso tenga aislados sus recursos, principalmente memoria, disco, red y cpu, gracias a los cgroups se pueden indicar al kernel de Linux los recursos que puede usar un contenedor y las cantidades de cada recurso que puede usar.
- **chroot:** Permite al contenedor tener visibilidad sobre los archivos donde tiene que trabajar de tal modo que no pueda acceder a otros recursos del sistema.
- **namespaces:** Permite aislar el contenedor en un SandBox de tal modo que el contenedor no pueda ver otros recursos del sistema operativo o de los demás contenedores, los namespaces además se dividen en varios tipos, pero los más importantes son:

  - **mount namespace:** Permite que un proceso tenga una visibilidad reducida de los directorio de trabajo.
  - **networking namespace:** Permite que cada contenedor tenga sus recursos de red separados y que los recursos de un contenedor no interfiera con los de los demás contenedores.
  - **process id namespace:** Permite que los procesos secundarios se aniden en el proceso principal establecido al iniciar el contenedor, de tal modo que al finalizar el proceso principal se finalice la ejecución del contenedor.

## Arquitectura de Kubernetes

La arquitectura de Kubernetes está conformada principalmente de dos grandes partes, los nodos master y los dos minion, siendo los master los que controlan el estado del cluster y los minion que son los que realizan las tareas como tal, la interacción con kubernetes se realiza mediante un CLI o mediante una interfaz de usuario, en ambos casos esta comunicación pasa por un API .
