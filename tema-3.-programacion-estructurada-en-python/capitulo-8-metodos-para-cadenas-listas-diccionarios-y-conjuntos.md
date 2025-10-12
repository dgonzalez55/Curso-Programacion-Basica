# Capítulo 8: Métodos para Cadenas, Listas, Diccionarios y Conjuntos

Si bien los tipos de datos como las cadenas, listas o diccionarios son los "_contenedores_" que almacenan la información en nuestros programas, su verdadero poder reside en los métodos que incorporan. Estos métodos son las "_herramientas_" que nos permiten manipular de manera sencilla y eficiente los principales tipos de datos estructurados: **cadenas de texto (`str`), listas (`list`), diccionarios (`dict`) y conjuntos (`set`).** Dominar este conjunto de herramientas es un paso crucial para evolucionar de escribir código que simplemente funciona a escribir <mark style="background-color:yellow;">**código**</mark><mark style="background-color:yellow;">**&#x20;**</mark>_<mark style="background-color:yellow;">**pythónico**</mark>_<mark style="background-color:yellow;">: limpio, legible y profesional</mark>.&#x20;

En este capítulo, exploraremos en detalle los métodos más importantes para los tipos de datos fundamentales, desvelando el potencial que ofrecen para resolver problemas complejos con elegancia y precisión.

### 8.1. Introducción: La potencia de los métodos integrados

Los métodos integrados de Python son funciones especializadas que cada tipo de dato ofrece para facilitar su manipulación. Estos métodos han sido optimizados por el equipo de desarrollo de Python y son mucho más eficientes que implementar la misma funcionalidad desde cero.

#### Características importantes:

* **Cadenas (str)**: Son inmutables, sus métodos devuelven nuevas cadenas.
* **Listas (list)**: Son mutables, muchos métodos modifican la lista original.
* **Diccionarios (dict)**: Ofrecen métodos para trabajar con pares clave-valor.
* **Conjuntos (set)**: Proporcionan operaciones matemáticas de conjuntos.

### 8.2. Métodos de cadenas (`str`)

Las cadenas de texto (`str`) son uno de los tipos de datos más omnipresentes en la programación. Desde la validación de la entrada de un usuario y la manipulación de nombres de archivo hasta el procesamiento de grandes volúmenes de texto, la capacidad de manejar _strings_ de forma eficaz es una habilidad fundamental. Python dota a las cadenas de un arsenal de métodos que actúan como una navaja suiza, ofreciendo la herramienta precisa para cada tarea de transformación, búsqueda, limpieza o formato.

{% hint style="warning" %}
**Las cadenas son inmutables**, por lo que **todos sus métodos devuelven una nueva cadena** sin modificar la original.
{% endhint %}

#### Métodos de transformación

Estos métodos permiten normalizar el texto cambiando entre mayúsculas y minúsculas. Es importante recordar que las cadenas son inmutables, por lo que todos estos métodos devuelven una nueva cadena modificada sin alterar la original.

| Método          | Descripción                                                                                                                | Ejemplo                                                                                                                                                                                     |
| --------------- | -------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `.upper()`      | Devuelve una copia de la cadena con todos los caracteres en mayúsculas.                                                    | `"hola".upper()` → `"HOLA"`                                                                                                                                                                 |
| `.lower()`      | Devuelve una copia de la cadena con todos los caracteres en minúsculas.                                                    | `"HOLA".lower()` → `"hola"`                                                                                                                                                                 |
| `.capitalize()` | Devuelve una copia de la cadena con su primer carácter en mayúscula y el resto en minúsculas.                              | `"python".capitalize()` → `"Python"`                                                                                                                                                        |
| `.title()`      | Devuelve una versión de la cadena en formato de título, donde la primera letra de cada palabra está en mayúscula.          | `"hola mundo".title()` → `"Hola Mundo"`                                                                                                                                                     |
| `.swapcase()`   | Devuelve una copia de la cadena invirtiendo mayúsculas por minúsculas y viceversa.                                         | `"HoLa".swapcase()` → `"hOlA"`                                                                                                                                                              |
| `casefold()`    | Devuelve una versión de la cadena apta para comparaciones sin distinción de mayúsculas, siendo más agresiva que `lower()`. | <p><code>cadena1 = "cataluña"</code></p><p><code>cadena2 = "CATaluña"</code></p><p><code>print(cadena1.casefold()</code></p><p> <code>== cadena2.casefold())</code> → <code>True</code></p> |

#### Métodos de limpieza y sustitución

Este grupo permite limpiar espacios y reemplazar contenido. Todos devuelven una nueva cadena modificada.

