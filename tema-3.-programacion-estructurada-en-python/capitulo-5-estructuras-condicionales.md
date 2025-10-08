# Capítulo 5: Estructuras condicionales

Las **estructuras condicionales** son los mecanismos que nos permiten que nuestros programas tomen decisiones. En lugar de ejecutar siempre las mismas instrucciones en el mismo orden, estas estructuras evalúan condiciones y, según el resultado, ejecutan diferentes bloques de código. Son fundamentales para crear programas inteligentes que puedan responder a diferentes situaciones.

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

### 5.2. Instrucción if: La decisión básica

La estructura `if` es la forma más simple de tomar una decisión en Python. Su sintaxis es:

```python
if condicion:
    # Código que se ejecuta si la condición es True
    instruccion1()
    instruccion2()
```

#### Características importantes

**1. Los dos puntos (`:`) son obligatorios**

```python
# ✅ Correcto
if edad >= 18:
    print("Eres mayor de edad")

# ❌ Error: faltan los dos puntos
if edad >= 18
    print("Eres mayor de edad")  # SyntaxError
```

**2. La indentación es obligatoria**

```python
# ✅ Correcto
if temperatura > 30:
    print("Hace calor")
    print("Bebe mucha agua")

# ❌ Error: falta indentación
if temperatura > 30:
print("Hace calor")  # IndentationError
```

**3. Pueden evaluarse múltiples tipos de valores**

```python
# Con números
if numero > 0:
    print("Positivo")

# Con strings
if nombre != "":
    print(f"Hola, {nombre}")

# Con listas (True si tiene elementos)
if lista_usuarios:
    print("Hay usuarios registrados")

# Con None
if resultado is not None:
    print("Se encontró un resultado")
```

#### Ejemplos prácticos básicos

```python
# Control de acceso
edad = int(input("¿Cuántos años tienes? "))
if edad >= 18:
    print("✅ Acceso permitido")
    print("Bienvenido al sistema")

# Validación de entrada
password = input("Introduce tu contraseña: ")
if len(password) < 8:
    print("❌ La contraseña debe tener al menos 8 caracteres")

# Estado del tiempo
temperatura = float(input("Temperatura actual: "))
if temperatura > 35:
    print("🌡️ ¡Hace mucho calor! Busca sombra")
if temperatura < 0:
    print("❄️ ¡Está helando! Abrígate bien")
```

### 5.3. Instrucción if-else: Alternativa binaria

La estructura `if-else` nos permite especificar qué hacer cuando la condición es `False`. Es perfecta para decisiones binarias (sí/no, verdadero/falso).

#### Sintaxis

```python
if condicion:
    # Código si la condición es True
    instrucciones_verdadero()
else:
    # Código si la condición es False
    instrucciones_falso()
```

#### Ejemplos prácticos

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

# Control de inventario
stock = int(input("Stock disponible: "))
if stock > 0:
    print("✅ Producto disponible")
    print(f"Quedan {stock} unidades")
else:
    print("❌ Producto agotado")
    print("Contacta con el proveedor")
```

#### Casos especiales con if-else

```python
# Evaluación de valores "falsy"
texto = input("Escribe algo: ")
if texto:  # True si texto no está vacío
    print(f"Has escrito: '{texto}'")
else:
    print("No has escrito nada")

# Verificación de divisibilidad
numero = int(input("Número: "))
if numero % 2 == 0:
    print(f"{numero} es par")
else:
    print(f"{numero} es impar")

# Autenticación simple
usuario_correcto = "admin"
password_correcta = "1234"

usuario = input("Usuario: ")
password = input("Contraseña: ")

if usuario == usuario_correcto and password == password_correcta:
    print("🔓 Acceso concedido")
    print("Bienvenido al sistema")
else:
    print("🔒 Acceso denegado")
    print("Usuario o contraseña incorrectos")
```

### 5.4. Instrucción if-elif-else: Múltiples alternativas

Cuando necesitamos evaluar múltiples condiciones mutuamente excluyentes, usamos `elif` (else if). Esta estructura nos permite crear **decisiones múltiples**.

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

#### Ejemplos prácticos

```python
# Sistema de calificaciones
nota = float(input("Introduce tu nota (0-10): "))

