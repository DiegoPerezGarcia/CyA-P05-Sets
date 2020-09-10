# Práctica 02. La clase Set

### Objetivos
Los objetivos de esta práctica son: 

* Practicar conocimientos de programación Orientada a Objetos en C++
* Practicar operaciones de entrada/salida (E/S) en ficheros de texto
* Ser capaz de desarrollar, compilar y ejecutar programas escritos en C++ en el entorno de trabajo IaaS
* Profundizar en los conocimientos de Visual Studio Code (VSC)

### Rúbrica de evaluacion de esta práctica
Se señalan a continuación los aspectos más relevantes (la lista no es exhaustiva)
que se tendrán en cuenta a la hora de evaluar esta práctica:

* El comportamiento del programa debe ajustarse a lo solicitado en este documento.
* El programa ha de ser fiel al paradigma de programación orientada a objetos (OOP).
* Ha de acreditarse capacidad para introducir cambios en el programa desarrollado.
* El alumnado ha de acreditar que es capaz de editar ficheros remotos en la VM de la asignautra usando VSC
* Modularidad: el programa ha de escribirse de modo que las diferentes funcionalidades
que se precisen sean encapsuladas en funciones y/o métodos cuya extensión textual se mantenga acotada.
* El código ha de estar escrito de acuerdo al estándar de la [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html).
* El programa desarrollado deberá compilarse utilizando la herramienta `make` y un fichero `Makefile`.

Si el alumnado tiene dudas respecto a cualquiera de estos aspectos, debiera acudir al
foro de discusiones de la asignatura para plantearlas allı́. 
Se espera que, a través de ese foro, el alumnado intercambie experiencias y conocimientos, ayudándose mutuamente
a resolver dichas dudas. 
También el profesorado de la asignatura intervendrá en las discusiones que pudieran suscitarse, si fuera necesario.
    
### Introducción
En Matemáticas, un [conjunto](https://en.wikipedia.org/wiki/Set_(mathematics))
finito es una colección finita de ciertos valores, sin ningún orden concreto ni valores repetidos. 
Cuando se trabaja con conjuntos finitos de elementos resulta natural realizar operaciones básicas como son la unión, la intersección o la diferencia de conjuntos.
C++ no tiene un tipo básico para representar conjuntos.
En otras prácticas de esta asignatura se utilizarán profusamente conjuntos para diversos desarrollos.
La forma natural de utilizar conjuntos en C++ es a través del [contenedor `set`](http://www.cplusplus.com/reference/set/set/) 
de la Standard Template Library (STL). 
No obstante, en esta práctica se propone el diseño de una clase propia que permita operaciones básicas con conjuntos.

### Ejercicio práctico
Se definirá una clase `Set` con los atributos y métodos convenientes para representar conjuntos de números
naturales (enteros positivos).

Para representar internamente los conjuntos se pueden utilizar diversas ideas, no obstante se propone aquí
una que puede dar buenos resultados.

Para representar un conjunto de enteros se utilizarán los bits de un valor de tipo `long`.
Si el bit i-ésimo está a 1 ello indicará que el número `i` pertenece al conjunto. 
Si ese bit está a 0, esto indica que el número `i` no pertenece al conjunto.
De este modo se puede representar conjuntos con tantos números naturales  como bits tiene
un valor de tipo `long` (esto es, `sizeof(long)`).
Si se pretende representar conjuntos con un número mayor de elementos, basta usar más de un
valor de tipo `long`.
Con un vector de `M` valores de tipo `long` se pueden representar conjuntos con un máximo de `8 * M * sizeof(long)` elementos.
El número de valores `long` que se utilicen en la representación interna del conjunto
debería ser uno de los atributos de la clase que se ha de definir.
Utilizando [aritmética de bits](https://www.cprogramming.com/tutorial/bitwise_operators.html) 
es fácil implementar las diferentes operaciones sobre conjuntos.

Se definirán al menos dos constructores.
El primero de ellos no tendrá argumentos y definirá un conjunto que tendrá como máximo `sizeof(long)`
elementos.
El segundo constructor tendrá un parámetro que indica el número máximo de elementos que podremos almacenar en
el conjunto.
De este modo se podría definir (por ejemplo):

`Set set1, set2(100);`

El conjunto `set1` podrá almacenar un máximo de `sizeof(long)` elementos, mientras que `set2` 
puede almacenar hasta 100 elementos.

Al menos se implementarán en la clase `Set` las siguientes operaciones sobre conjuntos: 
* [Unión](https://en.wikipedia.org/wiki/Union_(set_theory)) (`+`)
* [Complemento relativo](https://en.wikipedia.org/wiki/Complement_(set_theory)#Relative_complement) (`-`)
* [Intersección](https://en.wikipedia.org/wiki/Intersection_(set_theory)) (`*`)
* [Complementación](https://en.wikipedia.org/wiki/Complement_(set_theory)) (`!`)
* Asignación (`=`)

A la hora de calcular el complementario de un conjunto, se considerará que el [conjunto universal](https://en.wikipedia.org/wiki/Universe_(mathematics))
es aquél que contiene el máximo número de elementos posible en función de su representación interna.

Se ha de sobrecargar el operador `==` de modo que permita determinar si dos conjuntos son iguales.
Se han de definir métodos que permitan las siguientes operaciones:
* Insertar un elemento en un conjunto.
* Eliminar un elemento de un conjunto (supuesto que ya pertenece al mismo).
* Vaciar un conjunto (eliminar todos los elementos que lo componen).
* Determinar si un conjunto está vacío.
* Determinar si un determinado elemento pertenece al conjunto.

Se sobrecargarán convenientemente los operadores de inserción y extracción en flujos
de forma que sea posible leer y escribir un conjunto.
A efectos de entrada/salida el conjunto `A = {1, 2, 3}` se representará como `{1, 2, 3}`, es decir,
listando sus elementos separados por comas e insertados entre llaves.

Para comprobar el correcto funcionamiento de la práctica se implementará una calculadora
de conjuntos (programa `set_calculator.cc`):
desde un fichero (cuyo nombre se suministrará en línea de comandos) se extraerán lineas que
contienen expresiones cuyos operandos son conjuntos.
El programa escribirá en otro fichero (cuyo nombre es el segundo parámetro que se pasará a la
línea de comandos) el resultado de cada una de las expresiones del primer fichero.
Así pues el programa se invocará como:

`./set_calculator infile.txt outfile.txt`

### Referencias
* [Standard Template Library](http://www.cplusplus.com/reference/stl/)
* [Fundamental types](https://en.cppreference.com/w/cpp/language/types)
* [Bitwise Operators in C and C++](https://www.cprogramming.com/tutorial/bitwise_operators.html)
* [C++ Tutor](http://pythontutor.com/cpp.html#mode=display) Visualización online de la ejecución de código C++
* [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html) Guía de estilo de código 
