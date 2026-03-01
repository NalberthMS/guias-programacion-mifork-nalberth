<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Excepciones". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos, Encapsulación.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->

### TEMA 3. Excepciones

## 1. Empecemos un tema sobre control de errores en lenguajes de programación, con algo básico. En C, donde no existen las excepciones, pongamos un ejemplo de una raíz que toma número flotante positivo. Queremos controlar el error si la función recibe un número negativo. El usuario debe ser informado pero desde fuera de la función `raiz` ¿Cómo indicamos ese error?. Enumera dos opciones diferentes de diseñar, poniendo un ejemplo de código de cada una.

**Respuesta:**
Como hemos acordado no usar código real, te describo las dos estrategias clásicas en C:

1. **Devolver un valor especial "bandera":** Diseñamos la función para que, si recibe un número negativo, devuelva un valor numérico imposible para una raíz cuadrada (por ejemplo, un `-1.0` o un valor de tipo "No es un Número" si la librería matemática lo permite). Desde fuera de la función, evaluamos el resultado: si es `-1.0`, sabemos que hubo un error e informamos al usuario; si es positivo, mostramos el resultado.
2. **Usar parámetros por referencia para el error:** La función devuelve normalmente el resultado de la raíz, pero le pasamos como parámetro adicional un "puntero a una variable de error" (un número entero). Si la función detecta un negativo, cambia el valor de esa variable (por ejemplo, a `1` indicando error) y devuelve cero. Fuera de la función, primero comprobamos si la variable de error cambió a `1` para informar al usuario; si sigue en `0`, el cálculo fue un éxito.

---

## 2. Brevemente ¿Qué es una **"excepción"**? ¿Con qué objetivo las usa un programador cuando implementa funciones o cuando las llama?

**Respuesta:**
Una excepción es un evento anómalo que ocurre durante la ejecución de un programa y que rompe el flujo normal de las instrucciones. El objetivo principal al usarlas es separar la lógica "feliz" o normal del programa, de la lógica de gestión de errores. Esto permite que el código sea mucho más limpio de leer y que los errores no se pasen por alto accidentalmente.

---

## 3. Reescribe el mismo ejemplo de raiz, pero en Java, metiendo ese método en una clase `Calculadora` y llama a dicho método desde el método `main`, mostrando cómo se puede controlar desde fuera.

**Respuesta:**
Describiendo la lógica en Java:
Creamos una clase principal y una clase Calculadora. La Calculadora tiene un método para la raíz que evalúa si el número es negativo. Si lo es, en lugar de devolver un valor raro, **"lanza"** un objeto de tipo excepción con un mensaje que dice "No se pueden calcular raíces negativas".
En el método principal del programa, llamamos a esa función dentro de un bloque de **"intento"** (zona protegida). Inmediatamente después, ponemos un bloque de **"captura"** que está a la espera de esa excepción específica. Si el cálculo falla, el bloque de captura toma el control, recibe el objeto excepción, extrae su mensaje y se lo muestra al usuario de forma amigable.

---

## 4. ¿Qué es **"lanzar"** una excepción? ¿Qué es **"controlar"** o **"capturar"** una excepción? ¿Qué es que se **"propague"** una excepción? ¿Qué le va ocurriendo a las funciones en la pila de llamadas por donde se va propagando la excepción? ¿Las funciones que no la controlan se reanudan después de alguna forma? Explica con el mismo ejemplo anterior en Java de la raíz cuadrada.

**Respuesta:**

