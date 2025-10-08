# Capítulo 9: Estilo de código y PEP 8

El **estilo de código** es mucho más que una cuestión estética; es una práctica fundamental que mejora la legibilidad, mantenibilidad y colaboración en proyectos de software. **PEP 8** (Python Enhancement Proposal 8) es la guía de estilo oficial para el código Python, establecida por la comunidad de desarrolladores y respaldada por el creador del lenguaje, Guido van Rossum.

En este capítulo exploraremos los principios fundamentales del código limpio en Python, las reglas específicas de PEP 8, técnicas de documentación profesional, y herramientas para mantener consistencia en el estilo de código.

### 9.1. ¿Por qué es importante el estilo de código?

#### El código se lee más de lo que se escribe

Un estudio famoso en ingeniería de software indica que el código se **lee 10 veces más** de lo que se escribe. Esto significa que invertir tiempo en escribir código legible tiene un retorno de inversión enorme:

* **Mantenimiento más fácil**: Localizar y corregir errores es más rápido
* **Colaboración efectiva**: Otros desarrolladores pueden entender y contribuir
* **Menor tiempo de onboarding**: Nuevos miembros del equipo se adaptan más rápido
* **Reducción de errores**: Código claro reduce malentendidos y bugs
* **Eficiencia del desarrollo**: Menos tiempo perdido descifrando código existente

#### Ejemplo: Código difícil de leer vs. código limpio

```python
# ❌ Código difícil de leer
def c(l,f):
    r=[]
    for i in l:
        if f(i):r.append(i)
    return r

def p(n):
    if n<2:return False
    for i in range(2,int(n**0.5)+1):
        if n%i==0:return False
    return True

result=c(range(2,50),p)
print(result)
```

```python
# ✅ Código limpio y legible
def filtrar_lista(lista, funcion_filtro):
    """
    Filtra una lista aplicando una función de criterio.
    
    Args:
        lista: Lista de elementos a filtrar
        funcion_filtro: Función que determina si un elemento se incluye
    
    Returns:
        Lista con elementos que cumplen el criterio
    """
    resultado = []
    for elemento in lista:
        if funcion_filtro(elemento):
            resultado.append(elemento)
    return resultado

def es_numero_primo(numero):
    """
    Determina si un número es primo.
    
    Args:
        numero (int): Número a evaluar
        
    Returns:
        bool: True si es primo, False en caso contrario
    """
    if numero < 2:
        return False
    
    for divisor in range(2, int(numero ** 0.5) + 1):
        if numero % divisor == 0:
            return False
    
    return True

# Encontrar números primos entre 2 y 50
numeros_candidatos = range(2, 50)
numeros_primos = filtrar_lista(numeros_candidatos, es_numero_primo)
print(f"Números primos encontrados: {numeros_primos}")
```

### 9.2. Introducción a PEP 8

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

### 9.3. Reglas fundamentales de indentación

#### Espacios, no tabuladores

**Regla**: Usar **4 espacios** por nivel de indentación. Nunca mezclar espacios y tabuladores.

```python
# ✅ Correcto: 4 espacios por nivel
def calcular_promedio(numeros):
    if not numeros:
        return 0
    
    suma = 0
    for numero in numeros:
        suma += numero
    
    return suma / len(numeros)

# ❌ Incorrecto: 2 espacios (inconsistente con PEP 8)
def calcular_promedio(numeros):
  if not numeros:
    return 0
```

#### Continuación de líneas

**Límite de línea**: 79 caracteres (72 para docstrings y comentarios)

```python
# ✅ Correcto: Alineación con delimitador de apertura
def funcion_con_muchos_parametros(parametro_uno, parametro_dos,
                                  parametro_tres, parametro_cuatro):
    pass

# ✅ Correcto: Indentación adicional para distinguir argumentos
def funcion_con_muchos_parametros(
        parametro_uno, parametro_dos, parametro_tres,
        parametro_cuatro):
    pass

# ✅ Correcto: Operadores al inicio de línea (más legible)
ingresos_totales = (ingresos_ventas
                   + ingresos_servicios
                   + ingresos_inversiones
                   - gastos_operativos)

# ✅ Correcto: Listas largas
lista_ciudades = [
    'Madrid', 'Barcelona', 'Valencia', 'Sevilla',
    'Zaragoza', 'Málaga', 'Murcia', 'Palma',
    'Las Palmas', 'Bilbao'
]
```

