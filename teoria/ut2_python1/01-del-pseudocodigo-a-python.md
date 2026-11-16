# Del pseudocódigo a Python

## 1. ¿Qué es Python?

Python es un **lenguaje de programación interpretado**: un programa llamado **intérprete** lee el código línea a línea, de arriba abajo, y lo va ejecutando. No hace falta compilarlo antes.

Un programa en Python es un archivo de texto con la extensión **`.py`**, por ejemplo `hola.py`. Se puede escribir en cualquier editor, pero nosotros usamos **Visual Studio Code**, con la extensión de Python de Microsoft.

Todo lo que han hecho en pseudocódigo sirve tal cual: las variables, las decisiones y los bucles son los mismos. Lo que cambia es **cómo se escribe**.

---

## 2. Formas de ejecutar un programa

### 2.1. Con el botón ▶

Con el archivo `.py` abierto, pulsen el triángulo **▶** de arriba a la derecha. Se abre la **terminal** en la parte de abajo y ahí aparece lo que muestra el programa.

### 2.2. Con el menú contextual

Clic derecho sobre el código → **Run Python File in Terminal**. Hace exactamente lo mismo que el botón.

### 2.3. Desde la terminal

La terminal es la forma que funciona siempre, con cualquier editor o sin ninguno. Hay que estar en la carpeta donde está el archivo y escribir:

| Sistema | Orden |
|---|---|
| Windows | `py programa.py` |
| Mac y Linux | `python3 programa.py` |

Para moverse entre carpetas en la terminal se usa `cd`:

```
cd Programacion          → entra en la carpeta Programacion
cd ..                    → sube a la carpeta anterior
```

En VS Code, la terminal (**Terminal → Nueva terminal**) se abre directamente en la carpeta que tengan abierta.

### 2.4. Ejecutar solo un trozo

Seleccionen unas líneas y pulsen **Mayús + Intro**. VS Code ejecuta solo esas líneas. Es útil para probar algo rápido sin ejecutar el programa entero.

### 2.5. El modo interactivo

Si en la terminal escriben solo `py` (Windows) o `python3` (Mac y Linux), sin nombre de archivo, se abre el **modo interactivo**. Aparece `>>>` y cada línea que escriban se ejecuta al momento:

```
>>> 2 + 3
5
>>> print("Hola")
Hola
>>> exit()
```

Sirve para hacer pruebas, como una calculadora. Lo que escriban aquí **no se guarda**: para eso están los archivos `.py`. Para salir, `exit()`.

---

## 3. Cómo es un programa en Python

```python
# Mi primer programa
print("¡Hola, mundo!")
print("Estoy aprendiendo Python")
```

- **No hay `Algoritmo` ni `FinAlgoritmo`.** El programa empieza en la primera línea y termina en la última.
- **Una instrucción por línea.** No hace falta poner `;` al final.
- **Se ejecuta de arriba abajo**, igual que en pseudocódigo.
- **Distingue mayúsculas y minúsculas.** `print` funciona, pero `Print` da error. `nota` y `Nota` serían dos variables distintas.

### 3.1. Comentarios

Un comentario es texto que Python **ignora**. Sirve para explicar el código a quien lo lea, incluidos ustedes dentro de un mes.

```python
# Esto es un comentario de una línea

print("Hola")  # También se puede poner al final de una línea

"""
Esto es un texto de varias líneas.
Se usa sobre todo al principio de un archivo
para explicar qué hace el programa.
"""
```

### 3.2. La sangría

En pseudocódigo, `FinSi` o `FinMientras` marcan dónde acaba un bloque. **En Python no existen**: lo que va dentro de un `if`, `while` o `for` se marca con la **sangría**, que son **4 espacios** al principio de la línea.

```python
if edad >= 18:
    print("Eres mayor de edad")     # dentro del if
    print("Puedes votar")           # dentro del if
print("Fin")                        # fuera del if: se ejecuta siempre
```

En Python, la sangría **no es estética**: cambia lo que hace el programa. Si una línea tiene la sangría mal, Python da un `IndentationError` o, peor, el programa hace algo distinto de lo que querían.

VS Code pone 4 espacios cada vez que pulsan **Tab**, así que pueden usar el tabulador sin problema.

---

## 4. Cómo se escribe bien en Python: PEP 8

Python tiene una **guía de estilo oficial** que se llama **PEP 8**. No es obligatoria, porque el programa funciona igual sin seguirla, pero la sigue casi todo el código en Python que van a encontrar: librerías, documentación, ejemplos y empresas. Seguirla hace que el código sea más fácil de leer para cualquiera.

Lo más importante de PEP 8 para empezar:

### 4.1. Nombres en `snake_case`

Las variables (y más adelante las funciones) se escriben **en minúsculas y con las palabras separadas por guiones bajos**. Se llama `snake_case` porque el guion bajo recuerda a una serpiente que va por el suelo.

