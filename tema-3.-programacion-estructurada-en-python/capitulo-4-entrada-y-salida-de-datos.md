# Capítulo 4: Entrada y salida de datos

La comunicación entre un programa y el usuario es el pilar de cualquier aplicación interactiva. Sin la capacidad de **recibir datos** y **mostrar resultados**, un programa sería una caja negra aislada. Python proporciona dos funciones integradas, **`input()`** y **`print()`**, que actúan como las herramientas clave para gestionar esta comunicación a través de la consola, permitiendo un diálogo fluido y efectivo.

### 4.1. Función `input()`: lectura de datos

La función **`input()`** es el mecanismo principal para obtener datos del usuario durante la ejecución del programa. Su funcionamiento es simple pero tiene una característica fundamental que siempre debe tenerse en cuenta: <mark style="background-color:yellow;">**siempre devuelve una cadena de texto (**</mark><mark style="background-color:yellow;">**`str`**</mark><mark style="background-color:yellow;">**)**</mark>, sin importar lo que el usuario escriba.

#### Sintaxis básica de `input()`

```python
variable = input("Mensaje para el usuario: ")
```

#### Características fundamentales

<mark style="background-color:$primary;">**Siempre devuelve string**</mark>: Independientemente de lo que introduzca el usuario, `input()` siempre devuelve un objeto de tipo `str`.

```python
nombre = input("¿Cuál es tu nombre? ")
print(f"Tipo: {type(nombre)}")  # <class 'str'>
print(f"Valor: {nombre}")

edad_str = input("¿Cuántos años tienes? ")
print(f"Tipo: {type(edad_str)}")  # <class 'str'> (aunque introduzcas un número)
print(f"Valor: {edad_str}")
```

<mark style="background-color:$primary;">**Acepta un mensaje opcional**</mark>: El parámetro es opcional, pero es fundamental para la usabilidad.

```python
# Con mensaje (recomendado)
nombre = input("Introduce tu nombre: ")

# Sin mensaje (no recomendado)
edad = input()  # El usuario no sabe qué introducir
```

<mark style="background-color:$primary;">**Finaliza con Enter**</mark>: La entrada se completa cuando el usuario presiona la tecla Enter.

#### Ejemplos prácticos básicos

```python
# Información personal básica
nombre = input("¿Cuál es tu nombre? ")
ciudad = input("¿De qué ciudad eres? ")
hobby = input("¿Cuál es tu hobby favorito? ")

print(f"Hola {nombre}, qué interesante que vivas en {ciudad}")
print(f"Me parece genial que te guste {hobby}")

# Entrada de múltiples líneas
print("Cuéntame sobre ti (presiona Enter cuando termines):")
descripcion = input()
print(f"Gracias por compartir: {descripcion}")
```

{% hint style="warning" %}
Un <mark style="background-color:$warning;">**problema común**</mark> es que los usuarios pueden introducir **espacios en blanco al principio o al final** de su respuesta. Esto se puede solucionar fácilmente usando el método **`.strip()`** para limpiar la cadena de entrada.
{% endhint %}

```python
# ❌ Problema: espacios no deseados
nombre = input("Tu nombre: ")  # Usuario introduce "  Ana  "
print(f"Hola '{nombre}'")     # Hola '  Ana  '

# ✅ Solución: usar strip()
nombre = input("Tu nombre: ").strip()
print(f"Hola '{nombre}'")     # Hola 'Ana'
```

***

### 4.2. Conversión de tipos en la entrada

Dado que `input()` devuelve una cadena, si necesitamos realizar operaciones numéricas, es imprescindible convertir el valor a un tipo de dato apropiado, como `int` (entero) o `float` (decimal).

```python
# Convertir a entero
edad_str = input("¿Cuántos años tienes? ")
edad = int(edad_str)
print(f"El próximo año tendrás {edad + 1} años.")

# Convertir a decimal (más común hacerlo en una sola línea)
precio = float(input("Introduce el precio del producto: "))
precio_con_iva = precio * 1.21
```

{% hint style="warning" %}
Esta conversión puede fallar. Si el usuario introduce texto en lugar de un número, el programa se detendrá con un error **`ValueError`**. La forma robusta y profesional de manejar esta situación es utilizando una **estructura `try-except`**. Para facilitar esta tarea, podemos crear una función auxiliar reutilizable.
{% endhint %}