#### Líneas en blanco

**Separación lógica** del código:

```python
"""Módulo de utilidades matemáticas."""

import math
import random


# Dos líneas en blanco antes de clases de nivel superior
class CalculadoraCientifica:
    """Calculadora con operaciones científicas avanzadas."""
    
    def __init__(self):
        """Inicializa la calculadora."""
        self.historial = []
    
    # Una línea en blanco entre métodos
    def logaritmo(self, numero, base=math.e):
        """Calcula el logaritmo de un número en la base especificada."""
        if numero <= 0:
            raise ValueError("El número debe ser positivo")
        
        resultado = math.log(numero, base)
        self.historial.append(f"log_{base}({numero}) = {resultado}")
        return resultado


# Dos líneas en blanco antes de funciones de nivel superior
def generar_numeros_aleatorios(cantidad, minimo=1, maximo=100):
    """
    Genera una lista de números aleatorios.
    
    Args:
        cantidad (int): Número de elementos a generar
        minimo (int): Valor mínimo (incluido)
        maximo (int): Valor máximo (incluido)
    
    Returns:
        list: Lista de números aleatorios
    """
    return [random.randint(minimo, maximo) for _ in range(cantidad)]


def main():
    """Función principal del programa."""
    calc = CalculadoraCientifica()
    numeros = generar_numeros_aleatorios(5)
    
    print("Números generados:", numeros)
    
    for numero in numeros:
        try:
            log_natural = calc.logaritmo(numero)
            print(f"ln({numero}) = {log_natural:.4f}")
        except ValueError as e:
            print(f"Error con {numero}: {e}")


if __name__ == "__main__":
    main()
```

### 9.4. Convenciones de nomenclatura

#### Nombres de variables y funciones

**Regla**: `snake_case` (minúsculas con guiones bajos)

```python
# ✅ Variables correcto
edad_usuario = 25
temperatura_maxima = 35.7
lista_productos_activos = []
contador_intentos = 0

# ✅ Funciones correcto
def calcular_impuesto_total(precio_base, tasa_impuesto):
    """Calcula el impuesto total para un precio base."""
    return precio_base * tasa_impuesto

def validar_formato_email(direccion_email):
    """Valida que un email tenga formato correcto."""
    return "@" in direccion_email and "." in direccion_email

# ❌ Incorrecto: camelCase (estilo Java/JavaScript)
edadUsuario = 25
temperaturaMaxima = 35.7

def calcularImpuestoTotal(precioBase, tasaImpuesto):
    pass
```

#### Nombres de constantes

**Regla**: `UPPER_CASE` (mayúsculas con guiones bajos)

```python
# ✅ Constantes correcto
PI = 3.141592653589793
VELOCIDAD_LUZ = 299792458  # m/s
GRAVEDAD_TIERRA = 9.81     # m/s²
MAX_INTENTOS_LOGIN = 3
RUTA_ARCHIVO_CONFIG = "/etc/config.conf"
COLORES_PERMITIDOS = ['rojo', 'verde', 'azul', 'amarillo']

# Constantes en módulo separado
# configuracion.py
BASE_URL_API = "https://api.ejemplo.com/v1"
TIMEOUT_CONEXION = 30
DEBUG_MODE = True
```

#### Nombres de clases

**Regla**: `PascalCase` (primera letra de cada palabra en mayúscula)

```python
# ✅ Clases correcto
class Usuario:
    """Representa un usuario del sistema."""
    pass

class GestorBaseDatos:
    """Maneja operaciones de base de datos."""
    pass

class CalculadoraMatematicaAvanzada:
    """Calculadora con funciones científicas."""
    pass

class ErrorValidacionFormulario(Exception):
    """Excepción para errores de validación en formularios."""
    pass

# ❌ Incorrecto
class usuario:  # Debería ser Usuario
    pass

class gestor_base_datos:  # Debería ser GestorBaseDatos
    pass
```