if nota >= 9:
    print("📚 Excelente - ¡Felicidades!")
    calificacion = "Sobresaliente"
elif nota >= 7:
    print("📖 Notable - Muy buen trabajo")
    calificacion = "Notable"
elif nota >= 5:
    print("📝 Aprobado - ¡Enhorabuena!")
    calificacion = "Aprobado"
else:
    print("📉 Suspenso - Sigue estudiando")
    calificacion = "Suspenso"

print(f"Tu calificación es: {calificacion}")
```

```python
# Clasificador de IMC (Índice de Masa Corporal)
peso = float(input("Tu peso en kg: "))
altura = float(input("Tu altura en metros: "))

imc = peso / (altura ** 2)

print(f"Tu IMC es: {imc:.1f}")

if imc < 18.5:
    print("⚠️ Bajo peso")
    recomendacion = "Consulta con un nutricionista"
elif imc < 25:
    print("✅ Peso normal")
    recomendacion = "Mantén tus hábitos saludables"
elif imc < 30:
    print("⚠️ Sobrepeso")
    recomendacion = "Considera hacer más ejercicio"
else:
    print("🚨 Obesidad")
    recomendacion = "Consulta con un médico"

print(f"Recomendación: {recomendacion}")
```

```python
# Calculadora simple
print("=== CALCULADORA ===")
num1 = float(input("Primer número: "))
operador = input("Operador (+, -, *, /): ")
num2 = float(input("Segundo número: "))

if operador == "+":
    resultado = num1 + num2
    print(f"{num1} + {num2} = {resultado}")
elif operador == "-":
    resultado = num1 - num2
    print(f"{num1} - {num2} = {resultado}")
elif operador == "*":
    resultado = num1 * num2
    print(f"{num1} * {num2} = {resultado}")
elif operador == "/":
    if num2 != 0:
        resultado = num1 / num2
        print(f"{num1} / {num2} = {resultado}")
    else:
        print("❌ Error: División por cero")
else:
    print("❌ Operador no válido")
```

#### Importante: Orden de evaluación

```python
# ⚠️ Cuidado con el orden - el primer True "gana"
numero = 8

# Orden incorrecto
if numero > 0:
    print("Positivo")
elif numero > 5:
    print("Mayor que 5")  # Nunca se ejecutará
elif numero % 2 == 0:
    print("Par")  # Nunca se ejecutará

# Orden correcto (más específico a más general)
numero = 8
if numero % 2 == 0 and numero > 5:
    print("Par y mayor que 5")
elif numero % 2 == 0:
    print("Par")
elif numero > 5:
    print("Mayor que 5")
elif numero > 0:
    print("Positivo")
else:
    print("Cero o negativo")
```

### 5.5. Operador ternario: Decisión en una línea

Para decisiones simples, Python ofrece el **operador ternario**, que permite escribir un `if-else` en una sola línea.

#### Sintaxis

```python
valor_si_true if condicion else valor_si_false
```

#### Ejemplos básicos

```python
# Comparación tradicional vs ternario
edad = 20

# Forma tradicional
if edad >= 18:
    estado = "adulto"
else:
    estado = "menor"

# Forma ternaria (equivalente)
estado = "adulto" if edad >= 18 else "menor"
print(f"Eres {estado}")

# Más ejemplos
numero = -5
signo = "positivo" if numero > 0 else "negativo o cero"

temperatura = 25
ropa = "manga corta" if temperatura > 20 else "manga larga"

nota = 8.5
resultado = "aprobado" if nota >= 5 else "suspenso"
```

#### Casos prácticos del operador ternario

```python
# Formateo condicional
items = [1, 2, 3]
mensaje = f"Hay {len(items)} elemento{'s' if len(items) != 1 else ''}"
print(mensaje)  # "Hay 3 elementos"

# Validación de entrada
nombre = input("Tu nombre: ").strip()
nombre_final = nombre if nombre else "Anónimo"
print(f"Hola, {nombre_final}")

# Cálculo condicional
precio_base = 100
descuento_vip = True
precio_final = precio_base * 0.8 if descuento_vip else precio_base
print(f"Precio final: {precio_final}€")

