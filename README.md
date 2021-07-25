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

___

## 2.- Escenas del juego
A continuación, expondremos las diferentes escenas que forman el juego, explicando todos los elementos que aparecen en cada una de ellas. 

### Menú principal
La primera ventana que nos encontramos al iniciar el juego es el común menú principal.

**1.-PLAY:** Carga la escena de selección de dificultad.     
**2.-CONTROLS:** Activa la ventana que explica cómo son los controles del juego.     
**3.-SETTINGS:** Activa la ventana de configuración con todos los ajustes del juego.     
**4.-CLOSE:** Cierra y finaliza el juego.    

#### Ventana CONTROLS

**1.-Controles del Kart:** Teclas asignadas al control del player, posee dos posibilidades.     
**2.-Tecla de pause:** Tecla con la que se pausa el videojuego mientras se juega una carrera.     
**3.-Close CONTROLS:** Cierra la ventana de controls y vuelve al menú principal.     
**4.-CLOSE:** Cierra y finaliza el juego.     

#### Ventana SETTINGS

**1.-RESOLUTION:** Selector de la resolución del juego, obtiene los datos de la gráfica y los muestra.     
**2.-FULLSCREEN:** Marcador que escoge entre el modo ventana y el modo pantalla completa.     
**3.-GRAPHICS:** Selector de la calidad del juego, existen 4 configuraciones.     
**4.-RESET RANKINGS:** Borra los datos de los rankings de los circuitos y pone el top 10 a 0:00:00.     
**5.-Close SETTINGS:** Cierra la ventana de settings y vuelve al menú principal.     
**6.-CLOSE:** Cierra y finaliza el juego.     

2. Selección de dificultad 

![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.008.jpeg)

**1.-NAME:** Campo de texto donde se introduce el nombre que aparecerá en el ranking. **2.-100CC:** Dificultad baja del juego. Carga la escena de selección de circuitos 100cc. **3.-150CC:** Dificultad alta del juego. Carga la escena de selección de circuitos 150cc. **4.-BACK:** Vuelve a cargar la escena del menú principal. 

3. Selección de circuito 

![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.009.jpeg)

**1.-COUNTRY:** Carga la escena del mapa llamado country. **2.-OVAL:** Carga la escena del mapa llamado oval. **3.-LOOPING:** Carga la escena del mapa llamado looping. **4.-LONG:** Carga la escena del mapa llamado long. **5.-MOUNTAIN:** Carga la escena del mapa llamado mountain. **6.-BACK:** Vuelve a cargar la escena de menú principal. 

4. Carrera 

![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.010.jpeg)

**1.-TAB:** Tecla que activa la ventana de pause del circuito. 

**2.-LAPS:** Indicador de las vueltas realizadas hasta el momento y las totales. **3.-MENSAJES:** Rápidas indicaciones como que se comienza la última vuelta, etc. **4.-CURRENT:** Tiempo que se está haciendo en la vuelta actual. 

**5.-BEST LAP:** Mejor tiempo realizado en todas las vueltas hasta el momento. **6.-LAP x:** Tiempo realizado en la vuelta con dicho número. Vueltas anteriores. 

**2.4.2 Ventana pause** 

![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.011.jpeg)

**1.-SHADOWS:** Activa las nombras de los elementos del circuito. 

**2.-FRAMERATE COUNTER:** Activa el contador de FPS por pantalla. Esquina superior derecha. **3.-CONTROLS:** Activa la ventana de controls. 

**4.-DONE:** Cierra la ventana del menú pause. 

**5.-EXIT:** Carga la escena de selección de dificultad. 

5. Partida perdida 

![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.012.jpeg)

**1.-MENU:** Carga la escena del menú principal. 

**2.-PLAY AGAIN:** Carga la escena del selector de dificultad. 

6. Partida ganada 

![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.013.jpeg)

**1.-RANKING:** Carga la escena del ranking del circuito donde se ha ganado. **2.-MENU:** Carga la escena del menú principal. 

**3.-PLAY AGAIN:** Carga la escena del selector de dificultad. 

7. Ranking 

![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.014.jpeg)

**1.-RANKING:** Top 10 de jugadores y sus tiempos realizados. Por defecto 0:00:00. **2.-BACK:** Carga la escena del menú principal. 

3. Funcionalidades del juego ![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.015.png)
1. Red Neuronal (NNet) 

El objeto NNet se encarga de almacenar una red neuronal. Esta red, se encargará de controlar al agente. Su objetivo será aprender a conducir por un circuito. Las principales variables que tiene la red son: 

- **inputLayer:** Entradas que recibirá la red neuronal.** 
- **hiddenLayers:** Capas ocultas de la red neuronal.** 
- **outputLayer:** Salida de la red neuronal.** 
- **Weights:** Determina el peso de cada neurona de una capa a otra.** 
- **Bias:** Valor independiente a los weights y a los inputs de cada neurona.** 
- **Fitness:** Parámetro usado para estipular cómo de bien funciona la red neuronal.** 

La red cuenta con la función RunNetwork, que a través de una entrada por parámetro (el valor de la inputLayer) devolverá una lista de valores normalizados entre -1 y 1. En nuestro juego, la inputLayer es un conjunto de nueve sensores que determinan la proximidad del agente a los límites de la carretera. La outputLayer devuelve dos valores, una para determinar la velocidad y otro para terminar la cantidad de giro a izquierda o derecha. 

2. Algoritmo genético (GeneticManager) 

Clase encargada de gestionar el aprendizaje de las redes neuronales. Para ello entrenará de forma continuada a una población de agentes (redes neuronales) hasta conseguir el objetivo deseado. Para ese cometido, una vez completada una generación se cruzará a los mejores agentes para obtener hijos que combinen las características de ambos. De no especificar un número de cruces igual al número de la población inicial, se crearán hijos con valores aleatorios para añadir diversidad de genes. Al final de cada generación se guarda el agente con el mejor resultado para su posterior uso. Las principales variables de la clase son: 

