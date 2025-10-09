# Capítulo 1: Anatomía de un programa Python

Al igual que la arquitectura de un edificio define su solidez y funcionalidad, la estructura de un programa informático determina su robustez, legibilidad y mantenibilidad a largo plazo. Un código bien organizado no es un lujo, sino una necesidad profesional. Este capítulo sienta las bases para escribir código Python de alta calidad, explorando la anatomía estándar de un script, desde la disposición de sus componentes hasta las reglas sintácticas, como la indentación, que lo gobiernan. Dominar estos conceptos es el primer paso para pasar de escribir código que funciona a escribir código profesional.

### 1.1. La importancia de la estructura

Un programa Python exitoso comienza con una estructura bien definida. La organización del código es crucial en el desarrollo profesional por varias razones fundamentales:

* **Facilita la lectura**: Un código estructurado es más fácil de entender para otros desarrolladores y para uno mismo en el futuro.
* **Reduce errores**: Una lógica clara y ordenada minimiza la probabilidad de introducir errores sutiles (_bugs_).
* **Simplifica el mantenimiento**: Cuando es necesario modificar o ampliar el programa, una buena estructura permite localizar y cambiar partes del código de forma segura y eficiente.
* **Mejora la colaboración**: En un entorno de equipo, una estructura consistente permite que múltiples desarrolladores trabajen de manera cohesionada.

Esta filosofía está en el corazón de Python, cuyo lema "_la legibilidad cuenta_" (_readability counts_) subraya que <mark style="background-color:$primary;">**el código se escribe una vez, pero se lee muchas veces**</mark>.

***

### 1.2. Estructura típica de un script Python

Un script de Python profesional sigue una secuencia lógica y ordenada para sus componentes. Esta organización no es arbitraria; mejora la claridad y previsibilidad del código.

1. <mark style="background-color:$primary;">**Importaciones de librerías**</mark>: Al principio del archivo, se declaran todas las dependencias externas que el programa necesita, como módulos de la biblioteca estándar o de terceros.
2. <mark style="background-color:$primary;">**Definición de constantes**</mark>: A continuación, se definen los valores que se mantendrán fijos durante la ejecución. Por convención (PEP 8), sus nombres se escriben en mayúsculas (`UPPER_CASE`). Es importante señalar que Python no tiene un mecanismo de "constantes verdaderas"; esta es una convención para indicar al programador que el valor no debe ser modificado.
3. <mark style="background-color:$primary;">**Definición de funciones**</mark>: Aquí se agrupa la lógica reutilizable del programa en bloques de código modulares. Cada función realiza una tarea específica.
4. <mark style="background-color:$primary;">**Función principal**</mark>**&#x20;`main`**: Se considera el punto de partida lógico del programa. Encapsula el flujo principal de ejecución, orquestando las llamadas a otras funciones.
5. <mark style="background-color:$primary;">**Punto de entrada**</mark>**&#x20;`if __name__ == "__main__":`**: Este es un bloque crucial y el pilar sobre el que se construye la modularidad en Python. Su propósito es doble:
   * Permite que el script se ejecute directamente desde la terminal. El código dentro de este bloque solo se ejecuta cuando el archivo es el programa principal.
   * Permite que el script sea importado como un módulo en otro programa sin que su código principal se ejecute automáticamente. Este mecanismo es fundamental para crear librerías y módulos reutilizables, permitiendo que un mismo archivo sirva tanto como un programa independiente como una pieza de un sistema más grande.

A continuación se muestra un ejemplo completo que integra todos estos componentes:

```python
import math

# Constantes
PI = math.pi

def calcular_area_circulo(radio):
    """
    Calcula el área de un círculo dado su radio.

    Args:
        radio (float): El radio del círculo.

    Returns:
        float: El área del círculo.
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

***

### 1.3. Indentación: El corazón de la sintaxis Python

La indentación es, sin duda, la característica más distintiva de la sintaxis de Python. A diferencia de otros lenguajes de programación que utilizan llaves `{}` o palabras clave como `begin`/`end` para delimitar bloques de código, Python utiliza los espacios en blanco. Esta decisión de diseño obliga a escribir código visualmente limpio y estructurado.

#### Las reglas fundamentales de la indentación

**Obligatoriedad**: La indentación no es una sugerencia de estilo, sino una parte integral de la sintaxis. Un bloque de código mal indentado producirá un `IndentationError`.

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

**Consistencia**: Todas las líneas dentro de un mismo bloque de código deben tener exactamente el mismo nivel de indentación.

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

**Jerarquía**: Los bloques de código anidados deben tener un nivel de indentación superior al del bloque que los contienen.

```python
# Correcto: Indentación jerárquica
if numero > 0:
    print("Número positivo")
    if numero % 2 == 0:
        print("Y es par")
    else:
        print("Y es impar")
```

La guía de estilo [**PEP 8**](https://peps.python.org/pep-0008/) establece las siguientes convenciones recomendadas:

* Usar **4 espacios** por cada nivel de indentación.
* **Nunca mezclar espacios y tabuladores**, ya que pueden tener anchos diferentes y causar errores difíciles de depurar.

#### Técnicas para líneas largas

Para manejar líneas de código que superan el límite recomendado de 79 caracteres, existen dos técnicas:

**Continuación con contrabarra `\`**: Permite dividir una instrucción en varias líneas.

```python
condicion_compleja = condicion1 and condicion2 and \
                     condicion3 and condicion4 and \
                     condicion5
