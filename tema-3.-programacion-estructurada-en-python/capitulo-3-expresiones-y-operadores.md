# Capítulo 3: Expresiones y operadores

En programación, las **expresiones** son combinaciones de variables, literales, operadores y funciones que, después de su evaluación o cálculo, nos devuelven un valor de un tipo determinado. Los **operadores** son los símbolos que nos permiten realizar operaciones sobre estos valores: desde cálculos matemáticos básicos hasta comparaciones lógicas complejas.

En Python, existe una rica variedad de operadores que nos permiten manipular datos de formas muy sofisticadas. En este capítulo exploraremos todos los tipos de operadores disponibles, sus reglas de precedencia y cómo combinarlos para crear expresiones potentes y eficientes.

### 3.1. ¿Qué es una expresión?

Una **expresión** es una combinación de uno o más valores, variables, operadores y llamadas a funciones que Python puede evaluar para producir un resultado. Las expresiones son los bloques básicos de construcción de cualquier programa.

#### Tipos de expresiones

**1. Expresiones literales**: Valores constantes

```python
42                    # Expresión literal entera
3.14159              # Expresión literal flotante
"Hola mundo"         # Expresión literal string
True                 # Expresión literal booleana
```

**2. Expresiones con variables**: Utilizan identificadores

```python
edad                 # Variable simple
nombre_usuario       # Variable simple
lista[0]            # Acceso a elemento
diccionario["clave"] # Acceso a diccionario
```

**3. Expresiones aritméticas**: Combinan valores con operadores matemáticos

```python
3 + 5                # Suma simple
edad * 2             # Multiplicación con variable
(radio ** 2) * 3.14  # Expresión compleja con paréntesis
```

**4. Expresiones lógicas**: Evalúan a True o False

```python
edad >= 18           # Comparación
activo and verificado # Combinación lógica
not usuario_bloqueado # Negación
```

**5. Expresiones con funciones**: Incluyen llamadas a funciones

```python
len(lista)           # Función incorporada
max(a, b, c)        # Función con múltiples argumentos
math.sqrt(25)       # Función de módulo
```

### 3.2. Operadores aritméticos

Los operadores aritméticos nos permiten realizar operaciones matemáticas sobre números.

#### Operadores aritméticos básicos

| Operador | Nombre              | Ejemplo  | Resultado |
| -------- | ------------------- | -------- | --------- |
| `+`      | Suma                | `3 + 2`  | `5`       |
| `-`      | Resta               | `3 - 2`  | `1`       |
| `*`      | Multiplicación      | `3 * 2`  | `6`       |
| `/`      | División (flotante) | `3 / 2`  | `1.5`     |
| `//`     | División entera     | `3 // 2` | `1`       |
| `%`      | Módulo (resto)      | `3 % 2`  | `1`       |
| `**`     | Potencia            | `3 ** 2` | `9`       |

#### Ejemplos prácticos

```python
# Operaciones básicas
numero1 = 3
numero2 = 2

print(f"Suma: {numero1 + numero2}")           # Suma: 5
print(f"Resta: {numero1 - numero2}")          # Resta: 1
print(f"Multiplicación: {numero1 * numero2}") # Multiplicación: 6
print(f"División: {numero1 / numero2}")       # División: 1.5
print(f"Módulo: {numero1 % numero2}")         # Módulo: 1
print(f"División entera: {numero1 // numero2}") # División entera: 1
print(f"Potencia: {numero1 ** numero2}")      # Potencia: 9
```

#### División: diferencias importantes

```python
# División flotante (/) - Siempre devuelve float
print(10 / 3)    # 3.3333333333333335
print(10 / 2)    # 5.0 (float, no int)
print(10.0 / 3)  # 3.3333333333333335

# División entera (//) - Redondea hacia abajo
print(10 // 3)   # 3
print(10 // 2)   # 5
print(-10 // 3)  # -4 (redondea hacia abajo, no hacia cero)

# Para redondeo hacia cero con negativos
import math
print(math.trunc(-10 / 3))  # -3
```

#### Operador módulo: casos prácticos

```python
# Determinar si un número es par o impar
numero = 17
if numero % 2 == 0:
    print(f"{numero} es par")
else:
    print(f"{numero} es impar")

# Convertir segundos a minutos y segundos
total_segundos = 150
minutos = total_segundos // 60
segundos_restantes = total_segundos % 60
print(f"{total_segundos} segundos = {minutos} minutos y {segundos_restantes} segundos")

# Ciclar a través de valores (útil en listas circulares)
elementos = ["rojo", "verde", "azul"]
for i in range(10):
    color_actual = elementos[i % len(elementos)]
    print(f"Posición {i}: {color_actual}")
```