#### Nombres de módulos y paquetes

**Regla**: `minúsculas_cortas`, sin guiones bajos si es posible

```python
# ✅ Correcto
import datetime
import json
import sqlite3

# Módulos propios
import utilidades
import configuracion
import modelo_datos  # Solo si es necesario el guión bajo
```

#### Variables privadas y protegidas

```python
class Ejemplo:
    def __init__(self):
        # Público
        self.nombre = "Público"
        
        # Protegido (convención, no obligatorio)
        self._variable_interna = "Protegido"
        
        # Privado (name mangling)
        self.__variable_muy_privada = "Privado"
    
    def metodo_publico(self):
        """Método público de la clase."""
        return "Accesible desde fuera"
    
    def _metodo_protegido(self):
        """Método protegido (convención)."""
        return "Para uso interno de la clase"
    
    def __metodo_privado(self):
        """Método privado (name mangling)."""
        return "Muy difícil de acceder desde fuera"
```

### 9.5. Espacios en blanco y operadores

#### Operadores binarios

```python
# ✅ Correcto: Espacio alrededor de operadores
resultado = a + b
condicion = x < y and y < z
lista[inicio:fin]
funcion(argumento=valor)

# ❌ Incorrecto: Sin espacios o espacios inconsistentes
resultado=a+b
condicion = x<y and y< z
lista[ inicio : fin ]
funcion(argumento = valor)
```

#### Separadores y comas

```python
# ✅ Correcto
lista = [1, 2, 3, 4]
tupla = (a, b, c)
diccionario = {'clave': 'valor', 'otra': 'valor2'}

def funcion(arg1, arg2, arg3=None):
    pass

funcion(1, 2, arg3='valor')

# ❌ Incorrecto
lista = [1,2,3,4]
tupla = (a,b,c)
diccionario = {'clave':'valor','otra':'valor2'}

def funcion(arg1,arg2,arg3=None):
    pass

funcion(1,2,arg3 = 'valor')
```

#### Casos especiales

```python
# ✅ Correcto: Sin espacios para alta precedencia
c = (a + b) * (c + d)
z = x*x + y*y
lista[i+1:j-1]

# ✅ Correcto: Alineación en asignaciones múltiples
x        = 1
y        = 2
variable = 3

# ✅ Correcto: Sin espacios innecesarios
if x == 4:
    print(x, y)

dct['key'] = lst[index]

# ❌ Incorrecto: Espacios innecesarios
if x == 4 :
    print( x , y )

dct ['key'] = lst [index]
```

### 9.6. Comentarios y docstrings

#### Comentarios inline

```python
# ✅ Comentarios útiles que añaden valor
def calcular_precio_con_descuento(precio, descuento_porcentaje):
    # Validar que el descuento esté en rango válido
    if not 0 <= descuento_porcentaje <= 100:
        raise ValueError("Descuento debe estar entre 0 y 100")
    
    descuento = precio * (descuento_porcentaje / 100)  # Calcular cantidad
    return precio - descuento

# ❌ Comentarios obvios que no añaden valor
def sumar(a, b):
    resultado = a + b  # Sumar a y b
    return resultado   # Devolver el resultado
```

#### Comentarios de bloque

```python
def algoritmo_complejo(datos):
    """
    Implementa algoritmo de ordenamiento híbrido optimizado.
    
    Este algoritmo combina quicksort para arrays grandes y
    insertion sort para segmentos pequeños, proporcionando
    mejor rendimiento en casos reales.
    """
    
    # Caso base: arrays pequeños usan insertion sort
    # que es más eficiente para tamaños menores a 10 elementos
    if len(datos) < 10:
        return insertion_sort(datos)
    
    # Para arrays grandes, usar quicksort híbrido
    # que cambia a insertion sort en recursiones profundas
    return quicksort_hibrido(datos)
```

#### Docstrings: Documentación profesional

