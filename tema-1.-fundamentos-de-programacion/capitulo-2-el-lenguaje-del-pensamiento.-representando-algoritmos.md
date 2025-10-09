# Capítulo 2: El Lenguaje del Pensamiento. Representando Algoritmos

### 2.1. Introducción: Visualizando la Lógica

Antes de traducir un algoritmo a un lenguaje de programación, es fundamental tener una forma clara de representarlo y comunicarlo. Escribir la lógica en un formato intermedio nos ayuda a pensar, a detectar errores y a colaborar con otros. Las dos herramientas más extendidas para esta tarea son los diagramas de flujo y el pseudocódigo. Cada uno ofrece una perspectiva diferente: el primero es eminentemente gráfico y visual, mientras que el segundo se acerca más a la estructura del código real. Dominar ambos te dará una gran flexibilidad para diseñar soluciones.

***

### 2.2. Diagramas de Flujo: Una Visión Gráfica

Un diagrama de flujo es una representación gráfica de un algoritmo. Utiliza una serie de símbolos estandarizados conectados por flechas para mostrar la secuencia de operaciones y el flujo de control del programa. Es una herramienta excelente para visualizar la lógica general de un vistazo.

La simbología estándar incluye:

| Símbolo                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Nombre         | Función                                                                                                     |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- | ----------------------------------------------------------------------------------------------------------- |
| ![](data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHN0eWxlPSJiYWNrZ3JvdW5kOiB0cmFuc3BhcmVudDsgYmFja2dyb3VuZC1jb2xvcjogdHJhbnNwYXJlbnQ7IiB4bWxuczp4bGluaz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluayIgdmVyc2lvbj0iMS4xIiB3aWR0aD0iODJweCIgaGVpZ2h0PSI2MnB4IiB2aWV3Qm94PSItMC41IC0wLjUgODIgNjIiIGNvbnRlbnQ9IiZsdDtteEdyYXBoTW9kZWwmZ3Q7Jmx0O3Jvb3QmZ3Q7Jmx0O214Q2VsbCBpZD0mcXVvdDswJnF1b3Q7LyZndDsmbHQ7bXhDZWxsIGlkPSZxdW90OzEmcXVvdDsgcGFyZW50PSZxdW90OzAmcXVvdDsvJmd0OyZsdDtteENlbGwgaWQ9JnF1b3Q7MiZxdW90OyB2YWx1ZT0mcXVvdDsmcXVvdDsgc3R5bGU9JnF1b3Q7c3Ryb2tlV2lkdGg9MjtodG1sPTE7c2hhcGU9bXhncmFwaC5mbG93Y2hhcnQudGVybWluYXRvcjt3aGl0ZVNwYWNlPXdyYXA7JnF1b3Q7IHZlcnRleD0mcXVvdDsxJnF1b3Q7IHBhcmVudD0mcXVvdDsxJnF1b3Q7Jmd0OyZsdDtteEdlb21ldHJ5IHg9JnF1b3Q7MzUwJnF1b3Q7IHk9JnF1b3Q7MTgwJnF1b3Q7IHdpZHRoPSZxdW90OzgwJnF1b3Q7IGhlaWdodD0mcXVvdDs2MCZxdW90OyBhcz0mcXVvdDtnZW9tZXRyeSZxdW90Oy8mZ3Q7Jmx0Oy9teENlbGwmZ3Q7Jmx0Oy9yb290Jmd0OyZsdDsvbXhHcmFwaE1vZGVsJmd0OyI+PGRlZnMvPjxnPjxnIGRhdGEtY2VsbC1pZD0iV0l5V2xMazZHSlFzcWFVQktUTlYtMCI+PGcgZGF0YS1jZWxsLWlkPSJXSXlXbExrNkdKUXNxYVVCS1ROVi0xIj48ZyBkYXRhLWNlbGwtaWQ9ImgyWHdsUG14emRZMHZTNHdlSXBXLTgiLz48ZyBkYXRhLWNlbGwtaWQ9ImgyWHdsUG14emRZMHZTNHdlSXBXLTkiLz48ZyBkYXRhLWNlbGwtaWQ9ImgyWHdsUG14emRZMHZTNHdlSXBXLTEwIj48Zz48cGF0aCBkPSJNIDI1LjQ5IDEgTCA1Ni41MSAxIEMgNzAuMDQgMSA4MSAxNC40MyA4MSAzMSBDIDgxIDQ3LjU3IDcwLjA0IDYxIDU2LjUxIDYxIEwgMjUuNDkgNjEgQyAxMS45NiA2MSAxIDQ3LjU3IDEgMzEgQyAxIDE0LjQzIDExLjk2IDEgMjUuNDkgMSBaIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIiBzdHlsZT0iZmlsbDogbGlnaHQtZGFyaygjZmZmZmZmLCB2YXIoLS1nZS1kYXJrLWNvbG9yLCAjMTIxMjEyKSk7IHN0cm9rZTogbGlnaHQtZGFyayhyZ2IoMCwgMCwgMCksIHJnYigyNTUsIDI1NSwgMjU1KSk7Ii8+PC9nPjwvZz48L2c+PC9nPjwvZz48L3N2Zz4=) | Terminal       | <p>Representa el inicio o el final del algoritmo. </p><p>Ej: <code>INICIO</code>, <code>FIN</code>.</p>     |
| ![](<../.gitbook/assets/unknown (3).svg+xml>)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Línea de Flujo | Indica el orden de ejecución y conecta los demás símbolos.                                                  |
| ![](../.gitbook/assets/unknown.svg+xml)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Entrada/Salida | <p>Representa la lectura de datos o la presentación de resultados.</p><p>Ej: <code>Leer número</code>.</p>  |
| ![](<../.gitbook/assets/unknown (2).svg+xml>)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Proceso        | <p>Representa cualquier operación o cálculo.</p><p>Ej: <code>suma = a + b</code>.</p>                       |
| ![](<../.gitbook/assets/unknown (1).svg+xml>)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Decisión       | <p>Representa una bifurcación en el flujo basada en una condición.</p><p>Ej: <code>¿edad >= 18?</code>.</p> |

