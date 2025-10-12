# Capítulo 9: Manejo de excepciones

Una **excepción** es un error que ocurre durante la ejecución de un programa, pero que no necesariamente está vinculado a la sintaxis del código. El **manejo de excepciones** nos permite controlar estos errores de manera elegante, evitando que nuestros programas se detengan abruptamente y proporcionando una mejor experiencia al usuario.

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
# ❌ Sin manejo de excepciones - el programa se detiene
print(5 / 0)  # ZeroDivisionError: division by zero
print("Esta línea nunca se ejecutará")
```

#### Con manejo de excepciones

```python
# ✅ Con manejo de excepciones - el programa continúa
try:
    print(5 / 0)
except ZeroDivisionError:
    print("No se puede dividir por cero")

print("Esta línea sí se ejecutará")
```

### 9.2. Estructura básica: try-except

La estructura `try-except` es la forma fundamental de manejar excepciones en Python.

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
        print("❌ Error: No se puede dividir por cero")
        return None

# Pruebas
division_segura(10, 2)   # 10 ÷ 2 = 5.0
division_segura(10, 0)   # Error: No se puede dividir por cero
division_segura(15, 3)   # 15 ÷ 3 = 5.0
```

#### Capturar múltiples excepciones específicas

```python
def convertir_a_numero(entrada):
    """Convierte entrada de usuario a número con manejo de errores."""
    try:
        # Intentar convertir a entero primero
        if '.' not in entrada:
            return int(entrada)
        else:
            return float(entrada)
    except ValueError:
        print(f"❌ '{entrada}' no es un número válido")
        return None
    except TypeError:
        print(f"❌ El tipo de dato '{type(entrada)}' no se puede convertir")
        return None

# Pruebas
print(convertir_a_numero("42"))      # 42
print(convertir_a_numero("3.14"))    # 3.14
print(convertir_a_numero("abc"))     # Error: 'abc' no es un número válido
print(convertir_a_numero(None))      # Error: El tipo de dato...
```

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

### 9.4. Captura genérica con Exception

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

### 9.5. Cláusulas else y finally

#### else: Cuando NO ocurre ninguna excepción

```python
def leer_archivo_completo(nombre_archivo):
    """Lee un archivo con cláusula else."""
    try:
        with open(nombre_archivo, 'r', encoding='utf-8') as archivo:
            contenido = archivo.read()
    except FileNotFoundError:
        print(f"❌ El archivo '{nombre_archivo}' no existe")
        return None
    except PermissionError:
        print(f"❌ Sin permisos para leer '{nombre_archivo}'")
        return None
    else:
        # Se ejecuta SOLO si NO ocurrió ninguna excepción
        print(f"✅ Archivo '{nombre_archivo}' leído exitosamente")
        print(f"Tamaño: {len(contenido)} caracteres")
        return contenido
```

#### finally: Se ejecuta SIEMPRE

```python
def conexion_base_datos():
    """Simula conexión a base de datos con limpieza garantizada."""
    conexion = None
    try:
        print("🔌 Conectando a la base de datos...")
        # Simular posible fallo en la conexión
        import random
        if random.choice([True, False]):
            raise ConnectionError("No se puede conectar al servidor")
        
        conexion = "ConexionActiva"
        print("✅ Conexión establecida")
        
        # Operaciones con la base de datos
        print("📝 Ejecutando consultas...")
        resultado = "Datos obtenidos"
        return resultado
        
    except ConnectionError as e:
        print(f"❌ Error de conexión: {e}")
        return None
    else:
        print("✅ Operaciones completadas exitosamente")
    finally:
        # Se ejecuta SIEMPRE, haya o no excepción
        if conexion:
            print("🔌 Cerrando conexión a la base de datos")
        else:
            print("🔌 Limpiando recursos de conexión fallida")

# conexion_base_datos()  # Descomenta para probar
```

#### Ejemplo completo: Procesador de archivos con todas las cláusulas

