# Capítulo 5: Variables y Datos. Los Ladrillos del Código

### 5.1. Introducción: Almacenando Información

Para que un programa sea útil, necesita manejar información: el nombre de un usuario, el precio de un producto, la temperatura actual. Pero, ¿dónde guarda el programa esta información mientras trabaja? La respuesta está en las variables. Una variable es el mecanismo fundamental que permite a un programa almacenar y manipular datos de forma dinámica.

Imagina la memoria de tu ordenador como una gran cómoda con infinidad de cajones. Una variable es como uno de esos cajones:

* La etiqueta del cajón es el nombre de la variable (ej: `edad_usuario`).
* El contenido del cajón es el valor que almacena (ej: `25`).
* El tipo de cosas que puedes guardar en el cajón (calcetines, camisetas...) es el tipo de dato (números, texto, etc.).

Usar variables nos permite escribir programas flexibles que reaccionan a diferentes datos de entrada y situaciones.

***

### 5.2. El Enfoque de Python: Tipado Dinámico y Fuerte

Cada lenguaje de programación tiene su propia forma de gestionar las variables. Python se caracteriza por dos conceptos clave que lo hacen muy flexible pero también muy seguro: es de tipado dinámico y fuertemente tipado.

#### **5.2.1 Tipado Dinámico**

En muchos lenguajes, debes declarar de antemano qué tipo de dato va a contener una variable (ej: `int edad;`). Python, en cambio, tiene tipado dinámico: no necesitas declarar el tipo. Python lo infiere automáticamente a partir del valor que le asignas. Además, una misma variable puede cambiar de tipo durante la ejecución del programa.

```python
# Python infiere los tipos automáticamente
mi_variable = 42
print(f"Ahora la variable contiene {mi_variable} y es de tipo {type(mi_variable)}")

mi_variable = "Hola, mundo"
print(f"Ahora la variable contiene '{mi_variable}' y es de tipo {type(mi_variable)}")

mi_variable = True
print(f"Ahora la variable contiene {mi_variable} y es de tipo {type(mi_variable)}")
```

#### **5.2.1 Tipado Fuerte**

Que Python sea flexible no significa que sea descuidado. Python es fuertemente tipado, lo que significa que una vez que una variable tiene un tipo, no puedes realizar operaciones incompatibles con ese tipo. Esto previene muchos errores comunes.

Por ejemplo, no puedes sumar un número y una cadena de texto directamente:

```python
numero = 5
texto = "10"

# Esto provocará un error porque no se puede sumar un int y un str
# resultado = numero + texto 
# TypeError: unsupported operand type(s) for +: 'int' and 'str'

# Para que funcione, debemos hacer una conversión explícita:
# Convertir el texto a número:
resultado_numerico = numero + int(texto) # resultado_numerico será 15

# O convertir el número a texto:
resultado_texto = str(numero) + texto # resultado_texto será "510"
```

{% hint style="info" %}
**Contexto Adicional:** **¿Cómo lo hacen otros lenguajes?**

* **Java/C++ (Tipado Estático y Fuerte)**: Son el opuesto a Python. Debes declarar el tipo de cada variable (`int numero = 10;`) y este no puede cambiar. Son rígidos pero muy seguros y eficientes, ya que todos los tipos se conocen antes de la ejecución.
* **JavaScript (Tipado Dinámico y Débil)**: Es dinámico como Python, pero de tipado débil. Esto significa que intenta "adivinar" lo que quieres hacer con tipos incompatibles, a menudo con resultados inesperados. Por ejemplo, en JavaScript, `5 + "10"` no da un error, sino que produce la cadena `"510"`. Esto puede ocultar errores difíciles de encontrar.
{% endhint %}

Finalmente, es importante saber que en Python las variables deben ser inicializadas (darles un primer valor) antes de poder usarlas, y que la gestión de memoria (reservar y liberar los "cajones") es totalmente automática gracias a un proceso llamado "recolector de basura" (**garbage collector**).

***

### 5.3. Tipos de Datos Fundamentales

Python ofrece varios tipos de datos básicos para representar la información más común.

#### **5.3.1 Enteros**

Representan números enteros, sin parte decimal, tanto positivos como negativos. Una característica destacada de Python es que sus enteros tienen precisión ilimitada, lo que significa que puedes trabajar con números tan grandes como la memoria de tu ordenador lo permita.

```python
edad = 30
temperatura_exterior = -5
poblacion_mundial = 7_900_000_000 # Los guiones bajos se pueden usar para mejorar la legibilidad
```

#### **5.3.2 Punto Flotante**

Representan números con parte decimal. Son esenciales para cálculos científicos, financieros o cualquier medida que no sea entera.

```python
pi = 3.14159
precio_producto = 19.99
altura_metros = 1.78
```

{% hint style="warning" %}
**Atención a la precisión:** Los `float` no siempre son exactos debido a cómo se representan internamente en binario.
{% endhint %}

```python
resultado = 0.1 + 0.2
print(resultado) # Salida: 0.30000000000000004
```

Para aplicaciones que requieren una precisión decimal exacta (como en el ámbito financiero), Python ofrece la librería `decimal`.

#### **5.3.3 Booleanos**

Representan uno de dos valores: `True` (verdadero) o `False` (falso). Son la base de toda la lógica de decisión en programación.

```python
es_mayor_de_edad = True
ha_iniciado_sesion = False
```

En contextos lógicos (como en un `if`), muchos valores se evalúan implícitamente como `False`. Estos incluyen: `None`, `False`, el número `0` (o `0.0`), y cualquier colección vacía como una cadena `""`, una lista `[]` o un diccionario `{}`. Todos los demás valores se evalúan como `True`.

