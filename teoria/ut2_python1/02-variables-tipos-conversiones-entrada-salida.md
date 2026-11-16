# Variables, tipos, conversiones y entrada/salida

## 1. Variables

Una **variable** es un nombre que guarda un valor para usarlo después. Es la misma idea que en pseudocódigo: una caja con nombre.

### 1.1. Crear una variable

En Python, una variable se crea **la primera vez que se le da un valor**. No hay que anunciarla antes ni decir de qué tipo es.

```python
edad = 17
```

Se lee igual que en pseudocódigo: «edad **toma el valor** 17». El `=` de Python es el `<-` del pseudocódigo: **guarda**, no compara. Para comparar se usa `==` (lo verán en el apartado de operadores).

Funcionan las mismas reglas de la asignación que ya conocen:

```python
contador = 0
contador = contador + 1    # primero se calcula la derecha (0 + 1) y después se guarda
edad = 17
edad = 18                  # el 17 se pierde: una variable guarda un solo valor
```

### 1.2. Distintas formas de dar valor a las variables

**Una variable por línea.** La forma normal y la más clara.

```python
nombre = "Ana"
edad = 17
```

**Varias variables en una línea.** Se escriben los nombres separados por comas a la izquierda y los valores en el mismo orden a la derecha.

```python
nombre, edad, nota = "Ana", 17, 8.5
```

Es lo mismo que escribir las tres líneas por separado. Tiene que haber **el mismo número** de nombres que de valores.

**El mismo valor a varias variables.**

```python
suma = contador = 0      # suma vale 0 y contador vale 0
```

Útil para empezar varios contadores o acumuladores a la vez.

**Intercambiar dos variables.** En pseudocódigo necesitábamos una variable auxiliar:

```python
aux = a
a = b
b = aux
```

En Python se puede hacer en una sola línea:

```python
a, b = b, a
```

**Con el tipo indicado.** Se puede escribir de qué tipo es la variable poniendo `:` y el tipo después del nombre:

```python
edad: int = 17
precio: float = 2.5
nombre: str = "Ana"
```

Es **opcional** y Python **no lo comprueba**: si después guardan un texto en `edad`, no da error. Sirve como información para quien lee el código y para que VS Code avise de posibles errores. Lo verán mucho en código profesional.

**Sin valor todavía.** Si quieren crear una variable que de momento no guarda nada, se usa `None`, que significa «nada»:

```python
resultado = None
```

### 1.3. Python decide el tipo, y puede cambiar

Python deduce el tipo a partir del valor. Además, una misma variable **puede cambiar de tipo**:

```python
dato = 17          # dato es un entero
dato = "hola"      # ahora dato es un texto
```

Esto se llama **tipado dinámico**. Que se pueda no quiere decir que sea buena idea: una variable que cambia de tipo confunde a quien lee el código y provoca errores. **Cada variable, un solo tipo.**

### 1.4. Nombres válidos

Un nombre de variable:

- Puede tener **letras, números y guiones bajos** (`_`).
- **No puede empezar por un número**: `1nota` no vale, `nota1` sí.
- **No puede tener espacios** ni guiones: `nota final` y `nota-final` no valen.
- **No puede ser una palabra reservada** de Python, como `if`, `else`, `while`, `for`, `True`, `False`, `None`, `and`, `or`, `not`, `in`, `class` o `def`.
- **Distingue mayúsculas y minúsculas**: `nota` y `Nota` son variables distintas.

Python acepta tildes y `ñ` en los nombres (`año`), pero **es mejor evitarlas**: dan problemas en muchos otros lenguajes y herramientas. Mejor `anio`.

**Ojo con usar nombres de funciones de Python.** Esto no da error al principio, pero estropea la función:

```python
print = 5
print("Hola")      # TypeError: print ya no es la función, ahora es un 5
```

Eviten llamar a sus variables `print`, `input`, `int`, `str`, `float`, `list`, `type`, `sum`, `max` o `min`.

### 1.5. Cómo llamar a las variables: `snake_case`

La **guía de estilo oficial de Python (PEP 8)** dice que las variables se escriban **en minúsculas, con las palabras separadas por guiones bajos**. A esto se le llama **`snake_case`**:

```python
nota_final = 7.5           # ✔ snake_case
precio_con_iva = 12.10     # ✔
numero_de_intentos = 3     # ✔

notaFinal = 7.5            # funciona, pero es camelCase: en Python no se usa
```

En pseudocódigo usábamos `notaFinal` (`camelCase`). No es un error, pero **cada lenguaje tiene su costumbre**: en JavaScript o Java se usa `camelCase`, y en Python, `snake_case`. Como casi todo el código en Python que van a ver sigue PEP 8, conviene acostumbrarse desde el principio.

Y además, como siempre: **que el nombre diga lo que guarda**. `precio_total` es mucho mejor que `pt` o `x`.

### 1.6. Constantes

Python **no tiene constantes de verdad**: cualquier variable se puede cambiar. Por eso, para indicar que un valor no debe cambiar, se escribe **todo en MAYÚSCULAS**:

```python
IVA = 0.07
NOTA_APROBADO = 5
PIN_CORRECTO = 1234
```

Python no impide cambiarlas, pero cualquiera que lea `IVA` sabe que no debe tocarla. Las constantes se suelen poner **al principio del programa**.

---

## 2. Tipos de datos

| Tipo | Nombre en Python | Qué guarda | Ejemplos |
|---|---|---|---|
| Entero | `int` | Números sin decimales | `17`, `-3`, `0` |
| Real | `float` | Números con decimales | `2.5`, `-0.75`, `3.0` |
| Texto | `str` | Caracteres entre comillas | `"Ana"`, `'Hola'`, `"7"` |
| Lógico | `bool` | Solo `True` o `False` | `True`, `False` |
| Nada | `NoneType` | La ausencia de valor | `None` |

### 2.1. Enteros (`int`)

```python
edad = 17
temperatura = -3
habitantes = 1_200_000     # los guiones bajos se ignoran: ayudan a leer números grandes
```

### 2.2. Reales (`float`)

Los decimales se escriben con **punto**, nunca con coma:

```python
precio = 2.5       # ✔
precio = 2,5       # ✘ esto no es 2,5: crea dos valores, el 2 y el 5
```

`3.0` es un `float`, aunque no tenga parte decimal.

**Curiosidad:** los reales no siempre son exactos, porque el ordenador los guarda en binario.

```python
print(0.1 + 0.2)       # 0.30000000000000004
```

No es un fallo de Python: pasa en todos los lenguajes. Para mostrar el resultado redondeado, `round(0.1 + 0.2, 2)` da `0.3`.

### 2.3. Textos (`str`)

Un texto va **entre comillas**, simples o dobles: las dos funcionan igual.

```python
nombre = "Ana"
ciudad = 'Arrecife'
frase = "Me dijo 'hola'"          # comillas simples dentro de dobles
parrafo = """Texto
de varias
líneas"""
```

Recuerden: **`7` y `"7"` no son lo mismo**. El primero es un número y se puede operar con él; el segundo es un texto.

```python
print(7 + 3)        # 10
print("7" + "3")    # 73: con textos, + los une
```

### 2.4. Lógicos (`bool`)

Solo tienen dos valores, **`True` y `False`**, con la primera letra en **mayúscula**:

```python
aprobado = True
tiene_dni = False
mayor_de_edad = edad >= 18     # el resultado de una comparación es un bool
```

### 2.5. Saber el tipo de un valor: `type()`

```python
print(type(17))         # <class 'int'>
print(type(2.5))        # <class 'float'>
print(type("Ana"))      # <class 'str'>
print(type(True))       # <class 'bool'>
```

---

## 3. Conversiones entre tipos

A veces hay que pasar un dato de un tipo a otro. Sobre todo, porque **`input()` siempre devuelve texto**.

### 3.1. Conversiones explícitas

| Función | Convierte a | Ejemplo | Resultado |
|---|---|---|---|
| `int()` | entero | `int("25")` | `25` |
| | | `int(7.9)` | `7` (corta los decimales, no redondea) |
| | | `int(True)` | `1` |
| `float()` | real | `float("2.5")` | `2.5` |
| | | `float(3)` | `3.0` |
| `str()` | texto | `str(25)` | `"25"` |
| | | `str(2.5)` | `"2.5"` |
| `bool()` | lógico | `bool(0)` | `False` |
| | | `bool(5)` | `True` |
| | | `bool("")` | `False` (texto vacío) |
| | | `bool("hola")` | `True` |
| `round()` | redondear | `round(7.9)` | `8` |
| | | `round(3.14159, 2)` | `3.14` |

