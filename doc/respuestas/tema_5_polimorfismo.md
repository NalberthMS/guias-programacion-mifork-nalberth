<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Polimorfismo". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos, Encapsulación, Excepciones, Composición y Herencia.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# Tema 5. Polimorfismo - Respuestas

## 1. Brevemente, ¿qué es el **"polimorfismo"** y para qué sirve en programación orientada a objetos? ¿qué es la **"sobreescritura"** de métodos?
**Respuesta:**
El polimorfismo es la capacidad que tienen los objetos de diferentes clases relacionadas por herencia de responder de forma distinta al mismo llamado a un método. Sirve para escribir programas más genéricos, flexibles y fáciles de mantener, ya que puedes procesar colecciones de objetos distintos usando una misma interfaz o clase base sin preocuparte del tipo exacto de cada uno. 
La **sobreescritura** (overriding) es el mecanismo que hace posible el polimorfismo: consiste en que una subclase vuelve a definir un método que ya existía en su clase padre, proporcionando un comportamiento específico adaptado a la subclase.

## 2. ¿En qué consiste la **"ligadura dinámica"** o **"enlace tardío"**? ¿qué relación tiene con el polimorfismo? ¿hay que indicarlos explícitamente al programar o depende esto del lenguaje? Compara C++ y Java. Indicalo después también para Python.
**Respuesta:**
La ligadura dinámica (o enlace tardío) consiste en que el programa decide qué versión de un método ejecutar en **tiempo de ejecución** (mientras el programa corre), basándose en el tipo real del objeto en memoria, y no en el tipo de la variable que lo referencia. Es el motor interno que hace funcionar el polimorfismo.
* **Java:** La ligadura dinámica es automática y ocurre por defecto para todos los métodos de instancia (a menos que sean privados o `final`).
* **C++:** No es el comportamiento por defecto. Para que exista ligadura dinámica y polimorfismo, hay que indicarlo explícitamente marcando el método en la clase base con la palabra clave `virtual`.
* **Python:** Al ser un lenguaje de tipado dinámico, la ligadura tardía es natural y es la única forma en la que funciona. Se rige por el "Duck Typing" (si camina como pato y hace cuac, es un pato), determinando en tiempo de ejecución si el objeto posee el método invocado.

## 3. Pon un ejemplo sencillo en Java, de un `Soldado`, con un método `saluda`, con dos subclases: `Zapador` y `Artillero`... (explicado sin código)
**Respuesta:**
Imagina una clase base `Soldado` con un método para saludar de forma genérica. Las clases `Zapador` y `Artillero` heredan de `Soldado` pero cada una **sobreescribe** el saludo para decir su especialidad. 
Para ilustrar el polimorfismo, crearías una lista (o array) del tipo base genérico `Soldado`. Dentro de esa lista guardas mezclados tanto objetos `Zapador` como objetos `Artillero`. Al recorrer la lista con un bucle, le dices a cada elemento "saluda". Aunque la variable del bucle es genéricamente un `Soldado`, la ligadura dinámica se encarga de que, automáticamente, los zapadores saluden como zapadores y los artilleros como artilleros.

## 4. Si sobreescribo un método, ¿puedo invocar el método base para trabajar a partir de su resultado? Haz que zapador cambie ligeramente la forma de saludar... ¿qué palabra clave del lenguaje has usado para invocar al método de la clase base?
**Respuesta:**
Sí, es completamente posible invocar el comportamiento del método original desde dentro del método sobreescrito. En el caso del Zapador, dentro de su propio método de saludo, primero llamaría al saludo del soldado genérico y, a continuación, añadiría la frase "ZAPADOR A SUS ORDENES". 
La palabra clave que se utiliza en Java (y en muchos otros lenguajes) para referirse a la clase padre e invocar sus métodos es **`super`**. 

## 5. Al sobreescribir un método en Java, ¿qué restricciones existen sobre los tipos de los parámetros y el tipo de retorno? ¿Qué diferencia hay entre sobreescritura (*overriding*) y sobrecarga (*overloading*)? ¿Para qué sirve la anotación `@Override` y por qué es recomendable usarla siempre?
**Respuesta:**
* **Restricciones:** Al sobreescribir, el nombre del método y el tipo/cantidad de parámetros deben ser **exactamente iguales**. El tipo de retorno debe ser el mismo o un subtipo válido (retorno covariante). Además, no puedes hacer que el método sea más restrictivo (por ejemplo, si el padre es público, el hijo no puede ser privado).
* **Diferencia:** La **sobreescritura** reemplaza el comportamiento heredado (mismo nombre, mismos parámetros, distintas clases padre/hijo). La **sobrecarga** consiste en tener varios métodos con el mismo nombre en la misma clase, pero con diferentes parámetros (distinta firma).
* **Anotación `@Override`:** Sirve para decirle al compilador que tu intención es sobreescribir. Es muy recomendable usarla porque, si cometes un error tipográfico en el nombre del método o en los parámetros, el compilador lanzará un error avisándote de que en realidad no estás sobreescribiendo nada, evitándote dolores de cabeza.

