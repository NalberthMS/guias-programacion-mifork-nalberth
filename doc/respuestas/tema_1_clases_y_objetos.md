<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Clases y Objetos". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: ninguno.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->

# TEMA 1. Clases y objetos

## 1. ¿Cuáles son las cuatro características básicas de la programación orientada a objetos? Describe brevemente cada una

### Respuesta

1. Abstracción
Es la capacidad de modelar objetos del mundo real en código, seleccionando solo los datos y comportamientos relevantes para el sistema y omitiendo los detalles complejos innecesarios.
2. Encapsulamiento
Consiste en ocultar el estado interno (los datos) de un objeto para protegerlo de manipulaciones externas indebidas. El acceso a estos datos se controla a través de métodos públicos.
3. Herencia
Es el mecanismo que permite crear una nueva clase basada en una existente, adquiriendo sus atributos y métodos. Fomenta la reutilización del código.
4. Polimorfismo
Es la capacidad de que un mismo identificador o método se comporte de diferentes formas según el objeto al que se aplique.

## 2. Cita cuatro lenguajes populares que permitan la programación orientada a objetos

### Respuesta

1. **Java**
Es el lenguaje que estás estudiando. Es uno de los lenguajes orientados a objetos más "puros" y populares del mundo. Su lema es "escríbelo una vez, ejecútalo en cualquier lugar". Se usa masivamente en aplicaciones empresariales y desarrollo Android.

2. **C++**
Es una extensión del lenguaje C que añade orientación a objetos. Es famoso por su alto rendimiento y control sobre el hardware.
* *Nota:* Es el estándar en la industria de **videojuegos** de alto presupuesto (motores como Unreal Engine) y sistemas en tiempo real.

3. **C# (C Sharp)**
Creado por Microsoft, es muy similar a Java en sintaxis y funcionamiento. Es un lenguaje puramente orientado a objetos.
* *Nota:* Es el lenguaje principal del motor **Unity** para desarrollo de videojuegos.

4. **Python**
Aunque es multiparadigma (permite programar sin clases), en Python *todo* es un objeto. Es extremadamente popular hoy en día por su sencillez y su dominio en el campo de la Inteligencia Artificial y la Ciencia de Datos.

## 3. Los paradigmas anteriores a la POO, ¿Qué es la **programación estructurada**? y, todavía mejor, ¿Qué es la **programación modular**?

### Respuesta

#### A. Programación Estructurada

Es un paradigma de programación orientado a mejorar la claridad, la calidad y el tiempo de desarrollo de un programa mediante la restricción del flujo de control. Su base teórica se fundamenta en el **Teorema de la Estructura (Böhm y Jacopini, 1966)**, el cual establece que todo algoritmo computable puede ser implementado utilizando únicamente tres estructuras lógicas de control:

1. **Secuencia:** La ejecución de instrucciones en un orden lineal, una tras otra.
2. **Selección (Condicional):** La ejecución de bloques de código basada en el cumplimiento de una condición lógica (`if`, `switch`).
3. **Iteración (Bucles):** La repetición de un bloque de instrucciones mientras se cumpla una condición (`for`, `while`).

**Características principales:**

* **Eliminación del salto incondicional:** Se prohíbe o desaconseja el uso de la instrucción `GOTO`, la cual permite saltos arbitrarios en el código, dificultando la trazabilidad del flujo de ejecución (evitando el llamado "código espagueti").
* **Un solo punto de entrada y salida:** Cada bloque de estructura tiene un único punto de inicio y un único punto de fin, lo que facilita la depuración y el mantenimiento.

#### B. Programación Modular

Es un paradigma de diseño que consiste en la descomposición de un sistema de software complejo en unidades más pequeñas, manejables e independientes denominadas **módulos** (también conocidos como funciones, procedimientos o subrutinas, dependiendo del lenguaje).

Este paradigma aplica el principio de **"divide y vencerás"**, permitiendo abordar la complejidad del sistema por partes.

**Características principales:**