```python
def procesar_archivo_completo(nombre_archivo):
    """Ejemplo completo de manejo de excepciones con todas las cláusulas."""
    archivo = None
    resultado = None
    
    try:
        print(f"📁 Intentando abrir '{nombre_archivo}'...")
        archivo = open(nombre_archivo, 'r', encoding='utf-8')
        
        print("📖 Leyendo contenido...")
        contenido = archivo.read()
        
        print("🔢 Procesando datos...")
        lineas = contenido.strip().split('\n')
        numeros = [float(linea) for linea in lineas if linea.strip()]
        resultado = sum(numeros) / len(numeros)
        
    except FileNotFoundError:
        print(f"❌ El archivo '{nombre_archivo}' no existe")
    except PermissionError:
        print(f"❌ Sin permisos para leer '{nombre_archivo}'")
    except ValueError as e:
        print(f"❌ Error en los datos: {e}")
    except ZeroDivisionError:
        print(f"❌ El archivo está vacío o sin números válidos")
    except Exception as e:
        print(f"❌ Error inesperado: {e}")
    else:
        # Solo se ejecuta si NO hubo excepciones
        print(f"✅ Archivo procesado exitosamente")
        print(f"Promedio calculado: {resultado:.2f}")
    finally:
        # SIEMPRE se ejecuta
        if archivo:
            archivo.close()
            print("🔒 Archivo cerrado correctamente")
        print("🧹 Limpieza completada")
    
    return resultado

# Crear archivo de prueba
# with open('numeros.txt', 'w') as f:
#     f.write('10\n20\n30\n40\n50')

# procesar_archivo_completo('numeros.txt')
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
        print(f"❌ Error de tipo: {e}")
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

### 9.7. Lanzar excepciones personalizadas

#### raise: Lanzar excepciones manualmente

```python
def calcular_descuento(precio, descuento_porcentaje):
    """Calcula descuento con validaciones y excepciones personalizadas."""
    if precio < 0:
        raise ValueError("El precio no puede ser negativo")
    
    if not (0 <= descuento_porcentaje <= 100):
        raise ValueError("El descuento debe estar entre 0% y 100%")
    
    descuento = precio * (descuento_porcentaje / 100)
    precio_final = precio - descuento
    
    return {
        'precio_original': precio,
        'descuento_porcentaje': descuento_porcentaje,
        'descuento_cantidad': descuento,
        'precio_final': precio_final
    }

# Uso con manejo de errores
def aplicar_descuento_seguro(precio, descuento):
    """Aplica descuento con manejo de excepciones."""
    try:
        resultado = calcular_descuento(precio, descuento)
        print(f"✅ Precio original: {resultado['precio_original']:.2f}€")
        print(f"✅ Descuento ({resultado['descuento_porcentaje']}%): -{resultado['descuento_cantidad']:.2f}€")
        print(f"✅ Precio final: {resultado['precio_final']:.2f}€")
        return resultado
    except ValueError as e:
        print(f"❌ Error en los datos: {e}")
        return None

# Pruebas
aplicar_descuento_seguro(100, 20)    # ✅ Descuento aplicado
aplicar_descuento_seguro(-50, 10)    # ❌ El precio no puede ser negativo
aplicar_descuento_seguro(100, 150)   # ❌ El descuento debe estar entre 0% y 100%
```

#### Excepciones personalizadas con clases

```python
class ErrorValidacionEmail(Exception):
    """Excepción personalizada para errores de validación de email."""
    pass

class ErrorValidacionPassword(Exception):
    """Excepción personalizada para errores de validación de contraseña."""
    pass

def validar_email(email):
    """Valida un email con excepción personalizada."""
    if not email:
        raise ErrorValidacionEmail("El email no puede estar vacío")
    
    if "@" not in email:
        raise ErrorValidacionEmail("El email debe contener '@'")
    
    if not email.endswith(('.com', '.es', '.org', '.net')):
        raise ErrorValidacionEmail("El email debe terminar en .com, .es, .org o .net")
    
    return True

def validar_password(password):
    """Valida una contraseña con excepción personalizada."""
    if not password:
        raise ErrorValidacionPassword("La contraseña no puede estar vacía")
    
    if len(password) < 8:
        raise ErrorValidacionPassword("La contraseña debe tener al menos 8 caracteres")
    
    if not any(c.isupper() for c in password):
        raise ErrorValidacionPassword("La contraseña debe tener al menos una mayúscula")
    
    if not any(c.isdigit() for c in password):
        raise ErrorValidacionPassword("La contraseña debe tener al menos un número")
    
    return True