# Límites seguros
velocidad = int(input("Velocidad: "))
velocidad_segura = 120 if velocidad <= 120 else 120
print(f"Velocidad aplicada: {velocidad_segura} km/h")
```

#### ⚠️ Cuándo NO usar el operador ternario

```python
# ❌ Demasiado complejo para una línea
resultado = "excelente" if nota >= 9 else "notable" if nota >= 7 else "aprobado" if nota >= 5 else "suspenso"

# ✅ Mejor con if-elif-else tradicional
if nota >= 9:
    resultado = "excelente"
elif nota >= 7:
    resultado = "notable"
elif nota >= 5:
    resultado = "aprobado"
else:
    resultado = "suspenso"
```

### 5.6. Estructura match-case: Patrones avanzados (Python 3.10+)

Desde Python 3.10, disponemos de `match-case`, una estructura potente para **coincidencia de patrones**. Es similar al `switch` de otros lenguajes, pero mucho más versátil.

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
    case 0 | 1 | 2 | 3 | 4:  # Múltiples valores
        print("No Apto")
    case 5:
        print("Suficiente")
    case 6:
        print("Bien")
    case 7 | 8:
        print("Notable")
    case 9 | 10:
        print("Excelente")
    case _:
        print("Nota inválida")
```

#### Patrones con guardas (condiciones)

```python
# Usando guardas para rangos
nota = float(input("Introduce tu nota de programación: "))

print("Tu nota cualitativa es: ", end="")
match nota:
    case x if 0 <= x < 5:
        print("No Apto")
    case x if 5 <= x < 5.5:
        print("Suficiente")
    case x if 5.5 <= x < 6.5:
        print("Bien")
    case x if 6.5 <= x < 8.5:
        print("Notable")
    case x if 8.5 <= x <= 10:
        print("Excelente")
    case _:
        print("Nota inválida")
```

#### Patrones con estructuras de datos

```python
# Match con tuplas
def procesar_coordenada(punto):
    match punto:
        case (0, 0):
            return "Origen"
        case (x, 0):
            return f"En el eje X: {x}"
        case (0, y):
            return f"En el eje Y: {y}"
        case (x, y) if x == y:
            return f"Diagonal: ({x}, {y})"
        case (x, y):
            return f"Punto genérico: ({x}, {y})"

print(procesar_coordenada((0, 0)))    # "Origen"
print(procesar_coordenada((5, 0)))    # "En el eje X: 5"
print(procesar_coordenada((3, 3)))    # "Diagonal: (3, 3)"

# Match con listas
def analizar_lista(lista):
    match lista:
        case []:
            return "Lista vacía"
        case [x]:
            return f"Un elemento: {x}"
        case [x, y]:
            return f"Dos elementos: {x} y {y}"
        case [x, *resto]:
            return f"Primer elemento: {x}, resto: {resto}"

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
            print("👤 Mostrando perfil de usuario...")
            # Lógica para mostrar perfil
        case "2":
            print("⚙️ Abriendo configuración...")
            # Lógica para configuración
        case "3":
            print("❓ Mostrando ayuda...")
            print("Para más información, visita nuestro sitio web")
        case "4":
            print("👋 ¡Hasta luego!")
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

### 5.7. Condiciones complejas y anidamiento

#### Operadores lógicos en condiciones

```python
# AND - Todas las condiciones deben ser verdaderas
edad = 25
tiene_licencia = True
tiene_experiencia = True

if edad >= 18 and tiene_licencia and tiene_experiencia:
    print("✅ Puede trabajar como conductor")

# OR - Al menos una condición debe ser verdadera
es_estudiante = True
es_jubilado = False
tiene_descuento_especial = False

if es_estudiante or es_jubilado or tiene_descuento_especial:
    print("🎫 Tienes derecho a descuento")

# NOT - Negación de la condición
usuario_bloqueado = False
if not usuario_bloqueado:
    print("🔓 Acceso permitido")
```

#### Estructuras anidadas

```python
# Validación de usuario compleja
usuario = input("Usuario: ")
password = input("Contraseña: ")

