# Capítulo 5: PEP y documentación

### Introducción al Capítulo

El desarrollo de software es una disciplina inherentemente colaborativa. Es un hecho conocido que **el código se lee muchas más veces de las que se escribe**, ya sea por tus compañeros de equipo, por tu "yo" del futuro o por cualquiera que necesite mantener tu programa. Por esta razón, escribir código que sea claro y comprensible es tan importante como escribir código que funcione. En este capítulo, exploraremos los estándares y las herramientas que la comunidad Python ha creado para garantizar la calidad, la legibilidad y la mantenibilidad del código.

### **5.1. Python Enhancement Proposals (PEP)**

Los [**Python Enhancement Proposals (PEP)**](https://peps.python.org/) son los documentos de diseño que guían la evolución del lenguaje Python.

{% hint style="info" %}
Piensa en los PEPs como las "**propuestas de ley**" de la comunidad Python. Cualquier cambio significativo, desde una nueva característica de sintaxis hasta una guía de estilo, se propone, discute y documenta en un PEP, asegurando que el lenguaje evolucione de una manera ordenada, transparente y consensuada.
{% endhint %}

Existen varios tipos de PEP:

* **PEP de Estándares**: Proponen nuevas características o cambios en la implementación del lenguaje.
* **PEP Informativos**: Proporcionan directrices o recomendaciones a la comunidad, sin proponer cambios en el lenguaje en sí.
* **PEP de Proceso**: Describen los procesos que rodean a Python, como el propio sistema de PEPs.

Algunos de los PEPs más importantes son:

* [**PEP 1**](https://peps.python.org/pep-0001/): Define qué es un PEP y cómo es el proceso para proponerlos.
* [**PEP 8**](https://peps.python.org/pep-0008/): La guía de estilo oficial para el código Python.
* [**PEP 20**](https://peps.python.org/pep-0020/): El Zen de Python, la filosofía del lenguaje.
* [**PEP 484**](https://peps.python.org/pep-0484/): Introduce las anotaciones de tipo (Type Hints).

***

### **5.2. PEP 8: guía de estilo oficial**

**PEP 8** es la guía de estilo que dicta cómo formatear el código Python. En un entorno profesional, seguir el PEP 8 **no es opcional**. Es la base que permite que equipos enteros de desarrolladores escriban código con un estilo consistente, haciéndolo universalmente legible y fácil de mantener.

Aquí están algunas de las reglas más importantes:

* <mark style="background-color:$primary;">**Indentación**</mark>
  * **Porqué**: La indentación define la estructura lógica del código en Python.
  * **Regla**: Usa 4 espacios por nivel de indentación. No uses tabuladores.
* <mark style="background-color:$primary;">**Longitud de línea**</mark>
  * **Porqué**: Limitar la longitud de las líneas a 79 caracteres facilita la lectura y permite ver varios archivos de código uno al lado del otro, algo muy común al comparar cambios (diffs).
  * **Regla**: Líneas de código de máximo 79 caracteres. Comentarios y docstrings de máximo 72.
* <mark style="background-color:$primary;">**Líneas en blanco**</mark>
  * **Porqué**: Ayudan a organizar visualmente el código y a separar bloques lógicos.
  * **Reglas**:
    * Usa dos líneas en blanco para separar funciones y clases a nivel de módulo.
    * Usa una línea en blanco para separar métodos dentro de una clase.
* <mark style="background-color:$primary;">**Importaciones**</mark>
  * **Porqué**: Las importaciones en líneas separadas son más claras y facilitan la gestión de dependencias.
  * **Regla**: Cada importación debe ir en su propia línea.
* <mark style="background-color:$primary;">**Nomenclatura**</mark>
  * **Porqué**: Un sistema de nombres consistente hace que el código sea autoexplicativo.
  * **Reglas**:
    * `snake_case` para variables y funciones (minúsculas con guiones bajos).
    * `PascalCase` para clases (primera letra de cada palabra en mayúscula).
    * `UPPER_CASE` para constantes.
* <mark style="background-color:$primary;">**Espacios en operadores**</mark>
  * **Porqué**: Mejora la legibilidad al separar visualmente los componentes de una expresión.
  * **Regla**: Usa espacios alrededor de los operadores aritméticos (`=`, `+`, `-`, `*`, `/`) y de comparación (`==`, `!=`, `<`, `>`).
* <mark style="background-color:$primary;">**Comentarios**</mark>
  * **Porqué**: Los buenos comentarios explican el _porqué_ del código, no el _qué_.
  * **Reglas**:
    * Deben ser oraciones completas y mantenerse actualizados.
    * Empiezan con `#` seguido de un espacio.
    * Evita comentarios obvios que no aportan valor.

***

### **5.3. Recursos de documentación y comunidad**

Saber dónde encontrar respuestas es una de las habilidades más importantes de un programador.

#### Documentación Oficial&#x20;

El recurso más fiable y completo es siempre la documentación oficial en [docs.python.org](https://docs.python.org/). Contiene el tutorial oficial, la referencia completa del lenguaje y la documentación de toda la biblioteca estándar.

#### Herramientas Integradas&#x20;

Python incluye herramientas para obtener ayuda directamente desde el intérprete interactivo:

* `help()`: Muestra la documentación de cualquier objeto, función o módulo.
* `dir()`: Lista todos los atributos y métodos de un objeto.

#### Docstrings: Documentando tu propio código&#x20;

Un "**docstring**" es una cadena de texto que aparece como la primera declaración en un módulo, función, clase o método. Se convierte en el atributo `__doc__` de ese objeto y es lo que la función `help()` muestra. Documentar tu código es una práctica fundamental.

```python
def calcular_area(base, altura):
    """Calcula el área de un rectángulo.

    Esta función toma la base y la altura de un rectángulo y
    devuelve su área calculada.

    Args:
        base (float): La base del rectángulo.
        altura (float): La altura del rectángulo.

    Returns:
        float: El área calculada del rectángulo.
    """
    return base * altura
```

#### Recursos de la Comunidad

* [**Stack Overflow**](https://stackoverflow.com/questions/tagged/python): El mejor lugar para encontrar soluciones a problemas de programación específicos.
* [**Real Python**](https://realpython.com/): Ofrece tutoriales y artículos de alta calidad, desde nivel principiante hasta avanzado.
* [**GitHub**](https://github.com/topics/python): Permite explorar el código fuente de miles de proyectos Python, una excelente forma de aprender de ejemplos reales.
* [**Python.org**](https://www.python.org/)**:** El sitio oficial de la comunidad, con noticias, eventos y recursos educativos.

***

### Resumen del Capítulo

Escribir código profesional va más allá de hacerlo funcionar. Implica adherirse a estándares que garantizan su legibilidad y mantenibilidad. Los PEP, y en especial la guía de estilo PEP 8, son la base de la colaboración en el ecosistema Python. Complementado con una buena documentación (como los docstrings) y el conocimiento de los recursos de la comunidad, un desarrollador puede escribir código de alta calidad y encontrar ayuda eficientemente cuando la necesite.

#### 💡 Conceptos Clave:

* **PEP (Python Enhancement Proposal)**: Documentos que guían el desarrollo y los estándares de Python.
* **PEP 8**: La guía de estilo oficial, de seguimiento obligatorio en entornos profesionales para garantizar la legibilidad y consistencia del código.
* **Docstrings**: Cadenas de documentación integradas en el código que explican el propósito de funciones, clases y módulos.
* **Documentación Oficial**: El recurso principal y más fiable para aprender sobre el lenguaje y su biblioteca estándar.

#### 🤔 Preguntas de Reflexión:

1. ¿Por qué crees que un estándar de estilo como PEP 8 es más importante en lenguajes como Python, donde la indentación afecta la lógica del programa?
2. Si te unes a un nuevo proyecto y encuentras una función sin docstring, ¿cuáles son los primeros pasos que darías para entender qué hace?
3. ¿Qué beneficios directos para un equipo de desarrollo tiene la práctica de que todos sigan el mismo estándar de código?

Hemos completado el recorrido por la configuración de un entorno profesional. Ahora, es momento de hacer un balance de todo lo aprendido.

***
