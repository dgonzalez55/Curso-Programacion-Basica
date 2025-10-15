# Capítulo 2: Instalación y configuración del entorno

### Introducción al Capítulo

Este capítulo marca nuestro primer paso práctico y fundamental en el viaje como programadores de Python. Una correcta instalación y configuración del entorno no es un mero trámite, sino la construcción de los cimientos sobre los cuales edificaremos todo nuestro trabajo futuro. Un entorno bien configurado garantiza que nuestras herramientas funcionen de manera predecible, eficiente y nos permita concentrarnos en lo que realmente importa: resolver problemas con código.

### **2.1. Elección de la versión de Python**

En el mundo del software, usar la versión correcta de una herramienta es crucial. Para Python, la elección es clara y sencilla.

**Python 3 es la única versión vigente y profesionalmente aceptada.**

La versión Python 2.7, aunque fue muy popular, llegó al final de su ciclo de vida el 1 de enero de 2020. Esto significa que **ya no recibe actualizaciones de seguridad ni correcciones de errores**, lo que la hace completamente inviable para cualquier proyecto serio o profesional. La comunidad y todas las librerías importantes han migrado a Python 3.

**Principales diferencias: Python 2 vs. Python 3**

Los cambios entre versiones no fueron arbitrarios, sino que buscaron modernizar el lenguaje, corregir inconsistencias y mejorar la claridad.

| Aspecto                  | Python 2                    | Python 3                 | ¿Por qué el cambio?                                                                                                                                                        |
| ------------------------ | --------------------------- | ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Función `print`**      | `print "hola"`              | `print("hola")`          | Convierte `print` en una función, haciéndolo más consistente con el resto de funciones del lenguaje (como `len()` o `sum()`).                                              |
| **División de enteros**  | `5 / 2` → `2`               | `5 / 2` → `2.5`          | El comportamiento en Python 2 era inesperado para los principiantes. Python 3 lo hace más intuitivo, devolviendo un decimal.                                               |
| **Cadenas de texto**     | ASCII por defecto           | Unicode (UTF-8)          | Moderniza el manejo de texto para soportar caracteres de cualquier idioma del mundo de forma nativa, evitando errores de codificación.                                     |
| **Función `range`**      | `range()` y `xrange()`      | Solo `range()`           | Simplifica el lenguaje unificando las dos funciones. El nuevo `range()` es más eficiente en memoria, como lo era `xrange()`.                                               |
| **Función `input`**      | `input()` evalúa la entrada | `input()` retorna string | El comportamiento de `input()` en Python 2 era un riesgo de seguridad. Python 3 unifica todo en `input()` que siempre devuelve una cadena, siendo más seguro y predecible. |
| **Comparación de tipos** | `1 < "a"` → `False`         | `1 < "a"` → `TypeError`  | Permitir comparaciones entre tipos incompatibles ocultaba errores. Python 3 es explícito y lanza un error, evitando bugs lógicos.                                          |

***

### **2.2. Instalación en diferentes sistemas operativos**

A continuación, se detallan los pasos para instalar Python en los sistemas operativos más comunes.

<mark style="background-color:$primary;">**Windows**</mark>

