<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Encapsulación". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# TEMA 2. Encapsulación

## 1. En Programación Orientada a Objetos (POO), ¿Qué buscan la encapsulación y la ocultación de información? Enumera brevemente algunas ventajas.

### Respuesta

La **encapsulación** busca empaquetar en una sola unidad (la clase) tanto los datos como las funciones que los manipulan. La **ocultación** trata de proteger el funcionamiento interno del objeto, impidiendo que desde fuera se toque lo que no se debe.

**Ventajas:**

1. **Mantenibilidad:** Puedes cambiar cómo funciona algo por dentro sin romper el resto del programa.
2. **Integridad:** Protege los datos para que nadie meta valores inválidos (como una edad negativa).
3. **Simplicidad:** Quien usa el objeto no necesita saber cómo está hecho por dentro, solo cómo usarlo.
4. **Independencia:** Reduce la dependencia entre distintas partes del código.

## 2. ¿Qué se entiende por la interfaz pública de un objeto o clase en POO? Relación con la ocultación.

### Respuesta

La **interfaz pública** es el conjunto de métodos y propiedades que la clase deja "abiertos" para que el resto del mundo los use. Es como el panel de control o los botones de una máquina.
Se relaciona con la ocultación porque la interfaz pública es lo único visible; todo lo demás (los cables, engranajes y lógica interna) queda oculto para garantizar que la máquina se use correctamente.

## 3. ¿Por qué hay que diseñar con cuidado la interfaz pública? ¿Es fácil cambiarla?

### Respuesta

Hay que diseñarla con mucho cuidado porque es un "contrato" con otros programadores. Una vez que publicas tu clase y otros empiezan a usar tus métodos públicos, **es muy difícil cambiarla**. Si borras o cambias un método público después, romperás el código de todos los que lo estaban usando, obligando a reescribir muchas partes del sistema.

## 4. ¿Qué son las invariantes de clase y por qué la ocultación nos ayuda?

### Respuesta

Las **invariantes** son reglas lógicas que siempre deben ser verdad para que el objeto sea válido (por ejemplo: "un triángulo siempre debe tener tres lados" o "el saldo no puede ser menor que el límite de crédito").
La ocultación ayuda porque, al hacer los datos privados, obligas a pasar por un "filtro" (los métodos) antes de guardarlos. Ahí es donde verificas que se cumplan las reglas. Si los datos fueran públicos, cualquiera podría saltarse las reglas.

## 5. Ejemplo de clase Punto con ocultación. ¿Cuál es su interfaz pública?

### Respuesta

Imagina una clase llamada `Punto`. Tendría dos atributos privados para las coordenadas (llamémosles X e Y). Para usarla, tendría un **constructor público** que recibe dos números y los guarda en esos atributos privados. También tendría un **método público** llamado "calcular distancia al origen" que aplica la fórmula matemática de Pitágoras internamente y devuelve el resultado.

* **Interfaz pública:** Serían únicamente el constructor y el método de calcular distancia.
* **Significado:** "Público" significa que cualquiera puede usarlo; "privado" significa que solo la propia clase `Punto` puede ver o tocar esos datos.

## 6. En Java, ¿A quiénes se pueden aplicar los modificadores public o private?

### Respuesta

Se pueden aplicar a las **clases** (con restricciones), a los **atributos** (variables), a los **métodos** (funciones), a los **constructores** y a las clases internas.

## 7. ¿Existen más tipos de visibilidad aparte de pública y privada?

### Respuesta

Sí.

* En **Java** existe también la visibilidad "protegida" (para herencia y mismo paquete) y la visibilidad "por defecto" (o de paquete), que ocurre cuando no escribes nada y permite el acceso a las clases vecinas en la misma carpeta.
* En **otros lenguajes** como C# existe "internal", y en Python no existen restricciones reales, solo convenciones de nombres (usar guiones bajos para indicar "no toques esto").

