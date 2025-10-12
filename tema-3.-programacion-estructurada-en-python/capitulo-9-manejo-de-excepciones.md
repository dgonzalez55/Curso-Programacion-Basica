# Capítulo 9: Manejo de excepciones

Una **excepción** es un error que ocurre durante la ejecución de un programa y que interrumpe su flujo normal, pero no está necesariamente vinculado a un error de sintaxis. Pueden ser causadas por datos de entrada incorrectos, recursos no disponibles u operaciones inválidas. Un **manejo de excepciones** adecuado es la diferencia entre una aplicación frágil que se detiene inesperadamente y una aplicación robusta que puede anticipar, gestionar y recuperarse de los errores de forma elegante.

En Python, el manejo de excepciones se realiza mediante las estructuras `try`, `except`, `else` y `finally`, que nos permiten capturar errores específicos, manejarlos apropiadamente y ejecutar código de limpieza cuando sea necesario.

### 9.1. ¿Qué son las excepciones?

Las excepciones son eventos que interrumpen el flujo normal de ejecución de un programa. Aunque el código sea sintácticamente correcto, pueden ocurrir errores durante la ejecución por diversos motivos:

* **Entrada de usuario incorrecta**: El usuario introduce texto donde se espera un número
* **Recursos no disponibles**: Un archivo no existe o no se puede acceder
* **Operaciones inválidas**: División por cero, acceso a índices fuera de rango
* **Problemas de red**: Conexión perdida, servidor no responde
* **Memoria insuficiente**: El sistema no tiene suficientes recursos

#### Ejemplo básico sin manejo de excepciones

```python
# Sin manejo de excepciones - el programa se detiene
print(5 / 0)  # ZeroDivisionError: division by zero
print("Esta línea nunca se ejecutará")
```

#### Con manejo de excepciones

```python
# Con manejo de excepciones - el programa continúa
try:
    print(5 / 0)
except ZeroDivisionError:
    print("No se puede dividir por cero")

print("Esta línea sí se ejecutará")
```

### 9.2. Estructura básica: `try-except`

La forma fundamental de manejar excepciones en Python es con el bloque `try-except`.

* El código que podría generar un error se coloca dentro del bloque `try`.
* Si se produce una excepción dentro del bloque `try`, Python busca una cláusula `except` que coincida con el tipo de excepción. Si la encuentra, ejecuta el código de ese bloque.

#### Sintaxis básica

```python
try:
    # Código que puede generar una excepción
    codigo_riesgoso()
except TipoDeExcepcion:
    # Código que se ejecuta si ocurre esa excepción específica
    manejar_error()
```

#### Ejemplo práctico: División segura

```python
def division_segura(a, b):
    """Realiza una división manejando la excepción de división por cero."""
    try:
        resultado = a / b
        print(f"{a} ÷ {b} = {resultado}")
        return resultado
    except ZeroDivisionError:
        print("Error: No se puede dividir por cero")
        return None

# Pruebas
division_segura(10, 2)   # 10 ÷ 2 = 5.0
division_segura(10, 0)   # Error: No se puede dividir por cero
division_segura(15, 3)   # 15 ÷ 3 = 5.0
```

{% hint style="success" %}
Es una **buena práctica capturar las excepciones más específicas** posibles en lugar de errores genéricos.
{% endhint %}

### 9.3. Excepciones múltiples y jerarquía

#### Capturar múltiples excepciones con una sola cláusula

```python
def acceder_lista(lista, indice):
    """Accede a un elemento de la lista con manejo de errores múltiples."""
    try:
        elemento = lista[indice]
        print(f"Elemento en posición {indice}: {elemento}")
        return elemento
    except (IndexError, TypeError) as e:
        print(f"❌ Error de acceso: {e}")
        return None

# Pruebas
mi_lista = [1, 2, 3, 4, 5]
acceder_lista(mi_lista, 2)      # Elemento en posición 2: 3
acceder_lista(mi_lista, 10)     # Error: list index out of range
acceder_lista(mi_lista, "a")    # Error: list indices must be integers
```

#### Capturar excepciones en cascada

