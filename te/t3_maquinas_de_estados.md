# Máquinas de estados finitos (FSM)

Una máquina de estados finitos es un modelo de comportamiento de un sistema que se utiliza para modelar el comportamiento de inteligencias artificiales entre otras cosas.

En una máquina de estados tenemos varios elementos:

* **Estados**
* **Conexiones** entre estados.

Un *Estado* es una fase en la que se puede encontrar el modelo, el estado determina cómo se comporta el modelo. Las conexiones o transiciones entre estados nos indican de qué estado a qué otro estado podemos pasar. Esto se entiende fácilmente con un ejemplo.

<p align="center">
<img src="img/fsm.png" width="80%" />
</p>

Como vemos en la imagen, en este caso tenemos tres estados.

* Exploring (explorando)
* Attacking (atacando)
* Replenishing (reponiendo)

Además, tenemos cuatro transiciones entre estados. Si nos fijamos, podemos pasar del estado *atacando* al estado *reponiendo* pero no al revés, antes tendremos que pasar por el estado *explorando* y *atacando*.

El comportamiento de las máquinas de estados, como vemos es muy sencillo de entender.

El cambio de un estado a otro, como hemos dicho, viene marcado por las conexiones. En estas, además especificaremos las condiciones que se tienen que dar para que se transicione de estado. En el ejemplo que estamos viendo, si nos fijamos, las condiciones son si vemos o no al jugador y si tenemos más o menos vida.

Obviamente podemos personalizar las condiciones, haciendo que se tengan que cumplir más de una, que dependa del tiempo o que sean aleatorias.

> Podemos probar en el propio Unity a crear visualmente una máquina de estados para las animaciones. Aunque esta no sirva para modelar comportamiento nos puede venir bien para entender cómo funciona.

A nivel conceptual ya sabemos qué es una máquina de estados, estas son útiles para diferentes cosas, para todo aquello que tenga estados finitos fijos y que pueda cambiar de un estado a otro podemos utilizar las FSM. Unity utiliza las FSM para el sistema de animaciones.

Pongamos que tenemos un personaje que puede caminar, agacharse, correr, saltar o simplemente estar quieto. El personaje podrá estar en cualquier estado pero solo en uno a la vez (es decir que no puede estar corriendo y caminando al mismo tiempo). Como con las animaciones pasa esto, se utiliza un estado para cada animación y se definen posibles transiciones entre animaciones, ya que no podemos pasar de cualquier estado a cualquier otro. En nuestro caso por ejemplo podemos decidir que nuestro personaje no pueda pasar de estar corriendo a agachado.

> Las máquinas de estados es una técnica relativamente sencilla de implementar, además es útil si queremos que personas sin conocimientos de programación como un diseñador del juego puedan 'programar' el comportamiento de nuetra IA ya que podemos esquematizar y visualizar cómo se va a comportar.


## Contexto

En el contexto de la Inteligencia Artificial, utilizamos las máquinas de estados para modelar comportamientos. Exactamente como hemos visto en la imagen anterior, nuestro personaje controlado por la IA, tomará unas acciones dependiendo de diferentes variables que definiremos estratégicamente para simular un comportamiento inteligente.


## Implementación

Cuando implementamos una máquina de estados, es conveniente que cada estado tenga tres fases:

* Enter
* Update
* Exit

Cada una de estas nos servirá para una determinada tarea. La fase *Enter* se ejecutará una vez al entrar en el estado, aquí podemos preparar el contexto para que todo funcione.

En la fase *Update* actualizamos nuestro modelo y comprobamos las condiciones de salida.

La fase *Exit* se ejecutará antes de salir del estado y nos servirá para liberar todo aquello que ya no vamos a necesitar.