Cuando la conversión no tiene sentido, Python da un **`ValueError`**:

```python
int("hola")       # ValueError: "hola" no es un número
int("3.5")        # ValueError: int() no acepta un texto con decimales
int(float("3.5")) # 3: primero a float y después a int
```

### 3.2. Conversiones automáticas

Python convierte solo en algunos casos, siempre al tipo «más amplio»:

```python
print(3 + 2.5)      # 5.5: int + float da float
print(10 / 2)       # 5.0: la división / siempre da float
```

Pero **nunca mezcla texto y números** por su cuenta:

```python
print("Edad: " + 17)         # TypeError: no se puede sumar texto y número
print("Edad: " + str(17))    # ✔ Edad: 17
print("ja" * 3)              # jajaja: un texto por un entero lo repite
```

---

## 4. Operadores

### 4.1. Aritméticos

| Operador | Qué hace | Ejemplo | Resultado |
|---|---|---|---|
| `+` | Suma | `7 + 2` | `9` |
| `-` | Resta | `7 - 2` | `5` |
| `*` | Multiplicación | `7 * 2` | `14` |
| `/` | División (siempre da `float`) | `7 / 2` | `3.5` |
| `//` | División entera (cociente) | `7 // 2` | `3` |
| `%` | Resto de la división (el `MOD`) | `7 % 2` | `1` |
| `**` | Potencia | `7 ** 2` | `49` |

**Orden de las operaciones**, como en matemáticas:

1. Paréntesis `()`
2. Potencia `**`
3. `*`, `/`, `//`, `%`
4. `+`, `-`

```python
print(2 + 3 * 4)       # 14
print((2 + 3) * 4)     # 20
```

### 4.2. Asignación abreviada

Para actualizar una variable a partir de su propio valor hay una forma corta:

| Forma corta | Equivale a |
|---|---|
| `x += 1` | `x = x + 1` |
| `x -= 2` | `x = x - 2` |
| `x *= 3` | `x = x * 3` |
| `x /= 2` | `x = x / 2` |
| `x //= 2` | `x = x // 2` |
| `x %= 2` | `x = x % 2` |

Muy útil en contadores (`contador += 1`) y acumuladores (`suma += numero`).

En Python **no existe** `x++`, que sí está en otros lenguajes.

### 4.3. De comparación

Siempre dan como resultado `True` o `False`.

| Operador | Significado | Pseudocódigo |
|---|---|---|
| `==` | Igual | `=` |
| `!=` | Distinto | `<>` |
| `<` | Menor que | `<` |
| `>` | Mayor que | `>` |
| `<=` | Menor o igual | `<=` |
| `>=` | Mayor o igual | `>=` |

**Cuidado:** `=` guarda y `==` compara. Si escriben `if nota = 5:`, Python da un `SyntaxError`.

En Python se pueden **encadenar comparaciones**, como en matemáticas:

```python
nota_valida = 0 <= nota <= 10      # lo mismo que: nota >= 0 and nota <= 10
```

### 4.4. Lógicos

| Operador | Pseudocódigo | Es `True` cuando… |
|---|---|---|
| `and` | `Y` | se cumplen **las dos** condiciones |
| `or` | `O` | se cumple **al menos una** |
| `not` | `NO` | la condición es `False` (le da la vuelta) |

```python
edad = 20
tiene_entrada = False
print(edad >= 18 and tiene_entrada)     # False
print(edad >= 18 or tiene_entrada)      # True
print(not tiene_entrada)                # True
```

Como en pseudocódigo, sin paréntesis **`and` se evalúa antes que `or`**. Si dudan, pongan paréntesis.

---

## 5. Salida por pantalla: `print`

### 5.1. Lo básico

```python
print("Hola")
print("Tienes", 17, "años")      # Tienes 17 años
print()                          # línea en blanco
```

Con comas, `print` pone **un espacio** entre cada cosa y **cambia de línea** al terminar.

### 5.2. Cambiar el separador y el final: `sep` y `end`

```python
print("12", "11", "2026", sep="/")       # 12/11/2026
print("a", "b", "c", sep="")             # abc
print("Cargando", end="")
print("...")                             # Cargando... (en la misma línea)
```

