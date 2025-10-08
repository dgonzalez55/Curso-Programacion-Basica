# Capítulo 2: Variables, constantes y tipos

En programación, las variables son los recipientes que almacenan la información con la que trabaja nuestro programa. Imagina que la memoria de tu ordenador es como una enorme biblioteca, y las variables son las etiquetas que colocamos en las estanterías para saber dónde encontrar cada libro. En Python, estas etiquetas (variables) tienen reglas específicas sobre cómo pueden llamarse y qué tipos de información pueden almacenar.

En este capítulo exploraremos el sistema de tipos de Python, las reglas de nomenclatura, y comprenderemos cómo Python gestiona la memoria y los tipos de forma dinámica pero segura.

### 2.1. Identificadores, reglas y buenas prácticas

#### Definición de identificador

Un **identificador** es un nombre que utilizamos para referenciar variables, funciones, clases, módulos u otros objetos en Python. Es la etiqueta que asociamos con un valor almacenado en la memoria.

#### Reglas obligatorias para identificadores

**1. Carácter inicial**: Debe comenzar con una **letra** (a-z, A-Z) o **guion bajo** (\_)

```python
# ✅ Válido
nombre = "Ana"
_contador = 0
Usuario1 = "admin"

# ❌ Inválido
1usuario = "admin"    # Error: no puede empezar con número
-precio = 100         # Error: no puede empezar con guion
@email = "test"       # Error: @ no es válido
```

**2. Caracteres posteriores**: Pueden contener letras, números y guiones bajos

```python
# ✅ Válido
nombre_completo = "Ana García"
temperatura_2024 = 25.5
__valor_privado = 42

# ❌ Inválido
precio-final = 100    # Error: guion no válido
área_círculo = 3.14   # Error: caracteres especiales no ASCII
```

**3. Sensibilidad a mayúsculas**: Python distingue entre mayúsculas y minúsculas

```python
nombre = "Ana"
Nombre = "Pedro"
NOMBRE = "Juan"

print(nombre)  # Ana
print(Nombre)  # Pedro
print(NOMBRE)  # Juan
```

**4. Palabras reservadas**: No se pueden usar las palabras clave de Python

```python
# Palabras reservadas que NO puedes usar como identificadores
and, as, assert, break, class, continue, def, del, elif, else,
except, exec, finally, for, from, global, if, import, in, is,
lambda, not, or, pass, print, raise, return, try, while, with, yield

# ❌ Inválido
if = 5        # Error: 'if' es palabra reservada
class = "A"   # Error: 'class' es palabra reservada

# ✅ Alternativas válidas
condicion = True
tipo_clase = "A"
```

#### Convenciones de nomenclatura (PEP 8)

| Tipo                       | Convención                                                | Ejemplo                                |
| -------------------------- | --------------------------------------------------------- | -------------------------------------- |
| **Variables y funciones**  | `snake_case` (minúsculas con guiones bajos)               | `edad_usuario`, `calcular_promedio()`  |
| **Constantes**             | `UPPER_CASE` (mayúsculas con guiones bajos)               | `PI`, `MAX_INTENTOS`, `NOMBRE_ARCHIVO` |
| **Clases**                 | `PascalCase` (primera letra de cada palabra en mayúscula) | `Usuario`, `CalculadoraMatematica`     |
| **Variables privadas**     | Prefijo con guion bajo                                    | `_variable_interna`                    |
| **Variables muy privadas** | Doble guion bajo                                          | `__variable_muy_privada`               |
| **Módulos y paquetes**     | `minusculas_cortas`                                       | `utils.py`, `matematicas`              |

**Ejemplos de buenas prácticas:**

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

# ✅ Funciones con nombres verbos
def calcular_area_circulo(radio):
    return PI * radio ** 2

def validar_email(email):
    return "@" in email and "." in email
```

### 2.2. Tipado fuerte y dinámico en Python

Python implementa un sistema de **tipado fuerte y dinámico** que lo distingue de muchos otros lenguajes de programación.

#### Tipado dinámico

**El tipo se determina en tiempo de ejecución**, no necesitas declarar el tipo de la variable al crearla:

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

**Comparación con tipado estático (Java/C++):**

```java
// Java (tipado estático)
int numero = 42;        // Debes declarar el tipo
String texto = "Hola";  // No puedes cambiar el tipo después
```

#### Tipado fuerte

**Python no permite operaciones implícitas entre tipos incompatibles**:

```python
# ❌ Esto genera un error (TypeError)
resultado = 5 + "10"    # No puede sumar int + str

