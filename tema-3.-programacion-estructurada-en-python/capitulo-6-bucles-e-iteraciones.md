# Capítulo 6: Bucles e iteraciones

Los **bucles** o **estructuras iterativas** son construcciones que nos permiten ejecutar un bloque de código múltiples veces. Son fundamentales para automatizar tareas repetitivas, procesar colecciones de datos, implementar algoritmos y crear programas eficientes. En Python disponemos de dos tipos principales de bucles: `while` y `for`, cada uno optimizado para diferentes tipos de situaciones.

Además de los bucles básicos, Python proporciona sentencias de control (`break`, `continue`, `pass`) y características avanzadas como la cláusula `else` que hacen de la iteración una herramienta extremadamente poderosa y flexible.

### 6.1. ¿Cuándo necesitamos repetir código?

Los bucles son esenciales en situaciones como:

* **Procesamiento de datos**: Analizar cada elemento de una lista de ventas
* **Validación de entrada**: Seguir pidiendo datos hasta que sean válidos
* **Algoritmos matemáticos**: Calcular factoriales, series, aproximaciones
* **Interfaces de usuario**: Mostrar menús hasta que el usuario elija salir
* **Automatización**: Realizar la misma operación sobre múltiples archivos

Sin bucles, tendríamos que escribir código repetitivo y limitado:

```python
# ❌ Sin bucles: código repetitivo y limitado
print("Número 1")
print("Número 2")
print("Número 3")
print("Número 4")
print("Número 5")

# ✅ Con bucles: código limpio y flexible
for i in range(1, 6):
    print(f"Número {i}")
```

### 6.2. Bucle while: Repetición condicional

El bucle `while` ejecuta un bloque de código **mientras** una condición sea verdadera. Es ideal cuando **no sabemos exactamente cuántas veces** necesitaremos repetir el código.

#### Sintaxis básica

```python
while condicion:
    # Código que se repite
    instrucciones()
    # IMPORTANTE: modificar la condición para evitar bucle infinito
```

#### Ejemplo básico

```python
# Contador simple
contador = 1
while contador <= 5:
    print(f"Iteración {contador}")
    contador += 1  # CRUCIAL: modificar la variable de control

print("Bucle terminado")
```

#### Características importantes del while

**1. Evaluación previa**: La condición se evalúa ANTES de cada iteración

```python
numero = 10
while numero < 10:
    print("Esto nunca se ejecuta")
    numero += 1
```

**2. Puede no ejecutarse nunca**: Si la condición inicial es falsa

```python
x = 5
while x > 10:  # False desde el principio
    print("Nunca se ejecuta")
```

**3. Riesgo de bucle infinito**: Si la condición nunca se vuelve falsa

```python
# ❌ BUCLE INFINITO - ¡Evitar!
contador = 1
while contador <= 5:
    print("Infinito...")
    # contador += 1  # ¡Olvidamos incrementar!
```

#### Ejemplos prácticos con while

**Validación de entrada**

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

**Juego de adivinanza**

```python
import random

def juego_adivinanza():
    """Juego de adivinanza con intentos limitados."""
    numero_secreto = random.randint(1, 100)
    intentos = 0
    max_intentos = 7
    
    print("🎮 ¡Juego de Adivinanza!")
    print(f"Adivina el número entre 1 y 100 (tienes {max_intentos} intentos)")
    
    while intentos < max_intentos:
        try:
            intento = int(input(f"Intento {intentos + 1}: "))
            intentos += 1
            
            if intento == numero_secreto:
                print(f"🎉 ¡Correcto! Era {numero_secreto}")
                print(f"Lo adivinaste en {intentos} intentos")
                return True
            elif intento < numero_secreto:
                print("📈 El número es mayor")
            else:
                print("📉 El número es menor")
                
        except ValueError:
            print("❌ Por favor, introduce un número válido")
            intentos -= 1  # No contar intentos inválidos
    
    print(f"😞 Se acabaron los intentos. Era {numero_secreto}")
    return False

# juego_adivinanza()  # Descomenta para jugar
```

**Menú de aplicación**