| Método                      | Descripción                                                                                             | Ejemplo                                                                                                           |
| --------------------------- | ------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| `.strip()`                  | Elimina los caracteres especificados (espacios por defecto) del principio y del final.                  | `" hola ".strip()` → `"hola"`                                                                                     |
| `.lstrip()`                 | Elimina los caracteres especificados (espacios por defecto) solo del principio.                         | `" hola ".lstrip()` → `"hola "`                                                                                   |
| `.rstrip()`                 | Elimina los caracteres especificados (espacios por defecto) solo del final.                             | `" hola ".rstrip()` → `" hola"`                                                                                   |
| `removeprefix()`            | Si la cadena comienza con el prefijo, devuelve una copia sin él. De lo contrario, devuelve la original. | <p><code>cadena = "Cadena"</code> </p><p><code>print(cadena.removeprefix("Cad")))</code> → <code>"ena"</code></p> |
| `removesuffix()`            | Si la cadena termina con el sufijo, devuelve una copia sin él. De lo contrario, devuelve la original.   | <p><code>cadena = "Cadena"</code></p><p><code>print(cadena.removesuffix("ena")))</code> → <code>"Cad"</code></p>  |
| `.replace(old, new)`        | Devuelve una copia con todas las ocurrencias de una subcadena reemplazadas por otra.                    | `"hola mundo".replace("o", "0")` → `"h0la mund0"`                                                                 |
| `.replace(old, new, count)` | Devuelve una copia con las "n" ocurrencias de una subcadena reemplazadas por otra.                      | `"banana".replace("a", "o", 2)` → `"bonona"`                                                                      |

#### Métodos de búsqueda y conteo

Estos métodos son esenciales para localizar subcadenas o contar sus apariciones. Devuelven un valor numérico y no modifican la cadena original

| Método        | Descripción                                                                                   | Ejemplo                     |
| ------------- | --------------------------------------------------------------------------------------------- | --------------------------- |
| `.find(sub)`  | Devuelve el índice más bajo de la subcadena. Si no se encuentra, devuelve -1.                 | `"banana".find("a")` → `1`  |
| `.rfind(sub)` | Devuelve el índice más alto de la subcadena. Si no se encuentra, devuelve -1.                 | `"banana".rfind("a")` → `5` |
| `.index(sub)` | Devuelve el índice más bajo de la subcadena. Si no se encuentra, lanza un error `ValueError`. | `"banana".index("a")` → `1` |
| `.count(sub)` | Devuelve el número de apariciones no superpuestas de una subcadena.                           | `"banana".count("a")` → `3` |

#### Métodos de verificación

La familia de métodos `is...` es una herramienta de validación muy potente. Permiten verificar la naturaleza del contenido de una cadena de forma rápida y legible, devolviendo `True` o `False` sin necesidad de recurrir a expresiones regulares complejas.

| Método             | Descripción                                                                                              | Ejemplo                                 |
| ------------------ | -------------------------------------------------------------------------------------------------------- | --------------------------------------- |
| `.startswith(sub)` | Devuelve `True` si la cadena comienza con el prefijo especificado.                                       | `"python".startswith("py")` → `True`    |
| `.endswith(sub)`   | Devuelve `True` si la cadena termina con el sufijo especificado.                                         | `"archivo.py".endswith(".py")` → `True` |
| `isupper()`        | Devuelve `True` si todos los caracteres con mayúsculas/minúsculas están en mayúsculas.                   | `"ABC".isupper()` → `True`              |
| `islower()`        | Devuelve `True` si todos los caracteres con mayúsculas/minúsculas están en minúsculas.                   | `"abc".islower()` → `True`              |
| `.isdecimal()`     | Devuelve `True` si todos los caracteres son numéricos con valores del 0-9.                               | `"123".isdecimal()` → `True`            |
| `.isdigit()`       | Como la anterior pero incluyendo caracteres como superíndices (²).                                       | `"123".isdigit()` → `True`              |
| `.isnumeric()`     | Como la anterior pero incluyendo símbolos de fracción (¼).                                               | `"123".isnumeric()` → `True`            |
| `.isalpha()`       | Devuelve `True` si todos los caracteres son alfabéticos.                                                 | `"abc".isalpha()` → `True`              |
| `.isalnum()`       | Devuelve `True` si todos los caracteres son alfanuméricos (letras o números) y hay al menos un carácter. | `"abc123".isalnum()` → `True`           |
| `.isspace()`       | Devuelve `True` si todos los caracteres son espacios.                                                    | `" ".isspace()` → `True`                |

#### Métodos de división y unión

Los métodos `split()` y `join()` tienen una relación simbiótica y son fundamentales para la conversión entre cadenas y listas. `split()` deconstruye una cadena en una lista de subcadenas, mientras que `join()` construye una única cadena a partir de los elementos de un iterable.

