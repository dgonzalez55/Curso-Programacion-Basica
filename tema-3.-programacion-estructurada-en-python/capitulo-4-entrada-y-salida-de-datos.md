# Capítulo 4: Entrada y salida de datos

La comunicación entre el programa y el usuario es fundamental en cualquier aplicación. Python proporciona funciones integradas simples pero potentes para gestionar tanto la **entrada de datos** (lo que el usuario introduce) como la **salida de datos** (lo que el programa muestra). En este capítulo exploraremos las funciones `input()` y `print()`, técnicas de formateo avanzado, conversión de tipos, y buenas prácticas para crear interfaces de usuario claras e intuitivas.

La gestión adecuada de entrada y salida no solo hace que nuestros programas sean funcionales, sino también profesionales y fáciles de usar.

### 4.1. Función input(): lectura de datos

La función **`input()`** es la herramienta principal para recopilar información del usuario durante la ejecución del programa. Esta función siempre devuelve una **cadena de texto (string)**, independientemente de lo que el usuario introduzca.

#### Sintaxis básica de input()

```python
variable = input("Mensaje para el usuario: ")
```

#### Características fundamentales

**1. Siempre devuelve string**: Independientemente de lo que introduzca el usuario, `input()` siempre devuelve un objeto de tipo `str`.

```python
nombre = input("¿Cuál es tu nombre? ")
print(f"Tipo: {type(nombre)}")  # <class 'str'>
print(f"Valor: {nombre}")

edad_str = input("¿Cuántos años tienes? ")
print(f"Tipo: {type(edad_str)}")  # <class 'str'> (aunque introduzcas un número)
print(f"Valor: {edad_str}")
```

**2. Acepta un mensaje opcional**: El parámetro es opcional, pero es fundamental para la usabilidad.

```python
# Con mensaje (recomendado)
nombre = input("Introduce tu nombre: ")

# Sin mensaje (no recomendado)
edad = input()  # El usuario no sabe qué introducir
```

**3. Finaliza con Enter**: La entrada se completa cuando el usuario presiona la tecla Enter.

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

#### Problemas comunes y soluciones

**Problema**: Usuario introduce espacios al principio o final

```python
# ❌ Problema: espacios no deseados
nombre = input("Tu nombre: ")  # Usuario introduce "  Ana  "
print(f"Hola '{nombre}'")     # Hola '  Ana  '

# ✅ Solución: usar strip()
nombre = input("Tu nombre: ").strip()
print(f"Hola '{nombre}'")     # Hola 'Ana'
```

**Problema**: Entrada vacía

```python
# ❌ Sin validación
nombre = input("Tu nombre: ")
if nombre == "":
    print("No has introducido nada")

# ✅ Con validación mejorada
nombre = input("Tu nombre: ").strip()
if not nombre:  # Más pythónico
    print("El nombre no puede estar vacío")
else:
    print(f"Hola, {nombre}")
```

### 4.2. Conversión de tipos a la entrada

Dado que `input()` siempre devuelve strings, necesitamos convertir los datos al tipo apropiado para poder operar con ellos.

#### Conversiones básicas

**Convertir a entero (int)**

```python
# Conversión básica
edad_str = input("¿Cuántos años tienes? ")
edad = int(edad_str)
print(f"En 10 años tendrás {edad + 10} años")

# Conversión directa (más común)
edad = int(input("¿Cuántos años tienes? "))
print(f"En 10 años tendrás {edad + 10} años")
```

**Convertir a decimal (float)**

```python
# Para números con decimales
precio = float(input("¿Cuál es el precio del producto? "))
descuento = float(input("¿Qué descuento aplicar (0-100)? "))

precio_final = precio * (1 - descuento / 100)
print(f"El precio final es: {precio_final:.2f}€")
```

**Convertir a booleano (bool)**

```python
# Conversión a booleano (cuidado: casi todo es True en Python)
respuesta = bool(input("¿Estás de acuerdo? (escribe algo para sí): "))
print(f"Tu respuesta es: {respuesta}")

# Mejor: conversión personalizada
def convertir_a_booleano(texto):
    texto = texto.lower().strip()
    return texto in ['si', 'sí', 'yes', 'y', 'true', '1']

respuesta_str = input("¿Estás de acuerdo? (sí/no): ")
respuesta = convertir_a_booleano(respuesta_str)
print(f"Tu respuesta es: {respuesta}")
```

#### Manejo de errores en conversiones

```python
# ❌ Sin manejo de errores (puede fallar)
edad = int(input("Tu edad: "))  # Error si el usuario introduce "veinte"

# ✅ Con manejo de errores
def solicitar_edad():
    while True:
        try:
            edad = int(input("Tu edad: "))
            if edad < 0:
                print("La edad no puede ser negativa")
                continue
            return edad
        except ValueError:
            print("Por favor, introduce un número válido")

edad = solicitar_edad()
print(f"Tienes {edad} años")
```

#### Función auxiliar para entrada segura

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

### 4.3. Función print(): escritura y formateo

La función **`print()`** es mucho más versátil de lo que parece inicialmente. Permite mostrar información de múltiples formas y con gran control sobre el formato.