#### 🟢 Ventajas&#x20;

* **Claridad Visual**: Facilitan la comprensión rápida del flujo lógico.
* **Comunicación**: Son universalmente entendidos, incluso por personas sin perfil técnico.
* **Detección de Errores**: Los bucles infinitos o flujos incorrectos a menudo son evidentes visualmente.

#### 🔴 Limitaciones&#x20;

* **Complejidad:** Para algoritmos grandes, los diagramas se vuelven enormes y difíciles de manejar.
* **Modificación**: Un pequeño cambio en la lógica puede requerir redibujar una gran parte del diagrama.

#### Ejemplo: Diagrama de Flujo para Determinar si un Número es Par

<figure><img src="../.gitbook/assets/unknown (4).svg+xml" alt=""><figcaption></figcaption></figure>

Aunque son muy útiles para visualizar algoritmos sencillos, su rigidez y dificultad de modificación para problemas complejos nos llevan a buscar una alternativa más flexible: el pseudocódigo.

***

### 2.3. Pseudocódigo: Lógica en Lenguaje Humano

El pseudocódigo es un puente entre el lenguaje natural humano y el lenguaje de programación. Es una forma de describir un algoritmo utilizando una mezcla de palabras comunes (como "Si", "Mientras", "Leer") y una estructura similar a la del código, pero sin ceñirse a la sintaxis estricta de ningún lenguaje en particular.

Características Principales:

* **Lenguaje Natural Estructurado**: Usa palabras clave en español o inglés para denotar acciones y estructuras lógicas.
* **Flexibilidad**: No tiene reglas sintácticas estrictas. El objetivo es la claridad, no la compilación.
* **Facilidad de Traducción**: Su estructura lógica facilita enormemente la posterior escritura del código real en cualquier lenguaje.

#### **Sintaxis de Referencia para Pseudocódigo**

