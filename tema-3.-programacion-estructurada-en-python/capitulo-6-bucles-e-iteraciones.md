# Capítulo 6: Bucles e iteraciones

Los **bucles**, o **estructuras iterativas**, son uno de los conceptos más poderosos de la programación. Permiten ejecutar un bloque de código múltiples veces, automatizando tareas repetitivas que serían tediosas o imposibles de escribir manualmente. Su papel es fundamental para procesar colecciones de datos, implementar algoritmos y crear programas dinámicos y eficientes.

&#x20;En Python disponemos de dos tipos principales de bucles: `while` y `for`, cada uno optimizado para diferentes tipos de situaciones. Además, Python proporciona sentencias de control (`break`, `continue`, `pass`) y características avanzadas como la cláusula `else` que hacen de la iteración una herramienta extremadamente poderosa y flexible.

***

### 6.1. ¿Cuándo necesitamos repetir código?

Los bucles son esenciales en situaciones como:

* **Procesamiento de datos**: Analizar cada elemento de una lista de ventas
* **Validación de entrada**: Seguir pidiendo datos hasta que sean válidos
* **Algoritmos matemáticos**: Calcular factoriales, series, aproximaciones
* **Interfaces de usuario**: Mostrar menús hasta que el usuario elija salir
* **Automatización**: Realizar la misma operación sobre múltiples archivos

Sin bucles, tendríamos que escribir código repetitivo y limitado:

```python
#Sin bucles: código repetitivo y limitado
print("Número 1")
print("Número 2")
print("Número 3")
print("Número 4")
print("Número 5")

#Con bucles: código limpio y flexible
for i in range(1, 6): print(f"Número {i}")
```

***

### 6.2. Bucle `while`: Repetición condicional

El bucle **`while`** ejecuta un bloque de código **mientras** una condición especificada sea `True`. Es la herramienta ideal cuando <mark style="background-color:yellow;">**no se conoce de antemano el número exacto de iteraciones que se deben realizar**</mark>.

La estructura es simple, pero requiere una atención crucial: **la condición de control debe modificarse dentro del bucle** para que, eventualmente, se vuelva `False`. De lo contrario, se creará un bucle infinito que bloqueará el programa.

#### Sintaxis básica

```python
while condicion:
    # Código que se repite
    instrucciones()
    # IMPORTANTE: modificar la condición para evitar bucle infinito
```

#### Ejemplo básico

```python
contador = 1
while contador <= 5:
    print(f"Iteración número {contador}")
    contador += 1 # CRUCIAL: modificar la variable de control
```

Un caso de uso principal del bucle `while` es la validación de la entrada del usuario, donde se le solicita un dato repetidamente hasta que introduce uno válido.

```python
def pedir_edad():
    """Pide la edad hasta obtener un valor válido."""
    while True:
        try:
            edad = int(input("¿Cuál es tu edad? "))
            if 0 <= edad <= 120:
                return edad
            else:
                print("La edad debe estar entre 0 y 120 años")
        except ValueError:
            print("Por favor, introduce un número válido")

edad_usuario = pedir_edad()
print(f"Tu edad es: {edad_usuario}")
```

***

### 6.3. Bucle `for`: Iteración sobre secuencias

El bucle `for` está diseñado para **iterar sobre los elementos de una secuencia** (como una lista, tupla, cadena de texto, o un `range`). Es la opción preferida cuando **se conoce el número de iteraciones** o cuando se desea procesar cada elemento de una colección.

* <mark style="background-color:$primary;">**Iterar con**</mark><mark style="background-color:$primary;">**&#x20;**</mark><mark style="background-color:$primary;">**`range()`**</mark>**:** Para ejecutar un bloque un número específico de veces.
* **I**<mark style="background-color:$primary;">**terar sobre una lista**</mark>**:** Se puede acceder directamente a cada elemento. Para obtener tanto el índice como el valor, se utiliza la función `enumerate()`.
* <mark style="background-color:$primary;">**Iterar sobre una cadena**</mark>**:** Procesa la cadena carácter por carácter.
* <mark style="background-color:$primary;">**Iterar sobre un diccionario**</mark>**:** Por defecto, itera sobre las claves. Para iterar sobre valores o pares clave-valor, se usan los métodos `.values()` y `.items()`.

