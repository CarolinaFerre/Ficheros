# Ficheros
Apuntes y ejercicios de ficheros


Unidad 10: ESTRUCTURAS EXTERNAS: Ficheros
_____________________________________________




Conceptos:
____________

 Memoria principal, Memoria Secundaria, Fichero, Sistema de ficheros, tipos de ficheros, operaciones con
ficheros, organización de ficheros,Ficheros planos, texto y estructurados. Acceso a Bases de datos



INTRODUCCIÓN
_____________

Conceptos Previos:

- Memoria principal ( Limitada, muy rápida, volátil )

- Memoria secundaria ( Menos limitada, más lenta, no volátil)

Todo lo que hay en memoria principal desaparece cuando el ordenador se apaga. La permanencia de los datos
sólo se logra si almacenamos la información en memoria secundaria. Un programa no puede acceder
directamente a la memoria secundaria, tiene que transferir la información de la memoria secundaria a la
memoria principal, para que el programa pueda modificar los datos almacenados.


Diferencias entre ficheros y Tablas
___________________________________


Tablas                                       Fichero
_______________________________________________________________________________
CapacidadLimitada ( Memoria RAM)        Menos Limitada ( Memoria Secundaria Disco,
Cinta, etc)
Permanencia No permanente              Permanente
Acceso Inmediato A través de Sistema Operativo
Tamaño Fijo o Dinámico Variable
Dimensiones N dimensiones               Una dimensión



Fichero: Es un estructura informática para el almacenamiento de datos en memoria secundaria gestionado por
el sistema operativo. Un fichero es un conjunto de sectores físicos de un dispositivo de memoria secundaria
que guardan información sobre un tema concreto. El S.O. es el encargado de gestionar que sectores pertenece
a cada fichero, si están ocupado o libres, si tienen fallos, si el sector está completo, cual es el siguiente sector
de un fichero, los permisos de acceso, etc.

La estructura de control que gestiona la información sobre ficheros, sectores, ocupación, etc, se denomina
Sistema de ficheros. Existen distintos sistemas de ficheros según el sistema operativo con el que trabajemos:
FAT32, NTFS, EXT, HTS, RAISER, FS, SySV, ... 

Existen también sistemas de ficheros estándar,
independientes del sistema operativo, como el ISO 9660 que corresponde con el formato habitual de los CDROM de datos. Para poder trabajar con una unidad de almacenamiento, debemos crear la información sobre sistema de ficheros que reconoce el sistema operativo, a este proceso se le denomina comúnmente formatear.
Un fichero puede contener cualquier tipo de información: instrucciones en java, bytecode (.class) o en código
máquina (.exe, com, lib, obj, dll) , imágenes en distintos formatos ( jpg, gif, bmp), documentos de texto sin
formato (txt), con un formato especifico (rtf, docx, odt, html, pdf), sonido ( wav, mp3), video (avi,divx),
fichas de los clientes, una lista de alumnos, el registro de Windows, etc. 
 
 
La gran capacidad de la memoria RAM que ofrecen actualmente los ordenadores hace que gran parte del
tratamiento que antes se realizaba en base a ficheros, ahora se realice con estructuras en memoria RAM,
grabando la información a fichero sólo cuando es necesario. Para trabajar con grandes volúmenes de datos
se utiliza, por el contrario, los llamados Sistemas de Gestión de bases de Datos. Los SGBD facilitan
enormemente la labor al programador, ofreciendo un buen rendimiento y velocidad en acceso a los datos. La
aparición de Internet, las redes sociales, los smartphone, el Internet de las cosas (IoT) son fuente de una
enorme cantidad de datos no estructurados que las bases de datos convencionales no pueden manejar
adecuadamente. La gestión de esta inmensa cantidad de datos es un área en pleno desarrollo conocida como
BigData.


¿Que debe controlar el sistema operativo de una unidad de almacenamiento?

 Hay que tener control de los bloques libres y ocupados por cada fichero, mantener la información sobre los
directorios, manejar los buffers en las operaciones de entrada y salida, controlar que ficheros están abiertos,
por que programas, almacenar los premisos, permitir enlaces, controlar el acceso compartido a un mismo
fichero....

Una unidad de almacenamiento (Disco duro) puede tener varias particiones, cada partición tiene su propio
sistema de ficheros independiente. Un sistema operativo puede controlar distintas particiones con sistemas
de ficheros diferentes. Ej.- GNU/Linux ( Ext, ReiserFS, FAT) o Windows Server ( FAT, NTFS).
Generalmente es más seguro tener varias particiones que una sola muy grande.

