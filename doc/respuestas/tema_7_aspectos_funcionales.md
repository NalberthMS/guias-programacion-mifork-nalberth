<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Aspectos funcionales". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: clases y objetos, encapsulación, excepciones, composición, herencia, polimorfismo y genericidad.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->

## TEMA 7. Aspectos funcionales

### 1. ¿Qué es un puntero a una función? Pon un ejemplo de código en C, donde se define una función y que reciba una cadena de caracteres como parámetro y devuelva la cadena en mayúsculas. Crea un puntero en una variable local a dicha función llamado `aMayusculas` e invócala con el puntero.

**Respuesta:**
Un puntero a una función en lenguajes como C es una variable especial que, en lugar de guardar un dato (como un número o un texto), guarda la **dirección de memoria** donde se encuentra el código de una función concreta. 
En la práctica, primero definiríamos nuestra función tradicional que convierte un texto a mayúsculas. Luego, dentro de nuestro programa principal, declararíamos una variable llamada `aMayusculas` indicando que es un puntero a función y le asignaríamos la función que acabamos de crear. A partir de ese momento, podemos ejecutar la conversión a mayúsculas usando directamente la variable `aMayusculas` pasándole el texto, en lugar de llamar al nombre original de la función.

### 2. ¿Qué es una función lambda en un lenguaje de programación? Pon un ejemplo similar al anterior en Javascript y otro en Java con funciones lambda. Usa una variable local `aMayusculas` para apuntar a la función lambda.

**Respuesta:**
Una función lambda es una **función anónima** (no tiene nombre) que se puede tratar como un valor. Esto significa que puedes escribir la lógica de una función "al vuelo" y guardarla en una variable, pasarla como parámetro o devolverla.
* **En JavaScript:** Declararíamos una variable llamada `aMayusculas` y le asignaríamos directamente una "función flecha" que toma un texto como entrada y devuelve su versión en mayúsculas.
* **En Java:** Haríamos lo mismo. Declaramos una variable de tipo `Function` (un tipo especial de Java para indicar que entra un String y sale otro String), y le asignamos una expresión lambda (usando la sintaxis de flecha `->`) que coge un texto y lo convierte a mayúsculas.

### 3. ¿Qué es el paradigma funcional? ¿Por qué a algunos lenguajes orientados a objetos como Java 8, se les llama multi-paradigma? ¿Qué quiere decir que las funciones son "ciudadanos de primera clase"?

**Respuesta:**
* **Paradigma funcional:** Es un estilo de programación basado en el uso y composición de funciones matemáticas. Se centra en "qué" hay que hacer en lugar de "cómo", y evita modificar el estado de los datos externos (evita los "efectos secundarios").
* **Multi-paradigma:** Se llama así a Java (desde su versión 8) porque, aunque su núcleo principal sigue siendo la Orientación a Objetos (clases e instancias), introdujo características robustas del paradigma funcional (como las lambdas y los Streams), permitiendo al programador mezclar ambos estilos según le convenga.
* **Ciudadanos de primera clase:** Significa que las funciones tienen los mismos "derechos" que cualquier otra variable básica (como un número o un texto). Puedes guardar funciones en variables, pasarlas como argumentos a otras funciones o hacer que una función devuelva otra función como resultado.

### 4. Explica la sintaxis básica de una función lambda en Java.

**Respuesta:**
La sintaxis de una lambda en Java es muy concisa y se divide en tres partes separadas por una flecha (`->`):
1.  **Parámetros (a la izquierda):** Van entre paréntesis. A menudo no hace falta poner el tipo de dato porque el compilador lo adivina. Si es un solo parámetro, puedes omitir los paréntesis.
2.  **El operador flecha (en el centro):** Separa los parámetros del código que se va a ejecutar.
3.  **El cuerpo (a la derecha):** Es la lógica de la función. Si es una sola instrucción, no necesitas abrir llaves `{}` ni usar la palabra `return`. Si son varias líneas, abres llaves y usas `return` explícitamente.

