# Capítulo 7: Funciones integradas e iterables

Python viene equipado con una "_caja de herramientas_" de **funciones integradas** (_<mark style="background-color:yellow;">**built-in**</mark>_) que están siempre disponibles, sin necesidad de importar ningún módulo. Estas funciones cubren un amplio espectro de tareas comunes, desde operaciones matemáticas hasta la manipulación de colecciones de datos. Este capítulo explora las más importantes y se adentra en conceptos más avanzados como los **generadores**, que permiten manejar grandes volúmenes de datos de manera increíblemente eficiente.

### 7.1. ¿Qué son las funciones integradas?

Las **funciones integradas** (built-in functions) son funciones predefinidas que forman parte del núcleo de Python. Están siempre disponibles sin necesidad de importar módulos y están optimizadas para máximo rendimiento.

Puedes ver la lista completa ejecutando:

```python
print(dir(__builtins__))
```

Todas estas funciones están perfectamente documentadas en: [docs.python.org/3/library/functions.html](https://docs.python.org/3/library/functions.html)

***

### 7.2. Funciones matemáticas

A continuación se resumen algunas de las funciones más comunes para cálculos matemáticos.

#### Funciones matemáticas

| Función          | Descripción                                 | Ejemplo                      |
| ---------------- | ------------------------------------------- | ---------------------------- |
| `abs(x)`         | Devuelve el valor absoluto de `x`.          | `abs(-5)` → `5`              |
| `divmod(a, b)`   | Devuelve el cociente y el resto.            | `divmod(17, 5)` → `(3, 2)`   |
| `max(iterable)`  | Devuelve el valor máximo de un iterable.    | `max([1, 5, 3])` → `5`       |
| `min(iterable)`  | Devuelve el valor mínimo de un iterable.    | `min([1, 5, 3])` → `1`       |
| `pow(base, exp)` | Calcula `base` elevado a la potencia `exp`. | `pow(2, 3)` → `8`            |
| `round(n, d)`    | Redondea el número `n` a `d` decimales.     | `round(3.14159, 2)` → `3.14` |
| `sum(iterable)`  | Suma todos los elementos de un iterable.    | `sum([1, 2, 3])` → `6`       |

#### Ejemplos prácticos

```python
import math

# Operaciones matemáticas básicas
negativo = -20
dividendo = 33
divisor = 4
numeros = [1, 2, 3, 4, 5]

print(f"Valor absoluto: {abs(negativo)}")              # 20
print(f"División completa: {divmod(dividendo, divisor)}") # (8, 1)
print(f"Máximo: {max(numeros)}")                       # 5
print(f"Mínimo: {min(numeros)}")                       # 1
print(f"Potencia: {pow(2, 3)}")                        # 8
print(f"Pi redondeado: {round(math.pi)}")              # 3
print(f"Pi con 2 decimales: {round(math.pi, 2)}")     # 3.14
print(f"Pi con 3 decimales: {round(math.pi, 3)}")     # 3.142
print(f"Suma: {sum(numeros)}")                         # 15
```

***

### 7.3. Funciones para codificación y representación

A continuación se resumen algunas de las funciones más comunes para la codificación y representación de datos y valores numéricos.

| Función     | Descripción                                                 | Ejemplo                |
| ----------- | ----------------------------------------------------------- | ---------------------- |
| `bin(x)`    | Convierte un entero a su representación binaria.            | `bin(10)` → `"0b1010"` |
| `chr(x)`    | Devuelve el carácter correspondiente al código Unicode `i`. | `chr(65)` → `"A"`      |
| `hex(x)`    | Convierte un entero a su representación hexadecimal.        | `hex(255)` → `"0xff"`  |
| `oct(x)`    | Convierte un entero a su representación octal.              | `hex(8)` → `"0o10"`    |
| `ord(char)` | Devuelve el código Unicode del carácter `c`.                | `ord("A")` → `65`      |

#### Ejemplos prácticos

```python
# Conversiones y representaciones
hola_especial = "Niño"
valor_numerico = 666

print(f"Binario: {bin(valor_numerico)}")        # Binario: 0b1010011010
print(f"Carácter: {chr(65)}")                   # Carácter: A
print(f"Hexadecimal: {hex(valor_numerico)}")    # Hexadecimal: 0x29a
print(f"Octal: {oct(valor_numerico)}")          # Octal: 0o1232
print(f"Código Unicode: {ord('A')}")            # Código Unicode: 65
```

***

### 7.4. Funciones para iterables

Estas funciones son esenciales para trabajar con colecciones de datos como listas, tuplas o diccionarios.

#### Funciones de verificación y evaluación

Permiten **comprobar o analizar propiedades generales** de un conjunto de elementos. Pueden verificar condiciones lógicas o medir las características del iterable, como su longitud.

| Función         | Descripción                                                   | Ejemplo                              |
| --------------- | ------------------------------------------------------------- | ------------------------------------ |
| `all(iterable)` | Devuelve `True` si todos los elementos son verdaderos.        | `all([True, True, False])` → `False` |
| `any(iterable)` | Devuelve `True` si al menos un elemento es verdadero.         | `any([False, True, False])` → `True` |
| `len(obj)`      | Devuelve el número de elementos (la longitud) de un iterable. | `len([1, 2, 3])` → `3`               |

**Ejemplos prácticos**

```python
# Ejemplos de verificación
print(f"all([True, True, True]): {all([True, True, True])}")     # True
print(f"all([True, False, True]): {all([True, False, True])}")   # False
print(f"all([]): {all([])}")                                     # True (vacío)

print(f"any([False, False, True]): {any([False, False, True])}")  # True
print(f"any([False, False, False]): {any([False, False, False])}") # False
print(f"any([]): {any([])}")                                      # False (vacío)

print(f"len([1, 2, 3, 4, 5]): {len([1, 2, 3, 4, 5])}")          # 5
print(f"len('hola'): {len('hola')}")                             # 4
```

#### Funciones de transformación y generación de iteradores

Permiten **procesar, ordenar, combinar o filtrar** datos de manera funcional, devolviendo **nuevos iteradores** que pueden recorrerse con bucles o convertirse en listas.

<table><thead><tr><th>Función</th><th width="147">Operación</th><th>Descripción</th><th>Ejemplo</th></tr></thead><tbody><tr><td><code>enumerate(iterable)</code></td><td><strong>Enumeración</strong></td><td>Devuelve un iterador de tuplas que contienen un contador (índice) y el valor de cada elemento. Muy útil para bucles <code>for</code>.</td><td><p><code>list(enumerate(</code></p><p><code>['a','b']))</code> → <code>[(0,'a'), (1,'b')]</code></p></td></tr><tr><td><code>zip(*iterables)</code></td><td><strong>Combinación</strong></td><td>Combina múltiples iterables en paralelo, creando un iterador de tuplas donde cada tupla contiene un elemento de cada iterable de entrada.</td><td><p><code>list(zip([1,2],</code> </p><p><code>['a','b']))</code> → <code>[(1,'a'), (2,'b')]</code></p></td></tr><tr><td><code>map(func,iterable)</code></td><td><strong>Transformación</strong></td><td>Aplica una función a cada elemento de un iterable y devuelve un iterador con los resultados.</td><td><p><code>list(map(str.upper,</code> </p><p><code>['a','b']))</code> → <code>['A','B']</code></p></td></tr><tr><td><code>filter(func,iterable)</code></td><td><strong>Filtrado</strong></td><td>Devuelve un iterador con los elementos del iterable para los cuales la función devuelve <code>True</code>.</td><td><p><code>list(filter(</code></p><p><code>lambda x: x>0,</code> </p><p><code>[-2,3,0]))</code> → <code>[3]</code></p></td></tr><tr><td><code>sorted(iterable)</code></td><td><strong>Ordenación</strong></td><td>Devuelve una nueva lista ordenada a partir de los elementos del iterable.</td><td><code>sorted([3,1,2])</code> → <code>[1,2,3]</code></td></tr><tr><td><code>reversed(iterable)</code></td><td><strong>Inversión</strong></td><td>Devuelve un iterador que recorre el iterable en orden inverso.</td><td><code>list(reversed([1,2,3]))</code> → <code>[3,2,1]</code></td></tr></tbody></table>

**Ejemplos `enumerate()`: Indexar elementos**

```python
# enumerate() proporciona índice y valor
for index, value in enumerate(["a", "b", "c"]):
    print(f"{index}: {value}")

# Empezar desde un índice específico
for index, value in enumerate(["a", "b", "c"], start=1):
    print(f"{index}: {value}")
```

**Ejemplos `zip()`: Combinar elementos**

```python
# Combinar listas
nombres = ["Ana", "Carlos", "María"]
edades = [25, 30, 28]
ciudades = ["Madrid", "Barcelona", "Valencia"]

# zip() crea tuplas combinando elementos de cada lista
personas = list(zip(nombres, edades, ciudades))
print("Personas:", personas)
# [('Ana', 25, 'Madrid'), ('Carlos', 30, 'Barcelona'), ('María', 28, 'Valencia')]

# Iterar directamente
for nombre, edad, ciudad in zip(nombres, edades, ciudades):
    print(f"{nombre} ({edad} años) vive en {ciudad}")
```

**Ejemplos `map()`: Transformar elementos**

```python
# map() con función lambda para elevar al cubo
numeros = [1, 2, 3, 4]
cubos = list(map(lambda x: x**3, numeros))
print(f"Cubos: {cubos}")  # [1, 8, 27, 64]

# Aplicar función a múltiples listas
def sumar(x, y):
    return x + y

lista1 = [1, 2, 3]
lista2 = [10, 20, 30]
sumas = list(map(sumar, lista1, lista2))
print(f"Sumas: {sumas}")  # [11, 22, 33]

# Convertir strings a enteros
strings_numeros = ["1", "2", "3", "4", "5"]
enteros = list(map(int, strings_numeros))
print(f"Enteros: {enteros}")  # [1, 2, 3, 4, 5]
```

**Ejemplos `filter()`: Filtrar elementos**

```python
# filter() con función lambda para mostrar pares
def es_par(x):
    return x % 2 == 0

numeros = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
pares = list(filter(es_par, numeros))
print(f"Números pares: {pares}")  # [2, 4, 6, 8, 10]

# Versión con lambda
pares_lambda = list(filter(lambda x: x % 2 == 0, numeros))
print(f"Con lambda: {pares_lambda}")  # [2, 4, 6, 8, 10]

# Filtrar strings no vacíos
palabras = ["python", "", "java", "", "javascript"]
palabras_validas = list(filter(None, palabras))  # None filtra valores falsy
print(f"Palabras válidas: {palabras_validas}")
```

**Ejemplos `sorted()` y `reversed()`: Reordenar elementos**

```python
# sorted() devuelve una nueva lista ordenada
numeros = [3, 1, 4, 1, 5, 9, 2, 6]
ordenados = sorted(numeros)
print(f"Ordenados: {ordenados}")  # [1, 1, 2, 3, 4, 5, 6, 9]
​
# Ordenar por criterio personalizado
palabras = ["python", "java", "c", "javascript"]
por_longitud = sorted(palabras, key=len)
print(f"Por longitud: {por_longitud}")  # ['c', 'java', 'python', 'javascript']
​
# reversed() devuelve un iterador inverso
numeros = [1, 2, 3, 4]
for numero in reversed(numeros):
    print(numero, end=" ")  # 4 3 2 1
print()
```

***

### 7.5. Funciones de conversión de tipos

Estas funciones permiten transformar datos de un tipo a otro, una tarea fundamental en programación.

| Función           | Descripción                                                  | Ejemplo                                           |
| ----------------- | ------------------------------------------------------------ | ------------------------------------------------- |
| `bool(x)`         | Convierte `x` a un booleano.                                 | `bool(0)` → `False`                               |
| `int(x)`          | Convierte `x` a un entero.                                   | `int("42")` → `42`                                |
| `float(x)`        | Convierte `x` a un número de punto flotante.                 | `float("3.14")` → `3.14`                          |
| `str(x)`          | Convierte `x` a una cadena de texto.                         | `str(42)` → `"42"`                                |
| `list(iterable)`  | Convierte un iterable a una lista.                           | `list("abc")` → `['a', 'b', 'c']`                 |
| `tuple(iterable)` | Convierte un iterable a una tupla.                           | `tuple([1, 2, 3])` → `(1, 2, 3)`                  |
| `set(iterable)`   | Convierte un iterable a un conjunto (eliminando duplicados). | `set([1, 1, 2, 3])` → `{1, 2, 3}`                 |
| `dict()`          | Crea un diccionario.                                         | `dict([('a', 1), ('b', 2)])` → `{'a': 1, 'b': 2}` |

#### Ejemplos prácticos

```python
# Conversiones de tipo
print(f"bool(3): {bool(3)}")                    # True
print(f"bool(0): {bool(0)}")                    # False
print(f"int('33'): {int('33')}")               # 33
print(f"int(3.14): {int(3.14)}")               # 3
print(f"float('3.14'): {float('3.14')}")       # 3.14
print(f"str(3.14159): {str(3.14159)}")         # "3.14159"

# Crear colecciones
print(f"list('hello'): {list('hello')}")                    # ['h', 'e', 'l', 'l', 'o']
print(f"list(range(5, 3, -1)): {list(range(5, 3, -1))}")  # [5, 4]
print(f"set([1, 2, 3, 3, 2]): {set([1, 2, 3, 3, 2])}")    # {1, 2, 3}
print(f"tuple([1, 2, 3, 4, 5]): {tuple([1, 2, 3, 4, 5])}")# (1, 2, 3, 4, 5)

# Diccionario desde zip
claves = ['a', 'b', 'c']
valores = [1, 2, 3]
diccionario = dict(zip(claves, valores))
print(f"dict(zip(...)): {diccionario}")  # {'a': 1, 'b': 2, 'c': 3}
```

***

### 7.6. Generadores: Iteradores simplificados

Los **generadores** son una forma elegante y eficiente de crear iteradores. En lugar de construir una lista completa en memoria, un generador produce valores "bajo demanda" utilizando la palabra clave **`yield`**. Cada vez que se solicita un valor, la función generadora se ejecuta hasta el `yield`, entrega el valor y pausa su estado hasta la siguiente solicitud.

#### Generador básico

```python
def numeros_hasta(limite):
    """Generador que produce números de 0 hasta limite."""
    numero = 0
    while numero <= limite:
        yield numero
        numero += 1

# Usar el generador
gen = numeros_hasta(5)
print(next(gen))  # 0
print(next(gen))  # 1

# Usar en bucle
for num in numeros_hasta(3):
    print(num, end=" ")  # 0 1 2 3
print()
```

Los generadores son extremadamente eficientes en el uso de memoria, especialmente para secuencias muy largas. La sintaxis de las comprensiones de listas también se puede adaptar para crear expresiones generadoras, que son aún más concisas:

```python
import sys

# Comprensión de lista (almacena todo en memoria)
lista_cuadrados = [i**2 for i in range(10000)]

# Expresión generadora (no almacena nada, genera bajo demanda)
gen_cuadrados = (i**2 for i in range(10000))

print(f"Tamaño de la lista en memoria: {sys.getsizeof(lista_cuadrados)} bytes")
print(f"Tamaño del generador en memoria: {sys.getsizeof(gen_cuadrados)} bytes")
```

El resultado muestra una diferencia drástica en el uso de memoria, demostrando el poder de los generadores.

***

### Resumen del Capítulo

Las funciones integradas de Python y los conceptos de iteradores/generadores forman parte del arsenal fundamental de todo programador Python. Estas herramientas no solo simplifican el código, sino que también optimizan el rendimiento y el uso de memoria, especialmente cuando se trabaja con grandes volúmenes de datos.

#### 💡 Conceptos Clave:

* **Funciones matemáticas**: `abs`, `max`, `min`, `sum`, `pow`, etc.
* **Funciones para iterables**: `len`, `map`, `filter`, `zip`, `enumerate`, `sorted`, etc.
* **Conversión de tipos**: `int`, `float`, `str`, `list`, `tuple`, `set`, `dict`
* **Generadores**: Funciones que usan `yield` para generar valores bajo demanda
* **Eficiencia de memoria**: Generadores vs listas para grandes volúmenes de datos

#### 🤔 Preguntas de Reflexión:

1. ¿En qué situaciones son más útiles los generadores que las listas?
2. ¿Cómo pueden las funciones `map` y `filter` mejorar la legibilidad del código?
3. ¿Qué ventajas aporta `enumerate()` frente a usar `range(len())`?

#### 🔧 Ejercicio Práctico:

Crea un programa que:

1. Use funciones matemáticas para calcular estadísticas de un dataset
2. Use `map`, `filter` y `zip` para transformar y combinar datos
3. Compare rendimiento entre listas y generadores con datos grandes

Si bien estas herramientas integradas son potentes, nos falta aún por conocer cuáles son los métodos nativos que nos ofrecen las estructuras básicas de datos: **cadenas, listas, diccionarios y conjuntos**. En el siguiente capítulo se aborda cómo estos recursos permiten transformar, ordenar, buscar, filtrar y organizar la información de manera robusta, adaptable y "pythónica".

***
