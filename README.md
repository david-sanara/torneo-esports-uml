# ACTIVIDAD 03 LENGUAJE DE MARCAS. DIAGRAMAS UML.

En esta actividad he realizado un análisis de los casos de uso y de clases para una supuesta plataforma de eSports, así como la creación de sus diagramas correspondientes.

Si bien la plataforma podría ser mucho más extensa, he intentado resumir un poco los usos y clases principales para cumplir con la actividad, dentro de las limitaciones actuales.

Para la creación de la plataforma debemos tener en cuenta a un actor que administrará la plataforma y sus principales funciones como los torneos, principal elemento de la plataforma, así como los resultados, estadísticas, etc.
Esta plataforma será usada por jugadores y sus "mánagers", los cuales deben poder acceder al seguimiento de sus estadísticas y deberían poder generar inscripciones en torneo.
Para que las partidas del torneo sean justas, un actor independiente debe visualizarlas e impedir que se realicen trampas o victorias injustas, estos serán los árbitros, los cuales serán los responsables de los resultados así como de comentar las partidas.
El elemento principal de la plataforma son los espectadores, los cuales mediante registros y visitas, mantendrán viva la plataforma haciéndola interesante para posibles inversionistas que quieran anunciar sus productos en la plataforma, generando beneficios.

Por tanto, para el “Diagrama de casos de uso”, he detectado cinco posibles actores. 

- **Administrador**: 

Responsable de la creación de torneos y de generar el emparejamiento de equipos, el cual automáticamente "< < include > >" la comprobación necesaria de que estos equipos estén correctamente inscritos.
Por eso, tiene tambien la capacidad de inscribir jugadores o equipos en el torneo (en caso de ser necesario). Este uso de "inscripción" "< < include > >" dos usos necesarios, comprobar la existencia de un torneo creado, y que los equipos/jugadores inscritos cumplen los requisitos necesarios para dicho torneo.

El administrador también realiza la asignación del árbitro para el partido, así como de otras gestiones principales como puede ser la de gestionar la clasificación manteniendola actualizada.

- **Árbitro/Comentarista**:

Será la persona que visualice las partidas, las comente, registre los resultados, y además, sancione y pueda incluso modificar el resultado en caso de que sea necesario.

- **Mánager**:

Encargados de gestionar equipos y/o clubes. Registran los equipos en las competiciones, visualizan y realizan estratégias buscando mejores jugadores basándose en estadísticas para sus equipos. También podrán tanto aceptar como enviar solicitudes a jugadores, para incluirlos en los equipos que ellos gestionan.

- **Jugadores**:

Actores principales que jugan las partidas. Si participan de manera individual (en torneos o eventos individuales), podrán inscribirse ellos mismos. Si están dentro de un grupo serán los mánagers los encargados de hacerlo. También pueden acceder a todos los datos y estadísticas de la plataforma.

- **Espectadores**:

Darán visualizaciones y uso a la plataforma. Podrán usar la plataforma para ver los clubes, dentro de estos los equipos, y dentro de estos los jugadores, así como los jugadores individuales y las estadísticas generales. (Tiempo jugado, equipos y puntos por temporada, etc.).


El "diagrama de casos de uso" queda de la siguiente manera: 