```python
def mostrar_menu():
    """Muestra el menú principal."""
    print("\n" + "="*30)
    print("MENÚ PRINCIPAL")
    print("="*30)
    print("1. Ver datos")
    print("2. Agregar entrada")
    print("3. Configuración")
    print("4. Ayuda")
    print("0. Salir")
    print("-"*30)

def menu_principal():
    """Bucle principal del menú."""
    while True:
        mostrar_menu()
        
        opcion = input("Selecciona una opción: ").strip()
        
        if opcion == "1":
            print("📊 Mostrando datos...")
        elif opcion == "2":
            print("➕ Agregando entrada...")
        elif opcion == "3":
            print("⚙️ Configuración...")
        elif opcion == "4":
            print("❓ Mostrando ayuda...")
        elif opcion == "0":
            print("👋 ¡Hasta luego!")
            break
        else:
            print("❌ Opción no válida")
        
        input("\nPresiona Enter para continuar...")

# menu_principal()  # Descomenta para probar
```

### 6.3. Bucle for: Iteración sobre secuencias

El bucle `for` está diseñado para **iterar sobre secuencias** (listas, tuplas, strings, ranges, etc.). Es ideal cuando **sabemos cuántas iteraciones** necesitamos o queremos procesar cada elemento de una colección.

#### Sintaxis básica

```python
for elemento in secuencia:
    # Código que se ejecuta para cada elemento
    procesar(elemento)
```

#### For con range()

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

#### For con listas

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

#### For con strings

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

#### For con diccionarios

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

#### Ejemplos prácticos con for

**Análisis de datos**

```python
def analizar_ventas(ventas):
    """Analiza una lista de ventas mensuales."""
    total = 0
    mes_mejor = 0
    venta_maxima = 0
    
    print("📊 ANÁLISIS DE VENTAS ANUALES")
    print("="*40)
    
    for mes, venta in enumerate(ventas, 1):
        total += venta
        print(f"Mes {mes:2d}: {venta:>8.2f}€")
        
        if venta > venta_maxima:
            venta_maxima = venta
            mes_mejor = mes
    
    promedio = total / len(ventas)
    
    print("="*40)
    print(f"Total anual:    {total:>8.2f}€")
    print(f"Promedio:       {promedio:>8.2f}€")
    print(f"Mejor mes:      {mes_mejor} ({venta_maxima:.2f}€)")

# Datos de ejemplo
ventas_2024 = [12500, 13200, 11800, 14500, 15200, 16800,
               18500, 17200, 15800, 14200, 13500, 19500]

# analizar_ventas(ventas_2024)  # Descomenta para probar
```

**Tabla de multiplicar**

```python
def tabla_multiplicar(numero, hasta=10):
    """Genera la tabla de multiplicar de un número."""
    print(f"📋 TABLA DEL {numero}")
    print("-" * 20)
    
    for i in range(1, hasta + 1):
        resultado = numero * i
        print(f"{numero} × {i:2d} = {resultado:3d}")

# tabla_multiplicar(7)  # Descomenta para probar
```

**Procesamiento de texto**

```python
def estadisticas_texto(texto):
    """Calcula estadísticas de un texto."""
    palabras = texto.lower().split()
    
    # Contar caracteres
    total_caracteres = len(texto)
    caracteres_sin_espacios = len(texto.replace(' ', ''))
    
    # Contar palabras
    total_palabras = len(palabras)
    
    # Contar frecuencia de palabras
    frecuencia = {}
    for palabra in palabras:
        # Limpiar signos de puntuación básicos
        palabra_limpia = palabra.strip('.,;:!?')
        if palabra_limpia:
            frecuencia[palabra_limpia] = frecuencia.get(palabra_limpia, 0) + 1
    
    # Mostrar estadísticas
    print("📖 ESTADÍSTICAS DEL TEXTO")
    print("="*30)
    print(f"Caracteres:         {total_caracteres}")
    print(f"Caracteres (sin espacios): {caracteres_sin_espacios}")
    print(f"Palabras:           {total_palabras}")
    print(f"Palabras únicas:    {len(frecuencia)}")
    
    # Top 5 palabras más frecuentes
    palabras_ordenadas = sorted(frecuencia.items(), key=lambda x: x[1], reverse=True)
    print("\n🔝 TOP 5 PALABRAS MÁS FRECUENTES:")
    for i, (palabra, frecuencia_palabra) in enumerate(palabras_ordenadas[:5], 1):
        print(f"{i}. {palabra}: {frecuencia_palabra} veces")

# texto_ejemplo = """
# Python es un lenguaje de programación potente y fácil de aprender.
# Python tiene estructuras de datos eficientes y un enfoque simple
# pero efectivo a la programación orientada a objetos.
# """

# estadisticas_texto(texto_ejemplo)  # Descomenta para probar
```

