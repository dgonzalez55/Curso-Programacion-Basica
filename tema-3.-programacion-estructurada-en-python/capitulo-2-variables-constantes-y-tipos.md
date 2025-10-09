# Capítulo 2: Variables, constantes y tipos

En programación, las variables son los contenedores fundamentales que almacenan la información con la que trabaja un programa. Si la memoria del ordenador fuera una inmensa biblioteca, las variables serían como las etiquetas en las estanterías que nos indican dónde encontrar cada libro (dato). Sin ellas, sería imposible realizar cualquier cálculo o manipular información. Este capítulo explora cómo nombrar y utilizar correctamente estas "etiquetas", así como los diferentes tipos de datos que pueden referenciar, y las reglas que gobiernan su uso en Python.

### 2.1. Identificadores: Reglas y buenas prácticas

Un **identificador** es el nombre que damos a una variable, función, clase u otro objeto en Python. Es la "_etiqueta_" que asociamos a un valor en memoria.

Para nombrar identificadores, se deben seguir unas reglas obligatorias:

1. **Carácter inicial**: Debe comenzar con una **letra** (a-z, A-Z) o un **guion bajo** (`_`). Nunca puede empezar con un número.
   * _<mark style="background-color:$success;">**Válido**</mark>:_ `nombre`, `_contador`, `Usuario1`
   * _<mark style="background-color:$danger;">**Inválido**</mark>:_ `1usuario`, `-precio`, `@email`
2. **Caracteres posteriores**: Después del primer carácter, puede contener letras, números y guiones bajos.
   * _<mark style="background-color:$success;">**Válido**</mark>:_ `nombre_completo`, `temperatura_2024`
   * _<mark style="background-color:$danger;">**Inválido**</mark>:_ `precio-final` (el guion medio no está permitido)
3. **Sensibilidad a mayúsculas**: Python distingue entre mayúsculas y minúsculas. `nombre`, `Nombre` y `NOMBRE` son tres variables diferentes.
4. **Palabras reservadas**: No se pueden usar como identificadores las palabras clave del lenguaje (ej. `if`, `for`, `while`, `class`).

Además de las reglas, la guía de estilo PEP 8 establece convenciones para que el código sea más legible y consistente:

| Tipo                      | Convención                                        | Ejemplo                               |
| ------------------------- | ------------------------------------------------- | ------------------------------------- |
| **Variables y funciones** | `snake_case` (minúsculas con guiones bajos)       | `edad_usuario`, `calcular_promedio()` |
| **Constantes**            | `UPPER_CASE` (mayúsculas con guiones bajos)       | `PI`, `MAX_INTENTOS`                  |
| **Clases**                | `PascalCase` (cada palabra empieza con mayúscula) | `Usuario`, `CalculadoraMatematica`    |

#### **Ejemplos de buenas prácticas**

```python
# ✅ Nombres descriptivos y claros
edad_estudiante = 20
temperatura_maxima = 35.5
lista_nombres_usuarios = ["Ana", "Pedro", "María"]

# ❌ Nombres poco descriptivos
a = 20
t = 35.5
l = ["Ana", "Pedro", "María"]

# ✅ Constantes bien definidas
PI = 3.141592653589793
VELOCIDAD_LUZ = 299792458  # m/s
NUMERO_AVOGADRO = 6.02214076e23

# ✅ Funciones con nombres y verbos
def calcular_area_circulo(radio):
    return PI * radio ** 2

def validar_email(email):
    return "@" in email and "." in email
```

***

### 2.2. Tipado fuerte y dinámico en Python

El sistema de tipos de Python se define por dos conceptos clave: es de **tipado dinámico y fuerte.**

#### **Tipado dinámico**

Significa que no es necesario declarar el tipo de una variable al crearla. El tipo se determina en tiempo de ejecución, cuando se le asigna un valor. Además, una misma variable puede cambiar de tipo durante la ejecución del programa. Esto contrasta con lenguajes de tipado estático como Java o C++, donde el tipo de una variable se fija en su declaración y no puede cambiar.

```python
# No necesitas declarar el tipo
variable = 42           # Python entiende que es int
print(type(variable))   # <class 'int'>

# La misma variable puede cambiar de tipo
variable = "Hola mundo" # Ahora es string
print(type(variable))   # <class 'str'>

variable = [1, 2, 3]    # Ahora es lista
print(type(variable))   # <class 'list'>
```

**Comparación con tipado estático (Java)**

```java
// Java (tipado estático)
int numero = 42;        // Debes declarar el tipo
String texto = "Hola";  // No puedes cambiar el tipo después
```

#### **Tipado fuerte**