### 3.3. Operadores de cadenas

Las cadenas de texto tienen operadores específicos para manipulación.

#### Concatenación (+) y repetición (\*)

```python
cadena1 = "Hola"
cadena2 = "mundo"

# Concatenación
saludo = cadena1 + " " + cadena2
print(saludo)  # Hola mundo

# Repetición
separador = "-" * 30
print(separador)  # ------------------------------

patron = "Ha" * 3
print(patron)  # HaHaHa

# Combinando operadores
titulo = "=" * 20 + " TÍTULO " + "=" * 20
print(titulo)  # ==================== TÍTULO ====================
```

#### Operadores de acceso (slice)

```python
texto = "Python Programming"

# Acceso por índice
print(texto[0])      # P
print(texto[-1])     # g

# Slice (rebanadas)
print(texto[0:6])    # Python
print(texto[7:])     # Programming
print(texto[:6])     # Python
print(texto[7:10])   # Pro

# Slice con paso
print(texto[::2])    # Pto rgamn
print(texto[::-1])   # gnimmargorP nohtyP (reverso)
```

#### Operadores de pertenencia

```python
texto = "Hola mundo"

# Verificar si una subcadena está presente
print("Hola" in texto)      # True
print("adiós" in texto)     # False
print("HOLA" in texto)      # False (sensible a mayúsculas)

# Verificar si NO está presente
print("xyz" not in texto)   # True
print("mundo" not in texto) # False
```

### 3.4. Operadores de asignación

Combinan una operación aritmética con una asignación para código más conciso.

#### Operadores de asignación compuesta

| Operador | Equivalente      | Ejemplo   |
| -------- | ---------------- | --------- |
| `+=`     | `x = x + valor`  | `x += 5`  |
| `-=`     | `x = x - valor`  | `x -= 3`  |
| `*=`     | `x = x * valor`  | `x *= 2`  |
| `/=`     | `x = x / valor`  | `x /= 4`  |
| `//=`    | `x = x // valor` | `x //= 2` |
| `%=`     | `x = x % valor`  | `x %= 3`  |
| `**=`    | `x = x ** valor` | `x **= 2` |

#### Ejemplos prácticos

```python
# Contador tradicional
contador = 0
contador += 1      # contador = 1
contador += 5      # contador = 6

# Acumulador
suma = 10
suma += 20         # suma = 30
suma *= 2          # suma = 60
suma //= 3         # suma = 20

# Operaciones con strings
mensaje = "Hola"
mensaje += " mundo"  # mensaje = "Hola mundo"
mensaje *= 2         # mensaje = "Hola mundoHola mundo"

# Operaciones con listas
numeros = [1, 2, 3]
numeros += [4, 5]    # numeros = [1, 2, 3, 4, 5]
numeros *= 2         # numeros = [1, 2, 3, 4, 5, 1, 2, 3, 4, 5]
```

### 3.5. Operadores de comparación

Comparan valores y devuelven `True` o `False`.

#### Operadores de comparación básicos

| Operador | Significado       | Ejemplo  |
| -------- | ----------------- | -------- |
| `==`     | Igual a           | `a == b` |
| `!=`     | Diferente de      | `a != b` |
| `>`      | Mayor que         | `a > b`  |
| `<`      | Menor que         | `a < b`  |
| `>=`     | Mayor o igual que | `a >= b` |
| `<=`     | Menor o igual que | `a <= b` |

#### Operadores de identidad

| Operador | Significado                 | Uso          |
| -------- | --------------------------- | ------------ |
| `is`     | Mismo objeto en memoria     | `a is b`     |
| `is not` | Diferente objeto en memoria | `a is not b` |

#### Ejemplos prácticos

```python
# Comparaciones numéricas
num1 = 5
num2 = 3

print(f"{num1} == {num2}: {num1 == num2}")  # False
print(f"{num1} != {num2}: {num1 != num2}")  # True
print(f"{num1} > {num2}: {num1 > num2}")    # True
print(f"{num1} < {num2}: {num1 < num2}")    # False
print(f"{num1} >= {num2}: {num1 >= num2}")  # True
print(f"{num1} <= {num2}: {num1 <= num2}")  # False

# Comparaciones con strings
palabra1 = "Python"
palabra2 = "python"
print(f"'{palabra1}' == '{palabra2}': {palabra1 == palabra2}")  # False

# Identidad vs igualdad
lista1 = [1, 2, 3]
lista2 = [1, 2, 3]
lista3 = lista1

print(f"lista1 == lista2: {lista1 == lista2}")  # True (mismo contenido)
print(f"lista1 is lista2: {lista1 is lista2}")  # False (objetos diferentes)
print(f"lista1 is lista3: {lista1 is lista3}")  # True (mismo objeto)
```