| Método            | Descripción                                                                      | Ejemplo                                                                                                                                          |
| ----------------- | -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| `.split()`        | Devuelve una lista de subcadenas, utilizando un separador (espacio por defecto). | <p><code>"a b c".split()</code> → <code>["a", "b", "c"]</code></p><p><code>"a,b,c".split(",")</code> → <code>["a", "b", "c"]</code></p>          |
| `.rsplit(sep, n)` | Similar a `split()`, pero realiza la división desde la derecha.                  | `"a.b.c".rsplit(".", 1)` → `["a.b", "c"]`                                                                                                        |
| `splitlines()`    | Devuelve una lista de las líneas de la cadena, rompiendo en los saltos de línea. | <p><code>texto = "Hola\nJoe\nCom ho veus"</code> </p><p><code>print(texto.splitlines())</code> → <code>['Hola', 'Joe', 'Com ho veus']</code></p> |
| `.join(iterable)` | Une elementos con la cadena como separador                                       | `"-".join(["a", "b", "c"])` → `"a-b-c"`                                                                                                          |

#### Métodos de formato

Este grupo permite alinear texto y añadir "_padding_".

| Método     | Descripción                                                                                  | Ejemplo                                                                                                   |
| ---------- | -------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| `center()` | Centra la cadena en un ancho especificado, rellenando con un carácter (espacio por defecto). | `"129".center(10, "_")` →  `"____129___"`                                                                 |
| `ljust()`  | Justifica la cadena a la izquierda en un ancho especificado, rellenando a la derecha.        | `"129".ljust(10, "_")` → `"129_______"`                                                                   |
| `rjust()`  | Justifica la cadena a la derecha en un ancho especificado, rellenando a la izquierda.        | `"129".rjust(10, "_")` → `"_______129"`                                                                   |
| `zfill()`  | Rellena la cadena con ceros (`0`) a la izquierda hasta alcanzar el ancho especificado        | <p><code>numero = "129"</code></p><p><code>print(numero.zfill(10))</code> → <code>"0000000129"</code></p> |

#### Ejemplo práctico: Procesador de texto

```python
def procesar_texto(texto):
    """
    Procesa un texto aplicando varias transformaciones.
    
    Args:
        texto (str): Texto a procesar
        
    Returns:
        dict: Información procesada del texto
    """
    # Limpiar el texto
    texto_limpio = texto.strip().lower()
    
    # Obtener estadísticas
    palabras = texto_limpio.split()
    
    return {
        'original': texto,
        'limpio': texto_limpio,
        'palabras': len(palabras),
        'caracteres': len(texto_limpio),
        'primera_palabra': palabras[0] if palabras else '',
        'empieza_con_vocal': texto_limpio.startswith(('a', 'e', 'i', 'o', 'u')),
        'solo_letras': texto_limpio.replace(' ', '').isalpha()
    }

# Ejemplo de uso
resultado = procesar_texto("  ¡HOLA Mundo Python!  ")
print(resultado)
```

Una vez que hemos descompuesto y manipulado el texto, a menudo necesitamos organizar estos fragmentos en colecciones ordenadas, lo que nos lleva directamente a las listas.

***

### 8.3. Métodos de listas (`list`)

Las listas son la estructura de datos mutable y ordenada por excelencia en Python. Están diseñadas para gestionar eficientemente colecciones de elementos que pueden crecer, encogerse y cambiar durante la ejecución de un programa. Sus métodos proporcionan un control total sobre la adición, eliminación y organización de sus contenidos.

#### Métodos de adición

Estos métodos modifican la lista _in-place_ (en el lugar), alterando directamente el objeto original sin necesidad de reasignar la variable.

| Método                 | Descripción                                                                             | Ejemplo                                                                                                                                            |
| ---------------------- | --------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| `.append(item)`        | Añade un único elemento al final de la lista.                                           | <p><code>lista = [1, 2, 3]</code></p><p><code>lista.append(2)</code></p><p><code>print(lista)</code> → <code>[1, 2, 3, 2]</code></p>               |
| `.extend(iterable)`    | Añade todos los elementos de un iterable (como otra lista) al final de la lista actual. | <p><code>lista = [1, 2, 3, 4]</code></p><p><code>lista.extend([2, 7])</code></p><p><code>print(lista)</code> → <code>[1, 2, 3, 4, 2, 7]</code></p> |
| `.insert(index, item)` | Inserta un elemento en una posición específica, desplazando los elementos existentes.   | <p><code>lista = [1, 2, 3, 4]</code></p><p><code>lista.insert(0, 3)</code></p><p><code>print(lista)</code> → <code>[3, 1, 2, 3, 4]</code></p>      |

#### Métodos de eliminación

Estos métodos también modifican la lista _in-place_.

