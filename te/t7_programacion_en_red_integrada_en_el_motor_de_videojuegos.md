# Programación en Red integrada en el Motor de Videojuegos

Para la programación de videojuegos multijugador vamos a utilizar [Netcode for GameObjects](https://docs-multiplayer.unity3d.com/), esta es la solución oficial de Unity para los juegos en red.

En este documento veremos algunas claves para empezar a utilzizarlo.

## Documentación oficial

* [Documentación Netcode](https://docs-multiplayer.unity3d.com/netcode/current/about/index.html)
* [Network Manager](https://docs-multiplayer.unity3d.com/netcode/current/components/networkmanager)
* [Network Object](https://docs-multiplayer.unity3d.com/netcode/current/basics/networkobject)
* [Network Transform && Client Transform](https://docs-multiplayer.unity3d.com/netcode/current/components/networktransform)
* [Network Behaviour](https://docs-multiplayer.unity3d.com/netcode/current/basics/networkbehavior)
* [Network Variable](https://docs-multiplayer.unity3d.com/netcode/current/basics/networkvariable)
* [RPCs](https://docs-multiplayer.unity3d.com/netcode/current/advanced-topics/messaging-system)
* [Network Animator](https://docs-multiplayer.unity3d.com/netcode/current/components/networkanimator)

## Configuración

La configuración inicial es muy sencilla, simplemente instalaremos desde el Package Manager el paquete `Netcode for GameObjects`.
Si queremos tener además una pequeña demo de cómo se utilizan los componentes que incluye y cual es el flujo a seguir a la hora de programar, podemos desde el mismo Package Manager abrir abrir los Samples y Importar cualquiera de los que haya en el momento. En principio debería haber una pequeña demo llamada Bootstrap.

Hay un detalle de configuración sobre el Network Manager, está en el apartado de [Primeros Pasos](#primeros-pasos).

## Arquitectura

Antes de ponernos a programar nada, hay varias cosas básicas que tenemos que saber.

Netcode utiliza el [Protocolo UDP](https://es.wikipedia.org/wiki/Protocolo_de_datagramas_de_usuario) ya que por lo general, los juegos necesitan transmitir información de forma muy rápida y no nos importa si algo se pierde por el camino.

> El Protocolo UDP nos permite enviar información muy rápidamente, esto es imprescindible en muchos videojuegos multijugador ya que necesitamos actualizar el estado varias veces por segundo. Algunos de los inconvenientes de UDP frente a [TCP](https://es.wikipedia.org/wiki/Protocolo_de_control_de_transmisi%C3%B3n) es que no sabemos si los *paquetes están llegando ni si lo están haciendo de forma ordenada. Para casos muy comunes como la posición, rotación o escala de un objeto por ejemplo, Netcode nos abstrae de la programación compleja de la lógica para tener en cuenta estos retrasos.

Con Netcode utilizaremos una arquitectura Cliente - Servidor, en el que dependiendo de la infraestructura que tengamos podremos tener un servidor dedicado o lo que llamaremos Host, es decir que uno de los clientes, además de ser cliente, haga de servidor. Esto, tiene sus ventajas e inconvenientes.

## Primeros pasos

Lo primero que debemos conocer es el objeto / componente `NetworkManager`. Este es el objeto más importante ya que es el que controlará toda la lógica y las conexiones. Este objeto es imprescindible y desde él podemos configurar la ip, puerto o latencia entre otras cosas.

> Como configuración adicional:
>
> Componente Unity Transport > Protocol Type > Seleccionamos Unity Transport.

Además, en muchos casos queremos acceder a él desde código ya que tiene funciones como `StartClient`, `StartServer` o `ConnectedClientsList`.

Podemos acceder a él desde el código utilizando la propiedad estática `Singleton`.

```c#
// NetworkManager.Singleton;

NetworkManager.Singleton.StartClinet();


NetworkManager netManager = NetworkManager.Singleton;

foreach (NetworkClient client in netManager.ConnectedClientsList)
{
    Debug.Log(client.clientId);
}

```

> *[Singleton](https://es.wikipedia.org/wiki/Singleton)

Con Netcode for GameObjects, tendremos objetos que transmiten algún tipo de información a través de la red. Estos objetos que van a tener que sincronizar información con otros clientes o con el servidor tendrán que cumplir que:

1. Tienen el componente `NetworkObject` o uno de sus padres tiene el componente `NetworkObject`.
2. El script desde el que vamos a acceder a propiedades relacionadas con la red hereda de `NetworkBehaviour` y **no** de `MonoBehaviour`.
3. El objeto está añadido en el `NetworkManager` en la lista `NetworkObjects`.

Si se cumplen estos requisitos, nos funcionarán correctamente.

A parte de esta lista, en el `NetworkManager` tenemos un `PlayerPrefab`, este es el objeto que por defecto, se creará cuando un juegador se conecte.

## Anexo

* Paquete: Cuando hablamos de paquete nos referimos a información que viaja a través de la red.

* Singleton: Patron de diseño con el que nos aseguramos que de una clase determinada solo existe instanciada de esta.  