# Capítulo 3: Gestión de paquetes y entornos virtuales

### 3.1. PyPI y pip: el ecosistema de paquetes

**Python Package Index (PyPI)** es el repositorio oficial de paquetes de Python, accesible en [pypi.org](https://pypi.org). Contiene más de 400,000 paquetes desarrollados por la comunidad mundial de Python.

**pip** (Package Installer for Python) es la herramienta estándar para instalar, actualizar y gestionar paquetes de Python. Se incluye automáticamente desde Python 3.4+.

### 3.2. Operaciones básicas con pip

**Instalación de paquetes**

```bash
pip install nombre_paquete
```

**Instalación de versión específica**

```bash
pip install nombre_paquete==1.2.3
pip install "nombre_paquete>=1.0,<2.0"
```

**Actualización de paquetes**

```bash
pip install --upgrade nombre_paquete
```

**Desinstalación de paquetes**

```bash
pip uninstall nombre_paquete
```

**Información sobre paquetes**

```bash
pip show nombre_paquete
```

**Listar paquetes instalados**

```bash
pip list
```

**Listar paquetes obsoletos**

```bash
pip list --outdated
```

### 3.3. Entornos virtuales: aislamiento y gestión de dependencias

Los **entornos virtuales** son herramientas fundamentales para el desarrollo profesional en Python. Permiten crear espacios aislados con versiones específicas de Python y sus librerías, evitando conflictos entre proyectos.

**Ventajas de los entornos virtuales**:

* **Aislamiento de dependencias**: Cada proyecto tiene sus propias versiones de librerías
* **Facilita la ejecución**: Los proyectos son más fáciles de compartir y ejecutar
* **Control de versiones**: Mantiene versiones específicas para cada proyecto
* **Evita conflictos**: Previene incompatibilidades entre diferentes proyectos

**Instalación de virtualenv**

```bash
pip install virtualenv
```

**Creación de un entorno virtual**

```bash
virtualenv nombre_proyecto
```

**Activación del entorno virtual**

**Windows**:

```bash
nombre_proyecto\Scripts\activate
```

**macOS/Linux**:

```bash
source nombre_proyecto/bin/activate
```

Cuando el entorno está activo, el prompt del terminal mostrará el nombre del entorno: `(nombre_proyecto) $`

**Desactivación del entorno virtual**

```bash
deactivate
```

### 3.4. Archivos requirements.txt

El archivo `requirements.txt` es una convención estándar para documentar las dependencias de un proyecto Python.

**Generar requirements.txt**

```bash
pip freeze > requirements.txt
```

Este comando crea un archivo con todas las librerías instaladas y sus versiones exactas:

```
blinker==1.8.2
click==8.1.7
Flask==3.0.3
itsdangerous==2.2.0
Jinja2==3.1.4
MarkupSafe==2.1.5
Werkzeug==3.0.3
```

**Instalar desde requirements.txt**

```bash
pip install -r requirements.txt
```

**Ejemplo práctico completo**:

```bash
# 1. Crear entorno virtual
virtualenv mi_proyecto

# 2. Activar entorno (Linux/macOS)
source mi_proyecto/bin/activate

# 3. Instalar paquetes necesarios
pip install flask requests

# 4. Generar archivo de dependencias
pip freeze > requirements.txt

# 5. Desactivar entorno
deactivate
```

**Buenas prácticas**:

* Crear un entorno virtual para cada proyecto
* Mantener `requirements.txt` actualizado
* Usar versiones específicas en producción
* Documentar dependencias de desarrollo por separado (`requirements-dev.txt`)

### Resumen del Capítulo

La gestión adecuada de paquetes y entornos virtuales es esencial para el desarrollo profesional con Python. PyPI proporciona un ecosistema rico de librerías, mientras que los entornos virtuales garantizan el aislamiento y la reproducibilidad de los proyectos.

#### **💡 Conceptos Clave:**

* **PyPI**: Repositorio oficial con más de 400,000 paquetes
* **pip**: Herramienta estándar para gestión de paquetes
* **Entornos virtuales**: Aislamiento de dependencias por proyecto
* **requirements.txt**: Documentación estándar de dependencias

#### **🤔 Preguntas de Reflexión:**

1. ¿Por qué es crucial usar entornos virtuales en proyectos profesionales?
2. ¿Qué problemas puede causar la instalación global de paquetes?
3. ¿Cómo facilita `requirements.txt` la colaboración en equipos de desarrollo?

***