```python
def procesar_archivo(nombre_archivo):
    """Procesa un archivo con manejo escalonado de errores."""
    try:
        # Intentar abrir el archivo
        with open(nombre_archivo, 'r', encoding='utf-8') as archivo:
            contenido = archivo.read()
            numero = int(contenido.strip())
            resultado = 100 / numero
            print(f"Resultado: {resultado}")
            return resultado
            
    except FileNotFoundError:
        print(f"❌ El archivo '{nombre_archivo}' no existe")
    except PermissionError:
        print(f"❌ Sin permisos para leer '{nombre_archivo}'")
    except ValueError:
        print(f"❌ El contenido del archivo no es un número válido")
    except ZeroDivisionError:
        print(f"❌ El número en el archivo es cero (división por cero)")
    except Exception as e:
        print(f"❌ Error inesperado: {e}")
    
    return None

# Crear archivo de prueba
# with open('numero.txt', 'w') as f:
#     f.write('10')

# procesar_archivo('numero.txt')        # Resultado: 10.0
# procesar_archivo('inexistente.txt')   # El archivo no existe
```

### 9.4. Captura genérica con `Exception`

#### Capturar cualquier excepción

```python
def operacion_compleja(a, b, operacion):
    """Realiza operaciones matemáticas con manejo genérico de errores."""
    try:
        if operacion == '+':
            resultado = a + b
        elif operacion == '-':
            resultado = a - b
        elif operacion == '*':
            resultado = a * b
        elif operacion == '/':
            resultado = a / b
        elif operacion == '**':
            resultado = a ** b
        elif operacion == '//':
            resultado = a // b
        elif operacion == '%':
            resultado = a % b
        else:
            raise ValueError(f"Operación '{operacion}' no soportada")
        
        print(f"{a} {operacion} {b} = {resultado}")
        return resultado
        
    except Exception as e:
        print(f"❌ Error durante la operación: {type(e).__name__}: {e}")
        return None

# Pruebas
operacion_compleja(10, 2, '+')     # 10 + 2 = 12
operacion_compleja(10, 0, '/')     # Error: ZeroDivisionError: division by zero
operacion_compleja(10, 2, '&')     # Error: ValueError: Operación '&' no soportada
```

#### Información detallada del error

```python
import traceback

def funcion_con_error_detallado():
    """Demuestra cómo obtener información detallada de errores."""
    try:
        # Cadena de operaciones que pueden fallar
        datos = [1, 2, 3]
        indice = int(input("Introduce un índice: "))
        resultado = 10 / datos[indice]
        print(f"Resultado: {resultado}")
        
    except Exception as e:
        print("="*50)
        print("INFORMACIÓN DETALLADA DEL ERROR")
        print("="*50)
        print(f"Tipo de excepción: {type(e).__name__}")
        print(f"Mensaje: {e}")
        print(f"Argumentos: {e.args}")
        print("\nStack trace completo:")
        traceback.print_exc()
        print("="*50)

# funcion_con_error_detallado()  # Descomenta para probar
```

### 9.5. Las cláusulas `else` y `finally`

La estructura `try-except` puede ampliarse con dos cláusulas opcionales: `else` y `finally`.

* **`else`**: El bloque de código dentro de `else` se ejecuta solo si no ocurre ninguna excepción en el bloque `try`. Es útil para separar la lógica que debe ejecutarse cuando todo va bien.
* **`finally`**: El bloque de código dentro de `finally` se ejecuta siempre, sin importar si ocurrió una excepción o no. Su propósito principal es realizar tareas de "limpieza", como cerrar archivos o conexiones a bases de datos.

```python
def conexion_base_datos():
    """Simula conexión a base de datos con limpieza garantizada."""
    conexion = None
    try:
        print("Conectando a la base de datos...")
        conexion = "ConexionActiva" # Simula éxito
        print("Conexión establecida")
        # ... operaciones con la base de datos ...
    except ConnectionError as e:
        print(f"Error de conexión: {e}")
        return None
    else:
        print("Operaciones completadas exitosamente")
    finally:
        # Se ejecuta SIEMPRE, haya o no excepción
        if conexion:
            print("Cerrando conexión a la base de datos")
        else:
            print("Limpiando recursos de conexión fallida")
```