**Estilo Google/NumPy para docstrings:**

```python
def procesar_datos_ventas(archivo_csv, filtrar_fecha=None, incluir_descuentos=True):
    """
    Procesa un archivo CSV de datos de ventas y genera estadísticas.

    Este función lee un archivo CSV con datos de ventas, aplica filtros
    opcionales y calcula métricas estadísticas básicas. Los datos deben
    tener el formato: fecha, producto, cantidad, precio_unitario.

    Args:
        archivo_csv (str): Ruta al archivo CSV con datos de ventas.
        filtrar_fecha (datetime, optional): Solo procesar ventas posteriores
            a esta fecha. Por defecto None (procesa todas).
        incluir_descuentos (bool, optional): Si incluir productos con
            descuento en el cálculo. Por defecto True.

    Returns:
        dict: Diccionario con estadísticas calculadas conteniendo:
            - 'total_ventas': Número total de transacciones
            - 'ingresos_totales': Suma total de ingresos  
            - 'producto_top': Producto con más ventas
            - 'promedio_venta': Promedio de venta por transacción

    Raises:
        FileNotFoundError: Si el archivo CSV no existe.
        ValueError: Si el formato del CSV es incorrecto.
        PermissionError: Si no hay permisos de lectura del archivo.

    Example:
        >>> stats = procesar_datos_ventas('ventas_enero.csv')
        >>> print(f"Total ventas: {stats['total_ventas']}")
        Total ventas: 1250
        
        >>> # Filtrar por fecha
        >>> from datetime import date
        >>> stats = procesar_datos_ventas(
        ...     'ventas_enero.csv',
        ...     filtrar_fecha=date(2024, 1, 15)
        ... )

    Note:
        Esta función requiere que el archivo CSV tenga headers en la
        primera línea con los nombres: fecha, producto, cantidad, precio.
    """
    # Implementación de la función...
    pass


class GestorInventario:
    """
    Gestor de inventario para tienda online.

    Esta clase maneja las operaciones CRUD (Create, Read, Update, Delete)
    sobre el inventario de productos, incluyendo control de stock,
    actualizaciones de precios y generación de reportes.

    Attributes:
        productos (dict): Diccionario de productos indexado por ID.
        ubicacion_almacen (str): Ubicación física del almacén.
        capacidad_maxima (int): Capacidad máxima del almacén.

    Example:
        >>> inventario = GestorInventario('Almacén Central', 10000)
        >>> inventario.agregar_producto('LAP001', 'Laptop Gaming', 50, 899.99)
        >>> stock = inventario.consultar_stock('LAP001')
        >>> print(f"Stock disponible: {stock}")
        Stock disponible: 50
    """

    def __init__(self, ubicacion, capacidad_maxima=1000):
        """
        Inicializa el gestor de inventario.

        Args:
            ubicacion (str): Ubicación del almacén.
            capacidad_maxima (int, optional): Capacidad máxima. Por defecto 1000.
        """
        self.productos = {}
        self.ubicacion_almacen = ubicacion
        self.capacidad_maxima = capacidad_maxima

    def agregar_producto(self, id_producto, nombre, cantidad, precio):
        """
        Agrega un nuevo producto al inventario.

        Args:
            id_producto (str): Identificador único del producto.
            nombre (str): Nombre descriptivo del producto.
            cantidad (int): Cantidad inicial en stock.
            precio (float): Precio unitario del producto.

        Raises:
            ValueError: Si el producto ya existe o los datos son inválidos.

        Returns:
            bool: True si el producto fue agregado exitosamente.
        """
        # Implementación...
        pass
```

### 9.7. Imports y organización de módulos

#### Orden de imports

```python
"""
Orden recomendado para imports:
1. Módulos de biblioteca estándar
2. Módulos de terceros relacionados
3. Módulos locales de la aplicación
"""

# 1. Biblioteca estándar
import os
import sys
import json
import datetime
from pathlib import Path
from collections import defaultdict

# Línea en blanco para separar grupos

# 2. Librerías de terceros
import requests
import pandas as pd
import numpy as np
from flask import Flask, request, jsonify
from sqlalchemy import create_engine

# Línea en blanco para separar grupos

# 3. Módulos locales
import configuracion
import utilidades
from modelos import Usuario, Producto
from base_datos import GestorDB
```

