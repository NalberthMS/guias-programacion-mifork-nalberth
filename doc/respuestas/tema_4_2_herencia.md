<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Herencia". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos, Encapsulación, Excepciones y Composición.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
¡Claro que sí! Aquí tienes el cuestionario completo, uniendo cada una de tus preguntas con su respectiva respuesta directa y sin bloques de código, tal como lo necesitas:

---

### 1. En orientación a objetos, ¿qué es la **herencia** y su relación con "A es-un B"?. Explica las dos implicaciones principales: (1) **compatibilidad de tipos** y (2) **herencia de estado y comportamiento**. Pon un ejemplo en Java muy sencillo, donde un `Soldado` tiene un `nombre` (privado) y un método `saludar()` que muestra su nombre. Hay dos subtipos: un `Artillero`, que es capaz de disparar cohetes y un `Zapador` que pone minas, ambos heredan el atributo nombre y la capacidad de saludar. Además, y de forma específica, el artillero tiene un número de cohetes y el zapador un número de minas, accesibles mediante "getters" específicos. Respecto a la compatibilidad de tipos, aprovechémosla: crea un array de `Soldado`, mete varios de distinto tipo (son todos compatibles con `Soldado`). Recórrela y que todos te saluden.

**Respuesta:**
La **herencia** es un mecanismo que permite crear nuevas clases basadas en clases existentes, estableciendo una relación de tipo "A es-un B" (por ejemplo, un Perro es un Animal). 
* **Compatibilidad de tipos:** Significa que cualquier objeto de la subclase puede ser tratado como si fuera del tipo de la superclase. 
* **Herencia de estado y comportamiento:** La subclase recibe (hereda) los atributos y los métodos de la clase padre.


**Ejemplo explicado:**
Imagina una clase base `Soldado` con un atributo privado de texto para el nombre y un método público para saludar que imprime dicho nombre. Creamos dos subclases: `Artillero` (con un atributo numérico para cohetes y su "getter") y `Zapador` (con un atributo numérico para minas y su "getter"). Como ambos heredan de `Soldado`, ya saben saludar y tienen nombre internamente. 
Aprovechando la compatibilidad, podemos crear una lista o array definido para guardar objetos de tipo `Soldado`. En esa lista podemos meter indistintamente instancias de `Artillero` y de `Zapador`. Si hacemos un bucle para recorrer esa lista, le podemos pedir a cada elemento que ejecute el método de saludar; cada uno responderá correctamente porque, ante todo, todos son soldados.

---

### 2. Al crear los soldados concretos, ¿cuántos constructores se ejecutan y en qué orden? ¿Qué significa `super` dentro de un constructor? Si la clase base no tiene visible el constructor sin parámetros, ¿debo llamar a `super` siempre? 

**Respuesta:**
Al instanciar una subclase se ejecutan **dos** constructores: el de la superclase y el de la subclase. El orden de ejecución es "de arriba hacia abajo"; es decir, primero termina de ejecutarse el constructor de la clase base (para asegurar que los cimientos del objeto estén listos) y luego el de la subclase.

La palabra reservada `super` dentro de un constructor sirve para invocar explícitamente al constructor de la clase padre. Si la clase base no tiene un constructor vacío (sin parámetros) visible, **sí, es obligatorio** usar `super` pasando los argumentos necesarios en la primera línea del constructor de la subclase, ya que Java no sabría cómo construir la parte "padre" del objeto por sí solo.

---

### 3. Respecto a los objetos de subclases en memoria, los atributos privados de la superclase, ¿forman parte de una instancia de la subclase en memoria? En caso afirmativo ¿implica que se puedan usar desde el código de la subclase? Explícalo con el ejemplo de `Soldado` y alguna de sus subclases.

**Respuesta:**
**Sí**, los atributos privados de la superclase forman parte del espacio de memoria del objeto de la subclase (el objeto se construye completo). 

**No**, esto no implica que se puedan usar directamente desde el código de la subclase. Aunque el dato está en memoria, la restricción de visibilidad "private" del compilador impide que la subclase lo lea o modifique directamente. En el ejemplo del `Soldado`, un `Artillero` tiene en su memoria el atributo del nombre, pero si dentro del código del `Artillero` escribimos "this.nombre", dará error. Para acceder a él, el `Artillero` tendría que usar métodos públicos o protegidos provistos por `Soldado`, como un hipotético "getNombre()".

---

### 4. ¿Qué implica en términos de **extensibilidad** de código el hecho de que sean compatibles a nivel de tipos? Ilustra esto añadiendo un nuevo tipo de `Soldado` y demostrando que el código para pedir el saludo a todos los soldados no se modifica.

