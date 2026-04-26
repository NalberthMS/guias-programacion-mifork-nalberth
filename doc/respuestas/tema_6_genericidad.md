<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Genericidad". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: clases y objetos, encapsulación, excepciones, composición, herencia y polimorfismo.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# TEMA 6. Genericidad

---

### 1. Empleando `void*` en C o `Object` en Java, pon un ejemplo de una estructura de datos, que empleando un array primitivo, permita alojar cualquier tipo de dato.

**Respuesta:**
Para alojar cualquier tipo de dato sin usar genéricos reales en Java, crearíamos una clase (por ejemplo, una lista) que internamente utilice un array de tipo `Object`. Al crearla, le damos un tamaño. Como en Java absolutamente todas las clases heredan de `Object`, este array actuará como un "cajón desastre" donde podemos meter enteros, textos o cualquier objeto mezclado, sin que el compilador se queje al guardarlos.

### 2. Brevemente, ¿Qué significa la programación genérica? ¿Es el ejemplo anterior un ejemplo básico de programación genérica?

**Respuesta:**
La programación genérica es una forma de programar donde los algoritmos y estructuras de datos se escriben usando **tipos parametrizados** (es decir, tipos "comodín" que se definen más tarde, en el momento en que usas la clase). 

El ejemplo anterior (usando `Object`) **no es programación genérica real**. Es simplemente aprovecharse del polimorfismo y la herencia de Java. La verdadera genericidad permite al programa recordar el tipo exacto de dato que estás usando.

### 3. Indica los problemas respecto al chequeo de tipos, de emplear `void*` o `Object` cuando se crean estructuras de datos genéricas.

**Respuesta:**
Tiene dos problemas fundamentales:
1. **Obliga a hacer "downcasting":** Cuando sacas un elemento de tu lista, el programa solo sabe que es un `Object`. Para poder usarlo como texto o número, el programador tiene que forzar la conversión manualmente, lo cual es propenso a errores y ensucia el código.
2. **Cero seguridad al compilar:** Como el array acepta cualquier cosa, puedes meter un número en una lista que pensabas usar solo para textos. El programa no te avisará del error al programar. Fallará catastróficamente en **tiempo de ejecución** cuando intentes sacar ese número creyendo que era un texto.

### 4. Vamos entonces con mecanismos de mejora de la programación genérica ¿Qué son los parámetros de tipo?

**Respuesta:**
Son variables especiales (normalmente representadas con letras mayúsculas como T, E, K, V) que, en lugar de almacenar un valor como un número o un texto, **almacenan tipos de datos** (clases). Se ponen al definir la clase para indicar que trabajará con un "Tipo T", y el programador que la instancie decidirá en ese momento si esa T es un número, un texto, etc.

### 5. En Java existe "generics", en C++ existen "templates". Pon un ejemplo de uso de programación genérica en ambos, instanciando una lista o vector dinámico que solo admite `String`. Introduce valores, y luego haz un recorrido de ellos mostrando cómo cada elemento es del tipo concreto con seguridad.

**Respuesta:**
* **En Java:** Instanciaríamos una estructura, como un `ArrayList`, indicando explícitamente entre corchetes angulares que es de tipo texto (`<String>`). Al añadir palabras, el compilador verifica que no metamos números. Al recorrer la lista, no tenemos que adivinar ni forzar el tipo de dato: el programa ya sabe con certeza que son textos, permitiéndonos usar métodos de texto directamente con total seguridad.
* **En C++:** Usaríamos un `vector` de la biblioteca estándar, indicando también entre corchetes angulares que será de tipo texto (`<string>`). El resultado práctico es el mismo: seguridad absoluta al insertar datos y al recorrerlos, impidiendo fallos silenciosos.

### 6. Sobre el funcionamiento de la programación genérica. ¿Qué hace el compilador cuando se instancia una clase que tiene parámetros de tipo? ¿Hace lo mismo C++ y Java? ¿Qué es el "type erasure" de Java y la "instanciación de plantillas" de C++?

**Respuesta:**
Por debajo hacen cosas completamente distintas:
* **En C++ (Instanciación de plantillas):** El compilador lee la plantilla genérica y fabrica internamente una clase nueva y específica de código máquina para cada tipo que uses. Si haces una lista de números y otra de textos, C++ crea dos clases distintas compiladas. Es muy rápido, pero ocupa más espacio (fenómeno conocido como *code bloat*).
* **En Java (Type Erasure o borrado de tipos):** Solo existe una única clase real compilada. Durante la compilación, Java hace todas las comprobaciones de seguridad para ver que no te hayas equivocado mezclando tipos. Si todo está bien, **borra** la información del tipo genérico y lo sustituye internamente por `Object`, metiendo las conversiones forzadas (`castings`) de forma automática e invisible para el programador. En ejecución, el programa no tiene ni idea de qué tipo era la lista originalmente.