#### Imports relativos vs absolutos

```python
# ✅ Preferir imports absolutos (más claros)
from mi_proyecto.utilidades import formatear_fecha
from mi_proyecto.modelos.usuario import Usuario
from mi_proyecto.servicios.email import enviar_notificacion

# ✅ Imports relativos apropiados (dentro del mismo paquete)
from .utilidades import helper_function
from ..modelos import BaseModel
from ...configuracion import CONFIGURACION_BASE

# ❌ Evitar imports con wildcard
from mi_modulo import *  # No es claro qué se importa
```

### 9.8. Herramientas para mantener el estilo

#### Linters y formateadores

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

### 9.9. Casos prácticos: Refactoring de código

#### Ejemplo 1: Mejorando legibilidad

```python
# ❌ Código original difícil de leer
def proc(d,f,t):
    r=[]
    for i in d:
        if i['date']>=f and i['date']<=t:
            r.append(i)
    return r

# ✅ Código refactorizado siguiendo PEP 8
def filtrar_registros_por_fecha(registros, fecha_inicio, fecha_fin):
    """
    Filtra registros dentro de un rango de fechas.
    
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

#### Ejemplo 2: Organización de clase compleja

```python
# ❌ Clase mal organizada
class usr:
    def __init__(self,n,e,a):
        self.n=n
        self.e=e
        self.a=a
        self.__p=''
    def sp(self,p):self.__p=p
    def cp(self,p):return self.__p==p
    def info(self):return f'{self.n} ({self.a})'

# ✅ Clase bien organizada siguiendo PEP 8
class Usuario:
    """
    Representa un usuario del sistema con funcionalidades básicas.
    
    Esta clase encapsula la información básica de un usuario y proporciona
    métodos para gestión de contraseñas y obtención de información.
    
    Attributes:
        nombre (str): Nombre completo del usuario.
        email (str): Dirección de email del usuario.
        edad (int): Edad del usuario en años.
    """

    def __init__(self, nombre, email, edad):
        """
        Inicializa una nueva instancia de Usuario.
        
        Args:
            nombre (str): Nombre completo del usuario.
            email (str): Dirección de email válida.
            edad (int): Edad del usuario (debe ser positiva).
        
        Raises:
            ValueError: Si algún parámetro no es válido.
        """
        self.nombre = nombre
        self.email = email
        self.edad = edad
        self.__password = ''  # Password privado
        
        self._validar_datos_iniciales()

    def establecer_password(self, password):
        """
        Establece la contraseña del usuario.
        
        Args:
            password (str): Nueva contraseña del usuario.
        
        Raises:
            ValueError: Si la contraseña no cumple requisitos mínimos.
        """
        self._validar_password(password)
        self.__password = password

    def verificar_password(self, password):
        """
        Verifica si la contraseña proporcionada es correcta.
        
        Args:
            password (str): Contraseña a verificar.
        
        Returns:
            bool: True si la contraseña es correcta, False en caso contrario.
        """
        return self.__password == password

    def obtener_informacion_basica(self):
        """
        Obtiene información básica del usuario.
        
        Returns:
            str: Cadena con formato 'Nombre (Edad años)'.
        """
        return f'{self.nombre} ({self.edad} años)'

    def _validar_datos_iniciales(self):
        """Valida que los datos iniciales sean correctos."""
        if not self.nombre:
            raise ValueError("El nombre no puede estar vacío")
        
        if "@" not in self.email:
            raise ValueError("Email debe tener formato válido")
        
        if self.edad < 0:
            raise ValueError("La edad debe ser positiva")

    def _validar_password(self, password):
        """
        Valida que la contraseña cumpla requisitos mínimos.
        
        Args:
            password (str): Contraseña a validar.
        
        Raises:
            ValueError: Si la contraseña no es válida.
        """
        if len(password) < 8:
            raise ValueError("La contraseña debe tener al menos 8 caracteres")
        
        if not any(c.isupper() for c in password):
            raise ValueError("La contraseña debe tener al menos una mayúscula")
