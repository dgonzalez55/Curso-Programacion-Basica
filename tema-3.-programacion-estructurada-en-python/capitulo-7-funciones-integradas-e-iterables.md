# Capítulo 7: Funciones integradas e iterables

Python incluye de manera nativa un conjunto extenso de **funciones integradas** (built-in functions) que podemos utilizar sin necesidad de importar ningún módulo. Estas funciones cubren operaciones matemáticas, manipulación de tipos, trabajo con iterables y mucho más. Además, Python proporciona conceptos avanzados como **iteradores** y **generadores** que permiten trabajar de manera eficiente con secuencias de datos.

En este capítulo exploraremos las funciones más útiles del arsenal nativo de Python y aprenderemos a crear nuestros propios iteradores y generadores para optimizar el manejo de datos y memoria.

### 7.1. ¿Qué son las funciones integradas?

Las **funciones integradas** (built-in functions) son funciones predefinidas que forman parte del núcleo de Python. Están siempre disponibles sin necesidad de importar módulos y están optimizadas para máximo rendimiento.

Puedes ver la lista completa ejecutando:

```python
print(dir(__builtins__))
```

Todas estas funciones están perfectamente documentadas en: [docs.python.org/3/library/functions.html](https://docs.python.org/3/library/functions.html)

### 7.2. Funciones matemáticas

#### Funciones básicas

| Función          | Descripción       | Ejemplo                      |
| ---------------- | ----------------- | ---------------------------- |
| `abs(x)`         | Valor absoluto    | `abs(-5)` → `5`              |
| `divmod(a, b)`   | División y módulo | `divmod(17, 5)` → `(3, 2)`   |
| `max(iterable)`  | Valor máximo      | `max([1, 5, 3])` → `5`       |
| `min(iterable)`  | Valor mínimo      | `min([1, 5, 3])` → `1`       |
| `pow(base, exp)` | Potencia          | `pow(2, 3)` → `8`            |
| `round(x, n)`    | Redondeo          | `round(3.14159, 2)` → `3.14` |
| `sum(iterable)`  | Suma de elementos | `sum([1, 2, 3])` → `6`       |

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

#### Aplicación práctica: Calculadora estadística

```python
def estadisticas_basicas(datos):
    """Calcula estadísticas básicas de una lista de números."""
    if not datos:
        return None
    
    n = len(datos)
    suma_total = sum(datos)
    media = suma_total / n
    
    # Desviación estándar simple
    suma_cuadrados = sum((x - media) ** 2 for x in datos)
    desviacion = (suma_cuadrados / n) ** 0.5
    
    return {
        'cantidad': n,
        'suma': suma_total,
        'media': media,
        'mediana': sorted(datos)[n // 2],
        'minimo': min(datos),
        'maximo': max(datos),
        'rango': max(datos) - min(datos),
        'desviacion_std': desviacion
    }

# Ejemplo de uso
notas = [7.5, 8.2, 6.8, 9.1, 7.3, 8.7, 6.5, 9.5, 7.8, 8.4]
stats = estadisticas_basicas(notas)

print("📊 ESTADÍSTICAS DE NOTAS")
print("=" * 30)
for clave, valor in stats.items():
    print(f"{clave.replace('_', ' ').title():<15}: {valor:.2f}")
```

### 7.3. Funciones de codificación y representación

| Función      | Descripción                       | Ejemplo                          |
| ------------ | --------------------------------- | -------------------------------- |
| `ascii(obj)` | Representación ASCII              | `ascii("Niño")` → `"'Ni\\xf1o'"` |
| `bin(x)`     | Representación binaria            | `bin(10)` → `"0b1010"`           |
| `chr(x)`     | Carácter desde código Unicode     | `chr(65)` → `"A"`                |
| `hex(x)`     | Representación hexadecimal        | `hex(255)` → `"0xff"`            |
| `oct(x)`     | Representación octal              | `hex(8)` → `"0o10"`              |
| `ord(char)`  | Código Unicode de carácter        | `ord("A")` → `65`                |
| `repr(obj)`  | Representación oficial del objeto | `repr("texto")` → `"'texto'"`    |

#### Ejemplos prácticos

```python
# Conversiones y representaciones
hola_especial = "Niño"
valor_numerico = 666

print(f"ASCII: {ascii(hola_especial)}")         # ASCII: 'Ni\xf1o'
print(f"Binario: {bin(valor_numerico)}")        # Binario: 0b1010011010
print(f"Carácter: {chr(65)}")                   # Carácter: A
print(f"Hexadecimal: {hex(valor_numerico)}")    # Hexadecimal: 0x29a
print(f"Octal: {oct(valor_numerico)}")          # Octal: 0o1232
print(f"Código Unicode: {ord('A')}")            # Código Unicode: 65
print(f"Representación: {repr(hola_especial)}") # Representación: 'Niño'
```

#### Aplicación práctica: Conversor de bases numéricas

```python
def conversor_bases(numero, base_origen=10):
    """Convierte números entre diferentes bases."""
    try:
        # Convertir entrada a entero decimal
        if base_origen == 2:
            decimal = int(numero, 2)
        elif base_origen == 8:
            decimal = int(numero, 8)
        elif base_origen == 16:
            decimal = int(numero, 16)
        else:
            decimal = int(numero)
        
        # Mostrar en todas las bases
        print(f"🔢 CONVERSIÓN DE BASES")
        print(f"Entrada: {numero} (base {base_origen})")
        print("-" * 25)
        print(f"Decimal:      {decimal}")
        print(f"Binario:      {bin(decimal)}")
        print(f"Octal:        {oct(decimal)}")
        print(f"Hexadecimal:  {hex(decimal)}")
        
        return decimal
        
    except ValueError as e:
        print(f"❌ Error: {e}")
        return None

# Ejemplos
# conversor_bases("1010", 2)    # Binario a todas las bases
# conversor_bases("FF", 16)     # Hexadecimal a todas las bases
# conversor_bases("123")        # Decimal a todas las bases
```

### 7.4. Funciones para iterables (I)

#### Funciones de verificación

| Función         | Descripción                    | Ejemplo                              |
| --------------- | ------------------------------ | ------------------------------------ |
| `all(iterable)` | ¿Todos los elementos son True? | `all([True, True, False])` → `False` |
| `any(iterable)` | ¿Algún elemento es True?       | `any([False, True, False])` → `True` |
| `len(obj)`      | Longitud del objeto            | `len([1, 2, 3])` → `3`               |

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

#### enumerate(): Indexar elementos

```python
# enumerate() proporciona índice y valor
for index, value in enumerate(["a", "b", "c"]):
    print(f"{index}: {value}")

# Empezar desde un índice específico
for index, value in enumerate(["a", "b", "c"], start=1):
    print(f"{index}: {value}")
```

#### filter(): Filtrar elementos

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

### 7.5. Funciones para iterables (II)

#### map(): Transformar elementos

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

#### zip(): Combinar iterables

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

#### sorted() y reversed()

```python
# sorted() devuelve una nueva lista ordenada
numeros = [3, 1, 4, 1, 5, 9, 2, 6]
ordenados = sorted(numeros)
print(f"Ordenados: {ordenados}")  # [1, 1, 2, 3, 4, 5, 6, 9]

# Ordenar por criterio personalizado
palabras = ["python", "java", "c", "javascript"]
por_longitud = sorted(palabras, key=len)
print(f"Por longitud: {por_longitud}")  # ['c', 'java', 'python', 'javascript']

# reversed() devuelve un iterador inverso
numeros = [1, 2, 3, 4]
for numero in reversed(numeros):
    print(numero, end=" ")  # 4 3 2 1
print()
```

#### next() y iter()

```python
# Crear iterador manual
lista = [1, 2, 3]
iterador = iter(lista)

print(next(iterador))  # 1
print(next(iterador))  # 2
print(next(iterador))  # 3

# next(iterador)  # StopIteration error

# Con valor por defecto
iterador2 = iter([1, 2])
print(next(iterador2))              # 1
print(next(iterador2))              # 2
print(next(iterador2, "Fin"))       # "Fin" (no error)
```

### 7.6. Funciones de conversión de tipos

| Función    | Descripción             | Ejemplo                                           |
| ---------- | ----------------------- | ------------------------------------------------- |
| `bool(x)`  | Convierte a booleano    | `bool(0)` → `False`                               |
| `int(x)`   | Convierte a entero      | `int("42")` → `42`                                |
| `float(x)` | Convierte a decimal     | `float("3.14")` → `3.14`                          |
| `str(x)`   | Convierte a string      | `str(42)` → `"42"`                                |
| `list(x)`  | Convierte a lista       | `list("abc")` → `['a', 'b', 'c']`                 |
| `tuple(x)` | Convierte a tupla       | `tuple([1, 2, 3])` → `(1, 2, 3)`                  |
| `set(x)`   | Convierte a conjunto    | `set([1, 1, 2, 3])` → `{1, 2, 3}`                 |
| `dict(x)`  | Convierte a diccionario | `dict([('a', 1), ('b', 2)])` → `{'a': 1, 'b': 2}` |

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

### 7.7. Iteradores personalizados

Un **iterador** es un objeto que implementa el protocolo de iteración: `__iter__()` y `__next__()`. Permite recorrer elementos de manera eficiente en memoria.

#### Creando un iterador personalizado

```python
class CuentaRegresiva:
    """Iterador que cuenta regresivamente hasta 0."""
    
    def __init__(self, inicio):
        self.numero_actual = inicio
        self.numero_final = 0
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self.numero_actual >= self.numero_final:
            numero_actual = self.numero_actual
            self.numero_actual -= 1
            return numero_actual
        else:
            raise StopIteration

# Usar el iterador
cuenta = CuentaRegresiva(5)
print(next(cuenta))  # 5
print(next(cuenta))  # 4

# Usar en bucle for
for num in CuentaRegresiva(3):
    print(num, end=" ")  # 3 2 1 0
print()
```

#### Iterador para números pares

```python
class NumerosPares:
    """Iterador que genera números pares hasta un límite."""
    
    def __init__(self, limite):
        self.limite = limite
        self.numero = 0
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self.numero <= self.limite:
            resultado = self.numero
            self.numero += 2
            return resultado
        else:
            raise StopIteration

# Usar el iterador
for par in NumerosPares(10):
    print(par, end=" ")  # 0 2 4 6 8 10
print()
```

### 7.8. Generadores: Iteradores simplificados

Los **generadores** son una forma más sencilla de crear iteradores usando la palabra clave `yield`. Son más eficientes en memoria porque generan valores bajo demanda.

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

#### Generador de números primos

```python
def numeros_primos(limite):
    """Generador de números primos hasta un límite."""
    def es_primo(n):
        if n < 2:
            return False
        for i in range(2, int(n ** 0.5) + 1):
            if n % i == 0:
                return False
        return True
    
    for numero in range(2, limite + 1):
        if es_primo(numero):
            yield numero

# Usar el generador
print("Números primos hasta 20:")
for primo in numeros_primos(20):
    print(primo, end=" ")  # 2 3 5 7 11 13 17 19
print()
```

#### Generador de Fibonacci

```python
def fibonacci(limite):
    """Generador de la secuencia Fibonacci hasta un límite."""
    a, b = 0, 1
    while a <= limite:
        yield a
        a, b = b, a + b

# Usar el generador
print("Fibonacci hasta 100:")
for fib in fibonacci(100):
    print(fib, end=" ")  # 0 1 1 2 3 5 8 13 21 34 55 89
print()

# Lista de los primeros 10 números Fibonacci
primeros_10 = list(fibonacci(10**10))[:10]  # Límite alto, pero tomamos solo 10
print(f"Primeros 10 Fibonacci: {primeros_10}")
```

#### Ventajas de los generadores

```python
import sys

# Comparar memoria: lista vs generador
def crear_lista(n):
    return [i**2 for i in range(n)]

def crear_generador(n):
    return (i**2 for i in range(n))

# Medición de memoria
lista_grande = crear_lista(10000)
generador_grande = crear_generador(10000)

print(f"Memoria lista: {sys.getsizeof(lista_grande)} bytes")
print(f"Memoria generador: {sys.getsizeof(generador_grande)} bytes")

# El generador usa mucha menos memoria porque no almacena todos los valores
```

### 7.9. Casos prácticos avanzados

#### Procesador de archivos con generadores

```python
def leer_lineas_grandes(nombre_archivo):
    """Generador que lee un archivo línea por línea (eficiente para archivos grandes)."""
    try:
        with open(nombre_archivo, 'r', encoding='utf-8') as archivo:
            for numero_linea, linea in enumerate(archivo, 1):
                yield numero_linea, linea.rstrip('\n')
    except FileNotFoundError:
        print(f"❌ Archivo no encontrado: {nombre_archivo}")
        return

def analizar_archivo(nombre_archivo):
    """Analiza un archivo línea por línea usando un generador."""
    estadisticas = {
        'lineas': 0,
        'caracteres': 0,
        'palabras': 0,
        'lineas_vacias': 0
    }
    
    for numero, linea in leer_lineas_grandes(nombre_archivo):
        estadisticas['lineas'] += 1
        estadisticas['caracteres'] += len(linea)
        
        if not linea.strip():
            estadisticas['lineas_vacias'] += 1
        else:
            palabras = linea.split()
            estadisticas['palabras'] += len(palabras)
    
    return estadisticas

# Crear archivo de ejemplo para prueba
# with open('ejemplo.txt', 'w') as f:
#     f.write("Línea 1\nLínea 2\n\nLínea 4 con más palabras\n")

# stats = analizar_archivo('ejemplo.txt')
# print("Estadísticas del archivo:", stats)
```

#### Sistema de paginación

```python
def paginar(datos, tamaño_pagina=10):
    """Generador que pagina una lista de datos."""
    total_elementos = len(datos)
    total_paginas = (total_elementos + tamaño_pagina - 1) // tamaño_pagina
    
    for pagina in range(total_paginas):
        inicio = pagina * tamaño_pagina
        fin = min(inicio + tamaño_pagina, total_elementos)
        
        yield {
            'pagina': pagina + 1,
            'total_paginas': total_paginas,
            'datos': datos[inicio:fin],
            'total_elementos': total_elementos
        }

# Ejemplo de uso
productos = [f"Producto {i}" for i in range(1, 37)]  # 36 productos

print("📄 SISTEMA DE PAGINACIÓN")
print("="*40)

for info_pagina in paginar(productos, 5):
    print(f"Página {info_pagina['pagina']} de {info_pagina['total_paginas']}")
    for producto in info_pagina['datos']:
        print(f"  • {producto}")
    print()
    
    # Simular pausa entre páginas
    if info_pagina['pagina'] < info_pagina['total_paginas']:
        entrada = input("Presiona Enter para ver más o 'q' para salir: ")
        if entrada.lower() == 'q':
            break
```

#### Pipeline de procesamiento de datos

```python
def generar_datos(n):
    """Genera datos de ejemplo."""
    import random
    for i in range(n):
        yield {
            'id': i + 1,
            'nombre': f"Usuario_{i+1}",
            'edad': random.randint(18, 65),
            'salario': random.randint(20000, 80000)
        }

def filtrar_adultos(usuarios):
    """Filtra usuarios adultos (>= 25 años)."""
    for usuario in usuarios:
        if usuario['edad'] >= 25:
            yield usuario

def agregar_categoria_salario(usuarios):
    """Agrega categoría de salario a cada usuario."""
    for usuario in usuarios:
        if usuario['salario'] < 30000:
            categoria = 'Básico'
        elif usuario['salario'] < 50000:
            categoria = 'Medio'
        else:
            categoria = 'Alto'
        
        usuario['categoria_salario'] = categoria
        yield usuario

def procesar_usuarios(cantidad):
    """Pipeline de procesamiento usando generadores."""
    # Pipeline: generar -> filtrar -> categorizar
    datos = generar_datos(cantidad)
    adultos = filtrar_adultos(datos)
    usuarios_categorizados = agregar_categoria_salario(adultos)
    
    # Procesar solo los primeros 5 para mostrar
    contador = 0
    for usuario in usuarios_categorizados:
        print(f"ID: {usuario['id']}, Nombre: {usuario['nombre']}, "
              f"Edad: {usuario['edad']}, Salario: {usuario['salario']}€, "
              f"Categoría: {usuario['categoria_salario']}")
        
        contador += 1
        if contador >= 5:  # Mostrar solo primeros 5
            break

print("🔄 PIPELINE DE PROCESAMIENTO")
print("="*50)
# procesar_usuarios(1000)  # Descomenta para probar
```

### Resumen del Capítulo

Las funciones integradas de Python y los conceptos de iteradores/generadores forman parte del arsenal fundamental de todo programador Python. Estas herramientas no solo simplifican el código, sino que también optimizan el rendimiento y el uso de memoria, especialmente cuando se trabaja con grandes volúmenes de datos.

#### 💡 Conceptos Clave:

* **Funciones integradas**: Herramientas nativas optimizadas (`abs`, `max`, `sum`, `len`, etc.)
* **Funciones para iterables**: `map`, `filter`, `zip`, `enumerate`, `sorted`
* **Conversión de tipos**: `int`, `float`, `str`, `list`, `tuple`, `set`, `dict`
* **Iteradores**: Objetos que implementan `__iter__()` y `__next__()`
* **Generadores**: Funciones que usan `yield` para generar valores bajo demanda
* **Eficiencia de memoria**: Generadores vs listas para grandes volúmenes de datos

#### 🤔 Preguntas de Reflexión:

1. ¿En qué situaciones son más útiles los generadores que las listas?
2. ¿Cómo pueden las funciones `map` y `filter` mejorar la legibilidad del código?
3. ¿Qué ventajas aporta `enumerate()` frente a usar `range(len())`?
4. ¿Cuándo crearías un iterador personalizado en lugar de usar un generador?

#### 🔧 Ejercicio Práctico:

Crea un programa que:

1. Use funciones matemáticas para calcular estadísticas de una dataset
2. Implemente un generador para procesar archivos grandes línea por línea
3. Use `map`, `filter` y `zip` para transformar y combinar datos
4. Cree un iterador personalizado para una estructura de datos específica
5. Compare rendimiento entre listas y generadores con datos grandes