| Método          | Descripción                                                                       | Ejemplo                                                                                                                                                                                          |
| --------------- | --------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `.remove(item)` | Elimina la primera aparición de un elemento con el valor especificado.            | <p><code>lista = [3, 1, 2, 3, 4]</code></p><p><code>lista.remove(3)</code></p><p><code>print(lista)</code> → <code>[1, 2, 3, 4]</code></p>                                                       |
| `.pop(index)`   | Elimina y devuelve el elemento en el índice especificado (el último por defecto). | <p><code>lista = [1, 2, 3, 4]</code></p><p><code>elemento = lista.pop(0)</code></p><p><code>print(elemento)</code> → <code>1</code></p><p><code>print(lista)</code> → <code>[2, 3, 4]</code></p> |
| `.clear()`      | Elimina todos los elementos de la lista, dejándola vacía.                         | <p><code>lista = [1, 2, 3]</code></p><p><code>lista.clear()</code></p><p><code>print(lista)</code> → <code>[]</code></p>                                                                         |

#### Métodos de búsqueda

Este conjunto de métodos permite buscar elementos dentro de la lista.

| Método         | Descripción                                                           | Ejemplo                                                                                                |
| -------------- | --------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| `.index(item)` | Devuelve el índice de la primera aparición del elemento especificado. | <p><code>lista = [1, 2, 3, 2, 7]</code></p><p><code>print(lista.index(2))</code> → <code>1</code></p>  |
| `.count(item)` | Devuelve el número de veces que un elemento aparece en la lista.      | <p><code>lista = [1, 2, 3, 2, 7]</code></p><p><code>print(lista.count(2))</code> → <code>2</code> </p> |

#### Métodos de ordenación

Este conjunto de métodos permite reordenar los elementos dentro de una lista.

| Método                | Descripción                                                                                                                  | Ejemplo                                                                                                                                                   |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `.sort()`             | Ordena los elementos de la lista _in-place_ (modifica la lista original). Si no se indica nada, la ordenación es ascendente. | <p><code>lista = [2, 7, 2, 4]</code></p><p><code>lista.sort()</code></p><p><code>print(lista)</code> → <code>[2, 2, 4, 7]</code></p>                      |
| `.sort(reverse=True)` | Como la anterior, pero en orden descendente.                                                                                 | <p><code>lista = [2, 7, 2, 4]</code></p><p><code>lista.sort(reverse=True)</code></p><p><code>print(lista)</code> → <code>[7, 4, 2, 2]</code></p>          |
| `.sort(key=function)` | Ordena los elementos de la lista _in-place_ conforme el criterio de la función indicada.                                     | <p><code>palabras=["Hola","Pol"]</code>   </p><p><code>palabras.sort(key=len)</code></p><p><code>print(palabras)</code> → <code>["Pol","Hola"]</code></p> |
| `.reverse()`          | Invierte el orden de los elementos de la lista _in-place_.                                                                   | <p><code>lista = [2, 7, 2, 4]</code></p><p><code>lista.reverse()</code></p><p><code>print(lista)</code> → <code>[7, 4, 2, 2]</code></p>                   |

#### Métodos de copia

Este conjunto de métodos permite crear copias para evitar modificaciones no deseadas.

| Método    | Descripción                                                                                                                                       | Ejemplo                                                                                                                                                                                                                               |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `.copy()` | Devuelve una nueva copia superficial de la lista. Es crucial para evitar modificar la lista original accidentalmente al trabajar con referencias. | <p><code>original = [1, 2]</code></p><p><code>copia = original.copy()</code></p><p><code>copia.append(3)</code></p><p><code>print(original)</code> → <code>[1, 2]</code></p><p><code>print(copia)</code> → <code>[1, 2, 3]</code></p> |

#### Ejemplo práctico: Gestor de tareas

```python
class GestorTareas:
    """Gestor simple de tareas usando métodos de lista."""
    
    def __init__(self):
        self.tareas = []
        self.completadas = []
    
    def agregar_tarea(self, tarea):
        """Agrega una nueva tarea."""
        if tarea not in self.tareas:
            self.tareas.append(tarea)
            print(f"Tarea añadida: {tarea}")
        else:
            print("La tarea ya existe")
    
    def completar_tarea(self, indice):
        """Marca una tarea como completada."""
        if 0 <= indice < len(self.tareas):
            tarea = self.tareas.pop(indice)
            self.completadas.append(tarea)
            print(f"Tarea completada: {tarea}")
        else:
            print("Índice de tarea inválido")
    
    def listar_tareas(self):
        """Lista todas las tareas pendientes."""
        if self.tareas:
            print("Tareas pendientes:")
            for i, tarea in enumerate(self.tareas):
                print(f"  {i}: {tarea}")
        else:
            print("No hay tareas pendientes")
    
    def ordenar_tareas(self):
        """Ordena las tareas alfabéticamente."""
        self.tareas.sort()
        print("Tareas ordenadas alfabéticamente")

# Ejemplo de uso
gestor = GestorTareas()
gestor.agregar_tarea("Estudiar Python")
gestor.agregar_tarea("Hacer ejercicios")
gestor.agregar_tarea("Revisar código")
gestor.listar_tareas()
gestor.ordenar_tareas()
gestor.completar_tarea(0)
```

