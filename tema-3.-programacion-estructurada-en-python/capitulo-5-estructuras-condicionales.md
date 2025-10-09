# Capítulo 5: Estructuras condicionales

Los programas verdaderamente útiles no siguen un camino único y lineal; necesitan adaptarse y reaccionar a diferentes situaciones. Para ello, deben ser capaces de tomar decisiones. Las **estructuras condicionales** son los mecanismos que permiten controlar el flujo de ejecución de un programa, evaluando condiciones que resultan ser `True` o `False` y ejecutando distintos bloques de código en consecuencia. Son la base para crear software inteligente y dinámico.

En Python encontramos las estructuras `if`, `elif`, `else` y la moderna `match-case` (desde Python 3.10), además del operador ternario para casos simples. Estas herramientas nos permiten controlar el flujo de ejecución de nuestros programas de manera precisa y eficiente.

### 5.1. Introducción: ¿Por qué necesitamos tomar decisiones?

Imagina un programa que siempre ejecutara exactamente las mismas instrucciones. Sería predecible, pero también inútil en la mayoría de situaciones reales. Los programas útiles necesitan **adaptarse** a diferentes circunstancias:

* Un cajero automático debe verificar si el PIN es correcto
* Un videojuego debe decidir si el jugador ha ganado o perdido
* Una aplicación de temperatura debe mostrar si hace frío, calor o está templado
* Un sistema de notas debe determinar si un estudiante ha aprobado

Las estructuras condicionales nos permiten crear estos comportamientos adaptativos mediante la evaluación de **condiciones** (expresiones que se evalúan como `True` o `False`).

#### El concepto de condición

Una **condición** es una expresión que Python puede evaluar como verdadera (`True`) o falsa (`False`). Algunos ejemplos:

```python
# Condiciones simples
edad >= 18          # ¿Es mayor o igual a 18?
nombre == "Ana"     # ¿El nombre es exactamente "Ana"?
temperatura > 30    # ¿La temperatura es mayor a 30 grados?
len(password) >= 8  # ¿La contraseña tiene al menos 8 caracteres?

# Condiciones complejas
(edad >= 18) and (tiene_licencia == True)
(es_fin_de_semana) or (es_festivo)
not (saldo_cuenta < 0)
```

***

### 5.2. La instrucción `if`: La decisión básica

La estructura `if` es la forma más básica de toma de decisiones. Evalúa una condición y, si es `True`, ejecuta el bloque de código indentado que le sigue. La sintaxis siempre requiere dos puntos (`:`) al final de la condición y que el bloque de código subordinado esté indentado.

#### Sintaxis

```python
if condicion:
    # Código que se ejecuta si la condición es True
    instruccion1()
    instruccion2()
```

#### Ejemplo de uso

```python
# Control de acceso
edad = int(input("¿Cuántos años tienes? "))
if edad >= 18:
    print("Acceso permitido")
    print("Bienvenido al sistema")

# Validación de entrada
password = input("Introduce tu contraseña: ")
if len(password) < 8:
    print("❌ La contraseña debe tener al menos 8 caracteres")

# Estado del tiempo
temperatura = float(input("Temperatura actual: "))
if temperatura > 35:
    print("¡Hace mucho calor! Busca sombra")
if temperatura < 0:
    print("¡Está helando! Abrígate bien")
```

***

### 5.3. La instrucción `if-else`: Alternativa binaria

La estructura `if-else` gestiona decisiones binarias, donde hay dos posibles caminos. Si la condición del `if` es `True`, se ejecuta su bloque de código. Si es `False`, se ejecuta el bloque de código de la cláusula `else`.

#### Sintaxis

```python
if condicion:
    # Código si la condición es True
    instrucciones_verdadero()
else:
    # Código si la condición es False
    instrucciones_falso()
```

#### Ejemplo de uso

```python
# Clasificación de edad
edad = int(input("Tu edad: "))
if edad >= 18:
    print("Eres mayor de edad")
    print("Puedes votar y conducir")
else:
    print("Eres menor de edad")
    print("Disfruta tu juventud")

# Validación de número
numero = int(input("Introduce un número: "))
if numero >= 0:
    print(f"{numero} es positivo o cero")
else:
    print(f"{numero} es negativo")
```

***

### 5.4. La instrucción `if-elif-else`: Múltiples alternativas

Para gestionar múltiples condiciones mutuamente excluyentes, se utiliza la estructura `if-elif-else` (`elif` es una contracción de "else if"). Python evalúa las condiciones en orden: ejecuta el bloque de la primera condición que resulte `True` e ignora el resto de la cadena.

El orden de las cláusulas `elif` es crucial. Generalmente, se deben colocar de la más específica a la más general para evitar que una condición más amplia "capture" un caso que debería ser manejado por una más específica.

#### Sintaxis

```python
if condicion1:
    # Código si condicion1 es True
    instrucciones1()
elif condicion2:
    # Código si condicion2 es True (y condicion1 es False)
    instrucciones2()
elif condicion3:
    # Código si condicion3 es True (y anteriores son False)
    instrucciones3()
else:
    # Código si todas las condiciones anteriores son False
    instrucciones_por_defecto()
```