### 5. Ahora recibamos una función como parámetro a un método y la llamaremos desde dentro. Amplia los ejemplos anteriores de Java y JavaScript con un método llamado `transformar`, que reciba un `String` como parámetro y luego una función transformadora como lo es `aMayúsculas` y la invoque desde dentro.

**Respuesta:**
El concepto aquí es crear una "función de orden superior" (una función que recibe otras funciones). 
Definimos el método `transformar` para que exija dos cosas: el texto original y la función que dictará la regla de transformación. Dentro de `transformar`, lo único que hacemos es coger el texto y aplicarle esa regla que hemos recibido.
Al usarlo en nuestro programa, llamaríamos a `transformar` pasándole nuestro texto base y la variable `aMayusculas` (que guardaba nuestra lambda anterior). El método ejecutará internamente la regla de mayúsculas sobre el texto.

### 6. Ahora, invoca `transformar`, con una nueva función lambda directamente en la llamada a `transformar`, por ejemplo, una función lambda que invierta la cadena. Define la función de inversión justo cuando la estás pasando como parámetro.

**Respuesta:**
En lugar de guardar la regla en una variable previa, la escribimos "al vuelo" (inline). Llamamos a `transformar`, le pasamos el texto y, como segundo parámetro, escribimos directamente la expresión lambda completa con la lógica para darle la vuelta al texto. Esto demuestra lo útiles que son las lambdas para operaciones rápidas de un solo uso, evitándonos crear clases o variables innecesarias.

### 7. ¿Qué se entiende por cierre o "closure" en el contexto de las funciones lambda? Pon un ejemplo en Java de cómo una función lambda es capaz de acceder a una variable local en el contexto donde fue definida. Modifica el ejemplo anterior...

**Respuesta:**
Un "closure" (o clausura) es la capacidad que tiene una función lambda de "atrapar" y recordar las variables locales que existían a su alrededor en el momento y lugar en que fue creada, incluso si la lambda se ejecuta en otra parte del programa mucho después. 
* **Ejemplo:** Imagina que declaramos una variable de texto local llamada `prefijo` (por ejemplo, "Señor/a "). Luego, en la llamada a `transformar`, definimos una lambda que coge el texto de entrada y le concatena ese `prefijo`. La lambda ha "capturado" exitosamente la variable `prefijo` del exterior. En Java, la única condición para que esto funcione es que esa variable externa atrapada no cambie de valor después (debe ser "efectivamente final").

### 8. Reflexiona: ¿en qué se diferencia entonces una función lambda de los punteros a funciones que hay en C?

**Respuesta:**
La diferencia fundamental es precisamente el **closure (cierre)**. 
Un puntero a función en C es algo "frío": solo sabe dónde está el código, pero no tiene memoria del entorno ni puede atrapar variables locales del sitio donde fue declarado. 
Una función lambda, por el contrario, lleva una "mochila" incorporada con el contexto (las variables) del momento en que fue creada. Esto le da a las lambdas una potencia enorme para mantener el estado de forma segura sin recurrir a variables globales.

### 9. Devolvamos ahora funciones. Creemos ahora una función que sea capaz de crear funciones "descuento"... Prueba a crear dos descuentos distintos y aplicarlos a una cantidad. Explica la closure en la función descuento.

**Respuesta:**
Creamos una función constructora llamada `crearDescuento` que recibe un número (el porcentaje). En lugar de calcular un precio final, esta función **devuelve otra función** lambda. Esta nueva lambda es la que recibe el precio y le resta el porcentaje.
Si llamamos a `crearDescuento(20)` y `crearDescuento(50)`, obtenemos dos funciones distintas guardadas en dos variables. El **closure** es el protagonista aquí: la primera función generada "recuerda" para siempre que el porcentaje era 20, y la segunda "recuerda" que era 50, a pesar de que la función original `crearDescuento` ya terminó de ejecutarse hace tiempo.