{% hint style="info" %}
**Nota**: No existe un estándar universal para el pseudocódigo. Lo importante no es seguir una sintaxis al pie de la letra, sino ser claro y consistente en la forma de expresar la lógica. A continuación, se muestra una posible sintaxis como referencia.
{% endhint %}

**Palabras Clave:**

* <mark style="color:red;">**`PROGRAM`**</mark>, <mark style="color:red;">**`BEGIN`**</mark>, <mark style="color:red;">**`END`**</mark>: Para delimitar el programa y bloques de código.
* <mark style="color:red;">**`IN`**</mark>`()`: Para representar la entrada de datos (leer del usuario).
* <mark style="color:red;">**`OUT`**</mark>`()`: Para representar la salida de datos (mostrar en pantalla).
* <mark style="color:red;">**`IF`**</mark>` ``...`` `<mark style="color:red;">**`THEN`**</mark>` ``...`` `<mark style="color:red;">**`ELSE`**</mark>: Para estructuras condicionales.
* <mark style="color:red;">**`WHILE`**</mark>` ``...`` `<mark style="color:red;">**`THEN`**</mark>: Para bucles (mientras se cumpla una condición).
* <mark style="color:red;">**`AND`**</mark>, <mark style="color:red;">**`OR`**</mark>, <mark style="color:red;">**`NOT`**</mark>: Operadores lógicos.

Utilizaremos pues la siguiente estructura a nivel de algoritmo:

```pascal
PROGRAM NombreAplicacion
BEGIN
    [instrucciones]
    
    WHILE condicion==True THEN
    BEGIN
        [instrucciones del bucle]
    END
    
    IF condicion THEN
    BEGIN
        [instrucciones si verdadero]
    END
    ELSE
    BEGIN
        [instrucciones si falso]
    END
    
END
```

**Ejemplo 1: Programa de Zapping de TV**

Este pseudocódigo describe la lógica de una persona que hace zapping hasta que encuentra un canal que le gusta o se cansa.

```pascal
PROGRAM TVZapping
BEGIN
    // Inicializamos las variables de estado
    Gustar_Canal = "no"
    Cansado = "no"

    // Empezamos la secuencia
    Iniciar_TV()
    Seleccionar_canal_aleatorio()

    // Bucle principal: seguimos haciendo zapping mientras no nos guste el canal Y no estemos cansados
    WHILE Gustar_Canal=="no" AND Cansado=="no" THEN
    BEGIN
        // Cambiamos de canal y preguntamos al usuario
        Seleccionar_canal_aleatorio()
        Gustar_Canal = IN("¿Te gusta este canal? (si/no)") == "si"
        Cansado = IN("¿Estás cansado? (si/no)") == "si"
    END

    // Decisión final basada en cómo salimos del bucle
    IF Gustar_Canal=="si" THEN
        // Si encontramos un canal que nos gusta, lo vemos
        Mirar_Programa()
    ELSE
        // Si nos cansamos, apagamos la tele y hacemos otra cosa
        Parar_TV()
        Leer_Libro()
    END
END
```

**Ejemplo 2: Validación de Email (con Corrección Crítica)**

A veces, el pseudocódigo nos ayuda a detectar errores lógicos antes de escribir código. Veamos un ejemplo.

❌ **Versión Original (con error lógico):**

```pascal
PROGRAM Ex8-MailCheck
BEGIN
    cont = 5
    mail = IN("Introduce una dirección de correo electrónico")

    // ERROR LÓGICO AQUÍ
    WHILE textoContiene(mail,"@")==True AND esDominioValido(mail)==True THEN
    BEGIN
        cont = cont - 1
        IF cont==-1 THEN
            OUT("No tienes más intentos, inténtalo de nuevo más tarde.")
        ELSE
            mail = IN("Correo electrónico incorrecto, vuelve a intentarlo.")
        END
    END

    IF cont>=0 THEN
        OUT("Correo electrónico correcto")
    END
END
```

