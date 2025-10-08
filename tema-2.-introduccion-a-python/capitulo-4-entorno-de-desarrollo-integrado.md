# Capítulo 4: Entorno de desarrollo integrado

### 4.1. Visual Studio Code: instalación y configuración

**Visual Studio Code (VS Code)** es el IDE recomendado para desarrollo en Python debido a sus características profesionales y soporte nativo. Es multiplataforma, de código abierto y cuenta con un ecosistema extenso de extensiones.

**Ventajas de VS Code para Python**:

* **Multiplataforma**: Disponible para Windows, macOS y Linux
* **Código abierto**: Desarrollo transparente y gratuito
* **Ecosistema de extensiones**: Miles de extensiones disponibles
* **Comunidad activa**: Gran soporte y documentación
* **Versatilidad**: Soporta múltiples lenguajes de programación
* **Profesional**: Herramientas avanzadas de desarrollo

**Instalación**:

1. Descargar desde [code.visualstudio.com](https://code.visualstudio.com)
2. Seguir el asistente de instalación para el sistema operativo correspondiente
3. Configurar opciones iniciales de tema y teclado

### 4.2. Extensión de Python y Pylance

**Instalación de la extensión oficial de Python**

1. Abrir VS Code
2. Ir a la vista de extensiones (Ctrl+Shift+X)
3. Buscar "Python" de Microsoft
4. Instalar la extensión oficial

La extensión de Python incluye automáticamente:

* **Pylance**: Servidor de lenguaje avanzado con IntelliSense
* **Jupyter**: Soporte para notebooks interactivos
* **Depurador**: Herramientas de debugging integradas

**Características principales de Pylance**:

* **IntelliSense**: Autocompletado inteligente de código
* **Verificación de tipos**: Análisis estático del código
* **Navegación de código**: Ir a definición, encontrar referencias
* **Refactorización**: Renombrado inteligente y reestructuración
* **Importación automática**: Sugerencias de imports

**Configuración de pylint**

Para análisis estático del código, es recomendable instalar pylint:

```bash
python -m pip install --upgrade pip
pip install pylint
```

Pylint proporciona:

* Detección de errores sintácticos
* Verificación de estilo (PEP 8)
* Sugerencias de mejores prácticas
* Detección de código no utilizado

### 4.3. Creación y ejecución del primer programa

**Configuración del workspace**

1. **Abrir carpeta del proyecto**: File → Open Folder (Ctrl+K Ctrl+O)
2. **Crear archivo Python**: New File → `hello_world.py`

```python
print("Hola, Mundo!")
```

**Ejecución del programa**

**Método 1 - Ejecución directa**:

* Clic derecho en el archivo → "Run Python File in Terminal"
* Atajo de teclado: Ctrl+F5

**Método 2 - Terminal integrado**:

```bash
python hello_world.py
```

**Depuración del código**

1. **Establecer breakpoint**: Clic en el margen izquierdo junto al número de línea
2. **Iniciar depuración**: F5 o Run → Start Debugging
3. **Configurar depurador**: Seleccionar "Python File"

### 4.4. Depuración y configuración avanzada

**Archivo launch.json**

VS Code crea automáticamente `.vscode/launch.json` para configuraciones de depuración:

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Python: Archivo actual",
            "type": "python",
            "request": "launch",
            "program": "${file}",
            "console": "integratedTerminal"
        }
    ]
}
```

**Configuración con argumentos**

Para programas que requieren argumentos de línea de comandos:

```json
{
    "name": "Python con argumentos",
    "type": "python",
    "request": "launch",
    "program": "${file}",
    "console": "integratedTerminal",
    "args": ["--port", "8080", "--debug"]
}
```

**Herramientas de depuración**

**Panel de variables**: Muestra el estado de las variables locales y globales durante la ejecución.

**Consola de depuración**: Permite ejecutar código Python mientras el programa está pausado.

**Pila de llamadas**: Muestra la jerarquía de funciones llamadas.

**Controles de depuración**:

* **Continuar** (F5): Continúa la ejecución hasta el próximo breakpoint
* **Paso siguiente** (F10): Ejecuta la siguiente línea sin entrar en funciones
* **Entrar** (F11): Entra en la función llamada en la línea actual
* **Salir** (Shift+F11): Sale de la función actual
* **Reiniciar** (Ctrl+Shift+F5): Reinicia la sesión de depuración
* **Parar** (Shift+F5): Termina la sesión de depuración

**Errores comunes y soluciones**

**Error "pylint is not installed"**:

```bash
pip install pylint
```

**Error de depuración sin carpeta abierta**:

* Abrir la carpeta del proyecto (no solo el archivo)
* Crear configuración de depuración específica

**Problemas con rutas de Python**:

* Verificar que la extensión detecta el intérprete correcto
* Usar Ctrl+Shift+P → "Python: Select Interpreter"

### Resumen del Capítulo

Visual Studio Code proporciona un entorno de desarrollo profesional para Python con herramientas avanzadas de edición, depuración y análisis de código. La configuración adecuada del IDE y sus extensiones es fundamental para un flujo de trabajo eficiente.

#### **💡 Conceptos Clave:**

* **VS Code**: IDE multiplataforma y profesional para Python
* **Pylance**: IntelliSense avanzado y análisis estático
* **Depuración integrada**: Breakpoints, variables, consola interactiva
* **launch.json**: Configuración personalizada de ejecución

#### **🤔 Preguntas de Reflexión:**

1. ¿Qué ventajas aporta usar un IDE especializado frente a un editor simple?
2. ¿Cómo puede la depuración integrada acelerar el desarrollo y la corrección de errores?
3. ¿Por qué es importante la configuración de argumentos en el archivo launch.json?

***