- **Controller:** Coche a controlar.** 
- **Initial population:** Población inicial de agentes.** 
- **Mutation rate:** Probabilidad de mutación en una neurona al combinar dos genes.** 
- **Best Agent Selection:** Número de agentes que serán seleccionados entre toda la población como los mejores.** 
- **Worst  Agent  Selection:**  Número  de  agentes  que  serán  seleccionados  entre  toda  la población como los peores.** 
- **Number to crossover:** Número de hijos que se crearán a partir de los mejores agentes y los peores.  Es  importante  seleccionar  a  algunos  agentes  malos  para  que  los  hijos  no  se especialicen en hacer algo concreto. Dicho más técnicamente, para no caer en máximo locales.** 
- **Alpha:** Valor de ajuste a la hora de fusionar dos genomas de las selecciones.** 
- **Train circuit:** Número de circuito en el que correrá la red neuronal. Se usa para cargar el fichero que contiene los datos guardados del entrenamiento, así como para guardar el resultado de los tiempos realizados en la carrera.** 
- **Difficulty:** La dificultad en la que se ejecuta la carrera, es el segundo parámetro para definir el fichero mencionado anteriormente y también para guardar los resultados correctamente y poder diferenciar todos los rankings.** 
- **Genepool:** Lista de mejores y peores agentes de los cuales a partir de ellos será creada la nueva población.** 
- **Current Generation:** Variable de control que estipula el número de generación en la que nos encontramos.** 
- **Current  genoma:**  Variable  de  control  que  estipula  el  número  de  genoma  que  nos encontramos en el momento actual.** 
3. Control de la carrera 

Como se trata de un conjunto de clases, donde algunas de ellas venían programadas en tutoriales de  Unity  y  no  hemos  aprovechado  todo  su  potencial  de  código,  vamos  a  comentar  las funcionalidades que hemos usado o que hemos modificado a nuestro favor, para hacer funcionar el juego de manera correcta. 

Lo primero que observamos al iniciar la carrera es una cuenta atrás, esto además de simular las carreras reales, nos sirve para asegurarnos de que tanto el agente como el jugador comienzan la carrera exactamente al mismo tiempo. 

Tras atravesar la línea de meta por primera vez se activa los contadores de tiempo, en este caso, solo es visible por pantalla el del jugador. Para poder completar la vuelta y que suba al marcador, el jugador debe atravesar los aros que se encontrará en el circuito. Si se mantiene dentro del circuito y manteniendo la trazada correcta, los atravesará siempre. Esto se implementó para evitar trampas, ya que se podía atravesar la línea de meta avanzando y retrocediendo sobre la misma línea y subían las vueltas al marcador y por tanto los tiempos de carrera eran imbatibles. 

Por último, la funcionalidad más importante es la que detecta quién ha ganado la carrera. Si el agente termina antes las vueltas, se lanza la escena de derrota, por el contrario, si gana el jugador, se guardan los tiempos en el ranking y se carga la escena de victoria. 

4. Diseño de los mapas ![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.016.png)

Para la creación de los circuitos hemos tomado assets gratuitos de la tienda oficial de Unity. Los principales elementos: 

Piloto  ![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.017.png)![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.018.png)

Kart 

CheckPoint  ![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.019.png)![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.020.png)

Árbol 

Árbol 2  Piedra ![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.021.png)![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.022.png)

![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.023.png) Nube ![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.024.png)

Piedra 2 

![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.025.png) Ejemplo de trozo de pista ![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.026.png)

Ejemplo de trozo de pista 

Ejemplo de trozo de pista  ![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.027.png)![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.028.png)

Meta 

Para que el jugador y sobre todo, el agente no se saliera del mapa, se crearon unos bouding box a modo de muro, en las piezas para crear los circuitos, mostramos un antes y un después: 

![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.029.png)![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.030.png)

4.2 Circuitos 

Con estos elementos se han creado 5 circuitos, cada uno de ellos contará con varios puntos de control (checkPoints) por los que el jugador deberá pasar antes de cruzar la línea meta. De lo contrario, la vuelta no será válida. 

![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.031.png)![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.032.png)

Countrytrack  Longtrack 

Loopingtrack  ![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.033.png)![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.034.png)![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.035.png) Mountaintrack 

Ovaltrack 

5. Bibliografía ![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.036.png)

Self Driving Car in Unity [Part 1/3]:   [https://cutt.ly/smuE62f ](https://cutt.ly/smuE62f)Self Driving Car in Unity [Part 2/3]:   [https://cutt.ly/gmuRakM ](https://cutt.ly/gmuRakM)Self Driving Car in Unity [Part 3/3]:   [https://cutt.ly/mmuRjlc ](https://cutt.ly/mmuRjlc)Cómo hacer un juego de carrearas:   [https://cutt.ly/7muRQR7 ](https://cutt.ly/7muRQR7)Assets Karting Microgame:   [https://cutt.ly/pmuRSGW ](https://cutt.ly/pmuRSGW)Unity Karting Microgame tutorial:  [https://cutt.ly/zmuRM3o ](https://cutt.ly/zmuRM3o)Red neuronal aprende a manejar con IA:  [https://cutt.ly/FmuTqLq ](https://cutt.ly/FmuTqLq)Redes neuronales y algoritmos genéticos:   [https://cutt.ly/nmuTf9T ](https://cutt.ly/nmuTf9T)

![](Aspose.Words.4b7a7fe4-3c91-482d-bd93-57c1b3b9efac.037.png)
PAGE19 
