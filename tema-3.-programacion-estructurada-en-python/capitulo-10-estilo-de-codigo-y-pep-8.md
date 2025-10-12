# Capítulo 10: Estilo de código y PEP 8

El **estilo de código** es mucho más que una cuestión estética o de preferencia personal; es una práctica profesional que define la calidad, legibilidad y mantenibilidad del software. Un estilo consistente en un proyecto permite a los desarrolladores entender el código más rápidamente, colaborar de manera más efectiva y cometer menos errores. Para la comunidad Python, la guía de estilo oficial es **PEP 8**, un documento que establece las convenciones para escribir código Python claro y legible.

En este capítulo exploraremos los principios fundamentales del código limpio en Python, las reglas específicas de PEP 8, técnicas de documentación profesional, y herramientas para mantener consistencia en el estilo de código.

### 10.1. ¿Por qué es importante el estilo de código?

La máxima fundamental es que "_**el código se lee muchas más veces de las que se escribe**_". <mark style="background-color:yellow;">**Un código limpio no solo funciona, sino que también comunica su intención claramente**</mark>. Observe la diferencia:

#### <mark style="background-color:$danger;">**Antes: Código difícil de leer**</mark>

```python
def proc(d,f,t):
    r=[]
    for i in d:
        if i['date']>=f and i['date']<=t:
            r.append(i)
    return r
```

Este código funciona, pero es críptico. ¿Qué hacen `d`, `f` y `t`? ¿Cuál es el propósito de `proc`?

#### <mark style="background-color:$success;">**Después: Código limpio y legible**</mark>

```python
def filtrar_registros_por_fecha(registros, fecha_inicio, fecha_fin):
    """Filtra registros dentro de un rango de fechas.

    Args:
        registros (list): Lista de diccionarios con información de registros.
        fecha_inicio (date): Fecha de inicio del filtro (incluida).
        fecha_fin (date): Fecha final del filtro (incluida).

    Returns:
        list: Lista de registros que están en el rango especificado.
    """
    registros_filtrados = []
    for registro in registros:
        fecha_registro = registro['date']
        if fecha_inicio <= fecha_registro <= fecha_fin:
            registros_filtrados.append(registro)
    return registros_filtrados
```

La **versión refactorizada** es autoexplicativa gracias a **nombres descriptivos** y un _**docstring**_**&#x20;claro**, facilitando su mantenimiento y uso por otros programadores.

### 10.2. Introducción a PEP 8

#### ¿Qué es PEP 8?

**PEP 8** es el documento oficial que define la guía de estilo para código Python. Fue escrito por Guido van Rossum, Barry Warsaw y Nick Coghlan en 2001 y se actualiza regularmente. Su objetivo es promover la legibilidad y consistencia en el código Python.