* **Descomposición funcional:** El problema global se divide en subproblemas específicos, donde cada módulo es responsable de una tarea concreta.
* **Independencia y Abstracción:** Cada módulo actúa como una "caja negra"; posee una **interfaz** definida (parámetros de entrada y valores de retorno) que permite su uso sin necesidad de conocer su implementación interna.
* **Acoplamiento y Cohesión (Métricas clave):**
* Se busca una **alta cohesión**: Las instrucciones dentro de un módulo deben estar estrechamente relacionadas con una única funcionalidad.
* Se busca un **bajo acoplamiento**: La dependencia entre distintos módulos debe ser mínima, de modo que un cambio en un módulo afecte lo menos posible a los demás.

## 4. ¿Qué tres elementos definen a un objeto en programación orientada a objetos?

### Respuesta

### 1. Identidad (Identity)

Es la propiedad que permite diferenciar un objeto de otro, independientemente de que sus valores internos sean idénticos. En el mundo real, dos coches del mismo modelo y color son distintos; en programación, la identidad es lo que hace único a cada objeto dentro del sistema.

### 2. Estado (State)

Representa las características estáticas o propiedades del objeto en un momento determinado. El estado está compuesto por el conjunto de valores que tienen sus **atributos** (variables de instancia). El estado de un objeto es dinámico y puede cambiar a lo largo del tiempo como respuesta a la ejecución de sus métodos.

### 3. Comportamiento (Behavior)

Define lo que el objeto "sabe hacer" o cómo reacciona ante los mensajes que recibe. Determina las operaciones que se pueden realizar sobre el objeto y cómo estas pueden modificar su estado.

## 5. ¿Qué es una clase? ¿Es lo mismo que un objeto? ¿Qué es una instancia? ¿Todos los lenguajes orientados a objetos manejan el concepto de clase?

### Respuesta
**1. La Clase: El plano abstracto**
En el paradigma de la Programación Orientada a Objetos (POO), una clase se define como una plantilla o molde abstracto. Su función es describir la estructura y el comportamiento que tendrán los elementos creados a partir de ella. Una clase define los atributos (propiedades o datos) y los métodos (acciones o funciones), pero no contiene los datos en sí misma ni ocupa espacio en la memoria de ejecución como un objeto tangible. Una analogía común es considerar la clase como el plano arquitectónico de una casa: contiene todas las especificaciones necesarias para construirla, pero no es la casa física.

**2. El Objeto: La entidad concreta**
Un objeto es una entidad independiente que existe en la memoria del ordenador durante la ejecución del programa. Es el resultado de utilizar una clase como molde para crear un elemento funcional. A diferencia de la clase, el objeto tiene un estado propio (los valores específicos de sus atributos) y una identidad única. Siguiendo la analogía anterior, el objeto sería la casa ya construida siguiendo el plano; es tangible y funcional.

**3. La Instancia: La relación de concreción**
Aunque a menudo se utiliza como sinónimo de objeto, el término "instancia" hace referencia específica a la relación de origen entre un objeto y su clase. Se dice que un objeto es una "instancia" de una clase determinada. La "instanciación" es el proceso técnico (generalmente mediante el operador *new*) por el cual el sistema asigna memoria y crea un objeto basándose en la definición de la clase.

**4. Diferencias clave entre Clase y Objeto**
La distinción fundamental radica en la abstracción frente a la concreción. La clase es un concepto estático que existe en el código fuente (tiempo de compilación), mientras que el objeto es una entidad dinámica que existe en la memoria RAM (tiempo de ejecución). De una única clase se pueden crear (instanciar) múltiples objetos, cada uno con valores diferentes en sus atributos, pero compartiendo la misma estructura base.

**5. Modelos de Lenguajes: Clases vs. Prototipos**
No todos los lenguajes orientados a objetos utilizan clases. Existen dos enfoques principales:

* **Lenguajes basados en Clases:** Son los más extendidos en el ámbito académico y empresarial (Java, C++, C#, Python). En ellos, la clase es un requisito indispensable y previo para poder crear objetos.
* **Lenguajes basados en Prototipos:** En este modelo (utilizado por JavaScript o Lua), no existen las clases como moldes maestros. Los objetos se crean clonando otros objetos existentes, denominados prototipos, y extendiendo o modificando sus características según sea necesario.

## 6. ¿Dónde se almacenan en memoria los objetos? ¿Es igual en todos los lenguajes? ¿Qué es la **recolección de basura**? 

### Respuesta

**Gestión de Memoria y Recolección de Basura**

**1. ¿Dónde se almacenan los objetos en memoria?**
Para entender dónde viven los objetos, es necesario distinguir entre las dos áreas principales de la memoria RAM que utilizan los programas: el **Stack** (Pila) y el **Heap** (Montículo).

* **El Stack (Pila):** Es una zona de memoria ordenada, rápida y de tamaño limitado. Aquí se almacenan las llamadas a funciones y las variables locales.
* **El Heap (Montículo):** Es una zona de memoria grande, desordenada y dinámica.

En la mayoría de los lenguajes orientados a objetos (como Java, C# o Python), la distribución funciona así:

1. **El Objeto (los datos reales):** Se crea y almacena en el **Heap**. Ocupa un bloque de memoria que permanece allí hasta que se libera.
2. **La Referencia (la variable):** La variable que usas en tu código (ej. `miCoche`) se guarda en el **Stack**. Esta variable no contiene el objeto en sí, sino una "dirección" o puntero que indica en qué parte del Heap se encuentra el objeto.

**Analogía:** El *Stack* es tu bolsillo, donde guardas un papelito (la referencia) con una dirección escrita. El *Heap* es el almacén gigante donde está guardado el paquete real (el objeto) en esa dirección.

**2. ¿Es igual en todos los lenguajes?**
El concepto general de Stack y Heap es universal, pero el comportamiento varía según el lenguaje:

* **Lenguajes Gestionados (Java, Python, C#):** Casi todos los objetos se crean obligatoriamente en el **Heap**. El programador no tiene control directo sobre la memoria física.
* **Lenguajes No Gestionados (C++):** Aquí existe una diferencia crucial. En C++, tú decides.
* Puedes crear un objeto en el **Stack** (declarando `Coche miCoche;`). Es rapidísimo, pero el objeto muere automáticamente cuando se cierra la función.
* Puedes crear un objeto en el **Heap** (usando `new Coche();`). El objeto persiste hasta que tú decidas borrarlo manualmente.

**3. ¿Qué es la Recolección de Basura (Garbage Collection)?**
La Recolección de Basura (GC) es un mecanismo automático de gestión de memoria presente en lenguajes modernos como Java, Python o C#.

**El problema que resuelve:**
En lenguajes antiguos o de bajo nivel (como C++), si creas un objeto en el Heap con `new`, eres responsable de borrarlo con `delete` cuando dejas de usarlo. Si olvidas borrarlo, ese espacio de memoria queda ocupado para siempre ("fuga de memoria" o *memory leak*), lo que puede bloquear el ordenador.

**Cómo funciona el Garbage Collector:**
Es un proceso en segundo plano (como un robot de limpieza) que monitorea la memoria.

1. Revisa todos los objetos que hay en el Heap.
2. Identifica aquellos que **ya no tienen ninguna referencia** apuntando a ellos (es decir, el programa ha perdido el "papelito" con su dirección y ya no puede acceder a ellos).
3. Borra esos objetos automáticamente y libera el espacio para que pueda ser reutilizado.
## 7. ¿Qué es un método? ¿Qué es la **sobrecarga de métodos**? 

### Respuesta
**Métodos y Sobrecarga**

**1. ¿Qué es un método?**
Un método es un bloque de código que contiene una serie de instrucciones para realizar una tarea específica. En el contexto de la Programación Orientada a Objetos, los métodos representan el **comportamiento** de los objetos. Técnicamente, son funciones que están encapsuladas dentro de una clase.

Mientras que los atributos (variables) definen *cómo es* el objeto (sus datos), los métodos definen *qué puede hacer* el objeto (sus acciones). Por ejemplo, si la clase es `Coche`, sus métodos podrían ser `arrancar()`, `acelerar()` o `frenar()`.

**2. ¿Qué es la Sobrecarga de Métodos (Method Overloading)?**
La sobrecarga de métodos es una característica que permite definir dentro de una misma clase **múltiples métodos con el mismo nombre**, siempre y cuando tengan **diferentes parámetros** (diferente "firma").

El compilador distingue qué método debe ejecutar basándose en los argumentos que se le pasan al llamarlo. No es suficiente con cambiar el tipo de dato que devuelve el método; es obligatorio que cambie la lista de parámetros (ya sea en cantidad o en tipo de dato).

**3. ¿Para qué sirve la sobrecarga?**
La sobrecarga mejora la legibilidad y la usabilidad del código. Permite que el programador utilice una misma acción lógica de manera intuitiva sin tener que memorizar nombres diferentes para cada variación de la entrada.

* **Ejemplo práctico:** Imaginemos una calculadora.
* Sin sobrecarga, tendrías que crear métodos con nombres distintos: `sumarEnteros(int a, int b)` y `sumarDecimales(double a, double b)`.
* Con sobrecarga, simplemente llamas a `sumar(a, b)`. Si le pasas números enteros, el sistema busca y ejecuta la versión del método preparada para enteros. Si le pasas decimales, ejecuta la versión preparada para decimales.

**4. Diferencia clave: Sobrecarga vs. Sobreescritura**
Es crucial no confundir la **Sobrecarga** (Overloading) con la **Sobreescritura** (Overriding), ya que son conceptos distintos que a menudo se preguntan en exámenes:

* **Sobrecarga (Overloading):** Ocurre en la **misma clase**. Mismo nombre, **distintos parámetros**. Es una forma de añadir variantes de una acción.
* **Sobreescritura (Overriding):** Ocurre entre una **clase padre y una hija** (herencia). Mismo nombre, **mismos parámetros**. Sirve para modificar o reemplazar el comportamiento heredado.

Claro, aquí tienes el cuestionario completo con los enunciados seguidos de sus respuestas explicadas en formato de texto, listo para entregar.

---

**8. Ejemplo mínimo de clase en Java, que se llame Punto, con dos atributos, x e y, con un método que se llame `calculaDistanciaAOrigen`, que calcule la distancia a la posición 0,0. Por sencillez, los atributos deben tener visibilidad por defecto. Crea además un ejemplo de uso con una instancia y uso del método.**
### Respuesta

Para definir esta clase en Java, crearíamos una estructura llamada "Punto" que contendría dos atributos de tipo numérico decimal (doble precisión) para representar las coordenadas X e Y. Al tener visibilidad por defecto, no se les añadiría ningún modificador de acceso explícito (como *public* o *private*).

Dentro de esta clase, definiríamos un método llamado "calculaDistanciaAOrigen". La lógica interna de este método aplicaría el Teorema de Pitágoras: calcularía la raíz cuadrada de la suma de X al cuadrado más Y al cuadrado, devolviendo el resultado numérico.

Para utilizarla, en el programa principal se crearía una **instancia** de la clase "Punto" (un objeto específico) utilizando el operador de creación de objetos (*new*). Posteriormente, se asignarían valores numéricos a sus coordenadas (por ejemplo, asignar 3 a la X y 4 a la Y) y se llamaría al método mencionado para obtener la distancia, que en este caso resultaría en 5.

**9. ¿Cuál es el punto de entrada en un programa en Java? ¿Qué es `static` y para qué vale? ¿Sólo se emplea para ese método `main`? ¿Para qué se combina con `final`?**

### Respuesta

El punto de entrada de cualquier aplicación en Java es un método específico y obligatorio llamado **main**.

El modificador **static** significa que el método o atributo pertenece a la clase en general y no a un objeto o instancia en particular. Es estrictamente necesario para el método *main* porque, al arrancar el programa, todavía no existe ningún objeto creado en la memoria; por tanto, la Máquina Virtual necesita poder llamar a este método sin necesidad de instanciar la clase primero.

No se usa solo para el *main*; se utiliza para cualquier función que no requiera acceder a los datos internos (estado) de un objeto específico, o para variables que deben ser compartidas por todas las instancias de esa clase. Cuando se combina con **final**, se utiliza para definir constantes globales, es decir, valores que son compartidos por todos y que no pueden ser modificados una vez asignados.

**10. Intenta ejecutar un poco de Java de forma básica, con los comandos `javac` y `java`. ¿Cómo podemos compilar el programa y ejecutarlo desde linea de comandos? ¿Java es compilado? ¿Qué es la **máquina virtual**? ¿Qué es el *byte-code* y los ficheros `.class`?**

### Respuesta

Para ejecutar Java desde la línea de comandos, el proceso consta de dos pasos. Primero utilizamos el compilador (comando **javac**) pasándole el nombre del archivo fuente (con extensión .java). Esto genera un nuevo archivo con extensión **.class**. Después, utilizamos el lanzador (comando **java**) seguido del nombre de la clase para iniciar la ejecución del programa.

Java es un lenguaje híbrido: el código fuente se **compila** primero a un formato intermedio llamado **byte-code** (que es lo que contienen los archivos .class). Este byte-code no es código máquina real para el procesador físico, sino un conjunto de instrucciones para una máquina abstracta.

La **Máquina Virtual de Java (JVM)** es el software que actúa como un simulador de ordenador. Su función es leer ese *byte-code* e interpretarlo o traducirlo dinámicamente a las instrucciones específicas del sistema operativo real (Windows, Linux, macOS) en el que se esté ejecutando. Esto permite que el mismo archivo compilado funcione en cualquier sistema.

**11. En el código anterior de la clase `Punto` ¿Qué es `new`? ¿Qué es un **constructor**? Pon un ejemplo de constructor en una clase `Empleado` que tenga DNI, nombre y apellidos.**

La palabra clave **new** es el operador que solicita al sistema operativo que reserve un espacio nuevo en la memoria dinámica (Heap) para alojar un objeto nuevo.

Un **constructor** es un bloque de código especial dentro de la clase que se caracteriza por tener exactamente el mismo nombre que ella y no devolver ningún tipo de dato. Se ejecuta automáticamente justo después del operador *new*. Su función principal es **inicializar** el objeto, dándole valores iniciales válidos a sus atributos.

Como ejemplo, en una clase "Empleado", el constructor se definiría recibiendo como parámetros el DNI, el nombre y los apellidos. Dentro de su código, se encargaría de asignar esos datos recibidos a los atributos internos del objeto recién creado, asegurando que el empleado "nace" ya con sus datos personales rellenos correctamente.

**12. ¿Qué es la referencia `this`? ¿Se llama igual en todos los lenguajes? Pon un ejemplo del uso de `this` en la clase `Punto`.**

### Respuesta

La palabra clave **this** es una referencia autodefinida que se utiliza dentro de un método para señalar al **propio objeto** que está ejecutando el código en ese instante.

Su uso principal es resolver ambigüedades de nombres (scope). Por ejemplo, si en la clase "Punto" el constructor recibe un parámetro llamado "x" y el objeto tiene un atributo que también se llama "x", usamos **this.x** para referirnos al atributo del objeto, mientras que "x" a secas se refiere al parámetro recibido. De esta forma, el compilador sabe qué variable es cual.

Este concepto es universal en la programación orientada a objetos, aunque el nombre varía. En Python se llama *self*, en Visual Basic se llama *Me*, y en C# o C++ se mantiene como *this*.

**13. Añade ahora otro nuevo método que se llame `distanciaA`, que reciba un `Punto` como parámetro y calcule la distancia entre `this` y el punto proporcionado.**

### Respuesta

Para resolver esto, añadiríamos una función llamada "distanciaA" que aceptaría como argumento otro objeto de tipo "Punto".

La lógica del método consistiría en calcular la diferencia entre la coordenada X del objeto actual (accediendo mediante **this.x**) y la coordenada X del punto recibido como parámetro (accediendo mediante el nombre del parámetro punto X), y repetir la operación con las coordenadas Y. Finalmente, aplicaría la fórmula de la distancia euclidiana (raíz cuadrada de la suma de los cuadrados de esas diferencias) para devolver el resultado.

**14. El paso del `Punto` como parámetro a un método, es **por copia** o **por referencia**, es decir, si se cambia el valor de algún atributo del punto pasado como parámetro, dichos cambios afectan al objeto fuera del método? ¿Qué ocurre si en vez de un `Punto`, se recibiese un entero (`int`) y dicho entero se modificase dentro de la función?**

### Respuesta

En Java, el paso de parámetros de objetos funciona como un **paso por copia de la referencia**. Esto significa que cuando pasas un objeto "Punto" a un método, estás entregando una copia de la dirección de memoria donde vive el objeto. Si dentro del método usas esa referencia para modificar los atributos del punto (como cambiar su coordenada X), el cambio **sí afecta** al objeto original que está fuera, porque ambas referencias apuntan a la misma entidad en memoria.

Sin embargo, si pasas un dato primitivo como un número entero (**int**), se pasa una **copia del valor**. Si dentro de la función modificas ese número, solo estás alterando tu copia local; la variable original que estaba fuera de la función **no sufre ningún cambio** y permanece intacta.

**15. ¿Qué es el método `toString()` en Java? ¿Existe en otros lenguajes? Pon un ejemplo de `toString()` en la clase `Punto` en Java.**

### Respuesta

El método **toString** es una función especial que todos los objetos en Java heredan automáticamente de la clase base Object. Su propósito fundamental es devolver una representación en formato de texto (String) del estado del objeto.

Si no se modifica, devuelve un identificador técnico poco útil (generalmente la clase y la dirección de memoria). Es buena práctica **sobreescribirlo** para que devuelva información legible. Por ejemplo, en la clase "Punto", se programaría para que construya y devuelva una cadena de texto con el formato "(x, y)", insertando los valores reales de las coordenadas, lo cual facilita mucho la depuración y la impresión de datos por pantalla. Conceptos idénticos existen en otros lenguajes (como ***str*** en Python).

**16. Reflexiona: ¿una clase es como un `struct` en C? ¿Qué le falta al `struct` para ser como una clase y las variables de ese tipo ser instancias?**

### Respuesta

Sí, conceptualmente una clase es una evolución directa del **struct** del lenguaje C, ya que ambos son mecanismos para agrupar variables de distintos tipos de datos en una sola estructura lógica.

Lo que le falta al *struct* tradicional para ser una clase es:

1. **Comportamiento:** Los structs en C solo agrupan datos, no pueden contener métodos (funciones) dentro de su definición que operen sobre esos datos.
2. **Encapsulamiento:** En un struct, todos los datos son públicos por defecto; no existen mecanismos nativos de *private* o *protected* para ocultar información.
3. **Herencia y Polimorfismo:** No es posible crear jerarquías donde un struct herede propiedades de otro automáticamente.

**17. Quitemos un poco de magia a todo esto: ¿Como se podría “emular”, con `struct` en C, la clase `Punto`, con su función para calcular la distancia al origen? ¿Qué ha pasado con `this`?**

### Respuesta

Para "emular" la orientación a objetos en C, definiríamos un *struct* que contenga los datos X e Y. Dado que el *struct* no puede contener funciones, crearíamos una función externa estándar para calcular la distancia.

La clave de la emulación es que esa función externa debería recibir obligatoriamente un **puntero al struct** como primer parámetro. De esta forma, indicamos explícitamente sobre qué datos debe operar la función.

En esta emulación, ese puntero que pasamos manualmente (por ejemplo, llamado *p*) cumple exactamente la misma función que la referencia **this** en los lenguajes orientados a objetos. La diferencia radica en la automatización: en Java, el compilador pasa el **this** de forma invisible y automática en cada llamada a un método, mientras que en C nosotros, como programadores, tenemos que escribirlo y pasarlo explícitamente.