```python
def input_numerico(mensaje, tipo=int, minimo=None, maximo=None):
    """
    Solicita entrada numérica con validación.
    Args:
        mensaje (str): Mensaje a mostrar al usuario
        tipo (type): int o float
        minimo (number): Valor mínimo permitido
        maximo (number): Valor máximo permitido
    Returns:
        number: El número validado del tipo especificado
    """
    while True:
        try:
            valor = tipo(input(mensaje))
            if minimo is not None and valor < minimo:
                print(f"El valor debe ser mayor o igual a {minimo}")
                continue
            if maximo is not None and valor > maximo:
                print(f"El valor debe ser menor o igual a {maximo}")
                continue
            return valor
        except ValueError:
            tipo_nombre = "entero" if tipo == int else "decimal"
            print(f"Por favor, introduce un número {tipo_nombre} válido")

# Uso de la función
edad = input_numerico("Tu edad (0-120): ", int, 0, 120)
salario = input_numerico("Tu salario: ", float, 0)
```

***

### 4.3. Función `print()`: escritura y formateo

La función **`print()`** es la herramienta estándar para mostrar información en la consola. Es más versátil de lo que parece, gracias a sus parámetros opcionales:

* <mark style="background-color:$primary;">**Múltiples valores**</mark>: Se pueden pasar varios argumentos separados por comas, y `print()` los mostrará en una misma línea.
* <mark style="background-color:$primary;">**Parámetro**</mark><mark style="background-color:$primary;">**&#x20;**</mark><mark style="background-color:$primary;">**`sep`**</mark>: Permite personalizar el separador que se utiliza entre los argumentos (por defecto es un espacio).
* <mark style="background-color:$primary;">**Parámetro**</mark><mark style="background-color:$primary;">**&#x20;**</mark><mark style="background-color:$primary;">**`end`**</mark>: Permite cambiar el carácter que se añade al final de la línea (por defecto es un salto de línea `\n`).
* <mark style="background-color:$primary;">**Parámetro**</mark><mark style="background-color:$primary;">**&#x20;**</mark><mark style="background-color:$primary;">**`flush`**</mark>: Por defecto, Python **almacena en un buffer** lo que se imprime y lo envía de manera automática cuando corresponde. Esto puede causar que veas retraso en la salida en ciertos casos, especialmente en programas que imprimen en **tiempo real** o trabajan con **archivos y tuberías**.
  * `flush=False` → No fuerza el vaciado del buffer. La salida puede retrasarse.
  * `flush=True` → Fuerza que todo lo que se ha enviado a `print` se muestre inmediatamente.

#### Sintaxis y parámetros de `print()`

```python
print(*values, sep=' ', end='\n', file=sys.stdout, flush=False)
```

#### Parámetros principales

<mark style="background-color:$primary;">**Múltiples valores**</mark>: Puedes pasar varios argumentos

```python
nombre = "Ana"
edad = 25
ciudad = "Madrid"

print(nombre, edad, ciudad)  # Ana 25 Madrid
print("Nombre:", nombre, "Edad:", edad)  # Nombre: Ana Edad: 25
```

<mark style="background-color:$primary;">**Separador personalizado**</mark>**&#x20;(`sep`)**:

```python
print("Python", "Java", "C++", sep=", ")  # Python, Java, C++
print("2024", "10", "15", sep="-")        # 2024-10-15
print("A", "B", "C", sep="")              # ABC
print("X", "Y", "Z", sep=" -> ")          # X -> Y -> Z
```

<mark style="background-color:$primary;">**Final personalizado**</mark>**&#x20;(`end`)**:

```python
# Por defecto, print() añade un salto de línea
print("Primera línea")
print("Segunda línea")

# Cambiar el final
print("Sin salto ", end="")
print("de línea")  # Sin salto de línea

print("Cargando", end="")
for i in range(3):
    print(".", end="", flush=True)
print(" ¡Completado!")  # Cargando... ¡Completado!
```

<mark style="background-color:$primary;">**Flush inmediato**</mark>:

```python
import time

# Para efectos de escritura en tiempo real
for i in range(1, 6):
    print(f"Contador: {i}", end="\r", flush=True)  # Sobrescribe la línea
    time.sleep(1)
print("¡Terminado!")
```

***

### 4.4. Formateo avanzado de cadenas con f-strings

A partir de Python 3.6, las <mark style="background-color:$primary;">**f-strings**</mark> (cadenas literales formateadas) se han convertido en el método preferido para formatear cadenas. Son legibles, concisas y potentes. Se definen prefijando la cadena con la letra `f` o `F`.

Las f-strings permiten:

* **Incrustar variables y expresiones** directamente dentro de llaves `{}`.
* **Formatear números** con gran precisión.
* **Alinear y rellenar** el texto.
* **Usar separadores de miles** para mejorar la legibilidad de números grandes.

Aunque existen métodos más antiguos como `.format()` y el operador `%`, las <mark style="background-color:$primary;">**f-strings son la opción recomendada**</mark> para todo código nuevo por su claridad y eficiencia.

#### **Sintaxis básica**

```python
nombre = "Ana"
edad = 25

# Básico
mensaje = f"Hola, me llamo {nombre} y tengo {edad} años"
print(mensaje)

# Con expresiones
print(f"El próximo año tendré {edad + 1} años")
print(f"Mi nombre en mayúsculas: {nombre.upper()}")
```

#### **Formateo numérico**

```python
numero = 666
pi = 3.141592653589793

# Números enteros
print(f"Número: {numero}")           # Número: 666
print(f"Binario: {numero:b}")        # Binario: 1010011010
print(f"Hexadecimal: {numero:x}")    # Hexadecimal: 29a
print(f"Octal: {numero:o}")          # Octal: 1232

# Números decimales
print(f"Pi: {pi:.2f}")               # Pi: 3.14
print(f"Pi científico: {pi:.2e}")    # Pi científico: 3.14e+00
print(f"Pi porcentaje: {pi:.1%}")    # Pi porcentaje: 314.2%
```

#### **Alineación y relleno**

```python
texto = "Python"
numero = 42

# Alineación
print(f"|{texto:<20}|")    # |Python              | (izquierda)
print(f"|{texto:>20}|")    # |              Python| (derecha)  
print(f"|{texto:^20}|")    # |       Python       | (centrado)

# Relleno personalizado
print(f"|{texto:=^20}|")   # |=======Python=======|
print(f"|{numero:0>10}|")  # |0000000042|
print(f"|{numero:*^10}|")  # |****42****|
```

#### **Formateo con separadores de miles**

```python
poblacion = 47500000
precio = 1234.56

print(f"Población: {poblacion:,}")      # Población: 47,500,000
print(f"Precio: {precio:,.2f}€")        # Precio: 1,234.56€

# Separador personalizado (Python 3.1+)
import locale
locale.setlocale(locale.LC_ALL, '')
print(f"Precio local: {precio:n}€")     # Depende del locale del sistema
```

#### Ejemplos prácticos de formateo

```python
# Factura
def mostrar_factura(cliente, productos):
    total = sum(precio * cantidad for _, precio, cantidad in productos)
    
    print("=" * 50)
    print(f"{'FACTURA':^50}")
    print("=" * 50)
    print(f"Cliente: {cliente}")
    print("-" * 50)
    
    for nombre, precio, cantidad in productos:
        subtotal = precio * cantidad
        print(f"{nombre:<20} {precio:>8.2f}€ x {cantidad:>2} = {subtotal:>8.2f}€")
    
    print("-" * 50)
    print(f"{'TOTAL:':<37} {total:>8.2f}€")
    print("=" * 50)

# Uso
productos = [
    ("Laptop Dell XPS", 1299.99, 1),
    ("Mouse inalámbrico", 35.50, 2),
    ("Teclado mecánico", 89.99, 1)
]

mostrar_factura("Ana García", productos)
```

**Salida en consola:**

```
==================================================
                     FACTURA
==================================================
Cliente: Ana García
--------------------------------------------------
Laptop Dell XPS       1299.99€ x  1 =  1299.99€
Mouse inalámbrico       35.50€ x  2 =    71.00€
Teclado mecánico        89.99€ x  1 =    89.99€
--------------------------------------------------
TOTAL:                                 1460.98€
==================================================
```

#### Tabla de especificadores de formato

| Especificador | Descripción                      | Ejemplo                        |
| ------------- | -------------------------------- | ------------------------------ |
| `d`           | Entero decimal                   | `f"{42:d}"` → `"42"`           |
| `b`           | Binario                          | `f"{42:b}"` → `"101010"`       |
| `o`           | Octal                            | `f"{42:o}"` → `"52"`           |
| `x`           | Hexadecimal (minúsculas)         | `f"{42:x}"` → `"2a"`           |
| `X`           | Hexadecimal (mayúsculas)         | `f"{42:X}"` → `"2A"`           |
| `f`           | Punto flotante                   | `f"{3.14:.2f}"` → `"3.14"`     |
| `e`           | Notación científica (minúsculas) | `f"{1234:.2e}"` → `"1.23e+03"` |
| `E`           | Notación científica (mayúsculas) | `f"{1234:.2E}"` → `"1.23E+03"` |
| `%`           | Porcentaje                       | `f"{0.75:.1%}"` → `"75.0%"`    |
| `c`           | Carácter                         | `f"{65:c}"` → `"A"`            |
| `s`           | String                           | `f"{'texto':s}"` → `"texto"`   |