Ejemplo: El sistema de ficheros FAT

Es el tipo de partición sencilla utilizada en sistemas Windows . Es un sistema de ficheros bastante rápido y
seguro aunque no permite el control de usuarios en el acceso a los ficheros, por eso en las versiones modernas
se suele utilizar NTFS.


Esquema del una partición FAT:
_______________________________

Boot Tabla de asignación de ficheros Directorio Raíz Bloques de datos
En las particiones FAT la información de control de los archivos se almacena en los directorios. La asignación
de espacios se realiza mediante la gestión de una lista encadenada de bloques en la llamada tabla de asignación
de ficheros. El directorio raíz es un directorio especial que se tiene un tamaño fijo.
Información de un directorio en un partición FAT (Un archivo especial)

- Nombre del archivo
- Extensión
- Atributos (Sólo lectura, oculta, sistema, normal)
- Tamaño
- Hora y fecha de creación / modificación / acceso
- Puntero al primer bloque ocupado por el fichero en la Tabla de asignación de Ficheros

Un fichero no siempre se guarda en posiciones consecutivas, sino que puede utilizar varios bloques en
distintas posiciones. El recorrido completo del archivo puede implicar el posicionamiento en distintas
posiciones del disco duro. Este fenómeno se conoce como fragmentación y repercute negativamente en el
rendimiento de las operaciones de entrada y salida.
 
 
 
 
TIPOS DE ARCHIVOS
__________________

Según el uso:


Permanentes o Maestros

Son ficheros que se mantienen a la largo de todo el tiempo ( meses y años, mientras se utilice la aplicación o
programa que los trata). Pueden sufrir modificaciones aunque siempre serán parciales. A su vez, los podemos
subdividir según la frecuencia de actualización en:
- Ficheros de constantes. Pensemos por ejemplo en un fichero que contenga una tabla de
logaritmos, una tabla periódica, códigos postales, etc., su contenido permanece siempre
inalterable.
- Ficheros de situación. Son ficheros que se modifican con más frecuencia y que contienen la
situación actualizada. Guardan información susceptible a sufrir frecuentes modificaciones o
alteraciones. Ej.- Clientes de la empresa, saldos bancarios, etc.
- Ficheros históricos. Contienen información referente a resultados de operaciones, información
resumida, etc., a partir de las cuales se obtiene y confecciona un resumen o resultado final. A
partir de ellos pueden elaborarse estadísticas. Ej.- Apuntes contables, movimientos de almacén,
ventas mensuales, etc.



Temporales

-De movimientos o transacciones (transaction file).
Son ficheros de corta vida, que contienen información a cerca de los movimientos y
transacciones. Suelen servir para la consulta de los ficheros permanentes y producir junto a ellos la
información final. Ej.- Lista de entradas en almacén, pedidos, etc.
-De maniobra o trabajo (work file).

La mayoría de ellos se utilizar para realizar una operación determinada y luego desaparecen.
Contienen información referente a resultados intermedios que a su vez son suministrados a otros
programas. Ej.- Un fichero auxiliar para reordenar un fichero maestro de clientes.



Según su contenido

Ficheros de texto plano:

 Son fichero que almacenan líneas de caracteres separada por un saltos de línea. Se dice que son fichero de
texto plano pues no necesitan ningún programa especial para procesarlos. Se pueden leer y modificar
directamente con cualquier editor de texto. Los caracteres pueden que estar codificados en distinto formato
antiguamente utilizando 8 bits ( ASCII ) actualmente en formato UTF o similar, donde cada carácter ocupa
habitualmente 16 bit. Ej.- Ejemplos de este tipo de ficheros: txt, csv, html, javascript, java, ccs...
Ficheros binarios:
 Tiene una estructura más o menos compleja que impiden que puedan ser leídos o modificados directamente
sin un programa específico
Ficheros de registros: Almacenan una serie de datos del mismo tipo: fichas, registros..)
Ficheros con formatos específicos: Almacenan datos con una estructura compleja como por ejemplo:
imágenes, vídeo, sonidos, documentos formateados ( docx, odt, pdf) 
 
 
 
 
 
OPERACIONES SOBRE FICHEROS
______________________________