**Documento completo**: [peps.python.org/pep-0008/](https://peps.python.org/pep-0008/)

#### Filosofía de PEP 8

> "La legibilidad cuenta."
>
> _Zen de Python_

PEP 8 se basa en principios fundamentales:

1. **Consistencia**: El código debe seguir patrones predecibles
2. **Legibilidad**: Priorizar la comprensión sobre la brevedad
3. **Simplicidad**: Elegir la solución más clara y directa
4. **Colaboración**: Facilitar el trabajo en equipo

#### Cuándo ser flexible con PEP 8

PEP 8 incluye una importante advertencia: **"Una tonta consistencia es el duende de las mentes pequeñas"**. Hay situaciones donde es apropiado romper las reglas:

* Mantener compatibilidad con código legacy
* Cuando seguir PEP 8 reduce la legibilidad
* En APIs que deben mantener consistencia con librerías externas
* Cuando el equipo tiene convenciones específicas bien documentadas

### 10.3. Reglas clave de PEP 8

A continuación se resumen algunas de las reglas más importantes de PEP 8.

* <mark style="background-color:$primary;">**Indentación**</mark>: Usar **4 espacios** por nivel de indentación. Nunca mezclar espacios y tabuladores.
* <mark style="background-color:$primary;">**Longitud de línea**</mark>: Limitar todas las **líneas a un máximo de 79 caracteres** (72 para docstrings y comentarios).
* <mark style="background-color:$primary;">**Nomenclatura**</mark>:
  * **`snake_case` para variables y funciones** (`nombre_usuario`, `calcular_total`).
  * **`UPPER_CASE` para constantes** (`PI`, `MAX_CONEXIONES`).
  * **`PascalCase` para clases** (`Usuario`, `GestorDeArchivos`).
* <mark style="background-color:$primary;">**Espacios en blanco**</mark>: Usar espacios alrededor de los operadores (`x = y + z`) y después de las comas (`[1, 2, 3]`).
* <mark style="background-color:$primary;">**Comentarios y Docstrings**</mark>: Escribir comentarios que expliquen el "porqué" (la intención) y docstrings para todos los módulos, funciones y clases públicos.
* <mark style="background-color:$primary;">**Organización de**</mark><mark style="background-color:$primary;">**&#x20;**</mark><mark style="background-color:$primary;">**`import`**</mark>: Agrupar las importaciones en el siguiente orden, separadas por una línea en blanco:&#x20;
  1. Librerías estándar de Python (ej. `import os`).
  2. Librerías de terceros (ej. `import requests`).
  3. Módulos locales de la aplicación (ej. `from . import utils`).

### 10.4. Herramientas para el estilo

Afortunadamente, no es necesario memorizar todas las reglas de PEP 8. El ecosistema de Python ofrece herramientas automáticas cuyo uso es una práctica estándar en el desarrollo profesional.

* _<mark style="background-color:$primary;">**Linters**</mark>_<mark style="background-color:$primary;">**&#x20;**</mark><mark style="background-color:$primary;">**(Analizadores de código)**</mark>: Herramientas que analizan el código en busca de violaciones de estilo y errores potenciales.
  * `flake8`: Rápido y sencillo, combina varias herramientas para verificar PEP 8.
  * `pylint`: Más exhaustivo, realiza un análisis más profundo del código.
* _<mark style="background-color:$primary;">**Formatters**</mark>_<mark style="background-color:$primary;">**&#x20;**</mark><mark style="background-color:$primary;">**(Formateadores de código)**</mark>: Herramientas que reformatean automáticamente el código para que cumpla con las reglas de estilo.
  * `black`: El "formateador de código intransigente". Aplica un estilo único y consistente, eliminando debates sobre el formato.
  * `isort`: Ordena automáticamente las importaciones según las convenciones de PEP 8.

#### Linters y Formateadores

**1. flake8: Verificación de estilo PEP 8**

```bash
# Instalar
pip install flake8

# Usar
flake8 mi_archivo.py
flake8 mi_proyecto/

# Configuración en .flake8
[flake8]
max-line-length = 88
exclude = __pycache__, .git, venv
ignore = E203, W503
```

**2. black: Formateador automático**

```bash
# Instalar
pip install black

# Formatear archivos
black mi_archivo.py
black mi_proyecto/

# Ver cambios sin aplicar
black --diff mi_archivo.py
```

**3. isort: Organizar imports**

```bash
# Instalar
pip install isort

# Organizar imports
isort mi_archivo.py

# Configuración compatible con black
[tool.isort]
profile = "black"
multi_line_output = 3
```

**4. pylint: Análisis completo de código**

```bash
# Instalar
pip install pylint

# Analizar código
pylint mi_archivo.py
pylint mi_proyecto/
```

#### Configuración de editor (VSCode ejemplo)

```json
{
    "python.formatting.provider": "black",
    "python.linting.enabled": true,
    "python.linting.flake8Enabled": true,
    "python.linting.pylintEnabled": true,
    "editor.formatOnSave": true,
    "python.sortImports.args": ["--profile", "black"],
    "[python]": {
        "editor.codeActionsOnSave": {
            "source.organizeImports": true
        }
    }
}
```

#### Pre-commit hooks

```yaml
# .pre-commit-config.yaml
repos:
  - repo: https://github.com/psf/black
    rev: 22.3.0
    hooks:
      - id: black

  - repo: https://github.com/pycqa/flake8
    rev: 4.0.1
    hooks:
      - id: flake8

  - repo: https://github.com/pycqa/isort
    rev: 5.10.1
    hooks:
      - id: isort
```

### Resumen del Capítulo

El estilo de código no es solo una cuestión estética; es una práctica fundamental que mejora la calidad, mantenibilidad y colaboración en proyectos de software. PEP 8 proporciona un conjunto de reglas probadas que, cuando se siguen consistentemente, resultan en código Python más legible, profesional y mantenible.

#### 💡 Conceptos Clave:

* **PEP 8**: Guía oficial de estilo para código Python
* **Indentación**: 4 espacios por nivel, nunca tabuladores
* **Nomenclatura**: `snake_case` para variables/funciones, `PascalCase` para clases, `UPPER_CASE` para constantes
* **Espaciado**: Espacios apropiados alrededor de operadores y después de comas
* **Límite de línea**: 79 caracteres (72 para comentarios)
* **Documentación**: Docstrings descriptivos y comentarios que añaden valor
* **Herramientas**: black, flake8, isort, pylint para mantener consistencia automática

#### 🤔 Preguntas de Reflexión:

1. ¿Cómo puede el código limpio reducir el tiempo de desarrollo a largo plazo?
2. ¿En qué situaciones sería apropiado romper las reglas de PEP 8?
3. ¿Qué papel juegan las herramientas automáticas en el mantenimiento del estilo?
4. ¿Cómo pueden los docstrings mejorar la documentación automática de APIs?

#### 🔧 Ejercicio Práctico Final:

Refactoriza un proyecto existente para que:

1. Cumpla completamente con PEP 8
2. Tenga docstrings profesionales en todas las funciones y clases
3. Use herramientas automáticas (black, flake8, isort)
4. Tenga una estructura de carpetas organizada y lógica
5. Incluya configuración de pre-commit hooks para mantener calidad
