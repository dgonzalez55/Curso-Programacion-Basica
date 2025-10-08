# Capítulo 2: Instalación y configuración del entorno

### 2.1. Elección de la versión de Python

**Python 2 vs Python 3**: La última versión de Python 2 fue la 2.7 en 2010, cuyo soporte y mantenimiento finalizó el 1 de enero de 2020. Actualmente, **Python 3** es la única versión en desarrollo activo.

**Versión actual recomendada**: La última versión estable es **Python 3.13** (octubre 2024), con soporte extendido programado hasta octubre de 2029. Esta versión incluye mejoras significativas en rendimiento y nuevas características del lenguaje.

**Consideraciones de compatibilidad**: Aunque la gran mayoría de librerías han migrado a Python 3, en entornos legacy puede ser necesario usar Python 2.7. Para estos casos, existen herramientas de portabilidad disponibles en la documentación oficial.

**Principales diferencias Python 2 vs Python 3**:

| Aspecto                 | Python 2                          | Python 3                              |
| ----------------------- | --------------------------------- | ------------------------------------- |
| **Función print**       | `print "hola mundo"`              | `print("hola mundo")`                 |
| **División de enteros** | Retorna entero                    | Retorna decimal                       |
| **Cadenas**             | ASCII por defecto                 | Unicode UTF-8                         |
| **Función range**       | `range()` y `xrange()`            | Solo `range()` optimizado             |
| **Función input**       | Evalúa entrada                    | Siempre retorna string                |
| **Comparación tipos**   | Permite comparar tipos diferentes | Error al comparar tipos incompatibles |

### 2.2. Instalación en diferentes sistemas operativos

**Windows**

1. Descargar el instalador MSI desde [python.org/downloads](https://www.python.org/downloads/)
2. Ejecutar el instalador con privilegios de administrador
3. **Importante**: Marcar "Add python.exe to PATH" durante la instalación
4. Seleccionar "Install for all users" si se desea acceso global
5. Elegir ubicación personalizada si es necesario (por defecto: `C:\Python3X`)

**Opciones importantes del instalador**:

* **pip**: Se instala automáticamente (gestor de paquetes)
* **IDLE**: Entorno de desarrollo básico incluido
* **Documentación**: Documentación offline del lenguaje
* **tcl/tk**: Necesario para interfaces gráficas con Tkinter

**macOS**

Hasta macOS 12.2, el sistema incluye Python 2.7 preinstalado por Apple. Para instalar Python 3:

1. Descargar el instalador desde [python.org/downloads/mac-osx](https://www.python.org/downloads/mac-osx/)
2. Seguir el asistente de instalación
3. Python 3 se instala en `/usr/local/bin/python3`

**Alternativa con Homebrew**:

```bash
brew install python
```

**Linux**

La mayoría de distribuciones GNU/Linux incluyen Python preinstalado. Para instalar Python 3:

**Ubuntu/Debian**:

```bash
sudo apt update
sudo apt install python3 python3-pip
```

**CentOS/RHEL/Fedora**:

```bash
# Fedora
sudo dnf install python3 python3-pip

# CentOS/RHEL
sudo yum install python3 python3-pip
```

### 2.3. Configuración del PATH y verificación

**Verificación de la instalación**:

```bash
python --version
# o
python3 --version
```

**Verificación de pip**:

```bash
pip --version
# o
pip3 --version
```

**Configuración manual del PATH en Windows**: Si no se marcó la opción durante la instalación:

1. Panel de Control → Sistema → Configuración avanzada del sistema
2. Variables de entorno → Variables del sistema
3. Seleccionar "Path" → Editar
4. Añadir las rutas:
   * `C:\Python3X\`
   * `C:\Python3X\Scripts\`

**Acceso al intérprete interactivo**:

```bash
python
```

Esto abre el intérprete interactivo donde puedes ejecutar código Python línea por línea.

### Resumen del Capítulo

La correcta instalación y configuración de Python es fundamental para un desarrollo eficiente. Python 3 es la única versión recomendada actualmente, y la configuración adecuada del PATH garantiza el acceso global al intérprete y herramientas asociadas.

#### **💡 Conceptos Clave:**

* **Python 3**: Única versión en desarrollo activo
* **PATH**: Variable de entorno necesaria para acceso global
* **pip**: Gestor de paquetes incluido por defecto
* **Instalación multiplataforma**: Disponible para Windows, macOS y Linux

#### **🤔 Preguntas de Reflexión:**

1. ¿Por qué es importante configurar correctamente la variable PATH?
2. ¿Qué ventajas aporta usar la última versión estable de Python?
3. ¿En qué casos podría ser necesario mantener múltiples versiones de Python?

***