Mientras que las listas organizan los datos por su posición (índice), a menudo necesitamos estructuras que los organicen por un identificador único, lo que nos conduce a los diccionarios.

***

### 8.4. Métodos de diccionarios (`dict`)

Los diccionarios son una de las estructuras de datos más potentes de Python. Son fundamentales para modelar objetos del mundo real (como un usuario o un producto) y para realizar búsquedas de datos casi instantáneas a través de claves únicas. Sus métodos proporcionan un control total sobre las claves, los valores y los pares de elementos que componen el diccionario.

#### Métodos de acceso y visualización

Estos métodos permiten obtener los datos del diccionario sin modificar su contenido. `keys()`, `values()` e `items()` devuelven "vistas" dinámicas, que reflejan los cambios en el diccionario.

| Método                                                              | Descripción                                                                                                                                         | Ejemplo                                                                                                                                                                           |
| ------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p><code>.get(key)</code></p><p><code>.get(key, default)</code></p> | Devuelve el valor para una clave. A diferencia de `diccionario[clave]`, permite un valor por defecto si la clave no existe, evitando un `KeyError`. | <p> <code>alu= {"nombre": "Ana"}</code></p><p><code>print(alu.get("nombre"))</code> → <code>"Ana"</code></p><p><code>print(alu.get("email", "N/A"))</code> → <code>N/A</code></p> |
| .`keys()`                                                           | Devuelve una vista de todas las claves del diccionario.                                                                                             | <p><code>alu= {"nombre": "Ana", "edad": 21}</code> </p><p><code>print(list(alu.keys()))</code> → <code>['nombre', 'edad']</code></p>                                              |
| `.values()`                                                         | Devuelve una vista de todos los valores del diccionario.                                                                                            | <p><code>alu= {"nombre": "Ana", "edad": 21}</code> </p><p><code>print(list(alu.values()))</code> → <code>["Ana",21]</code></p>                                                    |
| `items()`                                                           | Devuelve una vista de todos los pares (clave, valor) como tuplas.                                                                                   | <p><code>alu = {"nombre": "Ana", "edad": 21}</code></p><p><code>print(list(alu.items()))</code> → <code>[('nombre', 'Ana'), ('edad', 21)]</code></p>                              |

#### Métodos de modificación y eliminación

Estos métodos alteran el contenido del diccionario _in-place_.

<table><thead><tr><th>Método</th><th width="233">Descripción</th><th>Ejemplo</th></tr></thead><tbody><tr><td><code>.update(other)</code></td><td>Actualiza el diccionario con los pares clave-valor de otro. Añade nuevas claves o modifica las existentes.</td><td><p><code>alu = {"nombre": "Joan"}</code> </p><p><code>alu.update({"edad": 21, "ciudad": "Barcelona"}))</code> → alu es ahora <code>{'nombre': 'Joan', 'edad': 21, 'ciudad': 'Barcelona'}</code></p></td></tr><tr><td><code>.pop(key)</code></td><td>Elimina y devuelve el valor asociado a una clave.</td><td><p><code>alu = {"nombre": "Joan", "edad": 21}</code></p><p><code>edad = alu.pop("edad")</code> </p><p><code>print(edad)</code> → <code>21</code></p><p><code>print(alu)</code> → <code>{'nombre': 'Joan'}</code></p></td></tr><tr><td><code>.popitem()</code></td><td>Elimina y devuelve el último par (clave, valor) insertado (a partir de Python 3.7).</td><td><p><code>alu = {"nombre": "Joan", "edad": 21}</code> </p><p><code>item = estudiante.popitem()</code></p><p><code>print(item)</code> → <code>('edad', 21)</code></p><p><code>print(alu)</code> → <code>{'nombre': 'Joan'}</code></p></td></tr><tr><td><code>.clear()</code></td><td>Elimina todos los elementos del diccionario.</td><td><p><code>alu = {"nombre": "Joan"}</code> </p><p><code>alu.clear()</code></p><p><code>print(alu)</code> → <code>{}</code></p></td></tr></tbody></table>

#### Métodos de **Creación y Copia**