#### Comparaciones encadenadas

```python
# Python permite comparaciones encadenadas
edad = 25
print(18 <= edad <= 65)  # True (equivale a: edad >= 18 and edad <= 65)

nota = 8.5
print(0 <= nota <= 10)   # True

# Comparación de múltiples valores
a, b, c = 5, 10, 15
print(a < b < c)         # True
print(a < b > c)         # False
```

### 3.6. Operadores lógicos

Permiten combinar expresiones booleanas.

#### Operadores lógicos básicos

| Operador | Descripción                                 | Ejemplo                    |
| -------- | ------------------------------------------- | -------------------------- |
| `and`    | Y lógico - True si ambos operandos son True | `True and False` → `False` |
| `or`     | O lógico - True si al menos uno es True     | `True or False` → `True`   |
| `not`    | Negación - Invierte el valor lógico         | `not True` → `False`       |

#### Tablas de verdad

**Operador AND**

| A     | B     | A and B |
| ----- | ----- | ------- |
| True  | True  | True    |
| True  | False | False   |
| False | True  | False   |
| False | False | False   |

**Operador OR**

| A     | B     | A or B |
| ----- | ----- | ------ |
| True  | True  | True   |
| True  | False | True   |
| False | True  | True   |
| False | False | False  |

**Operador NOT**

| A     | not A |
| ----- | ----- |
| True  | False |
| False | True  |

#### Ejemplos prácticos

```python
# Variables de ejemplo
edad = 25
tiene_licencia = True
tiene_seguro = False

# Operador AND
puede_conducir = edad >= 18 and tiene_licencia and tiene_seguro
print(f"¿Puede conducir? {puede_conducir}")  # False

# Operador OR
necesita_documentos = not tiene_licencia or not tiene_seguro
print(f"¿Necesita documentos? {necesita_documentos}")  # True

# Combinaciones complejas
es_adulto_con_documentos = edad >= 18 and (tiene_licencia and tiene_seguro)
print(f"¿Adulto con documentos? {es_adulto_con_documentos}")  # False
```

#### Evaluación de cortocircuito

Python utiliza **evaluación de cortocircuito** (short-circuit evaluation):

```python
# AND: si el primer operando es False, no evalúa el segundo
resultado = False and print("Esto no se ejecuta")

# OR: si el primer operando es True, no evalúa el segundo
resultado = True or print("Esto no se ejecuta")

# Ejemplo práctico para evitar errores
lista = []
# Sin cortocircuito causaría IndexError si la lista está vacía
if lista and lista[0] > 0:
    print("El primer elemento es positivo")

# Verificación segura de división
divisor = 0
if divisor != 0 and 10 / divisor > 2:
    print("El resultado es mayor que 2")
```

### 3.7. Operadores de pertenencia

Verifican si un elemento está presente en una secuencia.

#### Operadores in y not in

```python
# Con listas
numeros = [1, 2, 3, 4, 5]
print(3 in numeros)      # True
print(6 in numeros)      # False
print(6 not in numeros)  # True

# Con strings
texto = "Hola mundo"
print("Hola" in texto)      # True
print("adiós" in texto)     # False
print("Python" not in texto) # True

# Con diccionarios (verifica las claves)
persona = {"nombre": "Ana", "edad": 25}
print("nombre" in persona)     # True
print("apellido" in persona)   # False
print("Ana" in persona)        # False (verifica claves, no valores)

# Para verificar valores en diccionarios
print("Ana" in persona.values())  # True

# Con conjuntos
colores = {"rojo", "verde", "azul"}
print("rojo" in colores)     # True
print("amarillo" in colores) # False
```

### 3.8. Precedencia de operadores

La **precedencia de operadores** determina el orden en que se evalúan las operaciones en una expresión compleja.

#### Tabla de precedencia (de mayor a menor)

1. **Paréntesis**: `()`
2. **Potencia**: `**`
3. **Unarios**: `+x`, `-x`, `not x`
4. **Multiplicación, División, Módulo**: `*`, `/`, `//`, `%`
5. **Suma, Resta**: `+`, `-`
6. **Comparación**: `==`, `!=`, `<`, `<=`, `>`, `>=`, `is`, `is not`, `in`, `not in`
7. **Lógicos**: `not`, `and`, `or`

#### Ejemplos de precedencia

