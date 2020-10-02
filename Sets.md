# Práctica 04. La clase Set

### Objetivos
Los objetivos de esta práctica son: 

* Ejecutar comandos de Linux en la máquina virtual (VM) de la asignatura
* Ser capaz de desarrollar, editar de forma remota usando VSC, compilar y ejecutar programas escritos en C++ en su VM
* Que el alumnado codifique sus programas siguiendo lo estipulado en la Guía de Estilo de código de Google
* Que el alumno sea capaz de formatear su códgo en VSC siguiendo la guia de Estilo de Google
* Que el alumnado utilice la utilidad make y ficheros Makefile en sus proyectos
* Poner en práctica los conocimientos de programación estructurada
* Practicar conocimientos de programación Orientada a Objetos en C++
* Practicar operaciones de entrada/salida (E/S) en ficheros de texto

### Rúbrica de evaluacion de esta práctica
Se señalan a continuación los aspectos más relevantes (la lista no es exhaustiva)
que se tendrán en cuenta a la hora de evaluar esta práctica:

* El alumnado ha de acreditar conocimientos para trabajar con la shell de GNU/Linux en su VM
* El código ha de estar escrito de acuerdo al estándar de la [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html).
* El alumnado ha de acreditar que es capaz de formatear su código usando VSC de acuerdo al estándar anterior
* El alumnado ha de acreditar capacidad para editar ficheros remotos en la VM de la asignautra usando VSC
* El programa desarrollado deberá compilarse utilizando la herramienta `make` y un fichero `Makefile`
* El comportamiento del programa debe ajustarse a lo solicitado en este documento.
* Ha de acreditarse capacidad para introducir cambios en el programa desarrollado.
* Modularidad: el programa ha de escribirse de modo que las diferentes funcionalidades que se precisen sean encapsuladas en funciones y/o métodos cuya extensión textual se mantenga acotada.
* El programa ha de ser fiel al paradigma de programación orientada a objetos (OOPP4).

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

En el programa a desarrollar no ha de usar en modo alguno la [STL](http://www.cplusplus.com/reference/stl/).

Para representar internamente los conjuntos se pueden utilizar diversas ideas, no obstante se propone aquí
una que puede dar buenos resultados.

Para representar un conjunto de enteros se utilizarán los bits de un valor de tipo [`long`](https://en.wikipedia.org/wiki/Integer_(computer_science)#Long_integer).
Si el bit i-ésimo está a 1 ello indicará que el número `i` pertenece al conjunto. 
Si ese bit está a 0, esto indica que el número `i` no pertenece al conjunto.
De este modo se puede representar conjuntos con tantos números naturales  como bits tiene
un valor de tipo `long` (esto es, [`sizeof(long)`](https://www.tutorialspoint.com/cplusplus/cpp_sizeof_operator.htm)).
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

### Formateo automático del código
El código fuente escrito por un programador debiera ser conforme a las reglas de estilo de la organización para la que trabaja.
Ello facilita la legibilidad de los programas así como el trabajo en equipo: cualquier programador de la organización puede entender fácilmente el código escrito por otros desarrolladores puesto que todos siguen unas reglas comunes a la hora de escribir sus programas.
En el caso particular de esta asignatura, las reglas de estilo que se ha propuesto seguir son las de 
la [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html).
Estas reglas de estilo no son únicas. 
Algunas otras relevantes para el caso de C++ son:
* [GeoSoft's C++ Programming Style Guidelines](https://geosoft.no/development/cppstyle.html)
* [LLVM coding standards](https://llvm.org/docs/CodingStandards.html)
* [Chromium’s style guide](https://www.chromium.org/developers/coding-style)
* [Mozilla’s style guide](https://firefox-source-docs.mozilla.org/code-quality/coding-style/index.html)
* [WebKit’s style guide](https://webkit.org/code-style-guidelines/)
* [Microsoft’s style guide](https://docs.microsoft.com/en-us/dotnet/fundamentals/code-analysis/code-style-rule-options?view=vs-2017)

Y cada organización que no define las suyas propias suele adoptar alguna de éstas.

Hay fundamentalmente dos formas de garantizar que el código sigue uno de estos estándares.
La primera es adoptar la costumbre de escribir el código siempre atendiendo a las recomendaciones de estilo de la guía elegida.
Esta es posiblemente la más adecuada porque dota al programador de buenos hábitos a la hora de escribir su código y porque, salvo cuestiones 
opinables, las diferencias entre unas guías de estilo u otras no atañen a los aspectos más relevantes.
Se podría establecer un paralelismo con lo que ocurre al escribir en tu idioma natural: se puede utilizar un corrector ortográfico pero es muy conveniente que las personas sean capaces de escribir sin faltas de ortografía.
La otra opción es utilizar una herramienta que analice el código y lo reescriba de acuerdo a unas reglas de estilo.
Los [linters](https://en.wikipedia.org/wiki/Lint_(software)) son herramientas que cumplen con este cometido.
[clang-tidy](https://clang.llvm.org/extra/clang-tidy/), o [cpplint](https://github.com/google/styleguide/tree/gh-pages/cpplint)
son dos linters adecuados para usar con C++ y su función va más allá de corregir los errores de estilo porque pueden ser útiles para detectar y corregir errores comunes a la hora de programar.

La [extensión para código C++](https://code.visualstudio.com/docs/languages/cpp) de Microsoft  Visual Studio Code  (VSC)
suministra [soporte para dar formato al códifo fuente](https://code.visualstudio.com/docs/cpp/cpp-ide#_code-formatting) 
usando el [formato clang](https://clang.llvm.org/docs/ClangFormat.html) incluído con la extensión.
Una vez configurado el estilo que se desea para los proyectos, las combinaciones de teclas
`Ctrl+Shift+I` y `Ctrl+K Ctrl+F` permiten formatear un fichero completo o parte del mismo respectivamente.
Si en el espacio de trabajo se encuentra un fichero con nombre `.clang-format` el formato se aplica de acuerdo a las especificaciones de ese fichero.
En [este tutorial](https://leimao.github.io/blog/Clang-Format-Quick-Tutorial/) 
se explica cómo utilizar la herramienta [`clang-format`](https://clang.llvm.org/docs/ClangFormatStyleOptions.html) para crear un fichero `.clang-format` 
que siga alguno de los estilos soportados por la herramienta, uno de los cuales (`style=google`) es el que se usa en la asignatura.
En [este artículo](https://medium.com/@zamhuang/vscode-how-to-customize-c-s-coding-style-in-vscode-ad16d87e93bf)
se explica el significado de algunos de los ajustes definidos por el estilo.

### Referencias
* [Standard Template Library](http://www.cplusplus.com/reference/stl/)
* [Fundamental types](https://en.cppreference.com/w/cpp/language/types)
* [Bitwise Operators in C and C++](https://www.cprogramming.com/tutorial/bitwise_operators.html)
* [C++ Tutor](http://pythontutor.com/cpp.html#mode=display) Visualización online de la ejecución de código C++
* [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html) Guía de estilo de código 
* [Clang Format](https://clang.llvm.org/docs/ClangFormat.html) 
* [Format C/C++ Code Using Clang-Format](https://leimao.github.io/blog/Clang-Format-Quick-Tutorial/)
* [How to customize C++’s coding style in VSCode](https://medium.com/@zamhuang/vscode-how-to-customize-c-s-coding-style-in-vscode-ad16d87e93bf)
 