| Método                   | Descripción                                                                                    | Ejemplo                                                                                                                                                                                |
| ------------------------ | ---------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `fromkeys(keys,default)` | Crea un nuevo diccionario a partir de una secuencia de claves y un valor opcional por defecto. | <p><code>claves = ["nombre", "apellido"]</code> </p><p> <code>alu= dict.fromkeys(claves, "-")</code></p><p><code>print(alu)</code> → <code>{'nombre': '-', 'apellido': '-'}</code></p> |
| `copy()`                 | Devuelve una nueva copia superficial del diccionario.                                          | <p><code>original = {"a": 1}</code></p><p><code>copia = original.copy()</code></p><p><code>copia["b"] = 2</code></p><p><code>print(original)</code> → <code>{'a': 1}</code></p>        |

#### Ejemplo práctico: Sistema de estudiantes

```python
class SistemaEstudiantes:
    """Sistema para gestionar información de estudiantes."""
    
    def __init__(self):
        self.estudiantes = {}
    
    def agregar_estudiante(self, id_estudiante, nombre, edad):
        """Agrega un nuevo estudiante."""
        self.estudiantes[id_estudiante] = {
            'nombre': nombre,
            'edad': edad,
            'notas': [],
            'promedio': 0.0
        }
        print(f"Estudiante {nombre} agregado con ID {id_estudiante}")
    
    def agregar_nota(self, id_estudiante, nota):
        """Agrega una nota a un estudiante."""
        estudiante = self.estudiantes.get(id_estudiante)
        if estudiante:
            estudiante['notas'].append(nota)
            estudiante['promedio'] = sum(estudiante['notas']) / len(estudiante['notas'])
            print(f"Nota {nota} agregada a {estudiante['nombre']}")
        else:
            print("Estudiante no encontrado")
    
    def obtener_estadisticas(self):
        """Obtiene estadísticas generales."""
        if not self.estudiantes:
            return "No hay estudiantes registrados"
        
        estadisticas = {
            'total_estudiantes': len(self.estudiantes),
            'promedio_general': 0.0,
            'mejor_estudiante': '',
            'peor_estudiante': ''
        }
        
        promedios = []
        for id_est, datos in self.estudiantes.items():
            if datos['notas']:
                promedios.append((datos['promedio'], datos['nombre']))
        
        if promedios:
            promedios.sort()
            estadisticas['peor_estudiante'] = promedios[0][1]
            estadisticas['mejor_estudiante'] = promedios[-1][1]
            estadisticas['promedio_general'] = sum(p[0] for p in promedios) / len(promedios)
        
        return estadisticas

# Ejemplo de uso
sistema = SistemaEstudiantes()
sistema.agregar_estudiante("001", "Ana García", 20)
sistema.agregar_estudiante("002", "Pedro López", 19)
sistema.agregar_nota("001", 8.5)
sistema.agregar_nota("001", 9.0)
sistema.agregar_nota("002", 7.5)
print(sistema.obtener_estadisticas())
```

De las colecciones que asocian claves y valores, pasamos ahora a las colecciones que se centran únicamente en la unicidad de sus elementos: los **conjuntos**.

***

### 8.5. Métodos de conjuntos (`set`)

Los conjuntos son la implementación directa de la teoría matemática de conjuntos en Python. Su principal característica es que <mark style="background-color:yellow;">**solo almacenan elementos únicos y no están ordenados**</mark>. Son extremadamente eficientes para tareas como la eliminación de duplicados, las pruebas de pertenencia y la ejecución de operaciones lógicas como uniones, intersecciones y diferencias.

#### Métodos de adición y eliminación

| Método              | Descripción                                                                                   | Ejemplo                                                                                                                                     |
| ------------------- | --------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `.add(item)`        | Añade un elemento al conjunto (_in-place_). Si ya existe, no hace nada.                       | <p><code>conj = {1, 2}</code></p><p><code>conj.add(4)</code></p><p><code>print(conj)</code> → <code>{1, 2, 4}</code></p>                    |
| `.update(iterable)` | Añade múltiples elementos al conjunto (_in-place_). Los elementos ya existentes no se añaden. | <p><code>conj = {1, 2}</code></p><p><code>conj.update([1, 2, 3, 4])</code> </p><p><code>print(conj)</code> → <code>{1, 2, 3, 4}</code> </p> |
| `.remove(item)`     | Elimina un elemento del conjunto (_in-place_). Lanza `KeyError` si no existe.                 | <p><code>conj = {1, 2, 4}</code></p><p><code>conj.remove(2)</code></p><p><code>print(conj)</code> → <code>{1, 4}</code></p>                 |
| `.discard(item)`    | Elimina un elemento del conjunto (_in-place_). Sin error si no existe.                        | <p><code>conj = {1, 2, 4}</code></p><p><code>conj.discard(2)</code></p><p><code>print(conj)</code> → <code>{1, 4}</code></p>                |
| `.pop()`            | Elimina y devuelve un elemento arbitrario del conjunto (_in-place_).                          | <p><code>conj = {1, 2, 3}</code></p><p><code>elem = conj.pop()</code></p><p> → elem puede ser 1, 2 o 3</p>                                  |
| `.clear()`          | Elimina todos los elementos del conjunto (_in-place_).                                        | <p><code>conj = {1, 2, 3}</code></p><p><code>conj.clear()</code></p><p><code>print(conj)</code> → <code>set()</code></p>                    |