### 6.4. Sentencias de control de bucles

Python proporciona sentencias especiales para controlar el flujo dentro de los bucles.

#### break: Salir del bucle

La sentencia `break` termina inmediatamente el bucle actual y continúa con la siguiente instrucción después del bucle.

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

```python
# Bucle while con break
def pedir_numero_positivo():
    """Pide números hasta obtener uno positivo."""
    while True:  # Bucle infinito controlado
        try:
            numero = float(input("Introduce un número positivo: "))
            if numero > 0:
                print(f"¡Perfecto! Has introducido: {numero}")
                break  # Salir del bucle
            else:
                print("El número debe ser positivo")
        except ValueError:
            print("Debes introducir un número válido")

# pedir_numero_positivo()  # Descomenta para probar
```

#### continue: Saltar a la siguiente iteración

La sentencia `continue` salta el resto del código en la iteración actual y pasa a la siguiente iteración del bucle.

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

```python
# Validar lista de emails
emails = [
    "usuario@ejemplo.com",
    "email_invalido",  # Inválido
    "",               # Vacío
    "otro@sitio.org",
    "sin_arroba.com", # Inválido
    "valido@test.es"
]

emails_validos = []
for email in emails:
    # Saltar emails vacíos
    if not email:
        continue
    
    # Saltar emails sin @
    if "@" not in email:
        print(f"❌ Email inválido: {email}")
        continue
    
    # Saltar emails sin punto
    if "." not in email:
        print(f"❌ Email inválido: {email}")
        continue
    
    emails_validos.append(email)
    print(f"✅ Email válido: {email}")

print(f"\nEmails válidos encontrados: {len(emails_validos)}")
```

#### pass: Instrucción vacía

La sentencia `pass` no hace nada. Se usa como placeholder cuando necesitamos sintaxis válida pero no queremos ejecutar código.

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

#### Cláusula else en bucles

Una característica única de Python es que los bucles pueden tener una cláusula `else` que se ejecuta **solo si el bucle termina normalmente** (sin `break`).

```python
# Buscar elemento con else
def buscar_numero(lista, objetivo):
    """Busca un número en una lista."""
    for numero in lista:
        if numero == objetivo:
            print(f"✅ Encontrado: {objetivo}")
            break
    else:
        # Se ejecuta solo si NO se hizo break
        print(f"❌ No se encontró: {objetivo}")

numeros = [1, 3, 5, 7, 9]
buscar_numero(numeros, 5)  # Encontrado
buscar_numero(numeros, 6)  # No encontrado
```

```python
# Validar contraseña con intentos limitados
def validar_acceso():
    """Permite 3 intentos para introducir la contraseña correcta."""
    password_correcta = "python123"
    intentos_maximos = 3
    
    for intento in range(intentos_maximos):
        password = input(f"Contraseña (intento {intento + 1}/{intentos_maximos}): ")
        
        if password == password_correcta:
            print("🔓 Acceso concedido")
            break
    else:
        # Se ejecuta solo si se agotaron todos los intentos
        print("🔒 Acceso denegado - demasiados intentos fallidos")

# validar_acceso()  # Descomenta para probar
```

### 6.5. Bucles anidados

Los bucles anidados son bucles dentro de otros bucles. Son útiles para trabajar con estructuras bidimensionales (matrices, tablas) o para generar combinaciones.

```python
# Tabla de multiplicar completa
print("📋 TABLAS DE MULTIPLICAR (1-5)")
print("="*50)

for tabla in range(1, 6):
    print(f"\nTabla del {tabla}:")
    for multiplicador in range(1, 11):
        resultado = tabla * multiplicador
        print(f"  {tabla} × {multiplicador:2d} = {resultado:2d}")
```

```python
# Generar matriz
def crear_matriz(filas, columnas):
    """Crea una matriz de números secuenciales."""
    matriz = []
    numero = 1
    
    for fila in range(filas):
        fila_actual = []
        for columna in range(columnas):
            fila_actual.append(numero)
            numero += 1
        matriz.append(fila_actual)
    
    return matriz

def mostrar_matriz(matriz):
    """Muestra una matriz formateada."""
    for fila in matriz:
        for elemento in fila:
            print(f"{elemento:3d}", end=" ")
        print()  # Nueva línea después de cada fila

# matriz_3x4 = crear_matriz(3, 4)
# mostrar_matriz(matriz_3x4)
```