Significa que Python no permite operaciones implícitas entre tipos de datos incompatibles. Por ejemplo, intentar sumar un número y una cadena de texto provocará un error `TypeError`. Para que la operación funcione, es necesario realizar una conversión explícita: `5 + int("10")`. Esto previene errores comunes en lenguajes de tipado débil como JavaScript, que intentaría "adivinar" la intención del programador, a menudo con resultados inesperados.

**Python no permite operaciones implícitas entre tipos incompatibles**

```python
# ❌ Esto genera un error (TypeError)
resultado = 5 + "10"    # No puede sumar int + str

# ✅ Debes hacer la conversión explícita
resultado_numerico = 5 + int("10")    # 15
resultado_texto = str(5) + "10"       # "510"
```

**Comparación con tipado débil (JavaScript)**

```javascript
// JavaScript (tipado débil)
var resultado = 5 + "10";  // "510" - convierte automáticamente
```

#### Verificación de tipos

Para verificar el tipo de una variable, se pueden usar dos funciones:

* **`type()`**: Devuelve el tipo exacto de un objeto.
* **`isinstance()`**: Comprueba si un objeto es una instancia de una clase o de una tupla de clases. Generalmente es más flexible y recomendada, ya que también funciona correctamente con la herencia.

```python
# Función type() - tipo exacto
numero = 42
print(type(numero))                    # <class 'int'>
print(type(numero) == int)            # True

# Función isinstance() - más flexible (recomendada)
print(isinstance(numero, int))        # True
print(isinstance(numero, (int, float))) # True (¿es int O float?)

# Verificación de múltiples tipos
def procesar_dato(dato):
    if isinstance(dato, str):
        return dato.upper()
    elif isinstance(dato, (int, float)):
        return dato * 2
    else:
        return None
```

***

### 2.3. Tipos de datos básicos y colecciones

Python ofrece un rico conjunto de tipos de datos integrados.

#### Enteros (`int`)

Números sin decimales. Pueden ser positivos, negativos o cero, y su tamaño solo está limitado por la memoria disponible. Se pueden representar en diferentes bases y usar guiones bajos para mejorar la legibilidad.

```python
# Números enteros sin límite de tamaño
pequeño = 42
grande = 999999999999999999999999999999
negativo = -273

# Diferentes bases numéricas
binario = 0b1010      # Base 2: 10 decimal
octal = 0o12          # Base 8: 10 decimal
hexadecimal = 0xA     # Base 16: 10 decimal

# Separadores para legibilidad
poblacion_mundial = 7_900_000_000
print(poblacion_mundial)  # 7900000000
```

#### Punto flotante (`float`)

Números con decimales. Tienen una precisión limitada, lo que puede llevar a pequeños errores de redondeo. Se puede usar notación científica.

```python
# Números con decimales (precisión limitada)
pi = 3.141592653589793
temperatura = -40.5
muy_pequeño = 1e-10    # Notación científica: 0.0000000001
muy_grande = 2.5e6     # 2,500,000

# ⚠️ Atención: Problemas de precisión
print(0.1 + 0.2)       # 0.30000000000000004
print(0.1 + 0.2 == 0.3) # False

# Solución para cálculos precisos
from decimal import Decimal
a = Decimal('0.1')
b = Decimal('0.2')
print(a + b)           # 0.3
```

#### Booleanos (`bool`)

Representan valores de verdad. Solo pueden ser `True` o `False`. Ciertos valores, conocidos como "falsy", se evalúan como `False` en un contexto booleano.

```python
# Solo dos valores posibles
verdadero = True
falso = False

# Conversión implícita a booleano
print(bool(0))         # False
print(bool(1))         # True
print(bool(""))        # False (cadena vacía)
print(bool("Texto"))   # True
print(bool([]))        # False (lista vacía)
print(bool([1, 2]))    # True

# Valores que se evalúan como False
falsy_values = [None, False, 0, 0.0, "", [], {}, set()]
for valor in falsy_values:
    print(f"{valor} es {bool(valor)}")
```

#### Cadenas de texto (`str`)

Secuencias de caracteres. Son inmutables, lo que significa que no se pueden modificar una vez creadas. Esta inmutabilidad garantiza que el objeto no pueda ser modificado accidentalmente, haciéndolo seguro para usar como clave de diccionario o en entornos complejos como la programación multihilo.