#### Sintaxis y parámetros de print()

```python
print(*values, sep=' ', end='\n', file=sys.stdout, flush=False)
```

#### Parámetros principales

**1. Múltiples valores**: Puedes pasar varios argumentos

```python
nombre = "Ana"
edad = 25
ciudad = "Madrid"

print(nombre, edad, ciudad)  # Ana 25 Madrid
print("Nombre:", nombre, "Edad:", edad)  # Nombre: Ana Edad: 25
```

**2. Separador personalizado (sep)**:

```python
print("Python", "Java", "C++", sep=", ")  # Python, Java, C++
print("2024", "10", "15", sep="-")        # 2024-10-15
print("A", "B", "C", sep="")              # ABC
print("X", "Y", "Z", sep=" -> ")          # X -> Y -> Z
```

**3. Final personalizado (end)**:

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

**4. Flush inmediato**:

```python
import time

# Para efectos de escritura en tiempo real
for i in range(1, 6):
    print(f"Contador: {i}", end="\r", flush=True)  # Sobrescribe la línea
    time.sleep(1)
print("¡Terminado!")
```

#### Ejemplos prácticos avanzados

```python
# Separador para secciones
def imprimir_separador(titulo, caracter="=", longitud=50):
    print(caracter * longitud)
    print(f"{titulo:^{longitud}}")  # Centrado
    print(caracter * longitud)

imprimir_separador("DATOS DEL USUARIO")

# Tabular información
productos = [
    ("Laptop", 899.99, 5),
    ("Mouse", 25.50, 15),
    ("Teclado", 75.00, 8)
]

print("INVENTARIO")
print("-" * 40)
for nombre, precio, stock in productos:
    print(f"{nombre:<15} {precio:>8.2f}€ {stock:>5} unidades")
```

### 4.4. Formateo avanzado de strings

Python ofrece múltiples formas de formatear cadenas de texto. La más moderna y recomendada son las **f-strings** (formatted string literals).

#### F-strings (Python 3.6+) - Recomendado

**Sintaxis básica**

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

**Formateo numérico**

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

**Alineación y relleno**

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

**Formateo con separadores de miles**

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
    print(f"{'TOTAL:':<30} {total:>8.2f}€")
    print("=" * 50)

# Uso
productos = [
    ("Laptop Dell XPS", 1299.99, 1),
    ("Mouse inalámbrico", 35.50, 2),
    ("Teclado mecánico", 89.99, 1)
]

mostrar_factura("Ana García", productos)
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

#### Métodos alternativos (contexto histórico)

**Método .format() (Python 2.6+)**

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

**Formateo % (estilo C) - Desaconsejado**

```python
# Método antiguo, evitar en código nuevo
nombre = "Ana"
edad = 25

mensaje = "Hola, me llamo %s y tengo %d años" % (nombre, edad)
print(mensaje)
```

### 4.5. Casos prácticos avanzados

#### Calculadora interactiva

```python
def calculadora():
    """Calculadora interactiva con interfaz amigable."""
    print("=" * 40)
    print("       CALCULADORA PYTHON")
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

# calculadora()  # Descomenta para probar
```

#### Sistema de registro de usuario

```python
def registro_usuario():
    """Sistema de registro con validaciones."""
    print("🔐 REGISTRO DE USUARIO")
    print("-" * 30)
    
    # Recopilar información
    datos = {}
    
    # Nombre (requerido)
    while True:
        nombre = input("Nombre completo: ").strip()
        if len(nombre) >= 2:
            datos['nombre'] = nombre
            break
        print("❌ El nombre debe tener al menos 2 caracteres")
    
    # Edad (validación numérica)
    while True:
        try:
            edad = int(input("Edad: "))
            if 13 <= edad <= 120:
                datos['edad'] = edad
                break
            else:
                print("❌ La edad debe estar entre 13 y 120 años")
        except ValueError:
            print("❌ Introduce una edad válida")
    
    # Email (validación básica)
    while True:
        email = input("Email: ").strip().lower()
        if "@" in email and "." in email and len(email) >= 5:
            datos['email'] = email
            break
        print("❌ Introduce un email válido")
    
    # Ciudad (opcional)
    ciudad = input("Ciudad (opcional): ").strip()
    if ciudad:
        datos['ciudad'] = ciudad
    
    # Mostrar resumen
    print("\n" + "="*50)
    print("RESUMEN DE REGISTRO")
    print("="*50)
    print(f"👤 Nombre: {datos['nombre']}")
    print(f"🎂 Edad: {datos['edad']} años")
    print(f"📧 Email: {datos['email']}")
    if 'ciudad' in datos:
        print(f"🏙️  Ciudad: {datos['ciudad']}")
    
    # Confirmación
    confirmar = input("\n¿Confirmar registro? (s/n): ").lower()
    if confirmar.startswith('s'):
        print("\n✅ ¡Usuario registrado exitosamente!")
        return datos
    else:
        print("\n❌ Registro cancelado")
        return None

# usuario = registro_usuario()  # Descomenta para probar
```

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