## 8. ¿Los miembros privados están ocultos para otras clases o para otras instancias de la misma clase?

### Respuesta

Están ocultos para **otras clases**.
Sin embargo, un objeto sí puede ver los datos privados de **otro objeto de su misma clase**. Por ejemplo, si tienes un método para calcular la distancia entre dos puntos, el "Punto A" puede acceder directamente a las coordenadas privadas del "Punto B" porque ambos son de la familia `Punto`. La privacidad es a nivel de "tipo de dato", no de "instancia individual".

## 9. ¿Qué son los métodos "getter" y "setter"?

### Respuesta

Son métodos públicos que sirven de intermediarios. El **getter** sirve para leer un valor privado y el **setter** para modificarlo. Permiten controlar el acceso: por ejemplo, el "setter" puede comprobar si el valor es válido antes de guardarlo, algo que no podrías hacer si accedieras a la variable directamente.

## 10. ¿La ocultación mejora la seguridad contra "hackers"?

### Respuesta

**No.** No se refiere a seguridad informática (como contraseñas o encriptación). Se refiere a **seguridad contra errores de programación**. Evita que el programa falle porque alguien usó mal un objeto o dejó los datos en un estado incoherente.

## 11. Diferencia entre miembro de instancia y de clase. ¿Se pueden ocultar los de clase?

### Respuesta

* **Miembro de instancia:** Cada objeto tiene el suyo propio (ej. cada persona tiene su propio nombre).
* **Miembro de clase (estático):** Hay uno solo compartido por todos (ej. un contador de cuántas personas existen en total).
Sí, los miembros de clase también se pueden y deben ocultar (hacerlos privados) si son para uso interno.

## 12. ¿Tiene sentido que los constructores sean privados?

### Respuesta

**Sí.** Se usa cuando no quieres que nadie cree objetos de esa clase libremente. Es muy útil para clases que solo tienen herramientas (como `Math`) o para patrones de diseño específicos (como el Singleton, donde solo se permite que exista un único objeto de ese tipo).

## 13. ¿Cómo se indican los miembros de clase en Java? Ejemplo con la clase Punto.

### Respuesta

Se indican con la palabra clave **`static`**.
En el ejemplo del `Punto`, añadiríamos dos variables privadas y estáticas (compartidas) para guardar "la X más grande vista hasta ahora" y "la Y más grande". Cada vez que se cree un punto nuevo (en el constructor), comprobaríamos si sus coordenadas son mayores que las guardadas y, de ser así, actualizaríamos esas variables compartidas.

## 14. Método factoría para Punto con redondeo. ¿Usa static?

### Respuesta

Sería un método que recibe dos números con decimales. Dentro del método, se redondean esos números al entero más cercano usando matemáticas básicas. Finalmente, el método crea y devuelve un nuevo objeto `Punto` con esos valores redondeados.
**Sí, debe usar `static**`, porque es una herramienta para *fabricar* puntos nuevos, no una acción que realiza un punto que ya existe.

## 15. Cambiar implementación de Punto a un array sin tocar la interfaz pública.

### Respuesta

En lugar de tener dos variables sueltas (x, y), la clase tendría internamente una lista o arreglo de dos posiciones.

* El constructor recibiría `x` e `y`, pero guardaría `x` en la posición 0 y `y` en la posición 1 del arreglo.
* Los métodos de cálculo leerían del arreglo en vez de las variables.
Lo importante es que **la interfaz pública no cambia**: quien use la clase sigue enviando dos números y recibiendo resultados, sin enterarse de que por dentro ahora se usa un arreglo.

## 16. Si hay getter y setter públicos, ¿no es mejor hacer el atributo público?

### Respuesta

**No.** Aunque parezca lo mismo, usar métodos te da flexibilidad para el futuro. Si mañana quieres que al cambiar el valor se guarde un registro o se valide el dato, con el método "setter" puedes hacerlo sin romper el código de nadie. Con un atributo público, no tienes control.
La convención es: atributos siempre privados. Esto protege las invariantes de clase.