**Respuesta:**
La compatibilidad de tipos aporta una **extensibilidad** enorme gracias al Principio Abierto/Cerrado (Open/Closed Principle). Significa que podemos añadir nuevas funcionalidades al sistema sin tener que modificar el código que ya funciona. 

Si añadimos una nueva clase `Francotirador` que herede de `Soldado`, podemos instanciarla y meterla en el mismo array mencionado en la pregunta 1. El bucle que recorre el array pidiendo a todos que saluden **no sufre ninguna modificación**. El código antiguo es capaz de trabajar con clases nuevas automáticamente porque todas cumplen el contrato de ser un "Soldado".

---

### 5. En Java, cuando trabajo con referencias y herencia. ¿Puedo tener una referencia del supertipo que apunte a objetos reales de un subtipo? ¿Puedo invocar con la referencia del supertipo a métodos públicos del subtipo? ¿En qué consiste el **"upcasting"** y el **"downcasting"**? ¿Qué es el `instanceof`? Pon un ejemplo de recorrido de un array de `Soldado`, comprobando que, si el objeto real es un `Artillero`, solicite el número de cohetes que tiene y los imprima.

**Respuesta:**
* **¿Referencia supertipo a objeto subtipo?** Sí, es perfectamente válido y es la base del polimorfismo.
* **¿Invocar métodos públicos del subtipo?** No. El compilador solo te deja llamar a los métodos que estén definidos en la clase de la referencia (el supertipo), sin importar qué objeto haya debajo en memoria.
* **Upcasting:** Es convertir una referencia de un subtipo a un supertipo. Es seguro, implícito y automático.
* **Downcasting:** Es forzar a que una referencia de un supertipo se trate como un subtipo. Es explícito (requiere poner el tipo entre paréntesis) y es arriesgado, ya que puede fallar en tiempo de ejecución si el objeto no es realmente de ese subtipo.
* **instanceof:** Es un operador que evalúa en tiempo de ejecución si un objeto pertenece a una clase concreta (devuelve verdadero o falso).

**Ejemplo:** En el bucle que recorre el array de soldados, podemos poner un condicional preguntando si el elemento actual es un `instanceof Artillero`. Si la respuesta es afirmativa, hacemos un downcasting de ese soldado a una nueva variable de tipo Artillero. A través de esta nueva variable ya podemos llamar a su método específico para pedir el número de cohetes e imprimirlo.

---

### 6. Respecto a la ocultación de información y herencia, ¿qué significa acceso **"protegido"** de métodos y/o atributos? ¿Cómo se implementa en Java? Pon un ejemplo de uso de en la clase `Soldado` para que su nombre sea protegido y pueda usarse en el método de poner bombas del `Zapador`.

**Respuesta:**
El acceso **protegido** (protected) es un nivel de visibilidad intermedio. Significa que un atributo o método es accesible para la propia clase, para cualquier clase dentro del mismo paquete, y muy especialmente, para **todas sus subclases** (incluso si están en paquetes distintos).

En Java se implementa usando la palabra reservada `protected` en la declaración del atributo o método en lugar de `private` o `public`. 

**Ejemplo:** Si en la clase `Soldado` declaramos el atributo del nombre como protegido, la clase `Zapador` hereda un acceso directo a este. Dentro del método específico del zapador para poner bombas, podríamos escribir algo como imprimir en pantalla: "El zapador " + this.nombre + " acaba de poner una mina", leyendo el atributo directamente sin necesitar un método "getter".

---

### 7. En los lenguajes orientados a objetos ¿hay una **clase base** para todos los objetos? ¿Ocurre en todos los lenguajes? ¿Qué ocurre en Java?

**Respuesta:**
**No ocurre en todos los lenguajes.** Por ejemplo, en C++ no existe una clase base universal de la que hereden todas las demás por defecto.

Sin embargo, **en Java sí**. Existe una clase base universal llamada `java.lang.Object`. Todas las clases en Java, ya sean las del sistema o las que tú crees, heredan implícitamente de ella si no defines otra herencia explícita. Esto garantiza que todos los objetos en Java compartan métodos básicos como la comparación, la conversión a texto o la sincronización.

---

### 8. ¿Qué es la **"herencia múltiple"**? ¿Existe en Java herencia múltiple?

**Respuesta:**
La **herencia múltiple** de clases es un paradigma donde una subclase puede tener más de una clase padre directa (por ejemplo, un hidroavión que hereda a la vez de Avión y de Barco). 

**En Java NO existe la herencia múltiple para las clases.** Una clase solo puede hacer "extends" de una única clase padre. Esto se diseñó así para evitar el "Problema del Diamante" (conflictos sobre qué método heredar si dos padres tienen un método con el mismo nombre). Sin embargo, Java sí permite implementar múltiples "Interfaces", lo que simula algunos beneficios de la herencia múltiple pero sin sus problemas estructurales.

