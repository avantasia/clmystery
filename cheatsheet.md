Jugando con texto en la linea de comandos
=====================================

La linea de comandos (también conocida como interfaz de linea de comandos, CLI - command line interface, o la terminal)
es un interfaz basada en texto plano para ejecutar órdenes en un ordenador. Si alguna vez has visto alguna película 
de hackers de los 80, como *Juegos de Guerra*, donde observan un prompt en una pantalla negra y teclean comandos 
de uno en uno, es básicamente eso.

Tienes un prompt, y puedes escribir un comando y pulsar 'Enter' para ejecutarlo. Un ejemplo de comando sería:

	touch newfile.txt

Este comando creará un fichero llamado `newfile.txt`.

Como acceder a la linea de comandos
------------------------------

**Mac OS X:** Ir a /Applications/Utilities y hacer click en "Terminal" o buscar "Terminal" en Spotlight.

**Desktop Linux:** Puedes buscar la aplicación "Terminal" desde el Dash.  Seamos honestos de todas formas, si estás usando Linux, probablemente no necesitas este tutorial.

**Windows:** Windows es un caso un poco especial.  Si vas al menú de inicio y haces click en "Ejecutar", y después escribes "cmd" y pulsas enter, abrirá la versión de Windows de la línea de comandos. Desafortunadamente, la linea de comandos de Windows tiene su propio sistema, así que para el propósito de seguir estos ejemplos, debes instalar Cygwin, que te permitirá imitar una linea de comandos estilo Linux:

http://www.cygwin.com/

Un poco más de detalle
--------------------

Los comandos generalmente tienen el siguiente formato:

	[nombre del comando] [opción] [opción] [opción] ...

El prompt también te enseñará lo que hay en el directorio en el que estás actualmente. Cuando ejecutes un comando, lo harás en un directorio particular. Esto tiene importancia porque cuando ejecutes un comando que implica un nombre de fichero lo puedes especificar de dos formas:

#### Rutas Relativas

Especificar un fichero o directorio como una ruta relativa quiere decir que estás especificando donde se encuentra con relación al directorio en donde tu te encuentras. Por ejemplo, supongamos que estás en el subdirectorio 'Videos', que es subdirectorio de 'ficheros'. Verás este prompt:

	/files/videos$

Si ejecutas un comando como `touch newfile.txt`, creará `newfile.txt` dentro del directorio actual. Las rutas relativas no empiezan con una barra (/)

#### Rutas absolutas

Especificar un fichero o un directorio como una ruta absoluta quiere decir que estás especificando en donde se encuentra en el ordenador en términos absolutos, empezando desde el nivel más alto (/). Por ejemplo, pongamos que estás en el directorio 'videos', subdirectorio de 'files' de nuevo.

	/files/videos$

Si ejecutas un comando como `touch /files/music/newfile.txt`, creará el fichero `newfile.txt` dentro de un directorio diferente, el subdirectorio `music` del directorio `files`.  *Las rutas absolutas empiezan con barra (/).*

Si usas una ruta absoluta, el comando hará lo mismo sin importar desde que directorio lo ejecutes.

Así que estos dos comandos tendrán el mismo resultado desde el directorio `/files/videos`:

	/files/videos$ rm video.mp4
	(Esto borrará el fichero `video.mp4` desde el directorio actual)

	/files/videos$ rm /files/videos/video.mp4
	(Esto borrará el fichero `video.mp4` desde el directorio /files/videos/ , que da la casualidad de que es el directorio actual)

Los mismo comandos no tendrán el mismo resultado si estás en un directorio distinto:

	/files/text$ rm video.mp4
	(Esto intentará borrar el fichero video.mp4 del directorio 'text', porque es el directorio actual)

	/files/text$ rm /files/videos/video.mp4
	(Esto borrará el fichero del directorio /files/videos/ aunque no sea el directorio actual)

Recuerda:

**Empezar una ruta con una barra** significa que quieres especificar la ruta entera e ignorar el directorio en donde estás situado actualmente.
**No empezar una ruta con una barra** significa que quiere especificar la ruta empezando por el directorio en donde estás actualmente.