```python
# Sin paréntesis - precedencia natural
resultado = 2 + 3 * 4      # 2 + 12 = 14
print(resultado)

# Con paréntesis - cambia la precedencia
resultado = (2 + 3) * 4    # 5 * 4 = 20
print(resultado)

# Expresión compleja
resultado = 2 ** 3 + 4 * 5 - 6 / 2
# Evaluación: 8 + 20 - 3.0 = 25.0
print(resultado)

# Con paréntesis para claridad
resultado = (2 ** 3) + (4 * 5) - (6 / 2)
print(resultado)  # 25.0

# Precedencia con operadores lógicos
edad = 25
activo = True
resultado = edad > 18 and activo or False
# Evaluación: True and True or False = True
print(resultado)

# Mejor con paréntesis para claridad
resultado = (edad > 18 and activo) or False
print(resultado)  # True
```

#### Buenas prácticas con precedencia

```python
# ❌ Confuso sin paréntesis
if x > 0 and y > 0 or z > 0 and w > 0:
    pass

# ✅ Claro con paréntesis
if (x > 0 and y > 0) or (z > 0 and w > 0):
    pass

# ❌ Difícil de leer
precio_final = precio_base + precio_base * impuesto - descuento

# ✅ Más claro
precio_con_impuesto = precio_base + (precio_base * impuesto)
precio_final = precio_con_impuesto - descuento

# O incluso mejor
precio_final = precio_base * (1 + impuesto) - descuento
```

### 3.9. Operadores binarios (avanzado)

Los operadores binarios trabajan a nivel de bits. Son útiles en programación de bajo nivel y algoritmos específicos.

#### Operadores binarios básicos

| Operador | Nombre                   | Descripción                  |
| -------- | ------------------------ | ---------------------------- |
| `&`      | AND binario              | 1 si ambos bits son 1        |
| `\|`     | OR binario               | 1 si al menos un bit es 1    |
| `^`      | XOR binario              | 1 si los bits son diferentes |
| `~`      | NOT binario              | Invierte todos los bits      |
| `<<`     | Desplazamiento izquierda | Desplaza bits a la izquierda |
| `>>`     | Desplazamiento derecha   | Desplaza bits a la derecha   |

#### Ejemplos con operadores binarios

```python
# Números en binario para mejor comprensión
num_binario1 = 0b1010  # 10 en decimal
num_binario2 = 0b1100  # 12 en decimal

print(f"Binario 1: {num_binario1:08b} ({num_binario1})")
print(f"Binario 2: {num_binario2:08b} ({num_binario2})")

# Operaciones binarias
print(f"AND: {num_binario1 & num_binario2:08b} ({num_binario1 & num_binario2})")  # 1000 (8)
print(f"OR:  {num_binario1 | num_binario2:08b} ({num_binario1 | num_binario2})")  # 1110 (14)
print(f"XOR: {num_binario1 ^ num_binario2:08b} ({num_binario1 ^ num_binario2})")  # 0110 (6)

# Desplazamientos
print(f"Despl. izq: {num_binario1 << 1:08b} ({num_binario1 << 1})")  # 10100 (20)
print(f"Despl. der: {num_binario1 >> 1:08b} ({num_binario1 >> 1})")  # 0101 (5)
```

### Resumen del Capítulo

En este capítulo has explorado el rico ecosistema de operadores de Python, desde los aritméticos básicos hasta los binarios avanzados. Has aprendido cómo crear expresiones complejas, las reglas de precedencia que las gobiernan, y las mejores prácticas para escribir código claro y eficiente.

#### 💡 Conceptos Clave:

* **Expresiones**: Combinaciones de valores, variables y operadores que producen un resultado
* **Operadores aritméticos**: `+`, `-`, `*`, `/`, `//`, `%`, `**`
* **Operadores de comparación**: `==`, `!=`, `>`, `<`, `>=`, `<=`, `is`, `is not`
* **Operadores lógicos**: `and`, `or`, `not` con evaluación de cortocircuito
* **Operadores de pertenencia**: `in`, `not in`
* **Precedencia**: Orden de evaluación (paréntesis → potencia → multiplicación/división → suma/resta → comparación → lógicos)
* **Operadores de asignación**: `+=`, `-=`, `*=`, etc.

#### 🤔 Preguntas de Reflexión:

1. ¿Por qué Python tiene dos tipos de división (`/` y `//`) y cuándo usarías cada una?
2. ¿Qué ventajas aporta la evaluación de cortocircuito en operadores lógicos?
3. ¿Cómo pueden los paréntesis mejorar la legibilidad incluso cuando no son necesarios?
4. ¿En qué situaciones prácticas podrías usar el operador módulo (`%`)?

#### 🔧 Ejercicio Práctico:

Crea un programa que:

1. Calcule el IMC (Índice de Masa Corporal) usando operadores aritméticos
2. Determine la categoría usando operadores de comparación y lógicos
3. Verifique si la entrada es válida usando operadores de pertenencia
4. Use operadores de asignación para mantener estadísticas de uso