if usuario:  # Usuario no vacío
    if len(usuario) >= 3:
        if password:  # Contraseña no vacía
            if len(password) >= 8:
                print("✅ Credenciales válidas")
                # Verificar en base de datos...
            else:
                print("❌ La contraseña debe tener al menos 8 caracteres")
        else:
            print("❌ La contraseña no puede estar vacía")
    else:
        print("❌ El usuario debe tener al menos 3 caracteres")
else:
    print("❌ El usuario no puede estar vacío")
```

#### Mejor práctica: Validación con retorno temprano

```python
# Versión mejorada del ejemplo anterior
def validar_credenciales(usuario, password):
    """Valida las credenciales de usuario."""
    if not usuario:
        return False, "El usuario no puede estar vacío"
    
    if len(usuario) < 3:
        return False, "El usuario debe tener al menos 3 caracteres"
    
    if not password:
        return False, "La contraseña no puede estar vacía"
    
    if len(password) < 8:
        return False, "La contraseña debe tener al menos 8 caracteres"
    
    return True, "Credenciales válidas"

# Uso
usuario = input("Usuario: ")
password = input("Contraseña: ")

valido, mensaje = validar_credenciales(usuario, password)
if valido:
    print(f"✅ {mensaje}")
    # Continuar con la autenticación...
else:
    print(f"❌ {mensaje}")
```

### 5.8. Casos prácticos avanzados

#### Calculadora de impuestos

```python
def calcular_impuestos(ingresos_anuales):
    """Calcula impuestos según tramos."""
    
    if ingresos_anuales <= 12000:
        tasa = 0
        tramo = "Exento"
    elif ingresos_anuales <= 20000:
        tasa = 0.15
        tramo = "15%"
    elif ingresos_anuales <= 35000:
        tasa = 0.25
        tramo = "25%"
    elif ingresos_anuales <= 60000:
        tasa = 0.30
        tramo = "30%"
    else:
        tasa = 0.35
        tramo = "35%"
    
    impuestos = ingresos_anuales * tasa
    neto = ingresos_anuales - impuestos
    
    return {
        'bruto': ingresos_anuales,
        'impuestos': impuestos,
        'neto': neto,
        'tasa': tasa,
        'tramo': tramo
    }

# Uso
ingresos = float(input("Ingresos anuales: "))
resultado = calcular_impuestos(ingresos)

print(f"\n💰 CÁLCULO DE IMPUESTOS")
print(f"Ingresos brutos: {resultado['bruto']:,.2f}€")
print(f"Tramo fiscal: {resultado['tramo']}")
print(f"Impuestos: {resultado['impuestos']:,.2f}€")
print(f"Ingresos netos: {resultado['neto']:,.2f}€")
```

#### Sistema de reservas

```python
def procesar_reserva():
    """Sistema de reservas de hotel."""
    print("🏨 SISTEMA DE RESERVAS")
    
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
    else:  # temporada baja
        precio_base = 75
    
    # Calcular precio total
    precio_total = precio_base * dias
    
    # Suplemento por huéspedes extra
    if huespedes > 2:
        suplemento = (huespedes - 2) * 25 * dias
        precio_total += suplemento
        print(f"Suplemento por huéspedes extra: {suplemento}€")
    
    # Descuentos
    descuento = 0
    if vip:
        descuento += 0.15  # 15% descuento VIP
        print("🌟 Descuento VIP aplicado: 15%")
    
    if dias >= 7:
        descuento += 0.10  # 10% descuento estancia larga
        print("📅 Descuento estancia larga: 10%")
    
    # Aplicar descuentos
    if descuento > 0:
        ahorro = precio_total * descuento
        precio_total *= (1 - descuento)
        print(f"Ahorro total: {ahorro:.2f}€")
    
    # Mostrar resumen
    print("\n" + "="*40)
    print("RESUMEN DE RESERVA")
    print("="*40)
    print(f"Temporada: {temporada.title()}")
    print(f"Días: {dias}")
    print(f"Huéspedes: {huespedes}")
    print(f"Precio base: {precio_base}€/noche")
    print(f"TOTAL: {precio_total:.2f}€")
    
    return precio_total

# procesar_reserva()  # Descomenta para probar
```

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