- **`sep`** es lo que se pone **entre** los valores. Por defecto, un espacio.
- **`end`** es lo que se pone **al final**. Por defecto, un salto de línea.

### 5.3. Unir textos con `+`

```python
nombre = "Ana"
print("Hola, " + nombre + "!")            # Hola, Ana!
print("Tienes " + str(17) + " años")      # con números hay que convertir a str
```

Con `+` no se añaden espacios: los tienen que poner ustedes dentro de las comillas.

### 5.4. f-strings: la forma más cómoda

Poniendo una **`f`** delante de las comillas, todo lo que escriban **entre llaves `{}`** se sustituye por su valor:

```python
nombre = "Ana"
edad = 17
print(f"Hola, {nombre}. Tienes {edad} años.")
# Hola, Ana. Tienes 17 años.

print(f"El año que viene tendrás {edad + 1}")   # dentro de {} puede ir una operación
```

No hace falta convertir nada con `str()` ni preocuparse por los espacios. **Es la forma más usada en Python.**

Con las f-strings también se puede decidir **cuántos decimales** mostrar:

```python
precio = 27.6666
print(f"Total: {precio:.2f} €")      # Total: 27.67 €
```

`:.2f` significa «real con 2 decimales».

### 5.5. Caracteres especiales

| Se escribe | Qué hace |
|---|---|
| `\n` | Salto de línea |
| `\t` | Tabulación |
| `\"` | Unas comillas dentro de un texto con comillas dobles |
| `\\` | Una barra invertida |

```python
print("Línea 1\nLínea 2")
print("Nombre:\tAna")
```

---

## 6. Entrada por teclado: `input`

`input()` para el programa, espera a que el usuario escriba algo y pulse **Intro**, y devuelve lo que ha escrito. Es el `Leer` del pseudocódigo.

```python
nombre = input("¿Cómo te llamas? ")
print(f"Hola, {nombre}")
```

El texto entre paréntesis es el mensaje que ve el usuario. Así no hace falta un `print` antes. Dejen un **espacio al final** del mensaje para que lo que escriba el usuario no salga pegado.

### 6.1. `input` siempre devuelve texto

Aunque el usuario escriba un número, `input` devuelve un **`str`**:

```python
edad = input("Edad: ")       # el usuario escribe 17
print(edad + 1)              # TypeError: edad es "17", un texto
```

Para trabajar con números **hay que convertir**:

```python
edad = int(input("Edad: "))          # entero
precio = float(input("Precio: "))    # real
print(edad + 1)                      # 18
```

`int(input(...))` hace dos cosas: primero `input` lee el texto, y después `int` lo convierte en número.

Si el usuario escribe algo que no es un número, por ejemplo `hola`, el programa se para con un `ValueError`. Más adelante verán cómo controlar esos errores para que el programa no se pare.

---

## 7. Ejemplo completo

```python
"""
Calcula el precio final de un producto con IVA.
"""

IVA = 0.07

nombre_producto = input("Producto: ")
precio = float(input("Precio sin IVA: "))
unidades = int(input("Unidades: "))

subtotal = precio * unidades
total = subtotal * (1 + IVA)

print()
print(f"{unidades} x {nombre_producto}")
print(f"Subtotal: {subtotal:.2f} €")
print(f"Total con IVA: {total:.2f} €")
```

Ejecución:

```
Producto: Cuaderno
Precio sin IVA: 2.5
Unidades: 4

4 x Cuaderno
Subtotal: 10.00 €
Total con IVA: 10.70 €
```

---

## 8. Del pseudocódigo a Python

| Pseudocódigo | Python |
|---|---|
| `edad <- 17` | `edad = 17` |
| `contador <- contador + 1` | `contador += 1` |
| `aux <- a` · `a <- b` · `b <- aux` | `a, b = b, a` |
| `Escribir "Hola ", nombre` | `print("Hola", nombre)` o `print(f"Hola {nombre}")` |
| `Leer nombre` | `nombre = input()` |
| `Leer edad` | `edad = int(input())` |
| `Leer precio` | `precio = float(input())` |
| `Verdadero` · `Falso` | `True` · `False` |
| `n MOD 2` | `n % 2` |
| `a = b` · `a <> b` | `a == b` · `a != b` |
| `Y` · `O` · `NO` | `and` · `or` · `not` |