---

### 9. Las excepciones en los lenguajes orientados a objetos son objetos. Por tanto, se pueden crear excepciones personalizadas. Pon un ejemplo en Java de una excepción personalizada (`UsuarioNoEncontradoException`), que sea *no controlada* y que además este compuesto con un `Usuario`, para saber qué `Usuario` dio el problema. Permite además que se pueda incluir la causa, es decir, sobrecarga el constructor para tener una versión que permita añadir la causa subyacente. 

**Respuesta:**
Para crear una excepción **no controlada** en Java, nuestra clase personalizada debe heredar de `RuntimeException`. 

**Ejemplo conceptual:** Crearíamos una clase `UsuarioNoEncontradoException`. Por composición, le declaramos un atributo privado de tipo `Usuario`. 
El primer constructor recibiría un texto de mensaje y el objeto `Usuario`, pasaría el mensaje a la superclase con `super()` y guardaría el usuario en su atributo. 
Para permitir añadir la causa, crearíamos un segundo constructor sobrecargado que reciba el mensaje, el objeto `Usuario` y un objeto `Throwable` (la causa). En este constructor, llamaríamos a la superclase usando `super(mensaje, causa)` y guardaríamos también nuestro atributo de usuario. De esta forma la excepción es rica en contexto.

---

### 10. Herencia vs. Composición. Se dice que no se debe emplear herencia simplemente por reutilizar código, es decir, que si quiero reutilizar código simplemente, no debo pensar en herencia como primera opción ¿por qué?

**Respuesta:**
No se debe usar la herencia solo para reutilizar código porque la herencia establece una relación estructural muy rígida. Si la clase A tiene métodos útiles, pero la clase B no es conceptualmente un subtipo de A, hacer que B herede de A ensucia el diseño. 
B acabaría heredando comportamientos y atributos que no le corresponden ("interfaz inflada"). Además, crea un acoplamiento muy fuerte: si el día de mañana modificamos el código interno de la clase padre para sus propias necesidades, podríamos romper el funcionamiento de la clase hija inesperadamente.

---

### 11. Herencia vs. Composición. Se dice que se debe *"favorecer la composición frente a la herencia"*, ¿por qué?

**Respuesta:**

Se debe favorecer la composición ("tiene-un") frente a la herencia ("es-un") porque la composición es **mucho más flexible y modular**. 
Con la composición, construyes clases ensamblando pequeñas piezas funcionales (objetos) en lugar de crear árboles jerárquicos inmensos. Esto reduce el acoplamiento, permite cambiar el comportamiento de un objeto en tiempo de ejecución (cambiando los componentes internos) y facilita las pruebas de código. La herencia es una estructura estática y de caja blanca, mientras que la composición es dinámica y de caja negra.

---

### 12. Herencia vs. Composición. Se dice que la *"herencia rompe la encapsulación"*, ¿a qué se refiere esto?

**Respuesta:**
Se dice que la herencia rompe la encapsulación porque la subclase depende íntimamente de los detalles de implementación de la superclase. 
A diferencia de interactuar con un objeto externo usando solo sus métodos públicos (caja negra), una subclase a menudo tiene acceso a métodos protegidos y depende de cómo la clase padre gestiona su estado internamente. Si el creador de la superclase cambia la forma en que los métodos se llaman entre sí por dentro, puede estropear la lógica de una subclase que había sobrescrito (overriden) parte de ese comportamiento, exponiendo detalles internos que deberían haber estado ocultos.

---

### 13. Pongamos un ejemplo de dos alternativas para lo mismo. Tenemos un `Estudiante` y un `Trabajador`, ambos tienen datos en común: el DNI y el nombre. Modelemos esto de dos formas: uno por herencia, con una superclase `Persona`, y otro con composición, con una clase `DatosPersonales`. Se debe recibir una instancia de `DatosPersonales` en el constructor de la clase `Estudiante` y `Trabajador`.

**Respuesta:**
* **Alternativa por Herencia:** Crearíamos una superclase `Persona` que contenga los atributos DNI y nombre. Luego, las clases `Estudiante` y `Trabajador` se definirían indicando que heredan de (hacen "extends" de) `Persona`. En sus constructores recibirían los datos y llamarían al constructor del padre.
* **Alternativa por Composición:** Crearíamos una clase separada llamada `DatosPersonales` que agrupe el DNI y el nombre. Las clases `Estudiante` y `Trabajador` no heredarían de nadie. En su lugar, cada una tendría un atributo privado de tipo `DatosPersonales`. Al crear un estudiante o trabajador, su constructor exigiría recibir un objeto de tipo `DatosPersonales` ya creado, el cual se guardaría dentro de la clase, delegando a él todo lo referente a la identificación de la persona.