### 10. En Java, que es un lenguaje con comprobación estática de tipos, donde los tipos se declaran, toda función lambda tiene un tipo, que se conoce como interfaz funcional. ¿Qué es una interfaz funcional? ¿Qué requisitos tiene?

**Respuesta:**
Como Java necesita saber de qué tipo es cada cosa, no existe un tipo genérico llamado "Lambda". Las lambdas toman el tipo de una **Interfaz Funcional**.
Una interfaz funcional es una interfaz tradicional de Java que cumple un único requisito estricto: **tiene que tener un solo método abstracto** (sin implementar). La lambda que escribamos se convertirá automáticamente en la implementación de ese único método. A menudo se marcan con la etiqueta `@FunctionalInterface` para que el compilador avise si alguien añade por error un segundo método.

### 11. Creemos una interfaz funcional a mano. Por ejemplo, define la interfaz funcional del ejemplo que transforma la cadena en otra. Llámale `Transformador`.

**Respuesta:**
Para crearla, simplemente declaramos una interfaz pública llamada `Transformador`. Dentro de ella, definimos un solo método, que por ejemplo podríamos llamar `aplicarTransformacion`. Este método indicará que recibe un `String` como parámetro y que devuelve otro `String`. Con solo hacer eso, Java ya la reconoce como una interfaz funcional lista para ser usada por nuestras lambdas de texto.

### 12. Ahora hagamos la interfaz funcional algo más genérica y empleando generics, para que permita definir un `Transformador` de un tipo en otro. Pon un ejemplo de un transformador que redondea un `Double` en un `Integer`.

**Respuesta:**
Para que sirva para cualquier cosa, le añadimos parámetros genéricos a la interfaz (por ejemplo, `<T, R>`). Ahora el único método que tiene indicará que recibe un dato de tipo genérico `T` (la entrada) y devuelve un dato de tipo genérico `R` (el resultado).
Para el ejemplo del redondeo, crearíamos una variable indicando que su tipo es un `Transformador<Double, Integer>`. Le asignaríamos una lambda que recibe el decimal y devuelve el número entero redondeado. Ahora nuestra interfaz es universal.

### 13. `Transformador`, en su versión genérica, parece muy útil y reutilizable, hasta el punto de que es igual a una interfaz funcional que ya hay, que es `Function<T, R>`. Muestra las interfaces funcionales predefinidas que hay en Java.

**Respuesta:**
Java incluye un paquete completo con interfaces funcionales estándar para que no tengas que crear las tuyas. Las más importantes son:
* **`Function<T, R>`:** Recibe algo, lo transforma y devuelve un resultado (como nuestro transformador).
* **`Consumer<T>`:** Recibe un dato, hace algo con él (como imprimirlo), pero no devuelve nada. Lo "consume".
* **`Supplier<T>`:** No recibe nada, pero devuelve un dato. Lo "suministra" (útil para generar datos o instanciar objetos).
* **`Predicate<T>`:** Recibe un dato y devuelve un booleano (verdadero o falso). Actúa como un filtro o condición.

### 14. Vamos a ver ejemplos expresivos de funcional en Java. Estudiemos el `List.forEach`, como versión funcional del bucle `for`. Emplea el `forEach` para recorrer una lista de `Integer` y que muestre un mensaje si el entero es positivo.

**Respuesta:**
En lugar del tradicional bucle `for`, cogemos nuestra lista y llamamos a su método `forEach`. Este método espera recibir un `Consumer` (una lambda que hace algo con un dato y no devuelve nada). 
Le pasamos una lambda donde le decimos: "Toma este número entero; si es mayor que cero, imprímelo por pantalla". La propia lista se encarga de recorrerse a sí misma internamente y de aplicar esa regla a cada uno de sus elementos, haciendo el código mucho más limpio.