#### Sintaxis básica

```python
for elemento in secuencia:
    # Código que se ejecuta para cada elemento
    procesar(elemento)
```

#### For con `range()`

```python
# Números del 0 al 4
for i in range(5):
    print(i)

# Números del 1 al 5
for i in range(1, 6):
    print(i)

# Números del 2 al 10, de 2 en 2
for i in range(2, 11, 2):
    print(i)  # 2, 4, 6, 8, 10
```

#### For con `listas`

```python
# Iterar directamente sobre elementos
frutas = ["manzana", "banana", "naranja", "kiwi"]
for fruta in frutas:
    print(f"Me gusta la {fruta}")

# Obtener índice y elemento con enumerate()
for indice, fruta in enumerate(frutas):
    print(f"{indice + 1}. {fruta}")

# Iterar solo sobre índices
for i in range(len(frutas)):
    print(f"La fruta en posición {i} es {frutas[i]}")
```

#### For con `strings`

```python
palabra = "Python"
for letra in palabra:
    print(f"Letra: {letra}")

# Contar vocales
vocales = "aeiou"
palabra = "programación"
contador_vocales = 0

for letra in palabra:
    if letra.lower() in vocales:
        contador_vocales += 1

print(f"'{palabra}' tiene {contador_vocales} vocales")
```

#### For con `diccionarios`

```python
estudiante = {
    "nombre": "Ana",
    "edad": 22,
    "carrera": "Informática",
    "promedio": 8.5
}

# Iterar sobre claves
for clave in estudiante:
    print(f"{clave}: {estudiante[clave]}")

# Iterar sobre valores
for valor in estudiante.values():
    print(valor)

# Iterar sobre claves y valores
for clave, valor in estudiante.items():
    print(f"{clave.upper():<10} {valor}")
```

***

### 6.4. Sentencias de control de bucles

Python ofrece sentencias para controlar el flujo de ejecución dentro de un bucle:

* **`break`**: Termina el bucle de forma inmediata y prematura. El programa continúa con la primera instrucción después del bucle.
* **`continue`**: Salta el resto del código de la iteración actual y pasa directamente a la siguiente iteración.
* **`pass`**: Es una instrucción nula. No hace nada y se utiliza como un marcador de posición (_placeholder_) donde sintácticamente se requiere una instrucción, pero no se quiere ejecutar ningún código.

#### Ejemplo de uso de `break`

```python
# Buscar un elemento específico
numeros = [1, 3, 7, 12, 18, 25, 30]
objetivo = 18

for i, numero in enumerate(numeros):
    print(f"Revisando posición {i}: {numero}")
    if numero == objetivo:
        print(f"¡Encontrado! {objetivo} está en la posición {i}")
        break
else:
    print(f"No se encontró {objetivo}")
```

#### Ejemplo de uso de `continue`

```python
# Procesar solo números pares
numeros = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

print("Números pares y sus cuadrados:")
for numero in numeros:
    if numero % 2 != 0:  # Si es impar
        continue  # Saltar al siguiente número
    
    cuadrado = numero ** 2
    print(f"{numero}² = {cuadrado}")
```

#### Ejemplo de uso de `pass`

```python
# Placeholder durante desarrollo
for i in range(5):
    if i < 3:
        pass  # TODO: Implementar lógica aquí
    else:
        print(f"Procesando: {i}")

# Manejo temporal de excepciones
def funcion_en_desarrollo():
    try:
        resultado = operacion_compleja()
        return resultado
    except:
        pass  # Por ahora, ignorar errores
```

#### Cláusula `else` en bucles

Una característica particular de Python es la cláusula `else` en los bucles. El bloque de código `else` <mark style="background-color:yellow;">**se ejecuta solo si el bucle finaliza de forma natural**</mark>, es decir, sin haber sido interrumpido por una sentencia `break`. Es ideal para código que debe ejecutarse cuando una búsqueda no tiene éxito.