* **Lanzar:** Es el acto de señalar que algo ha fallado creando un objeto error y arrojándolo al sistema.
* **Capturar/Controlar:** Es interceptar ese objeto de error lanzado mediante una estructura de control para evitar que el programa se cuelgue y tomar medidas al respecto.
* **Propagar:** Si una función lanza una excepción y no la captura ella misma, el error "viaja" hacia atrás, a la función que la llamó, buscando quién la capture.
* **La pila de llamadas:** Las funciones por las que pasa la excepción se abortan de inmediato y se eliminan de la pila de llamadas. **No se reanudan nunca**.
* **Ejemplo:** Si el método raíz lanza la excepción, su ejecución se corta en seco. La excepción se propaga hacia el método principal. Como el método principal sí tiene una zona de captura, intercepta la excepción, el programa no "craseha", y la ejecución continúa pero desde el final del bloque de captura, no volviendo a la función de la raíz.

---

## 5. ¿Qué ventajas tiene frente a C, la **"propagación natural"** de las excepciones a través de la pila (*stack*) de llamadas?

**Respuesta:**
La gran ventaja es que no tienes que estar programando verificaciones manuales constantes (como los `if(error == 1)`) en cada paso intermedio. Si tienes una cadena de cinco funciones llamándose unas a otras, la función más profunda puede lanzar el error y este viajará automáticamente hasta la primera función que sepa cómo manejarlo, "saltándose" a todas las del medio. Además, evita los errores silenciosos: si nadie captura la excepción, el programa se detiene de forma segura alertando del fallo, mientras que en C, ignorar una comprobación de error suele llevar a comportamientos impredecibles más adelante.

---

## 6. En orientación a objetos, ¿las excepciones suelen ser objetos? ¿Qué ventajas tiene esto en términos de encapsulación? ¿Podemos entonces crear excepciones personalizadas?

**Respuesta:**
Sí, en la orientación a objetos, las excepciones son objetos de pleno derecho. La ventaja en encapsulación es que un único objeto puede agrupar muchísima información útil sobre el error (el mensaje detallado, el tipo de error, el rastro de por dónde ha pasado e incluso otros errores anidados), todo empaquetado y seguro. Y sí, esto nos permite crear nuestras propias clases de excepción personalizadas (como una `ExcepcionSaldoInsuficiente`) heredando de las clases base del sistema, lo que hace el código muy descriptivo.

---

## 7. En relación con las ventajas de la encapsulación, comparando el ejemplo en C con Java. ¿Qué **información esencial** lleva cualquier **objeto excepción** que es muy útil tener cuando se llega a un manejador?

**Respuesta:**
A diferencia de C, donde apenas tienes un número `-1`, un objeto excepción en Java viaja con:

1. Un mensaje de texto descriptivo del problema.
2. El tipo de error exacto (según la clase a la que pertenezca).
3. **La traza de la pila** (stack trace), que es la lista exacta de la línea de código, archivo y funciones por las que pasó desde que se originó hasta que se capturó.
4. A veces, otra excepción previa que originó a la actual (la "causa").

---

## 8. En Java, sobre el bloque **"try-catch"**, ¿se pueden tener más de un bloque `catch`? ¿cuántos bloques `catch` se ejecutan?

**Respuesta:**
Sí, se pueden colocar múltiples bloques de captura sucesivos, cada uno diseñado para atrapar un tipo distinto de error (uno para errores matemáticos, otro para errores de lectura de archivos, etc.). Sin embargo, **solo se ejecutará uno**: el primero que coincida con el tipo de excepción que se ha lanzado. Una vez que uno la captura, los demás se ignoran.

---

## 9. Si las excepciones producen rupturas en el código llamador, ¿cómo podemos garantizar que se ejecuta siempre finalmente un código necesario para cierre de ficheros, liberacion de recursos, antes de que continúe propagándose la excepción? Pon un ejemplo en Java con `finally`, tanto con `catch` como sin él.

**Respuesta:**
Se utiliza el bloque **"finalmente"** (`finally`), que se coloca al final de la estructura de intento/captura. El sistema garantiza que las instrucciones ahí dentro se ejecutarán siempre, sin importar cómo termine el bloque protegido.