def registrar_usuario(email, password):
    """Registra usuario con validaciones y excepciones personalizadas."""
    try:
        validar_email(email)
        validar_password(password)
        
        print(f"✅ Usuario registrado exitosamente: {email}")
        return True
        
    except ErrorValidacionEmail as e:
        print(f"❌ Error en email: {e}")
    except ErrorValidacionPassword as e:
        print(f"❌ Error en contraseña: {e}")
    except Exception as e:
        print(f"❌ Error inesperado: {e}")
    
    return False

# Pruebas
registrar_usuario("usuario@ejemplo.com", "MiPassword123")  # ✅ Usuario registrado
registrar_usuario("email_sin_arroba", "MiPassword123")     # ❌ Error en email
registrar_usuario("usuario@ejemplo.com", "corta")         # ❌ Error en contraseña
```

### 9.8. Casos prácticos avanzados

#### Sistema de login con reintentos

```python
def sistema_login():
    """Sistema de login con manejo de excepciones y límite de intentos."""
    usuarios = {
        "admin": "admin123",
        "usuario": "password",
        "test": "test123"
    }
    
    max_intentos = 3
    intentos = 0
    
    while intentos < max_intentos:
        try:
            print(f"\n🔐 LOGIN - Intento {intentos + 1} de {max_intentos}")
            usuario = input("Usuario: ").strip()
            password = input("Contraseña: ").strip()
            
            # Validaciones básicas
            if not usuario:
                raise ValueError("El usuario no puede estar vacío")
            
            if not password:
                raise ValueError("La contraseña no puede estar vacía")
            
            # Verificar credenciales
            if usuario not in usuarios:
                raise KeyError(f"Usuario '{usuario}' no existe")
            
            if usuarios[usuario] != password:
                raise ValueError("Contraseña incorrecta")
            
            # Login exitoso
            print(f"✅ Bienvenido, {usuario}!")
            return True
            
        except ValueError as e:
            print(f"❌ Error de validación: {e}")
        except KeyError as e:
            print(f"❌ Error de usuario: {e}")
        except KeyboardInterrupt:
            print("\n\n👋 Login cancelado por el usuario")
            return False
        except Exception as e:
            print(f"❌ Error inesperado: {e}")
        
        intentos += 1
        
        if intentos < max_intentos:
            continuar = input("\n¿Intentar de nuevo? (s/n): ").lower()
            if not continuar.startswith('s'):
                break
    
    print(f"\n🔒 Demasiados intentos fallidos. Acceso bloqueado.")
    return False

