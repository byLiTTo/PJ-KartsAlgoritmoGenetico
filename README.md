# Videojuego 3D - Algoritmo genético

___
:school: Universidad de Huelva: Grado Ingeniería Informática - Computación     
:computer: Asignatura: Programación de Videjuegos     
:books: Curso 2019-2020     
___

## 1.- Introducción
En este proyecto hemos desarrollado un microgame con la temática de karting. Se trata de un juego donde el personaje maneja un kart en varios circuitos, con el objetivo de quedar primero en todos ellos. Como contrincante tendrá a otro kart manejado por un agente que ha sido implementado mediante un algoritmo genético. 

Como reto añadido, el juego posee un ranking de todos los circuitos con el top 10 de los jugadores con mejores tiempos en todos los mapas. Estos tiempos son la suma de las tres vueltas que se realizan en todos los mapas, cuanto mejores tiempos se realicen, más alto podrá escalar en el ranking. 

El videojuego ha sido implementado en el lenguaje C#, usando el motor grafico de Unity en la versión 2020.3.2f1. 

Todos los assets y elementos utilizados en este proyecto son de libre uso y se encuentran en los foros oficiales de Unity, los enlaces irán apareciendo durante el desarrollo de este informe o bien se puede acudir directamente a la bibliografía donde aparecerán todos ellos.

## 2.- Escenas del juego
A continuación, expondremos las diferentes escenas que forman el juego, explicando todos los elementos que aparecen en cada una de ellas. 

### Menú principal
La primera ventana que nos encontramos al iniciar el juego es el común menú principal.

**1.-PLAY:** Carga la escena de selección de dificultad.     
**2.-CONTROLS:** Activa la ventana que explica cómo son los controles del juego.     
**3.-SETTINGS:** Activa la ventana de configuración con todos los ajustes del juego.     
**4.-CLOSE:** Cierra y finaliza el juego.     
