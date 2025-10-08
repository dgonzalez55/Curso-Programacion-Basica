# Capítulo 1: Anatomía de un programa Python

Bienvenido al fascinante mundo de la programación estructurada en Python. En este primer capítulo, exploraremos la estructura fundamental que debe seguir todo programa Python profesional, desde la importación de librerías hasta la organización del código principal. Comprenderás por qué Python ha elegido la **indentación** como pilar de su sintaxis y cómo esto contribuye a crear código limpio, legible y mantenible.

### 1.1. Introducción: La importancia de la estructura

Todo programa Python exitoso comienza con una estructura bien definida. Al igual que un arquitecto no construiría una casa sin planos, un programador profesional nunca debe escribir código sin una estructura clara. La organización adecuada del código no solo facilita su lectura y comprensión, sino que también reduce errores, facilita el mantenimiento y mejora la colaboración en equipo.

Python, con su filosofía de "la legibilidad cuenta" (**readability counts**), ha diseñado un conjunto de convenciones que veremos reflejadas en todos los programas bien escritos.

### 1.2. Estructura típica de un script Python

Un programa Python típico sigue una estructura organizada que incluye estos elementos en orden:

#### Importaciones de librerías

```python
import math
import sys
from datetime import datetime
```

Las importaciones se colocan al principio del archivo y organizan las dependencias externas que necesita nuestro programa.

#### Definición de constantes

```python
PI = math.pi
MAX_INTENTOS = 3
NOMBRE_ARCHIVO = "datos.txt"
```

Las constantes se definen en **MAYÚSCULAS** por convención (PEP 8), aunque Python no tiene constantes verdaderas.

#### Definición de funciones

```python
def calcular_area_circulo(radio):
    """
    Calcula el área de un círculo dado su radio.
    
    Args:
        radio (float): El radio del círculo
        
    Returns:
        float: El área del círculo
    """
    return PI * radio ** 2
```

#### Función principal (main)

```python
def main():
    """Función principal del programa."""
    try:
        radio = float(input("Introduce el radio del círculo: "))
        area = calcular_area_circulo(radio)
        print(f"El área del círculo con radio {radio} es: {area}")
    except ValueError:
        print("Por favor, introduce un valor válido para el radio.")
```

#### Punto de entrada del programa

```python
if __name__ == "__main__":
    main()
```

Este bloque garantiza que la función `main()` solo se ejecute cuando el archivo se ejecuta directamente, no cuando se importa como módulo.

**Ejemplo completo:**

```python
import math

# Constantes
PI = math.pi

def calcular_area_circulo(radio):
    """
    Calcula el área de un círculo dado su radio.
    
    Args:
        radio (float): El radio del círculo
        
    Returns:
        float: El área del círculo
    """
    return PI * radio ** 2

def main():
    """Función principal del programa."""
    try:
        radio = float(input("Introduce el radio del círculo: "))
        area = calcular_area_circulo(radio)
        print(f"El área del círculo con radio {radio} es: {area}")
    except ValueError:
        print("Por favor, introduce un valor válido para el radio.")

if __name__ == "__main__":
    main()
```

### 1.3. Indentación: El corazón de la sintaxis Python

La **indentación** es la característica más distintiva de Python. A diferencia de otros lenguajes que usan llaves `{}` o palabras clave como `begin/end`, Python utiliza la indentación para delimitar bloques de código.

#### Reglas fundamentales de indentación

**1. Obligatoriedad**: La indentación no es opcional en Python; es parte de la sintaxis.

```python
# Correcto
if edad >= 18:
    print("Es mayor de edad")
else:
    print("Es menor de edad")
```

```python
# ERROR: Falta indentación
if edad >= 18:
print("Es mayor de edad")  # IndentationError
```

**2. Consistencia**: Todos los elementos del mismo bloque deben tener la misma indentación.

```python
# Correcto
if condicion:
    instruccion_1()
    instruccion_2()
    instruccion_3()
```

```python
# ERROR: Indentación inconsistente
if condicion:
    instruccion_1()
   instruccion_2()  # IndentationError
```

**3. Jerarquía**: Los bloques anidados requieren niveles adicionales de indentación.

```python
# Correcto: Indentación jerárquica
if numero > 0:
    print("Número positivo")
    if numero % 2 == 0:
        print("Y es par")
    else:
        print("Y es impar")
```

#### Convención recomendada (PEP 8)

* **4 espacios por nivel de indentación**
* **No mezclar espacios y tabuladores**
* Configurar el editor para mostrar espacios en blanco

```python
# Recomendado: 4 espacios por nivel
def funcion():
    if condicion:
        for elemento in lista:
            if elemento > 0:
                print(elemento)
```

#### Técnicas para líneas largas

**Continuación con contrabarra `\`**:

```python
condicion_compleja = condicion1 and condicion2 and \
                     condicion3 and condicion4 and \
                     condicion5
```

**Continuación implícita en paréntesis**:

```python
lista_dias = ["lunes", "martes", "miércoles", "jueves", 
              "viernes", "sábado", "domingo"]
