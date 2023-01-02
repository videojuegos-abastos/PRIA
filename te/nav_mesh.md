Para implementar Pathfinding para cualquier objeto con los componentes que Unity nos proporciona, necesitaremos un agente y una malla. El agente
es el objeto que tendrá la capacidad de desplazarse inteligentemente, la malla es la superficie por donde éste se va a poder desplazar.

La malla, aunque la podemos crear en tiempo de ejecución, si siempre es igual, lo más óptimo es 



Los siguientes, son los componentes básicos para usar la navegación de Unity.

NavMeshAgent: Componente que llevará nuestro agente. Desde éste podemos controlar el *Tipo de Agente, su velocidad, aceleración o el modo de esquivar obstáculos.
El Tipo de Agente es el modelo físico del agente, según este la malla por la que se desplaza cambiará. Nuestro agente podría ser un Humanoide o un ogro
por ejemplo, el Ogro quizá poría ser más ancho y más alto por lo que se podrá acercar menos a los obstáculos (Por el hecho de ser más ancho),
pero podrá subir escalones más altos (Por ser más alto).

NavMesh Surface: El componente NavMeshSurface nos permite asignar una malla de navegación (NavMesh) a un objecto. Aunque podemos hacer un 'Bake'
en la pestaña 'Navigation', esto nos creará un NavMesh común a todos los 'NavMesh Agents', con lo que no podremos tener diferentes mallas de
navegación para distintos agentes. Si tenemos un "humanoide" y un "ogro", los dos tendrían que compartir la misma malla y si tenemos varios
agentes, probablemente no es eso lo que queramos.

Con NavMesh Surface, podemos guardarnos la malla en un objeto y controlar mejor para qué agente estamos haciendo el 'Bake' entre otras cosas.
Siempre es recomendable usar el NavMesh Surface.

NavMesh Modifier: El componente NavMeshModifier es un componente que podemos asignar a cualquier objeto para establecer cómo se tiene que comportar
a la hora de hacer el 'Bake'. Podemos definir un área (Walkable, No Walkable, etc...) o hacer que el 'Bake' no lo tenga en cuenta.

NavMesh Modifier Volume: Este componente es parecido al NavMeshModifier. La diferencia clave es que el primero, nos permite marcar un objeto, mientras
que este, nos permite marcar un volumen. Esto nos puede venir bien si el área que queremos establecer como "Dangerous" por ejemplo, no está delineada
por los objetos de nuestra escena.

NavMesh Link: Este componente nos permite enlazar dos NavMesh diferentes.


Pasos a seguir para que nuestro agente se mueva.

Marcar los objetos que van a componer el escenario y no se van a mover como 'static'.
