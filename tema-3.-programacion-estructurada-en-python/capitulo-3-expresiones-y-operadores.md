# Capítulo 3: Expresiones y operadores

Si las variables y los datos son los ladrillos de un programa, las **expresiones** y los **operadores** son el mortero que los une para construir estructuras lógicas. Una expresión es cualquier combinación de valores, variables y operadores que Python puede evaluar para producir un resultado. Dominar los operadores es esencial para manipular datos, realizar cálculos y tomar decisiones, formando el núcleo de la lógica de cualquier aplicación.

### 3.1. ¿Qué es una expresión?

Las **expresiones** son los bloques de construcción fundamentales de la lógica de un programa. Pueden ser tan simples como un número o tan complejas como una fórmula matemática. Se pueden clasificar en varios tipos como veremos a continuación.

#### Tipos de expresiones

<mark style="background-color:$primary;">**Expresiones literales**</mark>: Valores constantes.

```python
42                    # Expresión literal entera
3.14159              # Expresión literal flotante
"Hola mundo"         # Expresión literal string
True                 # Expresión literal booleana
```

<mark style="background-color:$primary;">**Expresiones con variables**</mark>: Utilizan identificadores que referencian valores.

```python
edad                 # Variable simple
nombre_usuario       # Variable simple
lista[0]            # Acceso a elemento
diccionario["clave"] # Acceso a diccionario
```

<mark style="background-color:$primary;">**Expresiones aritméticas**</mark>: Combinan valores numéricos con operadores matemáticos.

```python
3 + 5                # Suma simple
edad * 2             # Multiplicación con variable
(radio ** 2) * 3.14  # Expresión compleja con paréntesis
```

<mark style="background-color:$primary;">**Expresiones lógicas**</mark>: Se evalúan como `True` o `False` y se usan en estructuras de control.

```python
edad >= 18           # Comparación
activo and verificado # Combinación lógica
not usuario_bloqueado # Negación
```

<mark style="background-color:$primary;">**Expresiones con funciones**</mark>: Incluyen llamadas a funciones que devuelven un valor.

```python
len(lista)           # Función incorporada
max(a, b, c)        # Función con múltiples argumentos
math.sqrt(25)       # Función de módulo
```

***

### 3.2. Operadores Aritméticos

Estos operadores se utilizan para realizar operaciones matemáticas.

| Operador | Nombre              | Ejemplo  | Resultado |
| -------- | ------------------- | -------- | --------- |
| `+`      | Suma                | `3 + 2`  | `5`       |
| `-`      | Resta               | `3 - 2`  | `1`       |
| `*`      | Multiplicación      | `3 * 2`  | `6`       |
| `/`      | División (flotante) | `3 / 2`  | `1.5`     |
| `//`     | División entera     | `3 // 2` | `1`       |
| `%`      | Módulo (resto)      | `3 % 2`  | `1`       |
| `**`     | Potencia            | `3 ** 2` | `9`       |

Es crucial entender la diferencia entre la división flotante (`/`), que siempre devuelve un `float`, y la división entera (`//`), que trunca el resultado hacia el entero inferior más cercano. Con números negativos, `//` redondea "hacia abajo" (hacia menos infinito), por lo que `-10 // 3` es `-4`.

El operador módulo (`%`) es muy útil para tareas como determinar si un número es par o impar: `numero % 2 == 0`.

**Ejemplos básicos**

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

**Ejemplos de divisiones reales y enteras**

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

**Ejemplos de uso del operador módulo (`%`)**

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

***

### 3.3. Operadores de Cadenas

Las cadenas de texto tienen operadores específicos:

* <mark style="background-color:$primary;">**Concatenación**</mark>**&#x20;(`+`)**: Une dos cadenas.
* <mark style="background-color:$primary;">**Repetición**</mark>**&#x20;(`*`)**: Repite una cadena un número determinado de veces.
* <mark style="background-color:$primary;">**Acceso por índice y**</mark><mark style="background-color:$primary;">**&#x20;**</mark>_<mark style="background-color:$primary;">**slicing**</mark>_ **(`[start:end:step]`)**: Permite extraer caracteres o subcadenas. Los índices negativos cuentan desde el final.

**Ejemplos de Concatenación y Repetición**

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

**Ejemplos de accesso por índice y&#x20;**_**slicing**_

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

***

### 3.4. Operadores de Asignación

Los operadores de asignación compuesta son una forma abreviada de modificar el valor de una variable.