* **Con captura:** Intentamos abrir un archivo y leerlo. Si falla, lo capturamos para mostrar un aviso. Al final, en el bloque "finalmente", damos la orden de cerrar el archivo. Esto se ejecuta tanto si se leyó bien como si saltó el aviso.
* **Sin captura:** Intentamos abrir un archivo y leerlo. Si falla, decidimos no capturarlo para que el error suba a otra función, pero aún así ponemos un bloque "finalmente" para cerrar el archivo. Antes de que el error abandone nuestra función para seguir subiendo, el sistema hace una pausa, ejecuta el cierre del archivo, y luego deja que el error continúe su camino.

---

## 10. En Java, el bloque `finally` puede ir sin `catch`? ¿Se ejecuta siempre tanto si ocurre como si no ocurre una excepción? ¿Y si hay un `return` en medio del `try`?

**Respuesta:**

* Sí, puede ir perfectamente acompañando a un bloque de intento sin necesidad de un bloque de captura.
* Sí, se ejecuta absolutamente siempre, haya o no haya saltado un error.
* Sí, incluso si ponemos una instrucción de "retorno" (`return`) para salir anticipadamente del bloque de intento, el lenguaje intercepta esa salida, ejecuta primero el bloque "finalmente", y solo después efectúa el retorno real de la función.


## 11. En Java, qué son las excepciones **"controladas"** y las **"no controladas"**? ¿Qué papel juega `RuntimeException`? Pon un ejemplo de excepciones típicas controladas y no controladas que incluso nosotros mismos podríamos usar. Haz dos listas con 3 o 4 ejemplos de situación donde se suele preferir una excepción controlada y donde se suele preferir una excepción no controlada.

**Respuesta:**

* **Controladas:** Son aquellas que el compilador te *obliga* a gestionar. Si llamas a una función que las lanza, o pones un bloque de captura, o declaras en tu función que dejas pasar el error.
* **No controladas:** Derivan de la clase `RuntimeException`. Representan errores de programación o lógicos y el compilador no te obliga a poner estructuras de control para ellas, ya que en teoría deberían evitarse escribiendo buen código.
* **Lista para Controladas (situaciones externas al programa):**
1. Intentar conectar a una base de datos caída.
2. Leer un archivo que ha sido borrado del disco duro.
3. Conectarse a una API en internet y no tener conexión a red.


* **Lista para No controladas (errores lógicos del programador):**
1. Intentar acceder a la posición 10 de una lista que solo tiene 5 elementos.
2. Intentar usar un objeto que en realidad está "nulo" (vacío).
3. Pasar una letra cuando una función exigía estrictamente que el texto fuera un número.


## 12. ¿Qué es y para qué se usa `throws`? ¿Por qué es alternativa a capturar una excepción controlada?

**Respuesta:**
Es una advertencia que se pone en la "firma" o cabecera de una función para declarar al mundo: "Atención, este método podría lanzar esta excepción". Se usa como alternativa a capturarla porque a veces la función actual no sabe qué hacer con el error (por ejemplo, una función genérica que lee archivos no sabe si ante un error debe mostrar un mensaje en rojo o detener la aplicación). Al declararla con esta palabra, delega la responsabilidad de capturarla a la función que la haya llamado.

---

## 13. Pon un ejemplo en Java de firma de método que incluya `throws`, de una función que abre un fichero pero que declara que no le interesa menejar la excepción de si el fichero no existe, sino que se propague hacia arriba. Eso sí, acuérdate del `finally`.

**Respuesta:**
Describo el diseño:
Creamos una función llamada "procesarDocumento" que, en su declaración principal, indica expresamente que "lanza la excepción de archivo no encontrado".
Dentro de la función abrimos un bloque de intento, abrimos el fichero y leemos datos. No ponemos ningún bloque de captura para el error del archivo. Directamente ponemos un bloque "finalmente" donde nos aseguramos de liberar la memoria de lectura. Si el fichero no existe, la excepción salta, ignora el bloque de captura (que no existe), ejecuta la limpieza del bloque final y sale de la función hacia arriba, tal como prometió en su cabecera.