- [[Diagrama de casos de uso.]](https://github.com/david-sanara/AD-3.-Diagramas-UML/blob/main/Diagrama%20de%20Usos%20Definitivo%20Act3%20EEDD%20UML.drawio.png)

Para el "Diagrama de clases", he omitido los "getters/setters", "equals & hashCode", "constructores vacíos y llenos" y "toString para no ser repetitivo y resducir el volumen de trabajo. Las clases que he determinado son:

* **Torneo**. En esta clase encontramos su PK que es su id (int), su nombre, tres "List" (equipos, partidas y clasificación) y una fecha (Date).
Esta clase es la que podrá "crear los Torneos", principal actividad de la plataforma, así como eliminar equipos por diferentes razones (incumplan normas, crados por error, etc.). También será la clase encargada de crear las clasificaciones y de actualizarlas (archivar antiguas clasificaciones, mostrar las nuevas, etc).

Seguidamente hay tres clases. Equipo, Clasificación y Partida.

* **Equipo**: Como atributos tiene un id (PK, int), un nombre de equipo, y List<Jugador> que formarán cada equipo. Como métodos, se podrá RegistrarEquipo (crear equipo en la plataforma), añadir jugadores al equipo , inscribir un equipo en un torneo y consultar los equipos.

* **Clasificación**: Sus atributos son tres List(Equipos, Jugadores y Clubs). Tambiémn tendrá otros como puntos, posicionEquipoJugador, la fecha (Date) y una Foreign Key (FK) del Torneo que enlaza la clasificación con el Torneo correspondiente. Los métodos de esta clase son consultar(ver)la clasificación y actualizar la posición de los equipos/jugadores en la clasificación.

* **Partida**: Esta clase tiene su propia PK (Primary Key) que será su id (int). También tendrá como atributos equipo1, equipo2, fecha y resultado. Sus métodos son "Registrar Resultado", método automático tras el resultado de la partida y "Asignar Árbitro".

Enlazadas con estas, he creado cuatro subclases, Jugador, Club, Resultado y Árbitro.

* **Jugador**: Representa al jugador individual, con propio id que será su PK, y sus otros atributos son su nombre y su email. Los métodos que ofrece esta clase son; Registrar jugador, donde el jugador se puede registrar en la plataforma (crear perfil de jugador en la plataforma), y los métodos de aceptar una invitación a un equipo o enviar solicitud para unirse a un equipo. También tiene los métodos de consultarJugador (donde se ven los detalles del Jugador) y el método para que el jugador pueda inscribirse en Torneos o partidas individuales.

* **Club**: Sus atributos son su id (int, PK), nombre y List<Equipo>. Los métodos de esta clase son "Registrar Club" (creación del club en la plataforma), y "Añadir equipo en Club".

* **Resultado**: Compuesto por una FK del idPartida, un atributo "ganador", dos atributos "puntuaciones" (equip1 y equip2) y un atributo "penalizaciones". Los métodos de esta clase son "Establecer Resultado", el cual "confirma" el resultado registrado, y calcularEstadísticas, tomando los resultados gestiona todos los datos obtenidos de jugadores, equipos, resultados, etc. y devuelve objetos de "tiempo jugado", puntos, etc. para el abastecer el cálculo estadístico.

* **Árbitro**: Esta clase está formada por un id de árbitro con el que se identifica la clase (PK), un nombre y una List<Partida> que registra partidas asignadas.
Los métodos que genera la clase árbitro son "Modificar Resultado" y "Añadir Penalización".

Finalmente, he creado una última clase llamada "Estadística".

* **Estadística**: Está formada por objetos creados a través del método del cálculo estadístico así como de otros generados por resultados y otros métodos de clases. Todos los métodos que ofrece esta clase son para mostrar los diferentes cálculos estadísticos e información de interés para los usuarios.

El "diagrama de clases" quedaría de la siguiente manera: 

- [[Diagrama de clases.]](https://github.com/david-sanara/AD-3.-Diagramas-UML/blob/main/Diagrama%20de%20Clases%20Definitivo%20Act3%20EEDD%20UML.jpg)

## CONCLUSIÓN: 
La plataforma para eSports, está basada en unos actores que a través de partidas en consolas y otra plataforma de visualización, se basa en "Crear", "Gestionar" y "Recoger" datos de las partidas, jugadores y otros actores relacionados como los mánagers o los árbitros/comentaristas. Es como un "Sistema de Gestión", el cual se sostendra gracias a las visitas y los patrocinios. Por lo que la figura del árbitro que comenta las partidas será fundamental para generar engagement. 
Una vez realizado el diagrama de casos de uso y tener claro quienes van a interactuar con nuetra plataforma y qué usos necesitaremos (podría poner muchos más pero el trabajo se estaba alargando demasiado), he pasado al diagrama de clases teniendo en cuenta cuales serían las clases a programar y los atributos que podrían formar estas. Además, los métodos que cada clase puede generar, no tiene por qué ser usado exclusivamente por un actor, es decir, un actor podría tener acceso a varios métodos de diferentes clases.
La actividad podría haberse alargado bastante más pero se pedía algo resumido.
