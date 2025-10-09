# Capítulo 6: Interactuando con el Mundo. E/S y Operadores Lógicos

### 6.1. Introducción: Diálogo y Decisión

Un programa aislado del mundo exterior es de poca utilidad. Para ser verdaderamente funcionales, los programas necesitan comunicarse, es decir, recibir datos (Entrada) y mostrar resultados (Salida). Además, deben ser capaces de evaluar la información que reciben para tomar decisiones. Este capítulo se centra en las herramientas que permiten este diálogo y en los operadores que forman la base de la lógica de decisión.

***

### 6.2. El Operador de Asignación **`=`**

Ya hemos usado el operador `=` para dar valor a las variables, pero es crucial entender su funcionamiento exacto.

En programación, el símbolo `=` no significa "es igual a", como en matemáticas. Significa "asigna el valor de la derecha a la variable de la izquierda". Es una acción, una orden.

El proceso siempre es el mismo:

1. Se evalúa completamente la expresión que está a la derecha del `=`.
2. El resultado de esa evaluación se almacena en la variable de la izquierda.

Este concepto es clave para entender instrucciones como la siguiente:

```python
puntuacion = 100
# Lee esto como: "la nueva 'puntuacion' será el resultado de la 'puntuacion' actual más 10"
puntuacion = puntuacion + 10
print(puntuacion) # Salida: 110
```

#### **6.2.1 Operadores de Asignación Compuesta**

Para hacer el código más conciso, Python ofrece operadores que combinan una operación aritmética y una asignación. Ya los vimos en el capítulo anterior, pero recordamos su utilidad: `x += 5` es un atajo para `x = x + 5`.

#### **6.2.2 Asignación Múltiple**

Python permite asignar valores a varias variables en una sola línea, lo que resulta muy útil y elegante.

```python
# Asignar a varias variables a la vez
x, y, z = 10, 20, "hola"

# La forma "pythónica" de intercambiar los valores de dos variables
a = 50
b = 100
a, b = b, a # Ahora 'a' vale 100 y 'b' vale 50
```

***

### 6.3 Operadores de Comparación y Lógicos

Para que un programa pueda tomar decisiones, necesita comparar valores. Los operadores de comparación evalúan una relación entre dos valores y siempre devuelven un resultado booleano (`True` o `False`).

| Operador | Significado              |
| -------- | ------------------------ |
| `==`     | Igual a                  |
| `!=`     | No igual a (distinto de) |
| `<`      | Menor que                |
| `>`      | Mayor que                |
| `<=`     | Menor o igual que        |
| `>=`     | Mayor o igual que        |

{% hint style="danger" %}
&#x20;**Error Común:** `=` vs `==`&#x20;

Uno de los errores más frecuentes al empezar es confundir el operador de asignación `=` con el de comparación `==`. Recuerda que:

* `=`: Asigna un valor.
* `==`: Compara si dos valores son iguales.
{% endhint %}

Python permite comparaciones encadenadas de una forma muy legible:

```python
edad = 25
# En lugar de escribir: if edad >= 18 and edad <= 65:
# Podemos escribir:
if 18 <= edad <= 65:
    print("Estás en edad laboral.")
```

Los operadores lógicos (`and`, `or`, `not`) nos permiten combinar varias condiciones booleanas:

* `and`: Devuelve `True` solo si ambas condiciones son verdaderas.
* `or`: Devuelve `True` si al menos una de las condiciones es verdadera.
* `not`: Invierte el valor booleano (de `True` a `False` y viceversa).

```python
temperatura = 22
es_fin_de_semana = True

# ¿Hace buena temperatura Y es fin de semana?
if temperatura > 18 and es_fin_de_semana:
    print("¡Perfecto para ir a la playa!")

# ¿Tienes el día libre O estás de vacaciones?
dia_libre = False
estas_de_vacaciones = True
if dia_libre or estas_de_vacaciones:
    print("Tiempo para relajarse.")
```

***

### 6.4. Entrada de Datos: La Función `input()`

