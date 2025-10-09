# Capítulo 4: Entorno de desarrollo integrado

### Introducción al Capítulo

En este punto del curso, ya podrías empezar a escribir código en un editor de texto simple, pero eso sería como intentar construir un mueble de precisión con solo un martillo y un serrucho. Para ser verdaderamente productivos, necesitamos un **Entorno de Desarrollo Integrado (IDE)**. La diferencia es fundamental: un editor de texto es como un cuaderno y un bolígrafo, mientras que un IDE como [**Visual Studio Code**](https://code.visualstudio.com/) es un taller de alta tecnología equipado con autocompletado inteligente, un depurador, analizadores de código y control de versiones integrado, todo diseñado para maximizar tu productividad y minimizar los errores.

### **4.1. Visual Studio Code: instalación y configuración**

Recomendamos [**Visual Studio Code (VS Code)**](https://code.visualstudio.com/) como el IDE de elección para el desarrollo en Python por varias razones de peso:

* <mark style="background-color:$primary;">**Multiplataforma y Gratuito**</mark>: Funciona perfectamente en Windows, macOS y Linux.
* <mark style="background-color:$primary;">**Ecosistema de Extensiones**</mark>: Su mayor fortaleza. Permite personalizar y ampliar el editor para casi cualquier lenguaje o flujo de trabajo.
* <mark style="background-color:$primary;">**Comunidad Activa**</mark>: Cuenta con un soporte y una documentación excelentes, con actualizaciones constantes.
* <mark style="background-color:$primary;">**Herramientas Profesionales**</mark>: Ofrece características avanzadas como depuración integrada, control de Git y un terminal incorporado.

La instalación es sencilla:

1. Descarga el instalador desde su página oficial: [code.visualstudio.com](https://code.visualstudio.com/).
2. Sigue el asistente de instalación para tu sistema operativo.

***

### **4.2. Extensión de Python y Pylance**

La verdadera magia de VS Code para Python proviene de su extensión oficial.

1. Abre VS Code.
2. Ve a la vista de Extensiones (icono de bloques en la barra lateral o `Ctrl+Shift+X`).
3. Busca "Python" y instala la **extensión oficial publicada por Microsoft**.

Esta extensión instala automáticamente varios componentes clave:

* <mark style="background-color:$primary;">**Pylance**</mark>: Es un "servidor de lenguaje" que potencia la experiencia de edición. Proporciona **IntelliSense** (autocompletado de código increíblemente inteligente), navegación de código y verificación de tipos en tiempo real.
* <mark style="background-color:$primary;">**pylint (Linter)**</mark>: Es un analizador de estilo estático. Actúa como un "**profesor de estilo**" que revisa tu código mientras escribes y te señala errores o partes que no cumplen con las convenciones de la comunidad (PEP 8). Para que funcione, debes instalarlo en tu entorno, asegurándote primero de que `pip` esté actualizado:

```bash
python -m pip install --upgrade pip
pip install pylint
```

***

### **4.3. Creación y ejecución del primer programa**

Vamos a crear nuestro primer programa dentro de VS Code, siguiendo un flujo de trabajo profesional.

1. **Abrir una carpeta de proyecto**: En lugar de abrir archivos sueltos, siempre trabaja con carpetas. Ve a `Archivo → Abrir carpeta` y selecciona o crea una carpeta para tu proyecto.
2. **Crear un nuevo archivo**: Haz clic en el icono de nuevo archivo en el explorador de VS Code y nómbralo `hello_world.py`.
3. **Escribir el código**:

```python
print("Hola, Mundo!")
```

4. **Ejecutar el programa**:

* **Método 1 (Atajo)**: La forma más rápida es usar el atajo de teclado `Ctrl+F5` o hacer clic derecho en el editor y seleccionar "Run Python File in Terminal".
* **Método 2 (Terminal Integrado)**: Abre el terminal integrado (`Ctrl+Ñ` o `Ver → Terminal`) y ejecuta el script manualmente:

```bash
python hello_world.py
```

***

### **4.4. Depuración y configuración avanzada**

Escribir código es solo una parte del trabajo. Encontrar y corregir errores (bugs) es la otra, y la depuración es la habilidad esencial para ello.

{% hint style="info" %}
Depurar es como ser un **detective que investiga el código línea por línea para encontrar al culpable (el bug)**. El depurador de VS Code es tu lupa y tu kit de análisis forense.
{% endhint %}

#### **Controles de depuración**

1. **Establece un breakpoint**: Haz clic en el margen izquierdo, junto al número de línea. Aparecerá un punto rojo. La ejecución del programa se pausará en este punto.
2. **Inicia la depuración**: Presiona `F5` o ve a `Ejecutar → Iniciar depuración`.

Una vez pausado, tendrás acceso a los controles de depuración:

* **Continuar (F5)**: Sigue la ejecución hasta el siguiente breakpoint.
* **Paso a paso por encima (F10)**: Ejecuta la línea actual y pasa a la siguiente (sin entrar en las funciones que llame).
* **Paso a paso por dentro (F11):** Si la línea actual llama a una función, entra en esa función para depurarla.
* **Paso a paso para salir (Shift+F11)**: Sale de la función actual y vuelve al punto donde fue llamada.

<mark style="background-color:$primary;">**El archivo**</mark><mark style="background-color:$primary;">**&#x20;**</mark><mark style="background-color:$primary;">**`launch.json`**</mark>&#x20;

La primera vez que depuras, VS Code creará una carpeta `.vscode` con un archivo `launch.json`. Este archivo es donde se configuran los "_**parámetros de la investigación**_". Por ejemplo, si tu script necesita argumentos de línea de comandos, los puedes añadir aquí:

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Python: Archivo actual",
            "type": "python",
            "request": "launch",
            "program": "${file}",
            "console": "integratedTerminal",
            "args": ["--port", "8080", "--debug"]
        }
    ]
}
```

#### Errores Comunes y Soluciones

* **"pylint is not installed"**: Asegúrate de haber instalado `pylint` en tu entorno virtual activo (`pip install pylint`).
* **No puedo depurar**: La depuración requiere que hayas abierto una carpeta de proyecto, no solo un archivo. Si solo abres un fichero `.py`, las funciones de depuración estarán limitadas.
* **El intérprete de Python es incorrecto**: Usa `Ctrl+Shift+P` para abrir la paleta de comandos, escribe "Python: Select Interpreter" y asegúrate de que estás usando el intérprete de tu entorno virtual (`venv`).

***

### Resumen del Capítulo

Visual Studio Code, potenciado con la extensión de Python y herramientas como Pylance y Pylint, se transforma en un centro de mando completo para el desarrollo profesional. Hemos aprendido a configurar el entorno, escribir y ejecutar nuestro primer programa, y, lo más importante, a usar el depurador, una habilidad crítica que nos permitirá analizar y corregir nuestro código de manera eficiente.

#### 💡 Conceptos Clave:

* **VS Code**: Un IDE multiplataforma, extensible y profesional, ideal para el desarrollo en Python.
* **Pylance**: El servidor de lenguaje que proporciona autocompletado avanzado (IntelliSense) y análisis de código en tiempo real.
* **Depuración**: El proceso de encontrar y corregir errores en el código mediante el uso de breakpoints y la ejecución controlada paso a paso.
* **`launch.json`**: El archivo de configuración que permite personalizar las sesiones de depuración, como pasar argumentos de línea de comandos.

#### 🤔 Preguntas de Reflexión:

1. ¿Qué ventajas concretas ofrece el autocompletado de un IDE como VS Code frente a escribir código en un editor simple como el Bloc de notas?
2. ¿Por qué la habilidad de depurar es considerada más importante por muchos desarrolladores senior que la habilidad de escribir código rápidamente?
3. En un proyecto que procesa archivos, ¿cómo usarías la configuración `args` del `launch.json` para probar tu script con diferentes archivos de entrada sin modificar el código?

Ahora que tenemos nuestro taller configurado, es hora de aprender las reglas de estilo y las normas de la comunidad para escribir código limpio, profesional y comprensible para otros.

***