1. Descarga el instalador MSI desde la página oficial: [python.org/downloads](https://python.org/downloads/).
2. Ejecuta el instalador con privilegios de administrador.
3. <mark style="background-color:$warning;">**¡Importante!**</mark> Marca la casilla "**Add python.exe to PATH**" durante la instalación.
4. Selecciona "Install Now" para la instalación por defecto, que incluye `pip` y `IDLE`.

{% hint style="warning" %}
**¿Por qué añadir Python al PATH?**&#x20;

No añadir Python al PATH es como guardar un libro importante en una biblioteca gigante sin registrarlo en el catálogo. Para encontrarlo, tendrías que saber exactamente en qué estantería está (`C:\Python3X\python.exe`). El PATH es ese catálogo para el sistema operativo; le dice dónde buscar los programas ejecutables. Al añadirlo, puedes simplemente escribir `python` en cualquier terminal y el sistema sabrá dónde encontrarlo.
{% endhint %}

<mark style="background-color:$primary;">**macOS**</mark>&#x20;

El sistema operativo puede incluir una versión antigua de Python (Python 2.7) que no debe ser modificada. Para el desarrollo, siempre debes instalar tu propia versión de Python 3.

1. **Opción 1 (Recomendada)**: Descarga el instalador oficial desde [python.org/downloads/mac-osx](https://python.org/downloads/mac-osx/) y sigue el asistente. La nueva versión se instalará en `/usr/local/bin/python3`.
2. **Opción 2 (Avanzada)**: Si usas el gestor de paquetes Homebrew, puedes instalarlo con el comando:

```bash
brew install python
```

<mark style="background-color:$primary;">**Linux**</mark>&#x20;

La mayoría de distribuciones modernas ya incluyen Python 3. Para asegurarte de tener la última versión y el gestor de paquetes `pip`, puedes usar los siguientes comandos:

* **Ubuntu/Debian**:

```bash
sudo apt update
sudo apt install python3 python3-pip
```

* **CentOS/RHEL/Fedora**:

```bash
# Fedora
sudo dnf install python3 python3-pip

# CentOS/RHEL
sudo yum install python3 python3-pip
```

***

### **2.3. Configuración del PATH y verificación**

Una vez instalado, es crucial verificar que todo funcione correctamente. Abre una terminal o símbolo del sistema y ejecuta los siguientes comandos:

**Verificar la versión de Python:**

```bash
python --version
# o
python3 --version
```

_Resultado esperado:_ `Python 3.13.0` (o la versión que hayas instalado).

**Verificar la versión de pip:**

```bash
pip --version
# o
pip3 --version
```

_Resultado esperado:_ `pip 24.0 from ...` (la versión y ruta pueden variar).

**Configuración manual del PATH en Windows**: Si no se marcó la opción durante la instalación o si recibes un error de "comando no encontrado"**:**

1. Abre el Panel de Control → Sistema → Configuración avanzada del sistema.
2. Haz clic en "Variables de entorno".
3. En "Variables del sistema", selecciona la variable "Path" y haz clic en "Editar".
4. Añade dos nuevas entradas con las rutas donde se instaló Python:
   * `C:\Python3X\` (reemplaza `X` por tu versión)
   * `C:\Python3X\Scripts\`

**Acceso al intérprete interactivo**:

```bash
python
```

Esto abre el intérprete interactivo donde puedes ejecutar código Python línea por línea.

***

### **2.4. Instalación manual de PIP**

Existe la posibilidad de que el gestor de paquetes **pip** no se incluya en la versión actual del instalador de Python, siendo no obstante posible su instalación manual mediante cualquiera de los métodos que a continuación se recogen.

#### **Método `ensurepip`**

Python incluye de serie el módulo **`ensurepip`**, el cual permite la instalación de **pip** mediante la ejecución del siguiente comando a través de la terminal del sistema

```bash
# Windows
C:> py -m ensurepip --upgrade
# Linux / MacOS
$ python -m ensurepip --upgrade
```

_Para más información sobre el funcionamiento del módulo ensurepip:_ [_https://docs.python.org/3/library/ensurepip.html#module-ensurepip_](https://docs.python.org/3/library/ensurepip.html#module-ensurepip)

#### **Método `get-pip.py`**

Este método requiere la descarga y ejecución del script **`get-pip.py`** que contiene toda la lógica necesaria para la instalación de **pip** dentro del entorno utilizado.

1. Descarga el script del enlace oficial: [https://bootstrap.pypa.io/get-pip.py](https://bootstrap.pypa.io/get-pip.py)
2. Abre una terminal, accede a la carpeta que contiene el script `get-pip.py` y ejecuta el siguiente comando, según el sistema operativo utilizado.

```bash
# Windows
C:> py get-pip.py
# Linux / MacOS
$ python get-pip.py
```

3. Lee atentamente el resultado de la instalación en la terminal, pues puede requerirse la configuración adicional de las variables de entorno (cómo en el caso del propio Python).

_Para más información sobre el script get-pip.py:_ [_https://github.com/pypa/get-pip_](https://github.com/pypa/get-pip)

#### Métodos alternativos

Existen métodos alternativos a los ya descritos, cuyo detalle puede consultarse en la documentación oficial de pip: [https://pip.pypa.io/en/stable/installation/](https://pip.pypa.io/en/stable/installation/)

***

### Resumen del Capítulo

Una instalación limpia y una correcta configuración del PATH son el punto de partida indispensable para cualquier desarrollador de Python. Hemos establecido que Python 3 es la única versión viable para el desarrollo moderno y hemos aprendido a instalarlo y verificarlo en los principales sistemas operativos, sentando una base sólida para todo lo que construiremos a continuación.

#### 💡 Conceptos Clave:

* **Python 3**: La única versión del lenguaje con desarrollo activo y soporte de seguridad, siendo la elección obligatoria para proyectos nuevos.
* **PATH**: Una variable de entorno del sistema operativo que le indica dónde buscar archivos ejecutables, permitiendo ejecutar `python` y `pip` desde cualquier directorio.
* **pip**: El gestor de paquetes de Python, que se instala por defecto y es esencial para administrar las librerías.

#### 🤔 Preguntas de Reflexión:

1. ¿Qué riesgos de seguridad implica utilizar una versión de software que ha llegado al final de su ciclo de vida, como Python 2?
2. Además de la comodidad, ¿qué problemas de reproducibilidad podría causar el no tener el PATH configurado correctamente en un equipo de desarrollo?
3. ¿Por qué crees que es una buena práctica usar siempre la última versión _estable_ de un lenguaje, en lugar de la versión más reciente pero experimental (beta)?

Con el intérprete de Python instalado y accesible desde nuestra terminal, el siguiente paso lógico es aprender a gestionar las herramientas y librerías que usaremos con él.

***