#### ⚠️ Cuidado con la eficiencia

Los bucles anidados pueden ser costosos computacionalmente. La complejidad crece exponencialmente:

```python
import time

def ejemplo_eficiencia():
    """Demuestra el costo de bucles anidados."""
    tamaños = [100, 500, 1000]
    
    for tamaño in tamaños:
        inicio = time.time()
        
        contador = 0
        for i in range(tamaño):
            for j in range(tamaño):
                contador += 1  # Operación simple
        
        fin = time.time()
        tiempo = fin - inicio
        
        print(f"Tamaño {tamaño}x{tamaño}: {tiempo:.4f} segundos")
        print(f"  Operaciones: {contador:,}")

# ejemplo_eficiencia()  # Descomenta para probar (puede tardar)
```

### 6.6. Técnicas avanzadas con bucles

#### Comprensión de listas (List Comprehensions)

Una forma concisa de crear listas usando bucles:

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

#### enumerate() y zip()

Funciones útiles para bucles avanzados:

```python
# enumerate(): obtener índice y elemento
nombres = ["Ana", "Carlos", "María", "Jorge"]

for i, nombre in enumerate(nombres, 1):
    print(f"{i}. {nombre}")

# zip(): iterar múltiples listas simultáneamente
nombres = ["Ana", "Carlos", "María"]
edades = [25, 30, 28]
ciudades = ["Madrid", "Barcelona", "Valencia"]

for nombre, edad, ciudad in zip(nombres, edades, ciudades):
    print(f"{nombre}, {edad} años, vive en {ciudad}")
```

### 6.7. Casos prácticos avanzados

#### Simulador de cajero automático

```python
def cajero_automatico():
    """Simula un cajero automático simple."""
    saldo = 1000.0
    historial = []
    
    while True:
        print(f"\n💰 CAJERO AUTOMÁTICO")
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
            print(f"💵 Tu saldo es: {saldo:.2f}€")
            
        elif opcion == "2":
            try:
                cantidad = float(input("Cantidad a retirar: "))
                if cantidad <= 0:
                    print("❌ La cantidad debe ser positiva")
                elif cantidad > saldo:
                    print("❌ Saldo insuficiente")
                else:
                    saldo -= cantidad
                    historial.append(f"Retiro: -{cantidad:.2f}€")
                    print(f"✅ Has retirado {cantidad:.2f}€")
            except ValueError:
                print("❌ Cantidad inválida")
                
        elif opcion == "3":
            try:
                cantidad = float(input("Cantidad a depositar: "))
                if cantidad <= 0:
                    print("❌ La cantidad debe ser positiva")
                else:
                    saldo += cantidad
                    historial.append(f"Depósito: +{cantidad:.2f}€")
                    print(f"✅ Has depositado {cantidad:.2f}€")
            except ValueError:
                print("❌ Cantidad inválida")
                
        elif opcion == "4":
            if historial:
                print("📋 HISTORIAL DE TRANSACCIONES:")
                for i, transaccion in enumerate(historial, 1):
                    print(f"  {i}. {transaccion}")
            else:
                print("📋 No hay transacciones")
                
        elif opcion == "5":
            print("👋 ¡Gracias por usar nuestro cajero!")
            break
            
        else:
            print("❌ Opción no válida")

# cajero_automatico()  # Descomenta para probar
```

#### Generador de patrones

```python
def generar_patron_triangular(altura):
    """Genera un patrón triangular de asteriscos."""
    print(f"🔺 PATRÓN TRIANGULAR (altura: {altura})")
    
    for fila in range(1, altura + 1):
        espacios = " " * (altura - fila)
        asteriscos = "*" * (2 * fila - 1)
        print(f"{espacios}{asteriscos}")

def generar_patron_diamante(tamaño):
    """Genera un patrón de diamante."""
    print(f"💎 PATRÓN DIAMANTE (tamaño: {tamaño})")
    
    # Parte superior (incluyendo centro)
    for i in range(tamaño):
        espacios = " " * (tamaño - i - 1)
        asteriscos = "*" * (2 * i + 1)
        print(f"{espacios}{asteriscos}")
    
    # Parte inferior
    for i in range(tamaño - 2, -1, -1):
        espacios = " " * (tamaño - i - 1)
        asteriscos = "*" * (2 * i + 1)
        print(f"{espacios}{asteriscos}")

# generar_patron_triangular(5)
# print()
# generar_patron_diamante(4)
```

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