| Operador | Equivalente      | Ejemplo   |
| -------- | ---------------- | --------- |
| `+=`     | `x = x + valor`  | `x += 5`  |
| `-=`     | `x = x - valor`  | `x -= 3`  |
| `*=`     | `x = x * valor`  | `x *= 2`  |
| `/=`     | `x = x / valor`  | `x /= 4`  |
| `//=`    | `x = x // valor` | `x //= 2` |
| `%=`     | `x = x % valor`  | `x %= 3`  |
| `**=`    | `x = x ** valor` | `x **= 2` |

**Ejemplos prácticos:**

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

***

### 3.5. Operadores de Comparación y de Identidad

Estos operadores comparan dos valores y devuelven un booleano (`True` o `False`).

#### Operadores de comparación básicos

| Operador | Significado       | Ejemplo  |
| -------- | ----------------- | -------- |
| `==`     | Igual a           | `a == b` |
| `!=`     | Diferente de      | `a != b` |
| `>`      | Mayor que         | `a > b`  |
| `<`      | Menor que         | `a < b`  |
| `>=`     | Mayor o igual que | `a >= b` |
| `<=`     | Menor o igual que | `a <= b` |

**Ejemplos prácticos:**

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
```

#### Operadores de identidad

| Operador | Significado                 | Uso          |
| -------- | --------------------------- | ------------ |
| `is`     | Mismo objeto en memoria     | `a is b`     |
| `is not` | Diferente objeto en memoria | `a is not b` |

Es fundamental distinguir entre igualdad (`==`) e identidad (`is`):

* `==` compara el contenido o valor de los objetos.
* `is` comprueba si dos variables apuntan al mismo objeto en memoria.

**Ejemplos prácticos:**

```python
lista1 = [1, 2, 3]
lista2 = [1, 2, 3]
lista3 = lista1

print(lista1 == lista2)  # True (mismo contenido)
print(lista1 is lista2)  # False (objetos diferentes en memoria)
print(lista1 is lista3)  # True (apuntan al mismo objeto)
```

#### Comparaciones encadenadas

Python también permite encadenar comparaciones de forma muy legible: `18 <= edad <= 65`.

**Ejemplos prácticos:**

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

***

### 3.6. Operadores Lógicos

Los operadores lógicos (`and`, `or`, `not`) se usan para **combinar expresiones booleanas**.

* **`and`**: Devuelve `True` solo si ambos operandos son `True`.
* **`or`**: Devuelve `True` si al menos uno de los operandos es `True`.
* **`not`**: Invierte el valor booleano del operando.

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

**Ejemplos prácticos**

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

Una característica importante es la <mark style="background-color:$primary;">**evaluación de cortocircuito**</mark> (_short-circuit evaluation_). Python evalúa las expresiones lógicas de izquierda a derecha y se detiene tan pronto como conoce el resultado final.

* En una expresión `A and B`, si `A` es `False`, `B` no se evalúa.
* En una expresión `A or B`, si `A` es `True`, `B` no se evalúa.

Esto es útil para evitar errores, como intentar dividir por cero o acceder a un elemento de una lista vacía:

```python
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

***

### 3.7. Operadores de Pertenencia

Los operadores `in` y `not in` comprueban si un elemento existe dentro de una secuencia (como listas, tuplas, cadenas o diccionarios).

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

***

### 3.8. Precedencia de Operadores

La **precedencia de operadores** determina el orden en que se realizan las operaciones en una expresión. La jerarquía, de mayor a menor precedencia, es la siguiente:

1. **Paréntesis:** `()`
2. **Potencia:** `**`
3. **Operadores unarios:** `+x`, `-x`, `not x`
4. **Multiplicación, División, Módulo:** `*`, `/`, `//`, `%`
5. **Suma, Resta:** `+`, `-`
6. **Operadores de comparación, identidad y pertenencia:** `==`, `!=`, `is`, `in`, etc.
7. **Operadores lógicos:** `not`, `and`, `or`

Aunque Python sigue estas reglas de forma predecible, el uso explícito de paréntesis `()` es una marca de profesionalismo. No solo garantiza el orden de evaluación deseado, sino que, más importante aún, elimina la carga cognitiva para quien lee el código. Un código claro y sin ambigüedades previene errores sutiles y es un pilar de la programación defensiva.

**Ejemplos prácticos**

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

***

### 3.9. Operadores Binarios (Avanzado)

Python también incluye operadores a nivel de bits (`&`, `|`, `^`, `~`, `<<`, `>>`) que manipulan números enteros en su representación binaria. Su uso es menos común y se reserva para programación de bajo nivel, optimizaciones específicas o algoritmos criptográficos.

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

***

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

Una vez que dominamos cómo construir expresiones y manipular datos, el siguiente paso lógico es aprender a interactuar con el mundo exterior: recibir información del usuario y mostrarle resultados.

***