#### Ejemplo de uso

```python
nota = 7.5

if nota >= 9:
    calificacion = "Sobresaliente"
elif nota >= 7:
    calificacion = "Notable"
elif nota >= 5:
    calificacion = "Aprobado"
else:
    calificacion = "Suspenso"

print(f"Tu calificación es: {calificacion}")
```

***

### 5.5. El operador ternario: Decisión en una línia

El operador ternario es una forma compacta de escribir una estructura `if-else` simple en una sola línea.

#### Sintaxis

```python
valor_si_true if condicion else valor_si_false
```

#### Ejemplo de uso

```python
edad = 22
# Con operador ternario
estado = "Mayor de edad" if edad >= 18 else "Menor de edad"
print(estado)
```

{% hint style="danger" %}
Se recomienda encarecidamente reservar el operador ternario para asignaciones condicionales muy simples. Para cualquier lógica más compleja, una estructura `if-else` tradicional es siempre superior en legibilidad y mantenibilidad.
{% endhint %}

***

### 5.6. La estructura `match-case`: Patrones avanzados (Python 3.10+)

Introducida en Python 3.10, la estructura `match-case` ofrece una alternativa potente y legible al `if-elif-else`, especialmente para la coincidencia de patrones. Es más versátil que la instrucción `switch` de otros lenguajes.

Permite comparar un valor con varios patrones:

* <mark style="background-color:$primary;">**Valores literales**</mark>: Se pueden agrupar múltiples valores con el operador `|`.
* <mark style="background-color:$primary;">**Guardas**</mark>: Se puede añadir una condición `if` a un `case` para refinar el patrón.
* <mark style="background-color:$primary;">**Estructuras de datos**</mark>: Puede descomponer listas o tuplas.
* <mark style="background-color:$primary;">**Caso por defecto**</mark>: El patrón `case _` actúa como un comodín que coincide con cualquier valor si los casos anteriores no lo han hecho.

#### Sintaxis básica

```python
match expresion:
    case patron1:
        instrucciones1()
    case patron2:
        instrucciones2()
    case _:  # Caso por defecto (opcional)
        instrucciones_por_defecto()
```

#### Ejemplos con valores literales

```python
# Sistema de calificaciones con match-case
nota = int(input("Introduce tu nota (0-10): "))

print("Tu calificación cualitativa es: ", end="")
match nota:
    case 0 | 1 | 2 | 3 | 4: print("No Apto")
    case 5: print("Suficiente")
    case 6: print("Bien")
    case 7 | 8: print("Notable")
    case 9 | 10: print("Excelente")
    case _: print("Nota inválida")
```

#### Patrones con guardas (condiciones)

```python
# Usando guardas para rangos
nota = float(input("Introduce tu nota de programación: "))

print("Tu nota cualitativa es: ", end="")
match nota:
    case x if 0 <= x < 5: print("No Apto")
    case x if 5 <= x < 5.5: print("Suficiente")
    case x if 5.5 <= x < 6.5: print("Bien")
    case x if 6.5 <= x < 8.5: print("Notable")
    case x if 8.5 <= x <= 10: print("Excelente")
    case _: print("Nota inválida")
```

#### Patrones con estructuras de datos

```python
# Match con tuplas
def procesar_coordenada(punto):
    match punto:
        case (0, 0): return "Origen"
        case (x, 0): return f"En el eje X: {x}"
        case (0, y): return f"En el eje Y: {y}"
        case (x, y) if x == y: return f"Diagonal: ({x}, {y})"
        case (x, y): return f"Punto genérico: ({x}, {y})"

print(procesar_coordenada((0, 0)))    # "Origen"
print(procesar_coordenada((5, 0)))    # "En el eje X: 5"
print(procesar_coordenada((3, 3)))    # "Diagonal: (3, 3)"

# Match con listas
def analizar_lista(lista):
    match lista:
        case []: return "Lista vacía"
        case [x]: return f"Un elemento: {x}"
        case [x, y]: return f"Dos elementos: {x} y {y}"
        case [x, *resto]: return f"Primer elemento: {x}, resto: {resto}"

print(analizar_lista([]))           # "Lista vacía"
print(analizar_lista([5]))          # "Un elemento: 5"
print(analizar_lista([1, 2, 3, 4])) # "Primer elemento: 1, resto: [2, 3, 4]"
```

#### Ejemplo práctico: Menú de aplicación

```python
def mostrar_menu():
    print("\n=== MENÚ PRINCIPAL ===")
    print("1. Ver perfil")
    print("2. Configuración")
    print("3. Ayuda")
    print("4. Salir")
    return input("Selecciona una opción: ")

def ejecutar_opcion(opcion):
    match opcion:
        case "1":
            print("Mostrando perfil de usuario...")
            # Lógica para mostrar perfil
        case "2":
            print("Abriendo configuración...")
            # Lógica para configuración
        case "3":
            print("Mostrando ayuda...")
            print("Para más información, visita nuestro sitio web")
        case "4":
            print("¡Hasta luego!")
            return False  # Señal para salir
        case _:
            print("❌ Opción inválida")
    return True  # Continuar

# Bucle principal
while True:
    opcion = mostrar_menu()
    if not ejecutar_opcion(opcion):
        break
```

