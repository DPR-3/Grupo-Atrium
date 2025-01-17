El objetivo de esta práctica consiste en resolver una problemática de negocio mediante las técnicas que hemos aprendido en el módulo de Deep Learning. Asimismo, para emular el tipo de proyectos a los que un científico de datos puede enfrentarse, se dejará bastante libertad creativa al alumno, para que elija y busque sus propias fuentes de datos, algoritmos pre-hechos y pre-entrenados, que investigue el estado del arte, para de manera creativa y original resolver el problema de negocio que se propone combinado todos estos elementos inteligentemente.

En cuanto a los directorios, archivos, nomenclaturas etc, el alumno deberá utilizar la lógica y las buenas prácticas de programación y estructuración del código aprendidas hasta el momento para crear los módulos, ficheros, directorios, clases… más coherentes en base a los problemas que se pide solucionar.

 

Problema de negocio: Recomendador de vídeos.
-
Este será un recomendador de vídeos basado en contenido, es decir basado en los objetos que aparecen en los fotogramas de los propios vídeos. La premisa en la que basaremos este sistema es que dos vídeos serán más similares entre ellos cuantos más objetos similares haya entre ambos. Por ejemplo, si en ambos vídeos aparecen coches todo el rato serán más parecidos que si en uno aparecen coches frecuentemente y el otro perros y gatos casi todo el tiempo. Para resolverlo se deben seguir los siguientes pasos:

Descargar vídeos:
-
Se elegirán al menos 3 categorías diferentes de vídeos (ej: vídeos musicales, vídeos de mascotas y vídeos de coches) y se descargarán al menos 100 ejemplos por categoría. Se puede utilizar cualquier fuente que se desee, como por ejemplo Youtube.

Preprocesador de vídeos. 
-
Se deberá crear un script de Python que convierta cada vídeo en un conjunto de fotogramas con nombres consecutivos (ej: 1.jpg, 2.jpg, 3.jpg…) y guarde cada conjunto de fotogramas en un directorio distinto (se recomienda crear un directorio por categoría y dentro un directorio por vídeo). Las imágenes guardadas deberán tener todas la misma resolución (ej: 224x224) y se aconseja que se use el mismo framerate en todos (por ejemplo extraer 3 frames por segundo). Para no hacer el sistema muy pesado se recomienda mantener la resolución y el framerate bajos.

Detector de objetos basado en clasificador pre-entrenado. 
-
Se deberá conseguir una red neuronal convolucional de clasificación pre-entrenada que sea capaz de distinguir entre un buen número de objetos diferentes en imágenes (ej: Las 1000 clases diferentes de imagenet). Se creará un modelo a partir de esta red, cuya inferencia reciba un directorio con los fotogramas de un vídeo en orden y la salida sea un dataframe de pandas con 3 columnas: el número de fotograma, la clase más probable detectada y el grado de confianza que da la red para dicha clasificación. Bonus para subir nota: Basándonos en un modelo pre-entrenado usaremos nuestro propio dataset de imágenes más reducido con menos categorías que sea relevante al tipo de vídeos que queremos clasificar. Y cambiaremos la parte final del modelo para que tenga menos clases y lo re-entrenaremos con nuestro propio dataset, dejando la parte convolucional “congelada” con los pesos originales obtenidos en el conjunto de datos original (ej: imagenet). De esta manera, los outputs de la red serán más valiosos para nuestra tarea.

Clasificador de vídeos 
-
Se utilizarán las inferencias del modelo anterior como input para entrenar el clasificador de tipo de vídeo. Hay que tener en cuenta que los inputs son variables en tamaño ya que dependerán de la longitud del vídeo y su framerate, por lo que habrá realizar un post procesado de estos datos para que puedan ser utilizados como input a un clasificador al uso. Se sugiere por ejemplo crear un variable de entrada por cada tipo de objeto posible y asignarle como valor la "importancia" de dicho objeto en el vídeo. Esta "importancia" se podría calcular en base al número de fotogramas en los que aparece, así como teniendo en cuenta la "confiabilidad".

Bonus para subir nota: Detector de objetos basado en segmentación semántica.
-
Las imágenes de las películas pueden contener más de un objeto. Se sugiere que se use un modelo pre-entrenado de segmentación semántica (como MaskRCNN entrenado con MSCOCO) para crear un detector similar al primero. Este nuevo detector debe inferenciar un csv parecido al anterior, pero añadiendo una línea por cada objeto detectado en cada fotograma. Además, sería recomendable poner una nueva columna con el % de la imagen que ocupa dicho objeto (no es lo mismo un objeto que aparezca en primer plano que uno alejado). También, al igual que en el primer detector, se podrá hacer un transfer learning para un conjunto de clases que nos interesen especialmente si se cree necesario.

Recomendador de vídeos similares.
-
Basándonos en una de las inferencias de los detectores de objetos, se debe crear un sistema que las postprocese de tal manera que cada vídeo sea un punto en un espacio vectorial cuyas dimensiones estén dadas por cada objeto analizado, el post procesamiento creado para el clasificador, si se hizo correctamente puede ser suficiente. Mediante técnicas como KNN y distancia coseno se debe crear un sistema que te diga los 10 vídeos más parecidos dado un vídeo de entrada.