La función `input()` es la principal herramienta para que un programa reciba información del usuario a través del teclado. Su funcionamiento es simple pero tiene un detalle crucial:

`input()` siempre devuelve una cadena de texto (`str`).

Esto significa que si le pides al usuario un número, tendrás que convertirlo explícitamente a `int` o `float` antes de poder hacer operaciones matemáticas con él.

```python
# input() devuelve un string, aunque el usuario escriba un número
edad_str = input("Introduce tu edad: ") 

# Si intentamos sumar 1, dará un error
# proximo_año = edad_str + 1  # TypeError

# Debemos convertirlo primero
edad_num = int(edad_str)
proximo_año = edad_num + 1

print(f"El año que viene tendrás {proximo_año} años.")
```

{% hint style="success" %}
**Buenas Prácticas:** Nunca confíes en que el usuario introducirá los datos correctamente. ¿Qué pasa si en el ejemplo anterior el usuario escribe "veinte" en lugar de "20"? La función `int()` fallará y el programa se detendrá con un `ValueError`. Una práctica robusta es anticipar estos errores con un bloque `try-except`.
{% endhint %}

***

### 6.5. Salida de Datos: La Función `print()`

#### 6.5.1 Uso básico de `print()`

La función `print()` es la forma estándar de mostrar información en la pantalla. Aunque su uso básico es sencillo, tiene opciones para personalizar la salida.

```python
print("Hola", "mundo") # Salida: Hola mundo

# El parámetro 'sep' cambia el separador entre elementos
print("Hola", "mundo", sep="---") # Salida: Hola---mundo

# El parámetro 'end' cambia lo que se imprime al final (por defecto es un salto de línea)
print("Primera parte", end=" | ")
print("Segunda parte") # Salida: Primera parte | Segunda parte
```

#### **6.5.2 `f-strings`: El Estándar Moderno para Formatear**

Introducidas en Python 3.6, las **f-strings** (cadenas formateadas) son la forma más moderna, legible y eficiente de incluir variables y expresiones dentro de una cadena de texto. Se definen poniendo una `f` antes de la comilla de apertura.

```python
nombre = "Marie Curie"
premios_nobel = 2
precio = 49.95

# Sustitución simple de variables
print(f"La científica {nombre} ganó {premios_nobel} premios Nobel.")

# Formateo de números de punto flotante a 2 decimales
print(f"El precio del libro es: {precio:.2f} €")

# Alineación de texto dentro de un espacio de 15 caracteres
print(f"|{nombre:^15}|") # Centrado: |  Marie Curie  |
```

***

### Resumen del Capítulo

Hemos cubierto las herramientas esenciales para la interacción de un programa: el operador de asignación `=`, que da valor a las variables, y los operadores de comparación y lógicos, que permiten tomar decisiones. Hemos aprendido a recibir datos con `input()` (recordando siempre la conversión de tipos) y a mostrar información de forma profesional con `print()` y el poder de los f-strings.

#### **💡 Conceptos Clave**

* **Asignación vs. Comparación:** `x = 10` (asigna) vs `x == 10` (compara).
* **Operadores Lógicos:** `and`, `or`, `not` para combinar condiciones.
* **`input()`:** Lee datos del usuario, siempre devuelve un `str`.
* **`print()`:** Muestra datos en pantalla.
* **`f-strings`:** El método preferido para formatear cadenas de texto en Python.
* **Conversión de Tipos:** Funciones como `int()`, `float()`, `str()` para cambiar el tipo de un dato.

#### **🤔 Preguntas de Reflexión**

1. ¿Por qué es crucial validar siempre los datos que provienen del usuario? ¿Qué tipo de problemas puede causar no hacerlo en una aplicación real?
2. Explica con tus palabras la diferencia fundamental de comportamiento entre `and` y `or` al evaluar dos condiciones.
3. ¿Qué ventajas de legibilidad ofrecen las f-strings sobre métodos más antiguos como la concatenación con `+`?

***