<mark style="background-color:yellow;">**Análisis del Error:**</mark> La condición `WHILE` dice: "mientras el email contenga '@' Y el dominio sea correcto, ejecuta el bucle". Esto es lo contrario de lo que queremos. El bucle debería ejecutarse cuando el email es _incorrecto_ para pedir al usuario que lo reintente. El código original solo entraría en el bucle si el email ya es válido, lo cual no tiene sentido.

✅ **Versión Corregida:**

```pascal
PROGRAM Ex8-MailCheck
BEGIN
    cont = 5
    mail = IN("Introduce una dirección de correo electrónico")

    // CONDICIÓN CORREGIDA
    WHILE NOT(textoContiene(mail,"@")==True AND esDominioValido(mail)==True) THEN
    BEGIN
        cont = cont - 1
        IF cont==-1 THEN
            OUT("No tienes más intentos, inténtalo de nuevo más tarde.")
        ELSE
            mail = IN("Correo electrónico incorrecto, vuelve a intentarlo.")
        END
    END

    IF cont>=0 THEN
        OUT("Correo electrónico correcto")
    END
END
```

<mark style="background-color:yellow;">**Explicación de la Corrección:**</mark> La nueva condición `WHILE NOT (...)` invierte la lógica. Ahora el bucle se ejecuta si la condición de email válido _no_ se cumple, que es exactamente el comportamiento deseado para una validación.

#### **Del Pseudocódigo al Código Real**

El paso final es traducir el pseudocódigo a un lenguaje de programación. Observa la similitud:

<mark style="background-color:$info;">**Pseudocódigo:**</mark>

```pascal
PROGRAM CalculoPerimetro
BEGIN
    radio = IN("Introduce el radio del círculo")
    perimetro = 2 * 3.14159 * radio
    OUT("El perímetro es: " + perimetro)
END
```

<mark style="background-color:green;">**Código Python Equivalente:**</mark>

```python
# Definición de constantes
PI = 3.14159

# Entrada de datos (traducción de IN())
# Es necesario convertir el texto a un número flotante (float)
radio = float(input("Introduce el radio del círculo: "))

# Proceso
perimetro = 2 * PI * radio

# Salida de datos (traducción de OUT())
print(f"El perímetro es: {perimetro}")
```

El proceso de convertir pseudocódigo a código real implica:

1. **Adaptar Sintaxis**: Cambiar las palabras clave del pseudocódigo por la sintaxis del lenguaje objetivo
2. **Especificar Tipos de Datos**: Definir explícitamente los tipos de variables si el lenguaje lo requiere
3. **Manejar Entrada/Salida**: Reemplazar IN() y OUT() por las funciones específicas del lenguaje
4. **Optimizar**: Aplicar mejoras específicas del lenguaje de programación

***

### Resumen del Capítulo

En este capítulo, hemos explorado las dos herramientas principales para representar algoritmos: los diagramas de flujo y el pseudocódigo. Los diagramas de flujo ofrecen una visión gráfica excelente para algoritmos simples, mientras que el pseudocódigo proporciona una forma más flexible, detallada y cercana al código final, ideal para algoritmos complejos y para detectar errores lógicos en la fase de diseño.

#### **💡 Conceptos Clave**

* **Diagrama de Flujo**: Representación gráfica de un algoritmo. Ideal para visualización.
* **Pseudocódigo**: Descripción de un algoritmo en lenguaje natural estructurado. Ideal para el diseño lógico detallado.
* **Ventajas y Desventajas**: Cada método tiene sus fortalezas y es más adecuado para diferentes fases o tipos de problemas.

#### **🤔 Preguntas de Reflexión**

1. ¿En qué tipo de problema crees que un diagrama de flujo sería más útil que el pseudocódigo, y viceversa?
2. ¿Por qué el proceso de escribir pseudocódigo puede ayudar a un equipo de programadores a trabajar de forma más coordinada?
3. Toma el algoritmo de tu desayuno del capítulo anterior y represéntalo primero con un diagrama de flujo y luego con pseudocódigo.

***