```python
# Diferentes formas de definir strings
simple = 'Hola mundo'
doble = "Hola mundo"
triple = '''Texto de
múltiples
líneas'''

# Caracteres de escape
escapado = "Línea 1\nLínea 2\tTabulado"
path = r"C:\Users\nombre\Documents"  # Raw string (sin escape)

# Operaciones básicas
nombre = "Python"
print(len(nombre))          # 6
print(nombre[0])           # P
print(nombre[-1])          # n
print(nombre[2:5])         # tho
print(nombre.upper())      # PYTHON
print(nombre.lower())      # python
print("Py" in nombre)      # True

# Inmutabilidad
# nombre[0] = "J"  # ❌ Error: strings son inmutables
nuevo_nombre = "J" + nombre[1:]  # ✅ Crear nueva string
```

#### **Tipo `None`**

El tipo `None` representa la ausencia de valor. Es similar al `null` de otros lenguajes y se utiliza a menudo para indicar que una variable no tiene un valor asignado o que una función no devuelve nada explícitamente.

```python
# Representa la ausencia de valor
valor_nulo = None
print(type(valor_nulo))  # <class 'NoneType'>

# Uso típico en funciones
def buscar_usuario(id):
    if id == 1:
        return {"nombre": "Ana", "edad": 25}
    else:
        return None  # No se encontró el usuario

resultado = buscar_usuario(999)
if resultado is None:
    print("Usuario no encontrado")
```

#### **Colecciones**

**Listas (`list`)**&#x20;

Colecciones ordenadas y mutables de elementos. Pueden contener datos de diferentes tipos.

```python
# Creación y operaciones básicas
numeros = [1, 2, 3, 4, 5]
mixta = [1, "texto", 3.14, True]
vacia = []

# Acceso por índice
print(numeros[0])     # 1 (primer elemento)
print(numeros[-1])    # 5 (último elemento)
print(numeros[1:3])   # [2, 3] (slice)

# Modificación (son mutables)
numeros[0] = 100      # [100, 2, 3, 4, 5]
numeros.append(6)     # [100, 2, 3, 4, 5, 6]
numeros.insert(1, 99) # [100, 99, 2, 3, 4, 5, 6]
numeros.remove(3)     # [100, 99, 2, 4, 5, 6]

print(f"Longitud: {len(numeros)}")
```

**Tuplas (`tuple`)**

Colecciones ordenadas e inmutables. Una vez creadas, no se pueden modificar. Son más eficientes en memoria que las listas y, gracias a su inmutabilidad, pueden usarse como claves de diccionario.

```python
# Más eficientes en memoria que las listas
coordenadas = (10, 20)
colores = ("rojo", "verde", "azul")
un_elemento = (42,)  # Nota la coma para tupla de un elemento

# Acceso igual que listas
print(coordenadas[0])   # 10
print(colores[-1])      # azul

# ❌ No se pueden modificar
# colores[0] = "amarillo"  # Error: tuplas son inmutables

# Desempaquetado
x, y = coordenadas
print(f"X: {x}, Y: {y}")  # X: 10, Y: 20
```

**Rangos (`range`)**

Secuencias numéricas inmutables y eficientes en memoria, ya que no almacenan todos los números a la vez, sino que los generan bajo demanda.

```python
# Generan secuencias bajo demanda (eficientes en memoria)
rango1 = range(5)          # 0, 1, 2, 3, 4
rango2 = range(1, 6)       # 1, 2, 3, 4, 5
rango3 = range(0, 10, 2)   # 0, 2, 4, 6, 8

# Para ver el contenido, convertir a lista
print(list(rango1))  # [0, 1, 2, 3, 4]
print(list(rango2))  # [1, 2, 3, 4, 5]
print(list(rango3))  # [0, 2, 4, 6, 8]

# Uso típico en bucles
for i in range(3):
    print(f"Iteración {i}")
```

**Diccionarios (`dict`)**

Colecciones mutables de pares clave-valor, ordenadas por inserción desde Python 3.7+. Las claves deben ser únicas e inmutables.

```python
# Colecciones no ordenadas de pares clave-valor
estudiante = {
    "nombre": "Ana",
    "edad": 20,
    "carrera": "Informática",
    "activo": True
}

# Acceso y modificación
print(estudiante["nombre"])        # Ana
print(estudiante.get("email", "N/A"))  # N/A (con valor por defecto)

estudiante["edad"] = 21            # Modificar valor existente
estudiante["email"] = "ana@uni.es" # Añadir nueva clave
del estudiante["activo"]           # Eliminar clave

# Operaciones útiles
print(estudiante.keys())           # dict_keys(['nombre', 'edad', 'carrera', 'email'])
print(estudiante.values())         # dict_values(['Ana', 21, 'Informática', 'ana@uni.es'])
print(estudiante.items())          # dict_items([...])
```

**Conjuntos (`set`)**