#### Métodos alternativos (_legacy_)

**Método `.format()` (**_**Python 2.6+**_**)**

```python
# Aún funcional pero menos recomendado
nombre = "Ana"
edad = 25

mensaje = "Hola, me llamo {} y tengo {} años".format(nombre, edad)
print(mensaje)

# Con índices
mensaje = "Hola, me llamo {0} y tengo {1} años. {0} es un buen nombre".format(nombre, edad)
print(mensaje)

# Con nombres
mensaje = "Hola, me llamo {nom} y tengo {ed} años".format(nom=nombre, ed=edad)
print(mensaje)
```

**Formateo `%` (estilo C) -&#x20;**<mark style="background-color:$danger;">**Desaconsejado**</mark>

```python
# Método antiguo, evitar en código nuevo
nombre = "Ana"
edad = 25

mensaje = "Hola, me llamo %s y tengo %d años" % (nombre, edad)
print(mensaje)
```

***

### 4.5. Caso práctico: Calculadora interactiva

El siguiente ejemplo integra `input()`, `print()` y la conversión de tipos para crear una calculadora funcional que se ejecuta en la consola.

```python
def calculadora():
    """Calculadora interactiva con interfaz amigable."""
    print("=" * 40)
    print(" CALCULADORA PYTHON")
    print("=" * 40)
    while True:
        try:
            # Entrada de datos
            num1 = float(input("Primer número: "))
            operador = input("Operador (+, -, *, /, **): ").strip()
            num2 = float(input("Segundo número: "))
            
            # Cálculo
            if operador == "+":
                resultado = num1 + num2
            elif operador == "-":
                resultado = num1 - num2
            elif operador == "*":
                resultado = num1 * num2
            elif operador == "/":
                if num2 == 0:
                    print("❌ Error: División por cero")
                    continue
                resultado = num1 / num2
            elif operador == "**":
                resultado = num1 ** num2
            else:
                print("❌ Operador no válido")
                continue
            
            # Salida formateada
            print(f"\n✅ Resultado: {num1} {operador} {num2} = {resultado:.6g}")
            
            # Continuar o salir
            if input("\n¿Otra operación? (s/n): ").lower().startswith('n'):
                break
        except ValueError:
            print("❌ Error: Introduce números válidos")
        except KeyboardInterrupt:
            print("\n\n👋 ¡Hasta luego!")
            break
```

***

### Resumen del Capítulo

En este capítulo has dominado las herramientas fundamentales para la interacción con el usuario en Python. La función `input()` te permite recopilar información, mientras que `print()` y las f-strings te dan un control total sobre la presentación de datos. Estas habilidades son esenciales para crear aplicaciones interactivas y profesionales.

#### 💡 Conceptos Clave:

* **`input()`**: Siempre devuelve string, requiere conversión para otros tipos
* **Conversión de tipos**: `int()`, `float()`, validación con try-except
* **`print()`**: Parámetros `sep`, `end`, `flush` para control avanzado
* **F-strings**: Método moderno y potente para formateo de cadenas
* **Especificadores de formato**: Control preciso sobre números, alineación y relleno
* **Validación de entrada**: Esencial para aplicaciones robustas

#### 🤔 Preguntas de Reflexión:

1. ¿Por qué `input()` devuelve siempre string y no intenta detectar automáticamente el tipo?
2. ¿Qué ventajas ofrecen las f-strings frente a los métodos de formateo anteriores?
3. ¿Cómo puedes mejorar la experiencia de usuario al solicitar datos de entrada?
4. ¿En qué situaciones es importante el parámetro `flush=True` en `print()`?

#### 🔧 Ejercicio Práctico:

Crea un programa que:

1. Solicite datos personales (nombre, edad, salario) con validación
2. Calcule impuestos basados en tramos
3. Muestre una nómina formateada profesionalmente
4. Permita guardar múltiples empleados y mostrar estadísticas

Con la capacidad de recibir datos del usuario y presentarle resultados formateados, nuestros programas ya pueden interactuar con el mundo. El siguiente paso es dotarlos de inteligencia para que puedan tomar decisiones basadas en esa información, lo que nos lleva a las estructuras condicionales.

***