```

**Instrucciones de una línea**:

```python
# Permitido pero no recomendado para código complejo
if mostrar: print("¡Hola mundo!")
```

### 1.4. Comentarios y legibilidad

Los comentarios son fragmentos de texto que no se ejecutan y sirven para documentar el código. Son esenciales para el trabajo en equipo y el mantenimiento a largo plazo.

#### Tipos de comentarios en Python

**1. Comentarios de línea completa**:

```python
# Este es un comentario de línea completa
# Explica lo que hace el siguiente bloque de código
resultado = calcular_promedio(notas)
```

**2. Comentarios inline**:

```python
x = x + 1  # Incrementar contador de intentos
```

**3. Comentarios de múltiples líneas**:

```python
"""
Este es un comentario de múltiples líneas.
Útil para explicaciones largas o para
comentar temporalmente bloques de código.
"""
```

#### Docstrings: Documentación profesional

Los **docstrings** son comentarios especiales que documentan funciones, clases y módulos:

```python
def calcular_imc(peso, altura):
    """
    Calcula el Índice de Masa Corporal (IMC).
    
    El IMC se calcula dividiendo el peso (en kg) por el cuadrado 
    de la altura (en metros).
    
    Args:
        peso (float): Peso en kilogramos
        altura (float): Altura en metros
        
    Returns:
        float: El valor del IMC
        
    Raises:
        ValueError: Si el peso o la altura son negativos o cero
        
    Examples:
        >>> calcular_imc(70, 1.75)
        22.857142857142858
    """
    if peso <= 0 or altura <= 0:
        raise ValueError("Peso y altura deben ser positivos")
    
    return peso / (altura ** 2)
```

#### Buenas prácticas para comentarios

| ✅ Hacer                                | ❌ Evitar                         |
| -------------------------------------- | -------------------------------- |
| **Explicar el "por qué"**, no el "qué" | Comentarios obvios               |
| **Mantener comentarios actualizados**  | Comentarios desactualizados      |
| **Usar lenguaje claro y conciso**      | Comentarios excesivamente largos |
| **Comentar código complejo**           | Sobre-comentar código simple     |

```python
# ✅ Buen comentario
# Aplicamos descuento del 10% para clientes VIP
precio_final = precio_base * 0.9

# ❌ Comentario obvio
# Multiplicamos precio_base por 0.9
precio_final = precio_base * 0.9
```

### 1.5. Entrada, proceso y salida (modelo IPO)

El **modelo IPO** (Input-Process-Output) es un patrón fundamental en programación que estructura la lógica de cualquier programa:

1. **Input (Entrada)**: Recopilar datos del usuario, archivos, bases de datos, etc.
2. **Process (Proceso)**: Transformar, calcular o manipular los datos de entrada
3. **Output (Salida)**: Presentar los resultados al usuario, guardarlos en archivos, etc.

#### Implementación del modelo IPO

```python
def programa_calculadora():
    """Implementa una calculadora básica usando el modelo IPO."""
    
    # === ENTRADA (INPUT) ===
    print("=== Calculadora Básica ===")
    try:
        numero1 = float(input("Introduce el primer número: "))
        operador = input("Introduce el operador (+, -, *, /): ")
        numero2 = float(input("Introduce el segundo número: "))
    except ValueError:
        print("Error: Debes introducir números válidos")
        return
    
    # === PROCESO (PROCESS) ===
    if operador == "+":
        resultado = numero1 + numero2
    elif operador == "-":
        resultado = numero1 - numero2
    elif operador == "*":
        resultado = numero1 * numero2
    elif operador == "/":
        if numero2 != 0:
            resultado = numero1 / numero2
        else:
            print("Error: División por cero no permitida")
            return
    else:
        print("Error: Operador no válido")
        return
    
    # === SALIDA (OUTPUT) ===
    print(f"Resultado: {numero1} {operador} {numero2} = {resultado}")
```

#### Ventajas del modelo IPO

* **Claridad conceptual**: Separa responsabilidades de manera lógica
* **Fácil depuración**: Puedes probar cada fase por separado
* **Reutilización**: Las funciones de procesamiento pueden reutilizarse
* **Mantenibilidad**: Cambios en una fase no afectan necesariamente las otras

### 1.6. El shebang y ejecución de scripts

En sistemas Unix/Linux, puedes hacer que tu script Python sea ejecutable añadiendo una línea **shebang** al principio:

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
Script de ejemplo con shebang y codificación.
"""

def main():
    print("¡Hola desde Python!")

if __name__ == "__main__":
    main()
```

Esto permite ejecutar el script directamente:

```bash
chmod +x mi_script.py
./mi_script.py
```

### Resumen del Capítulo

En este capítulo has aprendido los fundamentos de la estructura de un programa Python profesional. La indentación obligatoria, el uso apropiado de comentarios y docstrings, y la aplicación del modelo IPO son los pilares sobre los que construirás programas robustos y mantenibles.

#### 💡 Conceptos Clave:

* **Estructura estándar**: Importaciones → Constantes → Funciones → Main → Punto de entrada
* **Indentación obligatoria**: 4 espacios por nivel, nunca mezclar con tabuladores
* **Comentarios útiles**: Explicar el "por qué", no el "qué"
* **Docstrings**: Documentación profesional de funciones y clases
* **Modelo IPO**: Entrada → Proceso → Salida para estructurar la lógica

#### 🤔 Preguntas de Reflexión:

1. ¿Por qué crees que Python eligió la indentación obligatoria en lugar de llaves como otros lenguajes?
2. ¿Qué ventajas aporta el patrón `if __name__ == "__main__":` en el desarrollo de módulos reutilizables?
3. ¿Cómo pueden los docstrings bien escritos mejorar la colaboración en equipos de desarrollo?
4. Describe una situación real donde el modelo IPO te ayudaría a estructurar mejor un programa.