```

**Continuación implícita**: Dentro de paréntesis `()`, corchetes `[]` o llaves `{}`, Python permite saltos de línea sin necesidad de una contrabarra, lo cual es más legible.

```python
lista_dias = ["lunes", "martes", "miércoles", "jueves", 
              "viernes", "sábado", "domingo"]
```

Además, es posible omitir la indentación eliminando el salto de línea cuando solo se afecta a una única instrucción, como suele ocurrir en estructuras `if` sencillas. No obstante, se recomienda aplicar este recurso únicamente en fragmentos muy simples, ya que su uso excesivo puede restar claridad y dificultar la lectura del código.

```python
# Permitido pero no recomendado para código complejo
if mostrar: print("¡Hola mundo!")
```

***

### 1.4. Comentarios y legibilidad

Los comentarios son fragmentos de texto dentro del código que el intérprete de Python ignora. Su propósito es documentar el código, explicar la lógica compleja y facilitar el trabajo en equipo y el mantenimiento futuro.

Existen varios tipos de comentarios:

**De línea completa**: Ocupan toda una línea y comienzan con `#`. Se usan para explicar el bloque de código que sigue.

```python
# Este es un comentario de línea completa
# Explica lo que hace el siguiente bloque de código
resultado = calcular_promedio(notas)
```

_**Inline**_: Se colocan en la misma línea que una instrucción, también precedidos por `#`. Deben usarse con moderación para aclaraciones breves.

```python
x = x + 1  # Incrementar contador de intentos
```

**De múltiples líneas**: Se crean usando comillas triples (`"""` o `'''`). Aunque técnicamente son cadenas de texto, se usan comúnmente para comentarios largos o para desactivar temporalmente bloques de código.

```python
"""
Este es un comentario de múltiples líneas.
Útil para explicaciones largas o para
comentar temporalmente bloques de código.
"""
```

#### **Docstrings**

Los <mark style="background-color:$primary;">**docstrings**</mark> son un tipo especial de comentario de múltiples líneas que se coloca como la primera instrucción en un módulo, función, clase o método. Son la forma profesional de documentar el código, ya que herramientas automáticas pueden extraerlos para generar documentación. Un docstring completo describe lo que hace el código, sus parámetros, lo que devuelve y los errores que puede lanzar.

```python
def calcular_imc(peso, altura):
    """Calcula el Índice de Masa Corporal (IMC).

    El IMC se calcula dividiendo el peso (en kg) por el cuadrado
    de la altura (en metros).

    Args:
        peso (float): Peso en kilogramos.
        altura (float): Altura en metros.

    Returns:
        float: El valor del IMC.

    Raises:
        ValueError: Si el peso o la altura son negativos o cero.

    Examples:
        >>> calcular_imc(70, 1.75)
        22.857142857142858
    """
    if peso <= 0 or altura <= 0:
        raise ValueError("Peso y altura deben ser positivos")
    return peso / (altura ** 2)
```

La clave para escribir buenos comentarios es explicar el "porqué" (la intención) y no el "qué" (la acción obvia).

```python
# ✅ Buen comentario
# Aplicamos descuento del 10% para clientes VIP
precio_final = precio_base * 0.9

# ❌ Comentario obvio
# Multiplicamos precio_base por 0.9
precio_final = precio_base * 0.9
```

***

### 1.5. El modelo IPO (Input-Process-Output)

El **modelo IPO** (Entrada-Proceso-Salida) es un patrón fundamental para estructurar la lógica de un programa o de una función. Propone dividir el código en tres fases claras y distintas, similar a una receta de cocina: los ingredientes son la _entrada_, el acto de cocinar es el _proceso_, y el plato final es la _salida_.

1. **Entrada (Input)**: Recopilar los datos necesarios. Esto puede implicar leer datos del teclado, un archivo, una base de datos o una red.
2. **Proceso (Process)**: Manipular los datos de entrada. Aquí se realizan los cálculos, transformaciones y la lógica principal del programa.
3. **Salida (Output)**: Presentar los resultados. Esto puede ser mostrar información en pantalla, guardarla en un archivo o enviarla a otro sistema.

El siguiente ejemplo de una calculadora simple ilustra este modelo, con comentarios que delimitan cada fase:

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

Adoptar el modelo IPO ofrece varias ventajas:

* **Claridad**: Separa las responsabilidades de forma lógica.
* **Fácil depuración**: Permite probar cada fase de forma aislada.
* **Reutilización**: La lógica del proceso puede ser empaquetada en funciones y reutilizada.
* **Mantenibilidad**: Los cambios en la entrada o la salida no afectan necesariamente al proceso.

***

### 1.6. El _shebang_ y ejecución de scripts

En sistemas operativos tipo Unix (como Linux o macOS), la línea _<mark style="background-color:$primary;">**shebang**</mark>_ es la primera línea de un script e indica al sistema qué intérprete debe usar para ejecutarlo. Para Python 3, se suele usar:

```python
#!/usr/bin/env python3

"""
Script de ejemplo con shebang.
"""

def main():
    print("¡Hola desde Python!")

if __name__ == "__main__":
    main()
```

Para que funcione, primero hay que dar permisos de ejecución al archivo y luego se puede ejecutar directamente desde la terminal:

```bash
# Dar permisos de ejecución
chmod +x mi_script.py

# Ejecutar el script
./mi_script.py
```

***

### Resumen del Capítulo

En este capítulo hemos sentado las bases de la programación estructurada en Python. La indentación, una estructura clara y una buena documentación son los pilares sobre los que construiremos programas robustos. Ahora que entendemos cómo organizar el código, el siguiente paso es explorar los datos que estos programas manipulan.

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

***