Un programa no puede trabajar directamente con la información contenida en un fichero. Las
operaciones sobre ficheros se hacen en base a llamadas a funciones del sistema operativo, que es quien
controla directamente el acceso al sistema de ficheros y al hardware de almacenamiento secundario. La mayor
parte de los lenguajes de programación utilizan un conjunto de funciones o procedimientos de librería para
solicitar estas operaciones al S.O.

Operaciones básicas (Implementadas directamente por el Sistema Operativo)
______________________________________________________________________________


Apertura (open) Solicitar acceso a un fichero al S.O.

Cerrar (close) Informar al S.O que ya vamos a dejar de usar el fichero para que libere
los recursos

Leer ( read) Transferir datos de fichero a una zona de memoria del programa

Escribir ( write) Transferir datos de una zona de memoria al fichero

Situarse ( seek) Cambiar la posición de lectura y escritura

Creación ( creat) Crear un fichero

Borrado ( unlink, remove) Borrar un fichero

Añadir ( Open especial) Abrir un fichero para escribir datos al final

Cambiar permisos (chmod) Cambiar permisos de acceso al fichero( lectura, escritura…)

Truncar ( trunc) Recortar el tamaño de un fichero ( eliminar datos del final)

OJO: No se puede insertar o recortar directamente la información que se guarda en un fichero. El único
método de cambiar el tamaño de un fichero es quitar o poner bytes al final del mismo.
Las operaciones sobre memoria secundaria son miles de veces más lentas que sobre memoria RAM. Para
mejorar el rendimiento de las operaciones de E/S sobre ficheros, el sistema operativo gestiona un conjunto
de almacenamientos intermedios o buffers que permiten que muchas operaciones de E/S se realicen en
memoria RAM, en vez de tener que acceder constantemente a la memoria Secundaria. Este tratamiento
puede provocar que después de un apagado repentino del ordenador, se hayan perdido datos, pues aunque
nuestro programa trabaje sólo con ficheros, puede que las operaciones se hayan hecho sobre el buffer y
que todavía el sistema operativo no haya volcado a disco. Hasta que no cerramos el fichero ( close ) no
tenemos la seguridad que todas la información escrita se ha guardado en memoria secundaria.
La utilización de discos SSD ( de estado sólido ) suponen acceso más rápido, aunque sigue siendo muy
inferior a la velocidad que ofrece la memoria RAM convencional.


Operaciones Secundarias (Mediante un conjunto de operaciones básicas)

- Copiado o Duplicación
- Concatenación
- Ordenación
- Mezcla
- Partición o rotura
- Compactación o Empaquetado



REGISTROS Y OPERACIONES SOBRE REGISTROS.
_________________________________________

Tradicionalmente los ficheros de datos contienen información organizada en una serie de registros.
Un registros es una serie de datos de distinto tipo, llamados comúnmente campos ( Similar una clase de java
que solo tiene atributos)

Elementos de un registro: (campo, subcampo, campo clave)
__________________________________________________________

Cuando un fichero está formado por una serie de registros se suelen definir un conjunto de operaciones
especificas que afectan a dichos registros.

 Consulta ( Lectura de un registro para acceder a su contenido)
 Modificación ( Modificar el contenido del registro y escribirlo en el fichero )
 Alta ( Escribir un nuevo registro en el fichero: implica una escritura al final o una reorganización )
 Baja ( Implica escribir en el fichero, marcarlo mediante un borrado lógico, posteriormente se suele
reorganizar el fichero y truncar el espacio libre)

- Normalmente las altas y las bajas son las operaciones más costosas en tiempo de ejecución.
Es muy habitual utilizar el término CRUD (Create, Read, Update, Delete) a una aplicación que puede crear
nuevos elementos, leerlos , modificarlos y borrarlos.

Actualmente las ficheros de registros no se suelen usar al ofrecer más flexibilidad y facilidad de uso los
sistemas de Bases de Datos.

Ejemplos de ejercicios típicos sobre ficheros de texto:
1. Mostrar el contenido de un fichero de texto.
2. Grabar o Añadir información a un fichero de texto.
3. Contar los caracteres, líneas y palabras de un fichero de texto.
4. Concatenar dos ficheros.
5. Mostrar parte de un fichero.
6. Copiar selectivamente.
7. Mostrar las primeras o las últimas líneas de un fichero.
8. Ordenar un fichero de texto mediante una tabla.