## 6. Entonces, cuando se estudia Java, ¿se emplea el polimorfismo desde el principio? Por ejemplo, sobreescribiendo `toString` o sobreescribiendo `equals`, ¿ya estoy usando polimorfismo?
**Respuesta:**
Sí, absolutamente. En Java, todas las clases heredan implícitamente de la clase maestra suprema llamada `Object`. Cuando creas una clase nueva y redefines los métodos `toString` o `equals`, estás sobreescribiendo métodos de la clase base `Object`. Cuando funciones como `System.out.println()` intentan imprimir tu objeto, invocan polimórficamente a tu versión del método `toString` en lugar de la versión por defecto.

## 7. ¿Qué es una **"clase abstracta"**? ¿Qué es un **"método abstracto"**? ¿Puedo crear instancias de una clase abstracta? Pongamos un ejemplo en Java: Redefinamos `Soldado`... ¿Donde debemos poner `abstract`?
**Respuesta:**
* Una **clase abstracta** es un "molde incompleto" o un concepto general del cual **no se pueden crear instancias** (no puedes hacer un `new` de ella). Sirve para que otras clases hereden de ella.
* Un **método abstracto** es un método que está declarado (se sabe su nombre y parámetros) pero no tiene implementación (no tiene cuerpo o código). Obliga a las subclases a programar dicho comportamiento.
* En el ejemplo del `Soldado`, pondríamos la palabra `abstract` en dos sitios: en la definición de la clase `Soldado` (para impedir que se creen soldados genéricos que no tengan especialidad) y en el método `atacar` (sin llaves ni código), forzando así a que `Zapador` y `Artillero` definan obligatoriamente cómo atacan.

## 8. ¿Qué efecto tiene la palabra clave `final` sobre métodos y clases en Java? ¿Cómo se relaciona con el polimorfismo? ¿Conoces algún ejemplo de clase `final` en la propia API estándar de Java?
**Respuesta:**
* **Sobre una clase:** Impide que la clase tenga descendencia (nadie puede heredar de ella).
* **Sobre un método:** Impide que el método pueda ser sobreescrito por las subclases.
* **Relación con el polimorfismo:** La palabra `final` es el "enemigo" del polimorfismo de herencia, ya que al prohibir la sobreescritura, bloqueas la capacidad de alterar o especializar comportamientos. Se usa por motivos de seguridad o diseño cerrado.
* Un ejemplo famoso de clase `final` en la API de Java es la clase `String`. Nadie puede crear una subclase de `String`.

## 9. En Java, qué son las **"interfaces"**? ¿Son como clases abstractas? ¿Una clase puede implementar más de una interfaz?
**Respuesta:**
Las interfaces son "contratos" o conjuntos de promesas de comportamiento. Definen qué métodos debe tener una clase sin importar cómo los implemente.
Son parecidas a las clases abstractas en el sentido de que no se pueden instanciar y obligan a implementar métodos, pero a diferencia de la herencia de clases (que determina "lo que es" un objeto), las interfaces determinan "lo que puede hacer" un objeto. 
Además, en Java no existe la herencia múltiple de clases, pero **una clase sí puede implementar tantas interfaces como desee** al mismo tiempo.

## 10. Vamos a poner un ejemplo nuevo con polimorfismo. Queremos implementar una clase `Punto`, con un método `calcularDistanciaA`... (explicado sin código)
**Respuesta:**
Se diseñaría una clase base o interfaz `Punto` con un método abstracto para calcular la distancia que reciba como parámetro otro `Punto` genérico. 
En las implementaciones (`Punto2D` y `Punto3D`), dentro del cálculo de distancia, se usaría la palabra reservada `instanceof` para preguntar si el punto recibido como parámetro es de su mismo tipo (es decir, un Punto2D verificando que recibe otro Punto2D). Si es así, se hace un *downcasting* (una conversión explícita) para tratar ese parámetro genérico como un `Punto2D` real y poder leer sus variables matemáticas exclusivas y aplicar la fórmula correcta.
La clase `Linea` simplemente guardaría dos objetos de tipo `Punto` genéricos. Para saber su propia longitud, la línea solo tendría que decirle al primer punto que calcule la distancia hasta el segundo punto. Gracias al polimorfismo, el cálculo se hace correctamente en el espacio 2D o 3D sin que la clase `Linea` tenga que hacer comprobaciones o saber con qué tipo de punto está trabajando.

## 11. ¿Qué es la **"herencia de interfaces"** en Java? ¿Existe **"herencia múltiple de interfaces"**? Pon un ejemplo de una interfaz `Fichero`...
**Respuesta:**
La herencia de interfaces permite que una interfaz herede (amplíe) los métodos definidos en otra interfaz.
En Java, a diferencia de las clases, **sí existe la herencia múltiple de interfaces** (una interfaz puede heredar de varias interfaces al mismo tiempo).
En el ejemplo mencionado, tendríamos primero una interfaz `Fichero` con un método que solo requiere leer un texto. Después, crearíamos una nueva interfaz `FicheroEscribible` que indique que extiende de `Fichero`. Esto significa que si una clase decide implementar `FicheroEscribible`, estará obligada por contrato a programar tanto los métodos propios de escritura y borrado, como el método de lectura que se ha heredado de la interfaz original.