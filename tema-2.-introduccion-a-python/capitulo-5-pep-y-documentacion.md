# Capítulo 5: PEP y documentación

### 5.1. Python Enhancement Proposals (PEP)

Los **Python Enhancement Proposals (PEP)** son documentos de diseño que proporcionan información a la comunidad Python o describen nuevas características, procesos o entornos relacionados con el lenguaje.

**Tipos de PEP**:

**PEP de estándares**: Proponen cambios que afectan la implementación del lenguaje, su sintaxis o bibliotecas estándar.

**PEP informativos**: Proporcionan información general, directrices o recomendaciones para la comunidad de desarrolladores.

**PEP de proceso**: Describen procesos relacionados con Python, como la propia propuesta y revisión de PEPs.

**PEPs más importantes**:

* **PEP 1**: Proceso de propuesta y formato de PEPs
* **PEP 8**: Guía de estilo para código Python (el más conocido)
* **PEP 20**: El Zen de Python
* **PEP 484**: Anotaciones de tipo (Type Hints)
* **PEP 572**: Expresiones de asignación (walrus operator `:=`)

### 5.2. PEP 8: guía de estilo oficial

**PEP 8** es la guía de estilo oficial para código Python. Define convenciones para escribir código Python de manera coherente y legible. Su cumplimiento es fundamental para proyectos profesionales.

**Aspectos clave del PEP 8**

**Indentación**:

* Utilizar 4 espacios por cada nivel de indentación
* No mezclar espacios y tabulaciones
* Los editores deben configurarse para mostrar espacios en blanco

**Longitud de línea**:

* Mantener las líneas de código por debajo de 79 caracteres
* Para comentarios y docstrings: máximo 72 caracteres
* Usar continuación de línea con `\` o paréntesis cuando sea necesario

**Espacios en operadores**:

```python
# Correcto
x = y + z
spam(ham[1], {eggs: 2})
i = i + 1

# Incorrecto
x=y+z
spam( ham[ 1 ], { eggs : 2 } )
i=i+1
```

**Nomenclatura**:

* **Variables y funciones**: `snake_case` (minúsculas con guiones bajos)
* **Constantes**: `UPPER_CASE` (mayúsculas con guiones bajos)
* **Clases**: `PascalCase` (primera letra de cada palabra en mayúscula)
* **Módulos**: nombres cortos en minúsculas

```python
# Correcto
def calcular_area_circulo(radio):
    PI = 3.14159
    return PI * radio ** 2

class CalculadoraGeometrica:
    pass
```

**Líneas en blanco**:

* 2 líneas en blanco antes de definiciones de clase y función a nivel de módulo
* 1 línea en blanco antes de definiciones de método dentro de clases
* Usar líneas en blanco para separar grupos de funciones relacionadas

**Importaciones**:

```python
# Correcto: importaciones separadas
import os
import sys
from subprocess import Popen, PIPE

# Incorrecto: importaciones múltiples en una línea
import sys, os
```

**Comentarios**:

* Los comentarios deben ser oraciones completas
* Usar # seguido de un espacio
* Mantener comentarios actualizados con el código
* Evitar comentarios obvios

```python
# Correcto: comentario útil
x = x + 1  # Incrementar contador de reintentos

# Incorrecto: comentario obvio
x = x + 1  # Sumar 1 a x
```

### 5.3. Recursos de documentación y comunidad

**Documentación oficial**

**docs.python.org**: La documentación oficial de Python es el recurso más completo y actualizado:

* Tutorial oficial para principiantes
* Referencia completa del lenguaje
* Biblioteca estándar documentada
* Guías de instalación y configuración

**Herramientas de documentación integradas**

**Función help()**:

```python
help(str.upper)  # Documentación de método
help(print)      # Documentación de función
```

**Función dir()**:

```python
dir(str)  # Lista todos los métodos disponibles para strings
dir()     # Lista variables en el ámbito actual
```

**Docstrings**: Documentación integrada en el código

```python
def calcular_area(base, altura):
    """
    Calcula el área de un rectángulo.
    
    Args:
        base (float): La base del rectángulo.
        altura (float): La altura del rectángulo.
    
    Returns:
        float: El área del rectángulo.
    """
    return base * altura
```

**Recursos de la comunidad**

**Stack Overflow**: La plataforma más utilizada para preguntas y respuestas sobre programación en Python.

**Reddit**: Comunidades como r/Python y r/learnpython para discusiones y aprendizaje.

**Python.org**: Sitio oficial con noticias, eventos y recursos educativos.

**PyPI**: Repositorio de paquetes con documentación de cada librería.

**GitHub**: Código fuente de proyectos Python y ejemplos prácticos.

**Real Python**: Tutoriales avanzados y artículos técnicos.

**Python Software Foundation (PSF)**: Organización que supervisa el desarrollo de Python y organiza eventos como PyCon.

### Resumen del Capítulo

Los PEP son documentos fundamentales que guían la evolución de Python, siendo PEP 8 el más importante para desarrolladores. La documentación oficial y los recursos de la comunidad proporcionan el soporte necesario para el aprendizaje continuo y la resolución de problemas.

#### **💡 Conceptos Clave:**

* **PEP**: Propuestas de mejora que guían el desarrollo de Python
* **PEP 8**: Guía de estilo oficial obligatoria para código profesional
* **Documentación oficial**: Recurso más completo y actualizado
* **Herramientas integradas**: `help()`, `dir()`, docstrings

#### **🤔 Preguntas de Reflexión:**

1. ¿Por qué es importante seguir las convenciones de PEP 8 en proyectos colaborativos?
2. ¿Cómo pueden los docstrings mejorar la mantenibilidad del código?
3. ¿Qué papel juega la comunidad Python en el ecosistema del lenguaje?

***