***

### 5.7. Anidamiento y condiciones complejas

Las estructuras condicionales se pueden anidar unas dentro de otras para crear lógicas más detalladas. Sin embargo, un anidamiento excesivo puede hacer que el código sea difícil de leer y mantener.

```python
# Ejemplo de anidamiento
if usuario_autenticado:
    if usuario_es_admin:
        print("Acceso de administrador concedido.")
    else:
        print("Acceso de usuario estándar.")
else:
    print("Acceso denegado.")
```

{% hint style="success" %}
Una **buena práctica** para reducir el anidamiento en funciones que realizan validaciones es la técnica de "**retorno temprano**" (_early return_). Consiste en comprobar las condiciones de error al principio y salir de la función inmediatamente si se cumplen, dejando el "camino feliz" al final sin indentación extra.
{% endhint %}

Para crear condiciones más elaboradas, se utilizan los operadores lógicos `and`, `or` y `not`.&#x20;

```python
# AND - Todas las condiciones deben ser verdaderas
edad = 25; tiene_licencia = True; tiene_experiencia = True

if edad >= 18 and tiene_licencia and tiene_experiencia:
    print("Puede trabajar como conductor")

# OR - Al menos una condición debe ser verdadera
es_estudiante = True; es_jubilado = False; tiene_descuento_especial = False

if es_estudiante or es_jubilado or tiene_descuento_especial:
    print("Tienes derecho a descuento")

# NOT - Negación de la condición
usuario_bloqueado = False
if not usuario_bloqueado:
    print("Acceso permitido")
```

***

### 5.8. Caso práctico: Sistema de reservas

Este ejemplo combina varias estructuras condicionales para calcular el precio de una reserva de hotel.

```python
def procesar_reserva():
    """Sistema de reservas de hotel."""
    print("SISTEMA DE RESERVAS")
    # Recopilar información
    temporada = input("Temporada (alta/media/baja): ").lower()
    dias = int(input("Número de días: "))
    huespedes = int(input("Número de huéspedes: "))
    vip = input("¿Cliente VIP? (s/n): ").lower() == 's'
    
    # Precio base según temporada
    if temporada == "alta":
        precio_base = 150
    elif temporada == "media":
        precio_base = 100
    else: # temporada baja
        precio_base = 75
    
    precio_total = precio_base * dias
    
    # Suplemento por huéspedes extra
    if huespedes > 2:
        suplemento = (huespedes - 2) * 25 * dias
        precio_total += suplemento
    
    # Descuentos
    descuento_vip_aplicado = precio_total * 0.15 if vip else 0
    descuento_larga_estancia = precio_total * 0.10 if dias >= 7 else 0
    precio_total -= (descuento_vip_aplicado + descuento_larga_estancia)
    
    # Mostrar resumen
    print("\n" + "="*40)
    print("RESUMEN DE RESERVA")
    print("="*40)
    print(f"Precio final: {precio_total:.2f}€")
```

***

### Resumen del Capítulo

Las estructuras condicionales son herramientas fundamentales que permiten a nuestros programas tomar decisiones inteligentes. Has aprendido a usar `if`, `elif`, `else`, el operador ternario y la moderna estructura `match-case` para crear programas que se adapten a diferentes situaciones y respondan de manera apropiada a las condiciones del entorno.

#### 💡 Conceptos Clave:

* **if**: Ejecución condicional simple
* **if-else**: Alternativa binaria (verdadero/falso)
* **if-elif-else**: Múltiples alternativas mutuamente excluyentes
* **Operador ternario**: Decisiones simples en una línea
* **match-case**: Coincidencia de patrones avanzada (Python 3.10+)
* **Condiciones complejas**: Uso de operadores lógicos `and`, `or`, `not`
* **Anidamiento**: Estructuras condicionales dentro de otras

#### 🤔 Preguntas de Reflexión:

1. ¿Cuándo es preferible usar `match-case` en lugar de múltiples `elif`?
2. ¿Qué problemas puede causar el orden incorrecto en una cadena `if-elif`?
3. ¿En qué situaciones el operador ternario mejora la legibilidad del código?
4. ¿Cómo puedes evitar el anidamiento excesivo en validaciones complejas?

#### 🔧 Ejercicio Práctico:

Crea un programa que:

1. Simule un sistema de login con múltiples intentos
2. Implemente un calculador de tarifas de taxi con diferentes zonas y horarios
3. Use `match-case` para procesar comandos de un chatbot simple
4. Valide formularios complejos con múltiples campos y reglas

Una vez que nuestros programas pueden tomar decisiones, el siguiente paso es dotarlos de la capacidad de repetir acciones. Esto nos lleva al mundo de los bucles y las iteraciones.