#### Métodos de operaciones de conjuntos

Estos métodos, junto con sus operadores equivalentes, realizan las operaciones lógicas fundamentales. Todos ellos devuelven un nuevo conjunto con el resultado, sin modificar los originales.

| Método                         | Operador | Descripción                                                                                           | Ejemplo                               |
| ------------------------------ | -------- | ----------------------------------------------------------------------------------------------------- | ------------------------------------- |
| `.union(other)`                | `\|`     | Devuelve un nuevo conjunto con los elementos que son comunes a ambos conjuntos.                       | `a.union(b)` o `a \| b`               |
| `.intersection(other)`         | `&`      | Devuelve un nuevo conjunto con los elementos que son comunes a ambos conjuntos.                       | `a.intersection(b)` o `a & b`         |
| `.difference(other)`           | `-`      | Devuelve un nuevo conjunto con los elementos del primer conjunto que no están en el segundo.          | `a.difference(b)` o `a - b`           |
| `.symmetric_difference(other)` | `^`      | Devuelve un nuevo conjunto con los elementos que están en uno de los dos conjuntos, pero no en ambos. | `a.symmetric_difference(b)` o `a ^ b` |

```python
conjunto_a = {1, 2, 3, 4}
conjunto_b = {3, 4, 5, 6}

print(conjunto_a.union(conjunto_b))             # {1, 2, 3, 4, 5, 6}
print(conjunto_a & conjunto_b)                  # {3, 4}
print(conjunto_a.difference(conjunto_b))        # {1, 2}
print(conjunto_a ^ conjunto_b)                  # {1, 2, 5, 6}
```

#### Métodos de verificación

| Método               | Descripción                                                               | Ejemplo                                                                                                                         |
| -------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| `.issubset(other)`   | Devuelve `True` si todos los elementos de este conjunto están en el otro. | <p> <code>a = {1, 2}</code></p><p> <code>c = {1, 2, 3}</code></p><p><code>print(a.issubset(c))</code> → <code>True</code></p>   |
| `.issuperset(other)` | Devuelve `True` si este conjunto contiene todos los elementos del otro.   | <p><code>a = {1, 2}</code></p><p> <code>c = {1, 2, 3}</code></p><p><code>print(a.issuperset(c))</code> → <code>False</code></p> |
| `.isdisjoint(other)` | Devuelve `True` si este conjunto no tiene elementos comunes en el otro.   | <p><code>a = {1, 2}</code></p><p> <code>c = {3, 4}</code></p><p><code>print(a.isdisjoint(c))</code> → <code>True</code></p>     |

#### Métodos de copia

| Método    | Descripción                 | Ejemplo                   |
| --------- | --------------------------- | ------------------------- |
| `.copy()` | Crea una copia del conjunto | `nuevo = conjunto.copy()` |

#### Ejemplo práctico: Análisis de datos

```python
def analizar_grupos_usuarios(grupo_a, grupo_b, grupo_c):
    """
    Analiza la relación entre diferentes grupos de usuarios.
    
    Args:
        grupo_a, grupo_b, grupo_c: Sets con IDs de usuarios
        
    Returns:
        dict: Análisis de los grupos
    """
    analisis = {}
    
    # Usuarios únicos totales
    todos_usuarios = grupo_a | grupo_b | grupo_c
    analisis['total_usuarios'] = len(todos_usuarios)
    
    # Usuarios en todos los grupos
    usuarios_comunes = grupo_a & grupo_b & grupo_c
    analisis['usuarios_en_todos'] = len(usuarios_comunes)
    
    # Usuarios exclusivos de cada grupo
    analisis['solo_grupo_a'] = len(grupo_a - grupo_b - grupo_c)
    analisis['solo_grupo_b'] = len(grupo_b - grupo_a - grupo_c)
    analisis['solo_grupo_c'] = len(grupo_c - grupo_a - grupo_b)
    
    # Usuarios en exactamente dos grupos
    ab_no_c = (grupo_a & grupo_b) - grupo_c
    ac_no_b = (grupo_a & grupo_c) - grupo_b
    bc_no_a = (grupo_b & grupo_c) - grupo_a
    
    analisis['exactamente_dos_grupos'] = len(ab_no_c) + len(ac_no_b) + len(bc_no_a)
    
    # Porcentajes
    if analisis['total_usuarios'] > 0:
        analisis['porcentaje_comunes'] = (len(usuarios_comunes) / analisis['total_usuarios']) * 100
    
    return analisis

# Ejemplo de uso
usuarios_premium = {1, 2, 3, 4, 5}
usuarios_activos = {3, 4, 5, 6, 7, 8}
usuarios_nuevos = {5, 6, 7, 9, 10}

resultado = analizar_grupos_usuarios(usuarios_premium, usuarios_activos, usuarios_nuevos)
print("Análisis de grupos de usuarios:")
for clave, valor in resultado.items():
    print(f"  {clave}: {valor}")
```