```

### 9.10. Proyecto final: Aplicación bien estructurada

#### Estructura de proyecto completa

```
mi_proyecto/
│
├── README.md
├── requirements.txt
├── setup.py
├── .flake8
├── .pre-commit-config.yaml
│
├── mi_proyecto/
│   ├── __init__.py
│   ├── configuracion.py
│   ├── utilidades.py
│   │
│   ├── modelos/
│   │   ├── __init__.py
│   │   ├── usuario.py
│   │   └── producto.py
│   │
│   ├── servicios/
│   │   ├── __init__.py
│   │   ├── autenticacion.py
│   │   └── base_datos.py
│   │
│   └── api/
│       ├── __init__.py
│       └── endpoints.py
│
├── tests/
│   ├── __init__.py
│   ├── test_usuarios.py
│   └── test_servicios.py
│
└── docs/
    ├── api.md
    └── instalacion.md
```

#### Ejemplo de módulo completo bien estructurado

```python
# mi_proyecto/servicios/autenticacion.py
"""
Servicio de autenticación para la aplicación.

Este módulo proporciona funcionalidades para registro, login y gestión
de sesiones de usuario, incluyendo validación de credenciales y 
generación de tokens de seguridad.
"""

import hashlib
import secrets
from datetime import datetime, timedelta
from typing import Dict, Optional, Tuple

from ..modelos.usuario import Usuario
from ..configuracion import (
    MAX_INTENTOS_LOGIN,
    DURACION_TOKEN_HORAS,
    SALT_PASSWORD
)