# sistema_login()  # Descomenta para probar
```

#### Procesador de datos CSV con validación

```python
def procesar_csv_ventas(nombre_archivo):
    """Procesa archivo CSV de ventas con manejo exhaustivo de errores."""
    ventas = []
    errores = []
    
    try:
        with open(nombre_archivo, 'r', encoding='utf-8') as archivo:
            lineas = archivo.readlines()
            
        print(f"📊 Procesando {len(lineas)} líneas...")
        
        for numero_linea, linea in enumerate(lineas, 1):
            try:
                # Saltar líneas vacías
                if not linea.strip():
                    continue
                
                # Parsear CSV simple (separado por comas)
                campos = [campo.strip() for campo in linea.strip().split(',')]
                
                if len(campos) != 4:
                    raise ValueError(f"Se esperan 4 campos, se encontraron {len(campos)}")
                
                fecha, producto, cantidad, precio = campos
                
                # Validar y convertir datos
                if not fecha:
                    raise ValueError("La fecha no puede estar vacía")
                
                if not producto:
                    raise ValueError("El producto no puede estar vacío")
                
                cantidad = int(cantidad)
                if cantidad <= 0:
                    raise ValueError("La cantidad debe ser positiva")
                
                precio = float(precio)
                if precio <= 0:
                    raise ValueError("El precio debe ser positivo")
                
                # Calcular total
                total = cantidad * precio
                
                venta = {
                    'fecha': fecha,
                    'producto': producto,
                    'cantidad': cantidad,
                    'precio': precio,
                    'total': total
                }
                
                ventas.append(venta)
                
            except ValueError as e:
                error = f"Línea {numero_linea}: {e}"
                errores.append(error)
                print(f"❌ {error}")
            except Exception as e:
                error = f"Línea {numero_linea}: Error inesperado - {e}"
                errores.append(error)
                print(f"❌ {error}")
    
    except FileNotFoundError:
        print(f"❌ El archivo '{nombre_archivo}' no existe")
        return None, None
    except PermissionError:
        print(f"❌ Sin permisos para leer '{nombre_archivo}'")
        return None, None
    except Exception as e:
        print(f"❌ Error al procesar archivo: {e}")
        return None, None
    
    # Generar reporte
    if ventas:
        total_ventas = sum(venta['total'] for venta in ventas)
        print(f"\n📈 REPORTE DE VENTAS")
        print("="*40)
        print(f"Ventas procesadas: {len(ventas)}")
        print(f"Errores encontrados: {len(errores)}")
        print(f"Total vendido: {total_ventas:.2f}€")
        
        # Top 3 productos
        productos_totales = {}
        for venta in ventas:
            producto = venta['producto']
            total = venta['total']
            productos_totales[producto] = productos_totales.get(producto, 0) + total
        
        top_productos = sorted(productos_totales.items(), key=lambda x: x[1], reverse=True)[:3]
        print(f"\nTop 3 productos:")
        for i, (producto, total) in enumerate(top_productos, 1):
            print(f"  {i}. {producto}: {total:.2f}€")
    
    return ventas, errores

# Crear archivo CSV de prueba
csv_contenido = """2024-01-15, Laptop, 2, 899.99
2024-01-16, Mouse, 5, 25.50
2024-01-17, Teclado, , 75.00
2024-01-18, Monitor, 1, 299.99
2024-01-19, Webcam, 3, abc
2024-01-20, Auriculares, 4, 45.99"""

# with open('ventas.csv', 'w', encoding='utf-8') as f:
#     f.write(csv_contenido)

# ventas, errores = procesar_csv_ventas('ventas.csv')
```

### 9.9. Mejores prácticas para el manejo de excepciones

#### ✅ Buenas prácticas

```python
# 1. Ser específico con las excepciones
try:
    numero = int(input("Número: "))
    resultado = 10 / numero
except ValueError:
    print("Entrada no válida")
except ZeroDivisionError:
    print("No se puede dividir por cero")

# 2. No capturar Exception genérica sin razón
# ❌ Evitar
try:
    codigo_complejo()
except Exception:
    pass  # Silencia todos los errores

# ✅ Mejor
try:
    codigo_complejo()
except SpecificError as e:
    logging.error(f"Error específico: {e}")
    # Manejo apropiado

# 3. Usar información del error
try:
    procesar_datos()
except FileNotFoundError as e:
    print(f"Archivo no encontrado: {e.filename}")
except PermissionError as e:
    print(f"Sin permisos para: {e.filename}")

# 4. Limpieza en finally
recurso = None
try:
    recurso = abrir_recurso()
    trabajar_con_recurso(recurso)
except Exception as e:
    print(f"Error: {e}")
finally:
    if recurso:
        cerrar_recurso(recurso)
```

#### ❌ Prácticas a evitar

```python
# 1. Capturar y no hacer nada
try:
    operacion_peligrosa()
except:
    pass  # ❌ Nunca hacer esto

# 2. Capturar Exception muy genéricamente
try:
    todo_el_programa()
except Exception:
    print("Algo salió mal")  # ❌ Demasiado genérico

# 3. Usar excepciones para control de flujo
try:
    while True:
        item = lista.pop()
        procesar(item)
except IndexError:
    pass  # ❌ Usar for loop en su lugar

# 4. No proporcionar información útil
try:
    procesar_archivo()
except:
    print("Error")  # ❌ ¿Qué error? ¿Dónde?
```

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