### 9.6. Excepciones comunes en Python

#### ValueError: Valor incorrecto

```python
def edad_valida(edad_str):
    """Valida y convierte edad con manejo específico de ValueError."""
    try:
        edad = int(edad_str)
        if not (0 <= edad <= 150):
            raise ValueError("La edad debe estar entre 0 y 150 años")
        return edad
    except ValueError as e:
        if "invalid literal" in str(e):
            print(f"❌ '{edad_str}' no es un número válido")
        else:
            print(f"❌ {e}")
        return None

# Pruebas
print(edad_valida("25"))     # 25
print(edad_valida("abc"))    # Error: 'abc' no es un número válido
print(edad_valida("200"))    # Error: La edad debe estar entre 0 y 150 años
```

#### TypeError: Tipo incorrecto

```python
def concatenar_elementos(lista):
    """Concatena elementos de una lista con manejo de TypeError."""
    try:
        if not isinstance(lista, list):
            raise TypeError("Se esperaba una lista")
        
        resultado = ""
        for elemento in lista:
            resultado += str(elemento) + " "
        
        return resultado.strip()
        
    except TypeError as e:
        print(f"Error de tipo: {e}")
        return None

# Pruebas
print(concatenar_elementos([1, 2, 3, "a"]))  # "1 2 3 a"
print(concatenar_elementos("no es lista"))   # Error: Se esperaba una lista
```

#### IndexError y KeyError

```python
def acceder_datos_seguros(datos, clave_o_indice):
    """Accede a datos con manejo de IndexError y KeyError."""
    try:
        if isinstance(datos, list):
            return datos[clave_o_indice]
        elif isinstance(datos, dict):
            return datos[clave_o_indice]
        else:
            raise TypeError("Datos deben ser lista o diccionario")
            
    except IndexError:
        print(f"❌ Índice {clave_o_indice} fuera de rango para lista de tamaño {len(datos)}")
    except KeyError:
        claves_disponibles = list(datos.keys()) if isinstance(datos, dict) else []
        print(f"❌ Clave '{clave_o_indice}' no existe. Claves disponibles: {claves_disponibles}")
    except TypeError as e:
        print(f"❌ {e}")
    
    return None

# Pruebas
lista = [1, 2, 3]
diccionario = {"a": 1, "b": 2, "c": 3}

print(acceder_datos_seguros(lista, 1))       # 2
print(acceder_datos_seguros(lista, 10))      # Error: Índice fuera de rango
print(acceder_datos_seguros(diccionario, "b"))  # 2
print(acceder_datos_seguros(diccionario, "z"))  # Error: Clave no existe
```

### 9.7. Lanzar excepciones con `raise`

Además de capturar excepciones, también podemos lanzarlas manualmente usando la palabra clave `raise`. Esto es útil para señalar errores basados en la lógica de negocio de nuestra aplicación. Para errores muy específicos, se pueden crear clases de excepción personalizadas heredando de `Exception`.

```python
class ErrorDeInventario(Exception):
    """Excepción para errores relacionados con el inventario."""
    pass

def vender_producto(stock_actual, cantidad):
    if cantidad <= 0:
        raise ValueError("La cantidad a vender debe ser positiva.")
    if stock_actual < cantidad:
        raise ErrorDeInventario("No hay stock suficiente para la venta.")
    return stock_actual - cantidad
```

### 9.8. Caso práctico: Sistema de login

Este ejemplo implementa un sistema de login robusto que maneja múltiples tipos de errores, incluyendo entradas inválidas y credenciales incorrectas, con un límite de intentos.

```python
def sistema_login():
    """Sistema de login con manejo de excepciones y límite de intentos."""
    usuarios = {"admin": "admin123", "usuario": "password"}
    max_intentos = 3
    intentos = 0
    
    while intentos < max_intentos:
        try:
            print(f"\nLOGIN - Intento {intentos + 1} de {max_intentos}")
            usuario = input("Usuario: ").strip()
            password = input("Contraseña: ").strip()
            
            if not usuario or not password:
                raise ValueError("Usuario y contraseña no pueden estar vacíos")
            
            if usuario not in usuarios:
                raise KeyError(f"Usuario '{usuario}' no existe")
                
            if usuarios[usuario] != password:
                raise ValueError("Contraseña incorrecta")
            
            print(f"Bienvenido, {usuario}!")
            return True
            
        except (ValueError, KeyError) as e:
            print(f"❌ Error: {e}")
            intentos += 1
        except KeyboardInterrupt:
            print("\n\nLogin cancelado.")
            return False
            
    print(f"\nDemasiados intentos fallidos. Acceso bloqueado.")
    return False
```