---

## 14. ¿Podemos poner en `throws` excepciones no controladas, como `RuntimeException`? ¿Debería el método llamador entonces poner `try-catch` en ese caso? ¿Qué sentido tendría?

**Respuesta:**
Sí, es posible declararlas en la cabecera, pero el compilador las ignorará a efectos de obligatoriedad. El método que nos llame **no** estará obligado a poner un bloque de captura, ni el programa fallará al compilar si no lo hace. El único sentido de hacer esto es puramente documental: sirve para avisar a otros programadores que lean el código de que esos errores lógicos específicos podrían llegar a ocurrir, pero no aporta ningún rigor técnico.

---

## 15. ¿Cuándo se recomienda usar excepciones controladas, como `IOException`, y cuándo no controladas como `IllegalArgumentException`? ¿Existen en todos los lenguajes ambas opciones? En los que sólo existe una opción, ¿cuál es la más habitual?

**Respuesta:**

* **Controladas:** Se recomiendan cuando el error es recuperable y se deba a circunstancias fuera del control del programador (fallos de red, de disco, permisos). Obligan al desarrollador a pensar un plan B.
* **No controladas:** Se recomiendan para fallos en la lógica del código (uso incorrecto de una función, datos mal formateados). Lo ideal aquí es arreglar el código antes de compilarlo, no rodearlo de capturas.
* **Otros lenguajes:** No. La división entre controladas y no controladas es una particularidad casi exclusiva de Java.
* En la gran mayoría de lenguajes modernos (C#, Python, Ruby, JavaScript), **todas las excepciones son no controladas**. Se confía en la disciplina del programador para capturar lo necesario sin que el compilador lo exija estrictamente.

---

## 16. ¿Tiene sentido lanzar excepciones dentro del `catch`? ¿Se puede relanzar la misma excepción capturada? ¿Cuándo tendría sentido hacer esto último? Pon ejemplos de ambos casos.

**Respuesta:**
Sí, tiene sentido en varias situaciones.

* **Relanzar la misma excepción:** Se captura el error, se hace algo al respecto a nivel local, y luego se vuelve a lanzar la misma excepción hacia arriba. Es útil cuando quieres registrar el error en un archivo de bitácora (log) oculto para los técnicos, pero necesitas que el error siga subiendo para que la interfaz le muestre un mensaje visual al usuario.
* **Lanzar una nueva dentro de la captura:** Se captura el error y, en su lugar, se lanza uno distinto. Útil para traducir errores técnicos a errores de negocio (ver la siguiente pregunta).

---

## 17. ¿En qué consiste que una excepción sea la **"causa"** de otra excepción? Pon un ejemplo en Java, donde capturemos una excepción de bajo nivel y la encapsulemos en otra personalizada de alto nivel. Cuando una excepción sale por pantalla y tiene una causa, ¿se ve?

**Respuesta:**
Consiste en el **encapsulamiento de excepciones** (o *wrapping*). Significa que capturamos un error muy técnico y lanzamos un error más fácil de entender para nuestro programa, pero guardando el error original dentro del nuevo como si fuera una "matrioska", para no perder la pista técnica.

* **Ejemplo:** Estamos guardando un perfil de usuario. Intentamos conectar a la base de datos y salta una "Excepción de Conexión SQL" (bajo nivel). La capturamos, y dentro lanzamos una nueva "Excepción de Registro de Usuario" (alto nivel), pasándole la excepción SQL como su "causa". El resto del programa solo se preocupa de que falló el registro, sin importarle que internamente sea una base de datos.
* **Visibilidad:** Sí, cuando este error llega hasta arriba y se imprime en pantalla o en consola de errores, se muestra el error de alto nivel seguido de una frase técnica que dice "Causado por:..." y muestra la traza original del error de bajo nivel.