### 7. Vamos a crear una nueva clase con parámetros de tipo. Define en Java una clase `Par`, que permite alojar dos valores de tipos diferentes. Incluye un constructor y un getter para cada tipo. Pon un ejemplo de uso de ese `Par`, por ejemplo para especificar el tipo de retorno de una función que devuelve en un `Par` la media y desviación típica de un array de `double`.

**Respuesta:**
Definiríamos la clase `Par` indicando que necesita dos parámetros de tipo (por ejemplo, `<T, U>`). Dentro de la clase, declararíamos dos variables privadas, una de tipo T y otra de tipo U, junto con un constructor para inicializarlas y sus métodos *getter* para obtener esos valores. 
Para el ejemplo de estadística, crearíamos la función que calcule la media y la desviación típica, e indicaríamos que devuelve un objeto `Par<Double, Double>`. Así, logramos devolver dos valores decimales desde una misma función, agrupados de forma limpia y garantizando su tipo.

### 8. En Java, se pueden declarar parámetros de tipo también a nivel de método, no solo a nivel de clase. Pon un ejemplo con un método genérico `seleccionaUno`, que pasados dos objetos del mismo tipo, te devuelva aleatoriamente uno de ellos. Muestra la diferencia de definirlo con dos `Object`, a definirlo con dos parámetros de tipo, en terminos de (i) evitar downcasting y (ii) forzar que ambos objetos sean del mismo tipo.

**Respuesta:**
* **Si usamos dos `Object`:** Podrías pasarle a la función un texto y un número a la vez. El compilador lo traga sin quejarse (no fuerza el tipo), pero te devuelve un `Object`. Al recibirlo, tienes que adivinar qué te ha devuelto y forzar la conversión (`downcasting`), asumiendo el riesgo de que el programa falle si te equivocas.
* **Si usamos un parámetro genérico `<T>`:** La función obliga a que los dos datos que le pases sean obligatoriamente del mismo tipo exacto (por ejemplo, dos textos). Además, el compilador sabe con un 100% de seguridad que te va a devolver un texto, evitándote tener que hacer ningún tipo de `downcasting`.

### 9. ¿Se pueden establecer restricciones en los parámetros de tipo? Por ejemplo, si quiero definir un tipo genérico `<T>`, ¿puedo decir que tenga que ser, al menos, un número para poder tratarlo como tal? Pon un ejemplo en Java de un `Punto` con dos coordenadas, metodos `getX`, `getY`, y una función `calcularDistanciaA` otro `Punto`. Permite que esas coordenadas sean cualquier tipo de número. Pon dos soluciones: una simplemente creando coordenadas de tipo `Number` y otra añadiendo generics para reforzar el chequeo de tipos y saber exactamente con qué tipo de número trabaja el `Punto`. En este caso y respecto al "type erasure", ¿cuál es el tipo final tras la compilación?

**Respuesta:**
Sí, se pueden restringir los parámetros genéricos usando la palabra clave `extends`.
* **Solución sin genéricos:** Se define la clase Punto declarando directamente las variables X e Y como de la clase genérica `Number`. 
* **Solución con genéricos:** Se usa un parámetro `<T>` para la clase, pero se le añade la restricción de que "T" debe heredar de número (`<T extends Number>`). Las coordenadas se declaran de tipo T.
* **Respecto al Type Erasure:** Como Java borra la información genérica al compilar y la sustituye por su límite superior, el resultado final tras compilar la solución con genéricos será estructuralmente **idéntico** al de la solución sin genéricos (ambas usarán la clase `Number` por debajo).

### 10. Sobre las soluciones anteriores. Si bien ambas permiten trabajar con distintos tipos de número sin duplicar la clase `Punto`, reflexiona sobre el refuerzo del chequeo de tipos con generics. ¿Permiten ambas crear un punto con una coordenada de tipo entero y la otra coordenada de tipo real? ¿Qué tipo devuelve el `getX` con la solucion sin generics y qué tipo devuelve el que tiene la solución con generics?

**Respuesta:**
* **Sobre mezclar tipos:** La solución sin genéricos **SÍ** permite crear un punto donde la "X" es un número entero y la "Y" es un decimal, porque simplemente exige que ambos sean un `Number` de forma independiente. La solución con genéricos **NO** lo permite de forma natural: si indicas al instanciar que el tipo genérico `T` es Entero, el compilador te obligará estrictamente a que ambas coordenadas sean enteros.
* **Sobre el tipo devuelto:** Al pedir la coordenada con `getX()`, la versión sin genéricos te devuelve un tipo abstracto `Number`, forzándote a ti a convertirlo al formato que necesites. La versión genérica te devuelve directamente el tipo exacto (`Integer`, `Double`...) con el que decidiste construir el punto.