### 9.9. Mejores prácticas

#### **✅ Buenas prácticas**

* <mark style="background-color:$primary;">**Sé específico al capturar excepciones**</mark>: Captura los errores concretos que esperas (`ValueError`, `FileNotFoundError`).
* <mark style="background-color:$primary;">**No silencies errores**</mark>: Evita los bloques `except: pass`, ya que ocultan problemas y dificultan la depuración.
* <mark style="background-color:$primary;">**Usa**</mark><mark style="background-color:$primary;">**&#x20;**</mark><mark style="background-color:$primary;">**`finally`**</mark><mark style="background-color:$primary;">**&#x20;**</mark><mark style="background-color:$primary;">**para la limpieza**</mark>: Garantiza que los recursos se liberen correctamente.

#### **❌ Prácticas a evitar**

* <mark style="background-color:$primary;">**No usar**</mark> [<mark style="background-color:$primary;">**`except`**</mark><mark style="background-color:$primary;">**&#x20;**</mark><mark style="background-color:$primary;">**vacío**</mark>](#user-content-fn-1)[^1]: Es el peor anti-patrón, ya que captura absolutamente todo, incluyendo `SystemExit` y `KeyboardInterrupt`.
* <mark style="background-color:$primary;">**No capturar**</mark><mark style="background-color:$primary;">**&#x20;**</mark><mark style="background-color:$primary;">**`Exception`**</mark><mark style="background-color:$primary;">**&#x20;**</mark><mark style="background-color:$primary;">**de forma genérica sin necesidad**</mark>: A menos que estés registrando el error y volviéndolo a lanzar, esto puede ocultar errores que no esperabas.
* <mark style="background-color:$primary;">**No usar excepciones para el control de flujo normal**</mark>: Son para situaciones excepcionales, no para la lógica habitual del programa.

### Resumen del Capítulo

El manejo adecuado de excepciones es fundamental para crear aplicaciones robustas y confiables. Python proporciona un sistema completo de manejo de errores que permite capturar, procesar y recuperarse de situaciones excepcionales de manera elegante, mejorando significativamente la experiencia del usuario y la estabilidad del software.

#### 💡 Conceptos Clave:

* **try-except**: Estructura básica para capturar y manejar errores
* **Excepciones específicas**: `ValueError`, `TypeError`, `FileNotFoundError`, etc.
* **else**: Se ejecuta solo si NO ocurre ninguna excepción
* **finally**: Se ejecuta SIEMPRE, para limpieza de recursos
* **raise**: Lanzar excepciones personalizadas
* **Excepciones personalizadas**: Crear clases de error específicas para tu aplicación

#### 🤔 Preguntas de Reflexión:

1. ¿Cuándo es apropiado usar `except Exception` en lugar de excepciones específicas?
2. ¿Qué diferencia existe entre los bloques `else` y `finally`?
3. ¿En qué situaciones crearías tus propias clases de excepción?
4. ¿Cómo puede el manejo de excepciones mejorar la experiencia del usuario?

#### 🔧 Ejercicio Práctico:

Crea un programa que:

1. Implemente un sistema de gestión de inventario con validaciones
2. Use excepciones específicas para diferentes tipos de errores
3. Incluya manejo de archivos con `try-except-finally`
4. Cree excepciones personalizadas para reglas de negocio
5. Proporcione mensajes de error informativos y opciones de recuperación

Escribir código que funciona y es robusto ante los fallos es solo la mitad de la ecuación. La otra mitad es escribirlo de una manera que sea clara, consistente y fácil de mantener; esto es precisamente lo que aprenderemos en el próximo capítulo.

[^1]: 