## 17. ¿Qué es una clase inmutable? ¿Ventajas?

### Respuesta

Una clase es **inmutable** si, una vez creado el objeto, sus datos nunca cambian. Un método modificador es aquel que cambia el estado; no siempre es un "setter", puede ser "avanzar" o "reiniciar".
**Ventajas:** Son más seguros, no dan sorpresas (efectos secundarios) y funcionan perfecto cuando se ejecutan varias tareas a la vez (multihilo) porque nadie puede modificarlos mientras otro los lee.

## 18. ¿Es recomendable poner setters siempre por defecto?

### Respuesta

**No.** Es una mala costumbre. Solo debes poner métodos para modificar datos si es estrictamente necesario que el objeto cambie. Si puedes diseñar tu clase para que sea inmutable (que no cambie), es mucho mejor y más robusto.

## 19. ¿La clase String es mutable o inmutable? ¿Qué pasa al concatenar?

### Respuesta

`String` es **inmutable**.
Cuando unes dos textos, no se modifica el original, sino que **se crea uno nuevo** en memoria con el resultado.
Si tienes que unir muchas cadenas (por ejemplo, en un bucle mil veces), no uses `String` directamente porque llenarás la memoria de basura. Debes usar clases especiales como `StringBuilder` que sí permiten modificación eficiente.

## 20. ¿Cómo se comparan objetos? ¿Identidad vs Contenido?

### Respuesta

* Por defecto, se compara la **identidad**: si son exactamente el mismo objeto en la memoria del ordenador.
* Para comparar por **contenido** (si tienen los mismos datos), se usa el método especial llamado `equals`.
* En las cadenas de texto (`String`), **nunca** uses el operador de igualdad normal (`==`), porque fallará si son dos objetos distintos con el mismo texto. Usa siempre el método `equals`.

## 21. ¿Qué son los "wrappers" (envoltorios)?

### Respuesta

Son clases que "disfrazan" un dato simple (como un número entero) para que parezca un objeto complejo. En Java esto se hace muchas veces de forma automática.
Sirven porque muchas estructuras de datos (como las listas inteligentes) solo aceptan objetos, no datos simples. No todos los lenguajes los necesitan; algunos lenguajes puros tratan todo como objetos desde el principio.

## 22. ¿Qué es un tipo enumerado? ¿Ventajas en encapsulación?

### Respuesta

Un enumerado es una lista fija de constantes con nombre (como los días de la semana o los palos de la baraja). En Java son clases reales y completas.
Su ventaja en encapsulación es que puedes guardar datos dentro de cada constante (por ejemplo, que el color "ROJO" sepa su código hexadecimal interno) y nadie puede crear colores nuevos ni modificar los existentes, garantizando un control total.

## 23. Crea un enumerado Mes con lógica interna.

### Respuesta

Definiríamos un tipo llamado `Mes` con las 12 constantes (ENERO, FEBRERO...).
Internamente, tendría dos atributos privados: `número` (del 1 al 12) y `días` (28, 30 o 31).
Usaríamos un **constructor privado** que se ejecuta automáticamente al iniciar el programa para asignar a cada mes sus días y su número. Así, podríamos preguntar `Mes.ENERO.getDias()` y nos respondería 31.

## 24. Añade lógica de estaciones al mes.

### Respuesta

Añadiríamos métodos que pregunten "¿es verano?" o "¿es invierno?". Estos métodos recibirían un dato extra: si estamos en el hemisferio norte o sur.
Dentro del método, usaríamos una lógica condicional: "Si es hemisferio norte y soy Diciembre, Enero o Febrero, entonces soy invierno. Si es hemisferio sur, invierto la respuesta". Así encapsulamos la complejidad de las estaciones dentro del propio mes.