class ServicioAutenticacion:
    """
    Servicio principal para manejo de autenticación de usuarios.
    
    Esta clase centraliza toda la lógica relacionada con autenticación,
    incluyendo registro, login, logout y validación de tokens.
    
    Attributes:
        usuarios_activos (dict): Diccionario de usuarios con sesión activa.
        intentos_fallidos (dict): Contador de intentos fallidos por usuario.
    """

    def __init__(self):
        """Inicializa el servicio de autenticación."""
        self.usuarios_activos: Dict[str, Dict] = {}
        self.intentos_fallidos: Dict[str, int] = {}

    def registrar_usuario(self, nombre: str, email: str, password: str) -> Tuple[bool, str]:
        """
        Registra un nuevo usuario en el sistema.
        
        Args:
            nombre (str): Nombre completo del usuario.
            email (str): Dirección de email única.
            password (str): Contraseña en texto plano.
        
        Returns:
            Tuple[bool, str]: (éxito, mensaje de resultado).
            
        Raises:
            ValueError: Si los datos de entrada no son válidos.
        """
        try:
            # Validar datos de entrada
            self._validar_datos_registro(nombre, email, password)
            
            # Verificar si el email ya existe
            if self._email_existe(email):
                return False, f"El email {email} ya está registrado"
            
            # Crear hash seguro de la contraseña
            password_hash = self._generar_hash_password(password)
            
            # Crear nuevo usuario
            nuevo_usuario = Usuario(
                nombre=nombre,
                email=email,
                password_hash=password_hash
            )
            
            # Guardar en base de datos (simulado)
            self._guardar_usuario(nuevo_usuario)
            
            return True, f"Usuario {email} registrado exitosamente"
            
        except ValueError as e:
            return False, f"Error de validación: {e}"
        except Exception as e:
            return False, f"Error inesperado durante registro: {e}"

    def iniciar_sesion(self, email: str, password: str) -> Tuple[bool, Optional[str]]:
        """
        Inicia sesión para un usuario registrado.
        
        Args:
            email (str): Email del usuario.
            password (str): Contraseña en texto plano.
        
        Returns:
            Tuple[bool, Optional[str]]: (éxito, token de sesión si es exitoso).
        """
        # Verificar si el usuario está bloqueado por intentos fallidos
        if self._usuario_bloqueado(email):
            return False, None
        
        try:
            # Obtener usuario de la base de datos
            usuario = self._obtener_usuario_por_email(email)
            if not usuario:
                self._registrar_intento_fallido(email)
                return False, None
            
            # Verificar contraseña
            if not self._verificar_password(password, usuario.password_hash):
                self._registrar_intento_fallido(email)
                return False, None
            
            # Generar token de sesión
            token = self._generar_token_sesion()
            
            # Registrar sesión activa
            self.usuarios_activos[token] = {
                'usuario': usuario,
                'timestamp': datetime.now(),
                'expira': datetime.now() + timedelta(hours=DURACION_TOKEN_HORAS)
            }
            
            # Limpiar intentos fallidos
            self.intentos_fallidos.pop(email, None)
            
            return True, token
            
        except Exception as e:
            print(f"Error durante login: {e}")
            return False, None

    def cerrar_sesion(self, token: str) -> bool:
        """
        Cierra la sesión de un usuario.
        
        Args:
            token (str): Token de la sesión a cerrar.
        
        Returns:
            bool: True si la sesión fue cerrada exitosamente.
        """
        if token in self.usuarios_activos:
            del self.usuarios_activos[token]
            return True
        return False

    def validar_token(self, token: str) -> Optional[Usuario]:
        """
        Valida un token de sesión y devuelve el usuario asociado.
        
        Args:
            token (str): Token a validar.
        
        Returns:
            Optional[Usuario]: Usuario asociado si el token es válido, None si no.
        """
        if token not in self.usuarios_activos:
            return None
        
        sesion = self.usuarios_activos[token]
        
        # Verificar si el token ha expirado
        if datetime.now() > sesion['expira']:
            del self.usuarios_activos[token]
            return None
        
        return sesion['usuario']

    # Métodos privados de utilidad
    
    def _validar_datos_registro(self, nombre: str, email: str, password: str) -> None:
        """Valida los datos de registro de usuario."""
        if not nombre or len(nombre.strip()) < 2:
            raise ValueError("El nombre debe tener al menos 2 caracteres")
        
        if not email or "@" not in email or "." not in email:
            raise ValueError("El email debe tener un formato válido")
        
        if len(password) < 8:
            raise ValueError("La contraseña debe tener al menos 8 caracteres")
        
        if not any(c.isupper() for c in password):
            raise ValueError("La contraseña debe tener al menos una mayúscula")
        
        if not any(c.isdigit() for c in password):
            raise ValueError("La contraseña debe tener al menos un número")

    def _generar_hash_password(self, password: str) -> str:
        """Genera hash seguro para una contraseña."""
        password_with_salt = password + SALT_PASSWORD
        return hashlib.sha256(password_with_salt.encode()).hexdigest()

    def _verificar_password(self, password: str, hash_almacenado: str) -> bool:
        """Verifica si una contraseña coincide con su hash."""
        hash_password = self._generar_hash_password(password)
        return hash_password == hash_almacenado

    def _generar_token_sesion(self) -> str:
        """Genera un token seguro para la sesión."""
        return secrets.token_urlsafe(32)

    def _email_existe(self, email: str) -> bool:
        """Verifica si un email ya está registrado."""
        # Simulación - en implementación real consultaría la BD
        return False

    def _obtener_usuario_por_email(self, email: str) -> Optional[Usuario]:
        """Obtiene usuario por email desde la base de datos."""
        # Simulación - en implementación real consultaría la BD
        return None

    def _guardar_usuario(self, usuario: Usuario) -> None:
        """Guarda usuario en la base de datos."""
        # Simulación - en implementación real guardaría en BD
        pass

    def _usuario_bloqueado(self, email: str) -> bool:
        """Verifica si un usuario está bloqueado por intentos fallidos."""
        return self.intentos_fallidos.get(email, 0) >= MAX_INTENTOS_LOGIN

    def _registrar_intento_fallido(self, email: str) -> None:
        """Registra un intento de login fallido."""
        self.intentos_fallidos[email] = self.intentos_fallidos.get(email, 0) + 1
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
