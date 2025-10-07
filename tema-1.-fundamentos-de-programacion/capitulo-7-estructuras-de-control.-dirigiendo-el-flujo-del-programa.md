# Capítulo 7: Estructuras de Control. Dirigiendo el Flujo del Programa

### 7.1. Introducción: Los Pilares de la Lógica

Hemos aprendido a manejar datos, pero ¿cómo organizamos las instrucciones para que el programa haga algo útil? La respuesta está en las estructuras de control. Son los bloques de construcción con los que se erige toda la lógica de un programa. Sorprendentemente, el **Teorema del Programa Estructurado** postula que cualquier algoritmo, sin importar su complejidad, puede ser implementado utilizando únicamente tres estructuras fundamentales:

* **Secuencial**: Las instrucciones se ejecutan una tras otra.
* **Alternativa (o Condicional)**: Se elige un camino de ejecución entre varios posibles.
* **Iterativa (o Repetitiva)**: Un bloque de instrucciones se repite múltiples veces.

Dominar estas tres estructuras es dominar la esencia de la programación.

### 7.2. Estructura Secuencial

Es la estructura más simple y natural. Las instrucciones del programa se ejecutan en el orden en que están escritas, de arriba hacia abajo, una después de la otra. Ya hemos estado usando esta estructura en todos los ejemplos anteriores.

El aspecto más crítico de la estructura secuencial es que el orden importa. Una instrucción que depende del resultado de otra debe ir después.

```python
# ORDEN CORRECTO
# Primero calculamos el resultado
resultado = 2 * 5
# Luego lo mostramos
print(resultado) # Salida: 10

# ORDEN INCORRECTO
# Intentamos mostrar el resultado antes de calcularlo
# print(resultado) # NameError: name 'resultado' is not defined
# resultado = 2 * 5
```

### 7.3. Estructuras Alternativas: Tomando Decisiones

Estas estructuras permiten que un programa tome diferentes caminos en función de si se cumple o no una condición.

#### **7.3.1 Simple**

Ejecuta un bloque de código solo si una condición es `True`.

```python
edad = 20
if edad >= 18:
    print("Eres mayor de edad.")
# Esta línea se ejecuta siempre, esté dentro o fuera del if.
print("Fin del programa.")
```

#### **7.3.2 Doble**

Ejecuta un bloque de código si la condición es `True` y otro bloque diferente si es `False`.

```python
divisor = 0
if divisor == 0:
    print("Error: No se puede dividir por cero.")
else:
    resultado = 10 / divisor
    print(f"El resultado es {resultado}.")
```

#### **7.3.3 Múltiple con `if-elif-else`**

Permite encadenar múltiples condiciones. El programa evalúa las condiciones en orden y ejecuta el primer bloque cuya condición sea `True`. Si ninguna es `True`, ejecuta el bloque `else` (si existe).

```python
nota = 7.5
if nota >= 9:
    print("Sobresaliente")
elif nota >= 7:
    print("Notable")
elif nota >= 5:
    print("Aprobado")
else:
    print("Suspenso")
```

#### **7.3.4 Múltiple con `match-case` (Python 3.10+)**

Esta estructura es una alternativa moderna y muy legible a largas cadenas de `if-elif-else`, especialmente cuando se compara una única variable contra varios valores concretos.

Ejemplo de menú con `if-elif-else`:

```python
opcion = "2"
if opcion == "1":
    print("Mostrando perfil...")
elif opcion == "2":
    print("Editando configuración...")
elif opcion == "3":
    print("Cerrando sesión...")
else:
    print("Opción no válida.")
```

Mismo ejemplo con `match-case`:

```python
opcion = "2"
match opcion:
    case "1":
        print("Mostrando perfil...")
    case "2":
        print("Editando configuración...")
    case "3":
        print("Cerrando sesión...")
    case _: # El guion bajo actúa como el 'else' por defecto
        print("Opción no válida.")
```

### 7.4. Estructuras Iterativas: El Poder de la Repetición

Las estructuras iterativas, o bucles, permiten ejecutar un bloque de código repetidamente, lo cual es fundamental para automatizar tareas. Todo bucle bien construido sigue cuatro reglas:

1. **Variable de control:** Una variable que controla el bucle.
2. **Inicialización:** La variable de control debe tener un valor inicial antes de empezar el bucle.
3. **Condición:** Una condición que se evalúa en cada iteración para decidir si el bucle continúa o termina.
4. **Actualización:** La variable de control debe modificarse dentro del bucle para que, eventualmente, la condición de fin se cumpla.

#### **7.4.1 El Bucle `while`**

El bucle `while` se repite mientras una condición sea `True`. Es ideal cuando no sabemos de antemano cuántas veces se debe repetir el bucle.

```python
# Ejemplo: Validar que la edad introducida esté en un rango correcto
edad = -1 # 2. Inicialización
while not (0 <= edad <= 120): # 3. Condición
    try:
        # 4. Actualización (dentro del input)
        edad = int(input("Introduce una edad válida (0-120): "))
    except ValueError:
        print("Por favor, introduce un número.")
print(f"Edad correcta registrada: {edad}")
```