### 15. Repasando el tema de genericidad, fíjate en la firma de `forEach`, ¿por qué se usa `Consumer<? super T>` y no `Consumer<T>`? Explica qué significa PECS, y explícalo para el caso de mejorar el ejemplo del método `transformar`...

**Respuesta:**
* **PECS** significa "Producer Extends, Consumer Super". Es una regla para flexibilizar la genericidad en Java. 
* Se usa `<? super T>` porque el `forEach` actúa como un **Consumidor** de los elementos de la lista. Si tienes una lista de Enteros (`Integer`), no necesitas obligatoriamente una lambda hecha solo para Enteros; también te serviría una lambda diseñada para Números genéricos (`Number`) o para Objetos (`Object`), ya que pueden absorber un Entero sin problema. Al usar `super`, permites lambdas de clases superiores.
* En nuestro método `transformar`, lo ideal sería aplicar PECS: la función transformadora debería recibir `<? super T>` (porque consume la entrada T) y debería devolver `<? extends R>` (porque produce el resultado R, permitiendo que devuelva cualquier subclase del resultado esperado).

### 16. Referencias a métodos. Podemos obtener una referencia a métodos de objetos o clases. Pon un ejemplo en JavaScript y en Java, de una clase `Persona` con un método `saludar`...

**Respuesta:**
A veces, una lambda lo único que hace es llamar a un método que ya existe. Las "referencias a métodos" son un atajo para escribir menos. 
Si creamos un objeto `Persona` con el nombre "Juan", podemos guardar una referencia directa a la acción de saludar de Juan en una variable (una especie de puntero al método de ese objeto concreto). 
Tanto en Java (usando doble dos puntos `::`) como en JavaScript (asignando el método y forzando el contexto con `bind`), al ejecutar luego esa variable local, el programa invocará el saludo sabiendo perfectamente que era el saludo del objeto "Juan", no de cualquier persona abstracta.

### 17. ¿Qué tipos de referencias a método se pueden hacer en Java?

**Respuesta:**
En Java existen cuatro tipos principales de referencias a métodos:
1.  **A un método estático:** (Ej. `Math::max`). Apunta a funciones de utilidad globales de una clase.
2.  **A un constructor:** (Ej. `Persona::new`). Muy útil cuando tienes operaciones funcionales cuyo único fin es crear e inicializar nuevos objetos del mismo tipo.
3.  **A un método de una instancia concreta:** (Ej. `juan::saludar`). Como vimos antes, apunta al método de un objeto que ya existe y está instanciado en la memoria.
4.  **A un método de cualquier instancia de un tipo arbitrario:** (Ej. `String::toUpperCase`). Aquí no hay un objeto concreto asignado aún. La referencia pide que, cuando se ejecute, se le pase un objeto de ese tipo y automáticamente llamará a ese método sobre el objeto recibido.

### 18. Otro ejemplo expresivo. Ordena una lista de `Persona`, cada persona tiene un nombre y una edad. Ordena la lista con `Collections.sort`... Crea dos versiones: Una con la función de comparación hecha manualmente, y otra empleando `Comparator`.

**Respuesta:**
* **Versión manual (Lambda):** A `Collections.sort` le pasamos una lambda que recibe dos objetos `Persona`. Dentro, abrimos llaves y escribimos la lógica tradicional: primero comparamos las edades mediante restas; si el resultado de la resta es distinto de cero (edades distintas), devolvemos ese número para ordenar. Si la resta da cero (misma edad), llamamos a la función de comparar alfabéticamente sus nombres y devolvemos eso.
* **Versión con `Comparator` (Fluida/Declarativa):** Java nos permite hacerlo sin escribir la lógica matemática. Pasamos al método de ordenar una instrucción construida con las herramientas de `Comparator`, que se lee como lenguaje humano: `Comparator.comparing` (extrae la edad) y lo encadenamos con `.thenComparing` (extrae el nombre). Esto genera automáticamente la función de ordenación compleja bajo el capó, siendo una muestra perfecta de la elegancia del paradigma funcional.