# ✅ Debes hacer la conversión explícita
resultado_numerico = 5 + int("10")    # 15
resultado_texto = str(5) + "10"       # "510"
```

**Comparación con tipado débil (JavaScript):**

```javascript
// JavaScript (tipado débil)
var resultado = 5 + "10";  // "510" - convierte automáticamente
```

#### Verificación de tipos

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

### 2.3. Tipos de datos básicos y colecciones

#### Tipos primitivos fundamentales

**Enteros (int)**

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

**Números de punto flotante (float)**

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

**Booleanos (bool)**

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

**Cadenas de texto (str)**

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

#### Tipos None

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

#### Colecciones básicas

**Listas (list) - Mutables y ordenadas**

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

**Tuplas (tuple) - Inmutables y ordenadas**

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

**Rangos (range) - Secuencias numéricas inmutables**

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

**Diccionarios (dict) - Mapas clave-valor mutables**

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

**Conjuntos (set) - Elementos únicos, no ordenados, mutables**

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

### 2.4. Constantes y su uso en Python

#### Convención para constantes

Python **no tiene constantes verdaderas** (inmutables por el lenguaje), pero por convención se utilizan identificadores en **MAYÚSCULAS** para indicar que un valor no debe modificarse:

```python
# ✅ Constantes bien definidas
PI = 3.141592653589793
VELOCIDAD_LUZ = 299792458  # metros por segundo
GRAVEDAD_TIERRA = 9.81     # m/s²
MAX_USUARIOS = 1000
NOMBRE_APLICACION = "MiApp"
COLORES_PERMITIDOS = ["rojo", "verde", "azul"]

# Uso en funciones
def calcular_area_circulo(radio):
    return PI * radio ** 2

def calcular_energia(masa):
    return masa * VELOCIDAD_LUZ ** 2

# ⚠️ Técnicamente puedes modificarlas, pero no deberías
# PI = 3.14  # Malo: rompe la convención
```

#### Organización de constantes

**En módulos separados:**

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

**En clases:**

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

#### Variables locales vs. globales

```python
# Variable global
contador_global = 0

def incrementar_contador():
    global contador_global  # Necesario para modificar variable global
    contador_global += 1

def ejemplo_scope():
    # Variable local
    contador_local = 10
    print(f"Local: {contador_local}")
    print(f"Global: {contador_global}")

# Demostración
incrementar_contador()
ejemplo_scope()
print(f"Contador global final: {contador_global}")  # 1
```

#### Gestión de memoria y referencias

```python
# Python gestiona la memoria automáticamente
a = [1, 2, 3]
b = a        # b apunta al mismo objeto que a
c = a[:]     # c es una copia superficial

a.append(4)
print(a)  # [1, 2, 3, 4]
print(b)  # [1, 2, 3, 4] - cambió porque apunta al mismo objeto
print(c)  # [1, 2, 3] - no cambió porque es una copia

# Verificar si dos variables apuntan al mismo objeto
print(a is b)  # True - mismo objeto
print(a is c)  # False - objetos diferentes
print(a == c)  # False - valores diferentes ahora

# Liberar referencias
del a  # Elimina la referencia, no necesariamente el objeto
```

### Resumen del Capítulo

En este capítulo has aprendido los fundamentos del sistema de variables y tipos de Python. Has comprendido las reglas de nomenclatura, el tipado dinámico pero fuerte, y los tipos de datos básicos que forman la base de cualquier programa Python. La correcta utilización de variables, constantes y tipos es fundamental para escribir código limpio, eficiente y mantenible.

#### 💡 Conceptos Clave:

* **Identificadores**: Nombres que siguen reglas estrictas y convenciones PEP 8
* **Tipado dinámico y fuerte**: Flexibilidad con seguridad
* **Tipos primitivos**: `int`, `float`, `bool`, `str`, `None`
* **Colecciones**: `list`, `tuple`, `range`, `dict`, `set`
* **Constantes**: Convención con MAYÚSCULAS, no inmutabilidad real
* **Ámbito**: Variables locales vs. globales

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