Si alguna vez no estás seguro de en qué directorio estás situado, puedes usar el comando `pwd` ((Print Working Directory) para obtener la ruta absoluta del directorio actual.

	~$ pwd
	/Users/Noah

Patrones de ficheros
-------------

En la mayoría de los casos cuando tienes que especificar un nombre de fichero o de directorio, también puedes especificar un **patrón** general que puede coincidir con múltiples ficheros.
Hay muchos matices a este respecto, pero la versión más básica es usar el asterisco (*) que coincide con cualquier cosa. También se le conoce como wildcard

	Borrar cualquier fichero en el directorio actual
	/files$ rm *

	Borrar cualquier fichero que acabe en '.txt'
	/files$ rm *.txt

	Borra cualquier fichero que empiece por'data'
	/files$ rm data*

Navegando
----------

Los dos comandos principales para navegar con el prompt de la linea de comandos son `cd` y `ls`.

`cd` es un comando para cambiar el directorio actual, y debe ser seguido por el directorio al que quieres cambiar.  También se puede especificar una ruta relativa.

	Esto te colocará en /files/videos
	/files$ cd videos	
	/files/videos$

	Esto te colocará en /videos, y luego el subdirectorio vines
	/files$ cd /videos
	/videos$ cd vines
	/videos/vines$

Puedes saltar múltiples niveles de una sola vez si quieres.

	Esto te colocará en /files/videos/short
	/files$ cd videos/short

Puedes usar `cd ..` para moverte un nivel arriba al directorio de nivel superior.

	Esto te colocará en /files
	/files/videos$ cd ..

`ls` listará los ficheros en el directorio actual.  Es útil para saber donde están, qué ficheros existen y qué subdirectorios existen.

	/photos$ ls	
	thumbnails  photo1.jpg  photo2.jpg

Usando `ls -l` sacará el listado verticalmente, con mucha información extra acerca del tamaño de los ficheros, permisos y fecha de última modificación:

	/photos$ ls -l
	-rw-rw-r-- 1 noah noah 58133 Oct 22 17:13 photo1.jpg
	-rw-rw-r-- 1 noah noah 75640 Oct 22 17:13 photo2.jpg
	drwxrwxr-x 2 noah noah 4096  Oct 22 17:13 thumbnails

Cuando tecleas el nombre de un directorio o fichero, puedes pulsar la tecla 'Tab' para autocompletar si es posible. Por ejemplo, en el directorio /photos, si escribes 

	/photos$ cd thu

y pulsas 'Tab,' rellenará el resto y te mostrará:

	/photos$ cd thumbnails

Sin embargo, si hay más de un fichero/directorio que coincida con lo que has escrito hasta el momento, no funcionará. Si escribes: 

	/photos$ rm pho

y pulsas 'Tab', no pasará nada porque podrías estar escribiendo `photo1.jpg` O `photo2.jpg`.

Salida de comandos
--------------

Todos los comandos de los que vamos a hablar dan como resultado texto. Cuando ejecutas el comando pulsando 'Enter', imprimirá un montón de salida en líneas debajo del prompt. Por ejemplo, `head [file]` 
imprimirá las primeras 10 líneas de un fichero.
	
	/files$ head names.txt
	Dan Sinker
	Erika Owens
	Noah Veltman
	Annabel Church
	Friedrich Lindenberg
	Sonya Song
	Mike Tigas
	Brian Abelson
	Manuel Aristaran
	Stijn Debrouwere
	/files$

Fíjate en que después de que imprima la salida, vuelve a proporcionar un prompt nuevo. Tener la salida en este formato es útil si estás curioseando lo que hay en los ficheros, pero muy a menudo querrás
hacer una de estas dos cosas: **mandar la saldida a un fichero**, o **mandar la salida a otro comando como entrada**.

### Mandando la salida a un fichero

Puedes enviar la salida a un fichero nuevo de esta manera:

	/files$ head names.txt > first10names.txt

Si first10names.txt no existe, se creará. Si ya existe, será sobreescrita.

Puedes anexar la salida al final de un fichero existente de esta manera:

	/files$ head names.txt >> allnames.txt

Esto añadirá la salida como 10 líneas nuevas al final de allnames.txt.

### Mandando la salida a otro comando como entrada

Puedes enviar la salida a otro comando usando el símbolo pipe (|). El comando `grep` busca patrones en un texto (más sobre esto más adelante), así que puedes usar esto para obtener las primeras 10 lineas
de un fichero, y luego buscar "Steve" en esas 10 líneas:

	/files$ head names.txt | grep "Steve"

Esto es básicamente lo mismo que hacer esto:

	/files$ head names.txt > temporaryfile.txt
	/files$ grep "Steve" temporaryfile.txt

Pero en vez de enviar primero la salida a un fichero y luego ejecutar el segundo comando en ese fichero, se "entuba" (pipe) la salida directamente del primer comando al segundo. Se pueden encadenar 
tantos comando como quieras:

	/files$ grep "United States" addresses.csv | grep "California" | head

Esto buscaría en el fichero addresses.csv líneas que contengan la frase "United States", después buscaría en los resultados líneas que contengan la palabra "California" y después imprimiría los primeros
10 resultados que coincidan.

Grep
----

El comando `grep` permite buscar una frase en uno o varios ficheros.  Por defecto, imprimirá cada línea que coincida con la búsqueda.

Imprimir las líneas que contienen la palabra "darkwing":

	/files$ grep "darkwing" famousducks.txt

Lo mismo que antes, pero la búsqueda ignora la diferencia entre mayúsculas y minúsculas:

	/files$ grep -i "darkwing" famousducks.txt

Busca coincidencias de la *palabra* exacta "Donald" en un fichero - Las palabras que contengan "Donald" como "McDonald" no cuentan:

	grep -w "Donald" famousducks.txt

Encuentra coincidencias para "McDuck" en cada fichero del directorio actual:

	grep "McDuck" *

Encuentra coincidencias para "McDuck" en cada fichero del directorio actual y cada subdirectorio, hasta el final:

	grep -r "McDuck" *

Para cada coincidencia de "Howard", imprime esa línea Y las 4 líneas a continuación (5 líneas en total):

	grep -A 4 "Howard" famousducks.txt

Para cada coincidencia de "Howard", imprime esa línea Y las 4 líneas previas (5 líneas en total):

	grep -B 4 "Howard" famousducks.txt

Para cada coincidencia de "Howard", imprime esa línea Y las 4 líneas a continuación  Y las 4 líneas previas (9 líneas en total):

	grep -C 4 "Howard" famousducks.txt

En vez de imprimir las líneas, imprime los nombres de ficheros en donde la búsqueda tiene coincidencias:

	grep -l "Daffy" *

Solo sacar el número de coincidencias:

	grep -c "Daffy" *

Mostrar los números de línea para los resultados coincidentes:

	grep -n "Daffy" famousducks.txt

Cat
---

El comando `cat` combina múltiples ficheros. Esto sacará por pantalla tres ficheros de una sola vez, como si fueran un solo fichero:

	cat turkey.txt duck.txt chicken.txt

Recuerda que esto solo sacará la salida por la terminal. Seguramente quieras crear un fichero nuevo que combine los anteriores:

	cat turkey.txt duck.txt chicken.txt > turducken.txt

turducken.txt contendrá todas las lineas de turkey.txt, seguidas por las de duck.txt, seguidas por las de chicken.txt.

Si quieres combinar todos los ficheros de un directorio, puedes usar el wildcard *:

	cat * > allfilescombined.txt

Head
----

El comando `head` imprimirá las primeras 10 líneas de un fichero:

	/files$ head names.txt

También puedes especificar un número diferente de líneas. Esto sacará por pantalla las primeras 15 líneas de un fichero.

	/files$ head -n 15 names.txt

O, si quieres sacar por pantalla todas las líneas del fichero EXCEPTO las últimas 15 líneas, puedes dar un número negativo:

	/files$ head -n -15 names.txt

Uno de los usos curiosos de head es poder echar un vistazo rápido en ficheros de texto grandes para ver qué hay dentro sin tener que esperar a que un editor de texto lo abra. !Esto es un asunto importante
cuando estamos hablando de un fichero de 1GB!

Tail
----

El comando `tail` es la inversa del comando head.  Sacará por pantalla las últimas 10 líneas de un fichero:

	/files$ tail names.txt

Esto sacará por pantalla las últimas 15 líneas de un fichero:

	/files$ tail -n 15 names.txt

O, si quieres imprimir todas las líneas de un fichero EXCEPTO las primeras 15, puedes añadir un signo +:

	/files$ tail -n +15 names.txt

Esto es útil si por ejemplo quieres eliminar la fila de cabecera de un fichero CSV:

	/files$ tail -n +1 names.txt > names-no-header.txt

Varios
-------------

Si solo quieres sacar por pantalla el contenido entero de un fichero en el terminal, puedes usar `cat` y no combinarlo con nada.  Esto es casi ir en contra de la finalidad de `cat`, pero es un truco útil.

	/files$ cat address.txt
	1600 Pennsylvania Avenue
	Washington, DC 20500

Si quieres ponerte en serio y abrir un fichero en un editor de textos que está integrado en la terminal, puedes probar `nano`:

	/files$ nano address.txt

¿Cuántas líneas hay en names.txt?

	/files$ wc -l names.txt
	18

Expresiones regulares
-------------------

Cuando se usa algo como `grep` para buscar, puedes buscar un término simple con solo letras, números y espacios. Pero si lo que quieres es buscar un patrón puedes usar lo que se llama una **expresión regular**. Las expresiones regulares usan caracteres especiales para representar patrones, como "cualquier número", "cualquier letra", "X o Y", "al menos tres letras minúsculas", etc.. 

No nos preocuparemos por los detalles por ahora, pero un operador útil es el punto (.). En el mundo de las expresiones regulares, esto quiere decir "Uno de cualquier caracter". Así que puedes buscar por algo como:

	/files$ grep -i "car.s" dictionary.txt

Esto coincidirá con palabras como `cards`,`carts`,`cares`, etc..  También coincidirá con el medio de la frase "scar story" (CAR S) porque "cualquier caracter" significa CUALQUIER caracter, incluído un espacio o un signo de puntuación.

Un ejemplo más:

	/files$ grep -i ".e.st" dictionary.txt

Esto coincidirá con palabras como `least`,`beast`, y `heist`.

Más de una manera de hacer las cosas
------------------------------

A veces hay muchos comandos iguales o combinaciones de comandos que alcanzan el mismo objetivo.

Ejemplo:

	/files$ head -n 12 names.txt | tail -n 5
	(Imprime las primeras 12 líneas y luego imprime las últimas 5 de eso)

	es lo mismo que

	/files$ tail -n +7 names.txt | head -n 5
	(Imprime todo menos las últimas 7 líneas, después imprime las primeras 5 líneas de eso)

	es prácticamente lo mismo que:

	/files$ tail -n +7 names.txt > temporaryfile.txt
	/files$ head -n 5 temporaryfile.txt
	/files$ rm temporaryfile.txt

	(Guarda todo menos las primeras 7 líneas en un fichero temporal, luego imprime las primeras 5 líneas de eso, luego borra el fichero temporal)

---

## Preguntas/Comentarios/Sugerencias ##
Noah Veltman  
Web: http://noahveltman.com  
Twitter: [@veltman](http://twitter.com/veltman)  
Email: [noah@noahveltman.com](mailto:noah@noahveltman.com)  

## Traducción por ##
David Carracedo  
Web: http://www.mundofido.com  
Twitter: [@avanta](http://twitter.com/avanta)  
Email: [david@adaformacion.es](mailto:david@adaformacion.es)  