```python
nota_final = 7.5          # ✔ snake_case: lo recomendado en Python
precio_con_iva = 12.10    # ✔

notaFinal = 7.5           # funciona, pero es camelCase: no es la costumbre de Python
NotaFinal = 7.5           # funciona, pero esta forma se reserva para otra cosa (las clases)
```

En pseudocódigo usamos `notaFinal`, que se llama `camelCase`. **No está mal**, pero cada lenguaje tiene su costumbre: en JavaScript o Java se usa `camelCase`, y en Python, `snake_case`. A partir de ahora, en Python, `snake_case`.

### 4.2. Constantes en MAYÚSCULAS

```python
IVA = 0.07
NOTA_APROBADO = 5
```

### 4.3. Otras reglas

- **Sangría de 4 espacios.**
- **Un espacio a cada lado** de `=` y de los operadores: `total = precio * 2`, no `total=precio*2`.
- **Después de una coma, un espacio**: `print("Hola", nombre)`.
- **Líneas no muy largas**, de unos 79 caracteres como mucho.
- **Nombres que digan lo que guardan**: `precio_total` mejor que `pt` o `x`.

---

## 5. Primer contacto con `print`

`print` muestra en la terminal lo que le pongan entre paréntesis. Es el `Escribir` del pseudocódigo.

```python
print("Hola")                  # un texto, entre comillas
print(25)                      # un número, sin comillas
print("Tengo", 25, "años")     # varias cosas separadas por comas
print()                        # una línea en blanco
```

Resultado:

```
Hola
25
Tengo 25 años

```

Cuando ponen varias cosas separadas por comas, `print` deja **un espacio** entre ellas y **cambia de línea** al final. En los apuntes de la actividad siguiente verán cómo cambiar eso y otras formas de mostrar resultados.

---

## 6. Cuando algo falla: leer un error

Cuando Python encuentra un error, para el programa y muestra un mensaje en la terminal. Asusta al principio, pero dice exactamente qué pasa y dónde:

```
Traceback (most recent call last):
  File "C:\Users\ana\Programacion\saludo.py", line 3, in <module>
    print("Hola", nombe)
                  ^^^^^
NameError: name 'nombe' is not defined. Did you mean: 'nombre'?
```

Se lee **de abajo arriba**:

1. **La última línea** dice el **tipo de error** y una explicación: `NameError`, la variable `nombe` no existe. Python incluso sugiere que quizá querían decir `nombre`.
2. **Encima**, la línea de código que ha fallado, con `^^^^^` señalando el trozo exacto.
3. **Más arriba**, el archivo y el **número de línea**: `line 3`.

Los errores más habituales al empezar:

| Error | Qué suele significar | Ejemplo |
|---|---|---|
| `SyntaxError` | Algo está mal escrito: falta un paréntesis, unas comillas, unos dos puntos… | `print("Hola"` |
| `IndentationError` | La sangría está mal: falta, sobra o no coincide | Una línea dentro de un `if` sin los 4 espacios |
| `NameError` | Se usa una variable que no existe o está mal escrita | `print(nombe)` |
| `TypeError` | Se mezclan tipos que no se pueden mezclar, como texto y número | `"Edad: " + 17` |
| `ValueError` | El tipo es correcto pero el valor no sirve | `int("hola")` |

**Consejo:** cuando salga un error, vayan a la línea que indica y miren también **la de antes**. Muchas veces el fallo de verdad está una línea más arriba, como un paréntesis que no se cerró.

---

## 7. Del pseudocódigo a Python: vista general

Esta tabla resume las equivalencias. Cada parte se explica con detalle en los apuntes de las siguientes actividades.

| Pseudocódigo | Python |
|---|---|
| `Algoritmo … FinAlgoritmo` | No hace falta |
| `// comentario` | `# comentario` |
| `x <- 5` | `x = 5` |
| `Escribir "Hola ", nombre` | `print("Hola", nombre)` |
| `Leer nombre` (texto) | `nombre = input()` |
| `Leer n` (número) | `n = int(input())` |
| `a = b` (comparar) | `a == b` |
| `a <> b` | `a != b` |
| `Y` · `O` · `NO` | `and` · `or` · `not` |
| `n MOD 2` | `n % 2` |
| `Verdadero` · `Falso` | `True` · `False` |
| `Si … Entonces … SiNo … FinSi` | `if …:` · `else:` |
| `Segun … De Otro Modo … FinSegun` | `match …:` · `case …:` · `case _:` |
| `Mientras … Hacer … FinMientras` | `while …:` |
| `Para i <- 1 Hasta 5 Hacer … FinPara` | `for i in range(1, 6):` |
| `FinSi`, `FinMientras`, `FinPara` | No existen: se marca con la sangría |