<mark style="background-color:$danger;">**⚠️ Peligro: Bucles Infinitos**</mark>

Si olvidas la regla de la actualización, la condición del bucle nunca cambiará a `False`, y el programa se quedará "atascado" repitiendo el mismo código para siempre. Esto se conoce como un bucle infinito.

#### **7.4.2 El Bucle `for`**

El bucle `for` se utiliza para iterar sobre una secuencia de elementos (como una lista o una cadena) o cuando sabemos exactamente cuántas veces queremos que se repita el código. En Python, se usa comúnmente con la función `range()`.

`range()` puede tener hasta tres argumentos:

* `range(stop)`: Genera números de 0 hasta `stop-1`.
* `range(start, stop)`: Genera números de `start` hasta `stop-1`.
* `range(start, stop, step)`: Genera números de `start` hasta `stop-1`, incrementando en `step`.

```python
# Ejemplo: Mostrar la tabla de multiplicar del 7
print("--- Tabla del 7 ---")
for i in range(1, 11): # Genera números del 1 al 10
    print(f"7 x {i} = {7 * i}")
```

#### **7.4.3 `while` vs. `for` : ¿Cuándo usar cada uno?**

| Característica | while                                                                                                                                          | for                                                                                                                               |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| **Uso Típico** | El número de iteraciones es desconocido; depende de una condición externa o de la entrada del usuario.                                         | El número de iteraciones es conocido de antemano o se itera sobre los elementos de una secuencia finita.                          |
| **Control**    | El programador es responsable de gestionar explícitamente la inicialización, la condición de fin y la actualización de la variable de control. | La iteración y la actualización de la variable de control son gestionadas implícitamente por la secuencia (`range`, lista, etc.). |
| **Riesgo**     | Mayor riesgo de bucles infinitos si se olvida actualizar la variable de control.                                                               | Menor riesgo, ya que el final está definido por la longitud de la secuencia.                                                      |

### 7.5. Control Avanzado de Bucles

A veces necesitamos un control más fino sobre el comportamiento de un bucle.

* `break`: Interrumpe y sale del bucle inmediatamente, sin importar la condición.
* `continue`: Salta el resto del código de la iteración actual y pasa directamente a la siguiente.

***

### Resumen del Capítulo

Hemos profundizado en las estructuras de control, que son los pilares lógicos de cualquier programa. El **Teorema del Programa Estructurado** nos asegura que solo necesitamos tres tipos de estructuras para implementar cualquier algoritmo: secuencial, alternativa (condicional) e iterativa (repetitiva).

La estructura secuencial es la ejecución ordenada de instrucciones, donde el orden es fundamental para la lógica.

Las estructuras alternativas (o condicionales, como `if`, `if-else`, y las cadenas `if-elif-else`) permiten al programa tomar decisiones en tiempo real basadas en la evaluación de una condición, incluyendo la estructura moderna `match-case` de Python.

Finalmente, las estructuras iterativas o bucles (como `while` y `for`) permiten la automatización de tareas repetitivas. Hemos identificado las reglas de oro para construir bucles (Inicialización, Condición y Actualización), y distinguido cuándo usar el bucle `while` (iteraciones desconocidas) o el bucle `for` (iteraciones conocidas o sobre una secuencia).

#### **💡 Conceptos Clave**:

* **Estructuras de Control:** Bloques fundamentales (Secuencial, Alternativa e Iterativa) para crear cualquier lógica de programa.
* **Secuencial:** Las instrucciones se ejecutan de arriba abajo; el orden es crucial.
* **Alternativa/Condicional:** Permite elegir un camino (`if-else`) basado en una condición booleana.
* **Estructura Iterativa (Bucle):** Bloque que se repite múltiples veces.
* **Reglas del Bucle:** El ciclo de vida de un bucle requiere una Variable de Control, su Inicialización, una Condición y su Actualización.
* **Bucle `while`:** Bucle que se repite mientras una condición sea `True`. Ideal para número de iteraciones desconocido.
* **Bucle `for`:** Bucle para iterar sobre una secuencia finita (p. ej., utilizando `range()`).
* **Bucle Infinito:** Ocurre cuando se olvida actualizar la variable de control, y la condición de fin nunca se alcanza

#### **🤔 Preguntas de Reflexión**:

1. Si tuvieras que diseñar un programa que pregunte al usuario si quiere continuar una operación (S/N), ¿usarías un bucle `for` o un bucle `while`? Justifica tu elección basándote en la regla de las iteraciones.
2. ¿Por qué el orden en que se escriben las condiciones en una cadena `if-elif-else` es crucial para la lógica, especialmente si las condiciones se solapan?
3. ¿Cómo te ayuda la estructura `match-case` a prevenir errores lógicos en comparación con una larga cadena `if-elif-else`?

***