Colecciones mutables y no ordenadas de elementos únicos. Son útiles para eliminar duplicados y realizar operaciones matemáticas de conjuntos (unión, intersección, etc.).

```python
# Elementos únicos, ideales para eliminar duplicados
numeros = {1, 2, 3, 3, 4, 4, 5}
print(numeros)  # {1, 2, 3, 4, 5} - duplicados eliminados

# Crear conjunto desde lista
lista_con_duplicados = [1, 2, 2, 3, 3, 3, 4]
conjunto_unico = set(lista_con_duplicados)
print(conjunto_unico)  # {1, 2, 3, 4}

# Operaciones de conjuntos
conjunto_a = {1, 2, 3, 4}
conjunto_b = {3, 4, 5, 6}

print(conjunto_a | conjunto_b)  # {1, 2, 3, 4, 5, 6} - unión
print(conjunto_a & conjunto_b)  # {3, 4} - intersección  
print(conjunto_a - conjunto_b)  # {1, 2} - diferencia
print(conjunto_a ^ conjunto_b)  # {1, 2, 5, 6} - diferencia simétrica
```

***

### 2.4. Constantes y su uso en Python

Como se mencionó anteriormente, **Python no tiene un mecanismo para crear constantes verdaderas**. La convención establecida por PEP 8 es utilizar nombres de variables completamente en mayúsculas (`UPPER_CASE`) para indicar que un valor no debe ser modificado.

```python
PI = 3.14159
VELOCIDAD_LUZ = 299792458
```

Técnicamente, es posible reasignar estas variables, pero hacerlo se considera una mala práctica.

#### Organización de constantes

**En módulos separados**

```python
# constantes.py
DATABASE_URL = "postgresql://localhost/miapp"
SECRET_KEY = "mi_clave_secreta_super_segura"
DEBUG = False
MAX_FILE_SIZE = 10 * 1024 * 1024  # 10 MB

# main.py
import constantes

def conectar_db():
    return conectar(constantes.DATABASE_URL)
```

**En clases**

```python
class Config:
    """Configuración de la aplicación."""
    DEBUG = False
    TESTING = False
    DATABASE_URI = "sqlite:///app.db"
    
class DevelopmentConfig(Config):
    DEBUG = True
    DATABASE_URI = "sqlite:///dev.db"
```

#### **Variables locales y globales**

El ámbito de una variable determina dónde es accesible.

* **Variables locales**: Se definen dentro de una función y solo son accesibles desde ella.
* **Variables globales**: Se definen en el nivel principal del script y son accesibles desde cualquier parte. Para modificar una variable global desde dentro de una función, se debe usar la palabra clave `global`.

```python
contador_global = 0

def incrementar_contador():
    global contador_global  # Indica que vamos a modificar la variable global
    contador_global += 1

incrementar_contador()
print(contador_global) # 1
```

***

### Resumen del Capítulo

En este capítulo has aprendido los fundamentos del sistema de variables y tipos de Python. Has comprendido las reglas de nomenclatura, el tipado dinámico pero fuerte, y los tipos de datos básicos que forman la base de cualquier programa Python. La correcta utilización de variables, constantes y tipos es fundamental para escribir código limpio, eficiente y mantenible.

#### 💡 Conceptos Clave:

* **Identificadores**: Nombres que siguen reglas estrictas y convenciones PEP 8
* **Tipado dinámico y fuerte**: Flexibilidad con seguridad
* **Tipos primitivos**: `int`, `float`, `bool`, `str`, `None`
* **Colecciones**: `list`, `tuple`, `range`, `dict`, `set`
* **Constantes**: Convención con MAYÚSCULAS, no inmutabilidad real
* **Ámbito**: Variables locales y. globales

#### 🤔 Preguntas de Reflexión:

1. ¿Qué ventajas y desventajas tiene el tipado dinámico de Python frente al tipado estático?
2. ¿Por qué Python eligió la inmutabilidad para strings y tuplas pero no para listas?
3. ¿En qué situaciones preferirías usar un diccionario frente a una lista?
4. ¿Cómo puede la correcta nomenclatura de variables mejorar la legibilidad del código?

#### 🔧 Ejercicio Práctico:

Crea un programa que:

1. Defina constantes para una tienda (IVA, descuento máximo, etc.)
2. Use diferentes tipos de datos para representar un producto
3. Implemente funciones que calculen precios finales
4. Demuestre el correcto uso de variables locales y globales

Ahora que conocemos los diferentes tipos de datos que podemos almacenar, estamos listos para aprender a operar con ellos. El siguiente capítulo explora las expresiones y los operadores, las herramientas que nos permiten construir la lógica de nuestros programas.

***