```python
def buscar_numero(lista, objetivo):
    """Busca un número en una lista e informa si no lo encuentra."""
    for numero in lista:
        if numero == objetivo:
            print(f"Encontrado: {objetivo}")
            break
    else:
        # Se ejecuta solo si el bucle for termina sin un break
        print(f"No se encontró: {objetivo}")

numeros = [1, 3, 5, 7, 9]
buscar_numero(numeros, 5) # Salida: Encontrado: 5
buscar_numero(numeros, 6) # Salida: No se encontró: 6
```

***

### 6.5. Bucles anidados

Un bucle anidado es **un bucle dentro de otro**. Son útiles para trabajar con estructuras de datos bidimensionales, como matrices (listas de listas), o para generar patrones como las tablas de multiplicar. Es importante usarlos con precaución, ya que su complejidad computacional puede crecer rápidamente y afectar al rendimiento.

```python
# Tabla de multiplicar completa
print("TABLAS DE MULTIPLICAR (1-5)")
print("="*50)

for tabla in range(1, 6):
    print(f"\nTabla del {tabla}:")
    for multiplicador in range(1, 11):
        resultado = tabla * multiplicador
        print(f"  {tabla} × {multiplicador:2d} = {resultado:2d}")
```

***

### 6.6. Técnicas avanzadas con bucles

#### Comprensión de listas (List Comprehensions)

La **comprensión de listas** (_list comprehensions_) es una sintaxis elegante y "pythónica" para **crear listas de forma concisa y eficiente a partir de un iterable**.&#x20;

**Sintaxis básica**

```python
[expresion for item in iterable if condicion]
```

**Ejemplo de uso**

```python
# Forma tradicional
cuadrados = []
for x in range(10):
    cuadrados.append(x ** 2)

# List comprehension (más pythónica)
cuadrados = [x ** 2 for x in range(10)]
print(cuadrados)  # [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

# Con condición
pares = [x for x in range(20) if x % 2 == 0]
print(pares)  # [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]

# Procesamiento de strings
palabras = ["python", "java", "javascript", "go"]
palabras_largas = [palabra.upper() for palabra in palabras if len(palabra) > 4]
print(palabras_largas)  # ['PYTHON', 'JAVASCRIPT']
```

#### Función  `enumerate()`

Permite **recorrer una secuencia (lista, tupla, cadena, etc.) obteniendo a la vez el índice y el valor** de cada elemento.\
Es una alternativa más limpia y legible que usar un contador manual.

**Sintaxis:**

```python
for indice, elemento in enumerate(iterable, inicio=0):
    ...
```

* `iterable`: la secuencia a recorrer.
* `inicio`: (opcional) valor inicial del índice (por defecto `0`).

**Ejemplo:**

```python
nombres = ["Ana", "Luis", "María"]
for i, nombre in enumerate(nombres, start=1):
    print(f"{i}. {nombre}")
```

**Salida:**

```
1. Ana
2. Luis
3. María
```

{% hint style="success" %}
**Ventaja:** evita crear variables como `contador = 0` y mantenerlas manualmente.
{% endhint %}

#### Función  `zip()`

Permite **combinar dos o más secuencias** en una sola, agrupando los elementos que ocupan la misma posición. El resultado es un _iterador de tuplas_.

**Sintaxis:**

```python
for elem1, elem2, ... in zip(iterable1, iterable2, ...):
    ...
```

**Ejemplo:**

```python
nombres = ["Ana", "Luis", "María"]
edades = [23, 31, 19]

for nombre, edad in zip(nombres, edades):
    print(f"{nombre} tiene {edad} años.")
```

**Salida:**

```
Ana tiene 23 años.
Luis tiene 31 años.
María tiene 19 años.
```

<mark style="background-color:yellow;">💡</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">**Notas:**</mark>

* `zip()` se detiene cuando una de las listas termina.
*   Puedes convertir el resultado en lista:

    ```python
    list(zip(nombres, edades))
    # [('Ana', 23), ('Luis', 31), ('María', 19)]
    ```

#### **Combinando `enumerate()` y `zip()`**

Puedes usar `enumerate()` y `zip()` juntos para recorrer **varias secuencias con índices**:

```python
for i, (nombre, edad) in enumerate(zip(nombres, edades), start=1):
    print(f"{i}. {nombre} ({edad} años)")
```

**Salida:**

```
1. Ana (23 años)
2. Luis (31 años)
3. María (19 años)
```

***

### 6.7. Caso práctico: Simulador de cajero automático

Este ejemplo completo integra bucles `while`, condicionales `if-elif-else`, manejo de entrada y formateo de salida para simular un cajero automático simple.

```python
def cajero_automatico():
    """Simula un cajero automático simple."""
    saldo = 1000.0
    historial = []
    
    while True:
        print(f"\nCAJERO AUTOMÁTICO")
        print(f"Saldo actual: {saldo:.2f}€")
        print("="*30)
        print("1. Consultar saldo")
        print("2. Retirar dinero")
        print("3. Depositar dinero")
        print("4. Ver historial")
        print("5. Salir")
        print("-"*30)
        opcion = input("Selecciona una opción: ").strip()
        
        if opcion == "1":
            print(f"Tu saldo es: {saldo:.2f}€")
        elif opcion == "2":
            try:
                cantidad = float(input("Cantidad a retirar: "))
                if 0 < cantidad <= saldo:
                    saldo -= cantidad
                    historial.append(f"Retiro: -{cantidad:.2f}€")
                    print(f"Has retirado {cantidad:.2f}€")
                else:
                    print("Cantidad inválida o saldo insuficiente")
            except ValueError:
                print("Cantidad inválida")
        elif opcion == "3":
            try:
                cantidad = float(input("Cantidad a depositar: "))
                if cantidad > 0:
                    saldo += cantidad
                    historial.append(f"Depósito: +{cantidad:.2f}€")
                    print(f"Has depositado {cantidad:.2f}€")
                else:
                    print("La cantidad debe ser positiva")
            except ValueError:
                print("Cantidad inválida")
        elif opcion == "4":
            if historial:
                print("HISTORIAL DE TRANSACCIONES:")
                for transaccion in historial:
                    print(f" • {transaccion}")
            else:
                print("No hay transacciones")
        elif opcion == "5":
            print("¡Gracias por usar nuestro cajero!")
            break
        else:
            print("Opción no válida")
```

***

### Resumen del Capítulo

Los bucles son herramientas fundamentales que permiten automatizar tareas repetitivas y procesar colecciones de datos de manera eficiente. Has aprendido a usar `while` para repeticiones condicionales, `for` para iterar sobre secuencias, y las sentencias de control que proporcionan flexibilidad avanzada en el manejo del flujo de iteración.

#### 💡 Conceptos Clave:

* **while**: Repetición mientras una condición sea verdadera
* **for**: Iteración sobre secuencias (listas, strings, ranges, etc.)
* **break**: Termina el bucle inmediatamente
* **continue**: Salta a la siguiente iteración
* **pass**: Instrucción vacía (placeholder)
* **else en bucles**: Se ejecuta si el bucle termina normalmente
* **enumerate()**: Obtiene índice y elemento simultáneamente
* **zip()**: Itera múltiples secuencias en paralelo

#### 🤔 Preguntas de Reflexión:

1. ¿Cuándo es preferible usar `while` en lugar de `for`?
2. ¿Qué problemas puede causar el uso incorrecto de `break` y `continue`?
3. ¿En qué situaciones es útil la cláusula `else` de los bucles?
4. ¿Cómo puedes evitar bucles infinitos en código de producción?

#### 🔧 Ejercicio Práctico:

Crea un programa que:

1. Implemente un sistema de gestión de tareas con menú interactivo
2. Use `while` para el bucle principal y validación de entrada
3. Use `for` para mostrar listas de tareas y estadísticas
4. Implemente búsqueda con `break` y filtrado con `continue`
5. Use bucles anidados para organizar tareas por categorías

Ahora que sabemos cómo repetir acciones, podemos explorar la "caja de herramientas" que Python nos ofrece de serie: un conjunto de funciones integradas que facilitan y potencian el trabajo con bucles, iterables y otros tipos de datos.

***