### 11. Hagamos un ejemplo avanzado. El siguiente código, con interfaz `Punto`, que define un método `calcularDistanciaA(Punto p)`, junto con las implementaciones `Punto2D` y `Punto3D`. Añade generics para asegurarnos que la sobreescritura del método calcular distancia a otro `Punto` siempre es sobre un `Punto` del mismo tipo, evitando `instanceof` y el downcasting.

**Respuesta:**
Para asegurar que un Punto 2D solo calcule distancias con otros Puntos 2D, hacemos que la propia interfaz Punto requiera un parámetro genérico recursivo (`Punto<T extends Punto<T>>`). Así, cuando la clase `Punto2D` implementa la interfaz, se pasa a sí misma como parámetro.
Esto le dice al compilador: "voy a implementar las reglas de Punto, pero obligando a que todo lo que reciba sea de mi mismo tipo exacto". Como consecuencia, el método de calcular distancia exigirá explícitamente en sus parámetros un `Punto2D`. De un plumazo, nos ahorramos tener que usar `instanceof` para verificar que el objeto es compatible, y nos ahorramos hacer el `downcasting`.

### 12. Dado que `String` es subtipo de `Object`, ¿significa eso que `List<String>` es subtipo de `List<Object>`? ¿Y que `String[]` es subtipo de `Object[]`? Razona por qué la respuesta es diferente en cada caso y qué problema en tiempo de ejecución puede aparecer con los arrays. A partir de estos ejemplos, define qué significa que un tipo genérico sea covariante, contravariante o invariante respecto a su parámetro de tipo.

**Respuesta:**
* ¿Es `List<String>` subtipo de `List<Object>`? **NO**.
* ¿Es `String[]` subtipo de `Object[]`? **SÍ**.
* **El problema de los arrays:** Al permitir la herencia, Java te deja guardar un array de textos dentro de una variable declarada como array de objetos. Si usas esa variable para intentar guardarle dentro un número, el compilador lo dará por bueno. Sin embargo, al ejecutar el programa se producirá un fallo crítico, porque el espacio de memoria original seguía siendo solo para textos. Las listas genéricas son más estrictas y prohíben esto desde el principio para evitar esos cuelgues.
* **Definiciones:**
    * **Covariante:** Significa que se respeta la herencia. Si A hereda de B, un conjunto de A hereda de un conjunto de B (permitido en arrays de Java).
    * **Contravariante:** Significa que se invierte la herencia. El supertipo actúa como si fuera el subtipo.
    * **Invariante:** Significa que no hay relación de herencia en absoluto. Aunque A herede de B, una Lista de A y una Lista de B son incompatibles entre sí (como ocurre con los genéricos en Java).

### 13. Java permite recuperar covarianza y contravarianza en tipos genéricos de forma controlada mediante wildcards. ¿Qué es un wildcard (`?`)? Muestra la diferencia entre `List<? extends T>` y `List<? super T>`, indicando en qué casos se usa cada uno. Pon dos ejemplos: (i) un método que reciba una lista de números y calcule su suma, usando `? extends`; (ii) un método que reciba una lista y le añada varios números enteros, usando `? super`.

**Respuesta:**
Un *wildcard* o comodín (`?`) representa un "tipo desconocido". Se usa para relajar la regla de que los genéricos sean invariantes, pero de forma segura:
* **Límite superior (`? extends T`):** Sirve para recuperar la **covarianza**. Acepta el tipo T o cualquier clase que herede de T. Se usa cuando la colección actuará como **productora** (solo vas a **leer** datos de ella). Por ejemplo, para sumar números, pedirías una lista de `? extends Number`. Esto te permite pasar una lista de Enteros o una de Decimales; como solo vas a leerlos, el programa sabe que, sea lo que sea, es seguro tratarlo como un Número.
* **Límite inferior (`? super T`):** Sirve para recuperar la **contravariza**. Acepta el tipo T o cualquier superclase de T. Se usa cuando la colección actuará como **consumidora** (solo vas a **insertar** datos en ella). Por ejemplo, para insertar enteros fijos en una lista, pedirías una lista de `? super Integer`. Esto te permite pasarle una lista de Enteros, una de Números genéricos o una de Objetos. Mientras la lista original admita un entero como mínimo, meterle un entero será una operación 100% segura.