#### **5.3.4 Cadenas de Texto**

Representan secuencias de caracteres. Son inmutables, lo que significa que una vez creada una cadena, no se puede modificar su contenido; cualquier operación que parezca modificarla en realidad crea una nueva cadena.

```python
nombre = "Ada Lovelace"

# Operaciones comunes:
# Concatenación
saludo = "Hola, " + nombre  # "Hola, Ada Lovelace"

# Indexación (acceder a un carácter por su posición, empezando en 0)
primera_letra = nombre[0]  # 'A'

# Slicing (rebanadas para obtener subcadenas)
apellido = nombre[4:]  # "Lovelace"

# Métodos útiles (crean nuevas cadenas)
nombre_mayusculas = nombre.upper()      # "ADA LOVELACE"
nombre_sin_espacios = "  Ana  ".strip() # "Ana"
saludo_modificado = saludo.replace("Hola", "Adiós") # "Adiós, Ada Lovelace"
```

#### **5.3.5 Verificación de Tipos**

A veces necesitas comprobar de qué tipo es una variable.

```python
valor = 10.5
print(type(valor))  # <class 'float'>

# isinstance() es más flexible, ya que también funciona con herencia
print(isinstance(valor, float))  # True
print(isinstance(valor, int))    # False
print(isinstance(valor, (int, float))) # True (¿es un int O un float?)
```

***

### 5.4. Operadores Aritméticos y Precedencia

#### **5.4.1 Operadores Aritméticos**

Son los símbolos que nos permiten realizar operaciones matemáticas.

<table><thead><tr><th>Operador</th><th>Descripción</th><th width="187">Ejemplo (a=17, b=5)</th><th>Resultado</th></tr></thead><tbody><tr><td><code>+</code></td><td>Suma</td><td><code>a + b</code></td><td><code>22</code></td></tr><tr><td><code>-</code></td><td>Resta</td><td><code>a - b</code></td><td><code>12</code></td></tr><tr><td><code>*</code></td><td>Multiplicación</td><td><code>a * b</code></td><td><code>85</code></td></tr><tr><td><code>/</code></td><td>División</td><td><code>a / b</code></td><td><code>3.4</code></td></tr><tr><td><code>//</code></td><td>División Entera</td><td><code>a // b</code></td><td><code>3</code></td></tr><tr><td><code>%</code></td><td>Módulo (Resto)</td><td><code>a % b</code></td><td><code>2</code></td></tr><tr><td><code>**</code></td><td>Potencia</td><td><code>a ** b</code></td><td><code>1419857</code></td></tr></tbody></table>

Python también ofrece operadores que combinan una operación aritmética y una asignación para un código más conciso.

| Operador  | Equivalente  |
| --------- | ------------ |
| `x += 5`  | `x = x + 5`  |
| `x -= 3`  | `x = x - 3`  |
| `x *= 2`  | `x = x * 2`  |
| `x /= 4`  | `x = x / 4`  |
| `x //= 3` | `x = x // 3` |
| `x %= 2`  | `x = x % 2`  |
| `x **= 2` | `x = x ** 2` |

#### **5.4.2 Aplicaciones Prácticas del Operador Módulo `%`**

El operador módulo es sorprendentemente útil:

* Determinar si un número es par o impar: Un número es par si `numero % 2 == 0`.
* Convertir unidades: Para pasar de segundos a minutos y segundos, puedes hacer `minutos = total_segundos // 60` y `segundos = total_segundos % 60`.

#### **5.4.3 Precedencia de Operadores**

Python sigue el orden estándar de las operaciones matemáticas. Las operaciones con mayor precedencia se realizan primero. Los paréntesis `()` se pueden usar para alterar este orden.

```python
# La multiplicación se hace antes que la suma
resultado = 2 + 3 * 4  # 2 + 12 = 14

# Los paréntesis fuerzan a que la suma se haga primero
resultado_con_parentesis = (2 + 3) * 4 # 5 * 4 = 20
```

El orden de precedencia (de mayor a menor) es: `()`, `**`, `* / // %`, `+ -`.

***

### Resumen del Capítulo

En este capítulo hemos introducido las variables como los contenedores de datos de un programa. Hemos analizado el enfoque de Python de tipado dinámico y fuerte, que ofrece flexibilidad sin sacrificar la seguridad. Hemos detallado los tipos de datos fundamentales (`int`, `float`, `bool`, `str`) y hemos explorado los operadores aritméticos y sus reglas de precedencia.

#### **💡 Conceptos Clave**

* **Variable:** Un nombre simbólico asociado a un valor que puede cambiar.
* **Tipado Dinámico vs. Estático:** Si el tipo de la variable se comprueba en tiempo de ejecución o de compilación.
* **Tipado Fuerte vs. Débil:** Si el lenguaje permite operaciones entre tipos incompatibles.
* **Tipos de Datos:** `int`, `float`, `bool`, `str`.
* **Operadores Aritméticos:** `+`, `-`, `*`, `/`, `//`, `%`, `**`.
* **Precedencia:** El orden en que se evalúan las operaciones.

#### **🤔 Preguntas de Reflexión**

1. ¿Qué ventajas y desventajas crees que tiene el tipado dinámico de Python en un proyecto grande con muchos programadores?
2. ¿Por qué es importante entender los problemas de precisión inherentes a los números `float` en aplicaciones financieras?
3. Describe un escenario práctico, además de los mencionados, donde el operador módulo (`%`) podría ser muy útil.

***