***

### 8.6. Técnicas avanzadas y mejores prácticas

#### Encadenamiento de métodos

```python
# Procesamiento en cadena de una frase
frase = "  PYTHON es un LENGUAJE de programación  "
resultado = frase.strip().lower().replace("python", "Python").title()
print(resultado)  # Python Es Un Lenguaje De Programación
```

#### Uso seguro de métodos

```python
# Acceso seguro a diccionarios
usuario = {"nombre": "Ana", "edad": 25}

# ❌ Puede causar KeyError
# email = usuario["email"]

# ✅ Acceso seguro
email = usuario.get("email", "No especificado")
```

#### Métodos que modifican vs. que devuelven

```python
# Métodos que MODIFICAN la lista original
lista = [3, 1, 4, 1, 5]
lista.sort()  # Modifica lista
print(lista)  # [1, 1, 3, 4, 5]

# Función que DEVUELVE nueva lista
lista_original = [3, 1, 4, 1, 5]
lista_ordenada = sorted(lista_original)  # No modifica original
print(lista_original)  # [3, 1, 4, 1, 5]
print(lista_ordenada)   # [1, 1, 3, 4, 5]
```

#### Optimización con operadores

```python
# Para conjuntos, los operadores suelen ser más legibles
conjunto_a = {1, 2, 3}
conjunto_b = {2, 3, 4}

# Ambas formas son válidas
union_metodo = conjunto_a.union(conjunto_b)
union_operador = conjunto_a | conjunto_b

# Los operadores son más concisos para operaciones múltiples
resultado = conjunto_a | conjunto_b | {5, 6} | {7, 8}
```

***

### Resumen del Capítulo

Hemos explorado el rico ecosistema de métodos integrados que Python ofrece para sus principales tipos de colecciones. El dominio de los métodos de `str`, `list`, `dict`, y `set` es un pilar fundamental para escribir código Python que no solo sea funcional, sino también _pythónico_, eficiente y fácil de mantener. Estas herramientas nos permiten pasar de simplemente almacenar datos a interactuar con ellos de forma inteligente y poderosa.

#### **💡 Conceptos Clave**

* **Métodos de Cadena**: Herramientas para transformar, validar, buscar, limpiar, dividir, unir y formatear texto.
* **Métodos de Lista**: Funciones para gestionar colecciones ordenadas y mutables, permitiendo añadir, eliminar, ordenar y buscar elementos dinámicamente.
* **Métodos de Diccionario**: Mecanismos para administrar eficientemente colecciones de pares clave-valor, optimizados para búsquedas y modelado de datos.
* **Métodos de Conjunto**: Operaciones lógicas y matemáticas para trabajar con colecciones de elementos únicos, ideales para eliminar duplicados y realizar comparaciones.
* **Modificación&#x20;**_**In-Place**_**&#x20;vs. Devolución de Copia**: Es crucial distinguir entre métodos que modifican el objeto original (ej. `list.sort()`) y aquellos que devuelven un nuevo objeto modificado (ej. `str.upper()`), ya que afecta al estado de nuestras variables.

#### **🤔 Preguntas de Reflexión**

1. ¿En qué situación preferirías usar `diccionario.get(clave)` en lugar de `diccionario[clave]` para acceder a un valor?
2. ¿Cuál es la diferencia fundamental en el propósito de `list.append()` vs. `list.extend()` al añadir elementos a una lista?
3. Describe un caso de uso práctico donde una operación de `set.intersection()` sería significativamente más eficiente que iterar sobre dos listas para encontrar elementos comunes.

#### **🔧 Ejercicio Práctico**

Crea un programa que:

1. Procese un archivo de texto dividiéndolo en palabras usando métodos de cadenas
2. Almacene estadísticas de cada palabra en un diccionario (frecuencia, longitud)
3. Use listas para mantener las palabras ordenadas por diferentes criterios
4. Emplee conjuntos para identificar palabras únicas y encontrar similitudes entre textos
5. Genere un reporte formateado usando todos los métodos aprendidos

Ahora que dominas las operaciones esenciales sobre los principales tipos estructurados, en el próximo capítulo aprenderás a gestionar los **errores y excepciones**, una habilidad imprescindible para escribir programas confiables y profesionales.

***
