# Estructuras de control en Python

Las estructuras de control son las mismas que en pseudocódigo: **selectivas** (Si, Según) e **iterativas** (Mientras, Para). Lo que cambia es la forma de escribirlas.

## 1. Bloques: dos puntos y sangría

En Python, todas las estructuras de control siguen el mismo patrón:

1. La línea que abre la estructura **termina en dos puntos `:`**.
2. Las instrucciones que van **dentro** llevan **4 espacios** de sangría.
3. El bloque termina cuando una línea vuelve a la sangría de antes. **No hay `FinSi`, `FinMientras` ni `FinPara`.**

```python
if edad >= 18:                   # termina en :
    print("Mayor de edad")       # dentro: 4 espacios
    print("Puede votar")         # dentro
print("Fin")                     # fuera: sin sangría
```

Los dos errores más típicos:

```python
if edad >= 18                    # SyntaxError: faltan los dos puntos
    print("Mayor de edad")

if edad >= 18:
print("Mayor de edad")           # IndentationError: falta la sangría
```

---

## 2. Selectivas: `if`

### 2.1. Selectiva simple: `if`

Si se cumple la condición, se ejecuta el bloque. Si no, no pasa nada y el programa sigue.

```python
total = float(input("Total de la compra: "))
if total > 50:
    total -= 5
    print("¡5 € de descuento!")
print(f"A pagar: {total} €")
```

### 2.2. Selectiva doble: `if` · `else`

```python
numero = int(input("Número: "))
if numero % 2 == 0:
    print("Es par")
else:
    print("Es impar")
```

`else` no lleva condición y también termina en `:`. Siempre se ejecuta **una de las dos** ramas.

### 2.3. Selectiva múltiple: `if` · `elif` · `else`

En pseudocódigo usábamos Si anidados. En Python existe **`elif`** («else if»), que hace lo mismo pero mucho más ordenado:

```python
nota = float(input("Nota: "))
if nota < 5:
    print("Insuficiente")
elif nota < 6:
    print("Suficiente")
elif nota < 7:
    print("Bien")
elif nota < 9:
    print("Notable")
else:
    print("Sobresaliente")
```

- Puede haber **tantos `elif` como hagan falta**.
- El `else` final es opcional.
- Se ejecuta **solo la primera** rama cuya condición se cumple. Las demás ya no se comprueban. Por eso, como en pseudocódigo, **el orden de las condiciones importa**.

Comparen con lo mismo en Si anidados:

```python
if nota < 5:
    print("Insuficiente")
else:
    if nota < 6:
        print("Suficiente")
    else:
        if nota < 7:
            ...
```

Funciona igual, pero cada nivel añade sangría y se vuelve difícil de leer. **Usen `elif`.**

### 2.4. `if` anidados

Un `if` dentro de otro sigue siendo útil cuando la segunda pregunta solo tiene sentido si se cumple la primera:

```python
edad = int(input("Edad: "))
if edad >= 18:
    carne = input("¿Tienes carné? (s/n): ")
    if carne == "s":
        print("Puedes conducir")
    else:
        print("Necesitas el carné")
else:
    print("Eres menor de edad")
```

### 2.5. Condiciones compuestas

Se pueden combinar condiciones con `and`, `or` y `not`:

```python
if edad >= 18 and tiene_entrada:
    print("Puede entrar")

if dia == "sábado" or dia == "domingo":
    print("Fin de semana")

if not aprobado:
    print("Hay que recuperar")

if 0 <= nota <= 10:
    print("Nota válida")
```

### 2.6. Forma corta: la expresión condicional

Cuando solo hay que elegir **un valor** entre dos, se puede escribir en una línea:

```python
resultado = "Aprobado" if nota >= 5 else "Suspenso"
```

Es lo mismo que:

```python
if nota >= 5:
    resultado = "Aprobado"
else:
    resultado = "Suspenso"
```

Úsenla solo para casos sencillos. Si no queda clara, mejor el `if` normal.

---

## 3. Selectiva por casos: `match` (el Según)

`match` compara **una variable** con **valores concretos**. Es el equivalente del Según y existe desde **Python 3.10**.

```python
opcion = int(input("1. Sumar  2. Restar  3. Multiplicar: "))
match opcion:
    case 1:
        print("Has elegido sumar")
    case 2:
        print("Has elegido restar")
    case 3:
        print("Has elegido multiplicar")
    case _:
        print("Opción no válida")
```

- Cada `case` es un valor posible.
- **`case _:`** es el **De Otro Modo**: se ejecuta si no coincide ningún caso anterior.
- Solo se ejecuta **un** caso.

Varios valores en el mismo caso se separan con **`|`** (que se lee «o»):

```python
match dia:
    case "sábado" | "domingo":
        print("Fin de semana")
    case _:
        print("Día laborable")
```

**¿`match` o `if`?** Igual que en pseudocódigo: `match` para comparar una variable con **valores concretos** (un menú de opciones); `if` para **rangos** o condiciones (`nota < 5`, `edad >= 18 and …`). Todo lo que se hace con `match` se puede hacer con `if` · `elif`, y en mucho código antiguo lo verán así, porque `match` es reciente.

---

## 4. Iterativa: `while` (el Mientras)

Repite el bloque **mientras se cumpla la condición**. La condición se comprueba **antes** de cada vuelta.

```python
pin = int(input("Introduce el PIN: "))
while pin != 1234:
    print("PIN incorrecto")
    pin = int(input("Introduce el PIN: "))
print("Acceso permitido")
```

Se usa cuando **no sabemos cuántas veces** se va a repetir: depende de lo que haga el usuario o de algo que cambia durante el programa.

### 4.1. Contadores y acumuladores

Igual que en pseudocódigo: **se les da valor antes del bucle** y se actualizan dentro.

```python
suma = 0          # acumulador: empieza en 0
cantidad = 0      # contador: empieza en 0

numero = int(input("Número (0 para terminar): "))
while numero != 0:
    suma += numero
    cantidad += 1
    numero = int(input("Número (0 para terminar): "))

print(f"Has escrito {cantidad} números y suman {suma}")
```

Este patrón (leer antes del bucle, comprobar, procesar y volver a leer al final) es el típico cuando el usuario indica con un valor especial que quiere terminar. A ese valor (aquí, el `0`) se le llama **centinela**.

### 4.2. Cuidado con el bucle infinito

Si nada dentro del bucle hace que la condición llegue a ser falsa, el bucle **no termina nunca**:

```python
i = 1
while i <= 5:
    print(i)          # escribe 1 para siempre: i nunca cambia
```

Falta `i += 1` dentro del bucle. Si les pasa, paren el programa con **Ctrl + C** en la terminal.

### 4.3. `while True` con `break`

A veces es más claro repetir «siempre» y salir con **`break`** cuando se cumple algo:

```python
while True:
    pin = int(input("Introduce el PIN: "))
    if pin == 1234:
        break
    print("PIN incorrecto")
print("Acceso permitido")
```

Así no hay que pedir el PIN dos veces (antes del bucle y dentro). Funciona como el Repetir… Hasta Que del pseudocódigo, que en Python no existe.

---

## 5. Iterativa: `for` (el Para)

Se usa cuando **sabemos cuántas veces** hay que repetir. En Python, `for` recorre una serie de valores, y para generar números se usa **`range()`**.

```python
for i in range(1, 11):
    print(f"7 x {i} = {7 * i}")
```

La variable `i` toma un valor distinto en cada vuelta. No hace falta darle valor antes ni sumarle 1: lo hace el propio `for`.

### 5.1. Las tres formas de `range`

| Forma | Valores que genera | Ejemplo | Resultado |
|---|---|---|---|
| `range(fin)` | de 0 hasta `fin - 1` | `range(5)` | 0, 1, 2, 3, 4 |
| `range(inicio, fin)` | de `inicio` hasta `fin - 1` | `range(1, 6)` | 1, 2, 3, 4, 5 |
| `range(inicio, fin, paso)` | de `inicio` hasta antes de `fin`, de `paso` en `paso` | `range(0, 11, 2)` | 0, 2, 4, 6, 8, 10 |
| | con paso negativo, hacia atrás | `range(10, 0, -1)` | 10, 9, …, 1 |

**Lo más importante: el valor de `fin` nunca se incluye.** Por eso, para ir de 1 a 10 se escribe `range(1, 11)`. Es el error más típico al pasar del pseudocódigo:

| Pseudocódigo | Python |
|---|---|
| `Para i <- 1 Hasta 10 Hacer` | `for i in range(1, 11):` |
| `Para i <- 0 Hasta n - 1 Hacer` | `for i in range(n):` |
| `Para i <- 10 Hasta 1 Con Paso -1 Hacer` | `for i in range(10, 0, -1):` |

### 5.2. Contadores y acumuladores con `for`

```python
suma = 0
for i in range(1, 5):
    suma += i
print(suma)       # 10 (1 + 2 + 3 + 4)
```

```python
n = int(input("¿Cuántas notas? "))
suma = 0
aprobados = 0
for i in range(n):
    nota = float(input(f"Nota {i + 1}: "))
    suma += nota
    if nota >= 5:
        aprobados += 1
print(f"Media: {suma / n:.2f}")
print(f"Aprobados: {aprobados}")
```

Fíjense en `{i + 1}`: `i` va de 0 a `n - 1`, pero al usuario le mostramos «Nota 1», «Nota 2»…

### 5.3. `for` no solo cuenta números: recorrer textos y listas

En Python, `for` puede recorrer **cualquier serie de valores**, no solo números. En cada vuelta, la variable toma **el siguiente elemento**. Esto lo van a usar continuamente.

Antes, una presentación rápida de las **listas**, que son los arrays del pseudocódigo. Las verán a fondo más adelante:

```python
notas = [6, 3, 8, 4, 9]                        # lista de enteros
precios = [2.5, 8.0, 1.2]                      # lista de reales
nombres = ["Ana", "Luis", "Marta"]             # lista de textos
print(notas[0])                                # 6: las posiciones empiezan en 0
print(len(notas))                              # 5: len() es el Longitud() del pseudocódigo
```

#### Recorrer un texto, letra a letra

```python
palabra = "programa"
for letra in palabra:
    print(letra)
```

En cada vuelta, `letra` vale un carácter: `p`, `r`, `o`, `g`… Comparen con el pseudocódigo, donde había que usar posiciones:

```python
# Al estilo del pseudocódigo: con la posición
for i in range(len(palabra)):
    print(palabra[i])

# Al estilo de Python: directamente cada letra
for letra in palabra:
    print(letra)
```

Los dos hacen lo mismo. El segundo es más corto y no hay que pensar en `len() - 1`.

Ejemplo: contar vocales.

```python
palabra = input("Palabra: ")
vocales = 0
for letra in palabra:
    if letra in "aeiou":          # in comprueba si la letra está dentro de "aeiou"
        vocales += 1
print(f"Tiene {vocales} vocales")
```

#### Recorrer una lista de números

```python
notas = [6, 3, 8, 4, 9]
aprobados = 0
for nota in notas:
    if nota >= 5:
        aprobados += 1
print(f"Aprobados: {aprobados}")
```

Fíjense en el nombre: la lista se llama en **plural** (`notas`) y la variable del `for`, en **singular** (`nota`). Es la costumbre, y así se lee casi como una frase: «para cada nota en notas…».

#### Recorrer una lista de textos

```python
alumnos = ["Ana", "Luis", "Marta"]
for alumno in alumnos:
    print(f"Hola, {alumno}")
```

Funciona exactamente igual que con números: `for` no mira de qué tipo son los elementos.

```python
frutas = ["manzana", "pera", "plátano"]
for fruta in frutas:
    print(f"{fruta} tiene {len(fruta)} letras")
```

#### Cuando hace falta la posición: `range(len(...))` y `enumerate`

A veces necesitan saber **en qué posición** está cada elemento, por ejemplo para mostrar «1. Ana», «2. Luis»… Hay dos formas:

```python
alumnos = ["Ana", "Luis", "Marta"]

# Con range y len: i es la posición
for i in range(len(alumnos)):
    print(f"{i + 1}. {alumnos[i]}")

# Con enumerate: da la posición y el elemento a la vez
for i, alumno in enumerate(alumnos):
    print(f"{i + 1}. {alumno}")
```

Las dos muestran:

```
1. Ana
2. Luis
3. Marta
```

`enumerate` es la forma preferida en Python. `range(len(...))` es útil cuando necesitan la posición para **otra lista** con los mismos datos en el mismo orden:

```python
dias = ["Lun", "Mar", "Mié", "Jue", "Vie"]
temperaturas = [22, 27, 19, 31, 25]
for i in range(len(dias)):
    print(f"{dias[i]}: {temperaturas[i]} grados")
```

Esto también se puede hacer con **`zip`**, que recorre las dos listas a la vez:

```python
for dia, temperatura in zip(dias, temperaturas):
    print(f"{dia}: {temperatura} grados")
```

#### Recorrer al revés

```python
palabra = "roma"
for letra in reversed(palabra):
    print(letra, end="")        # amor
print()

for i in range(10, 0, -1):      # 10, 9, 8, …, 1
    print(i)
```

#### Buscar el mayor (o el menor) de una lista

```python
notas = [6, 3, 8, 4, 9]
mayor = notas[0]                # se empieza por el primero, no por 0
for nota in notas:
    if nota > mayor:
        mayor = nota
print(f"Nota más alta: {mayor}")
```

Python ya trae funciones que lo hacen solas: `max(notas)`, `min(notas)` y `sum(notas)`. Está bien conocerlas, pero **primero tienen que saber hacerlo con el bucle**: en los ejercicios se pedirá así para practicar el recorrido.

#### Bucles anidados

Un `for` dentro de otro: el de dentro hace **todas** sus vueltas por cada vuelta del de fuera.

```python
for tabla in range(1, 4):
    for i in range(1, 4):
        print(f"{tabla} x {i} = {tabla * i}")
    print()                         # línea en blanco entre tablas
```

```python
alumnos = ["Ana", "Luis"]
for alumno in alumnos:
    for letra in alumno:
        print(letra, end=" ")
    print()
# A n a
# L u i s
```

#### Resumen: formas de `for`

| Quiero recorrer… | Se escribe | La variable vale… |
|---|---|---|
| Números de 0 a n − 1 | `for i in range(n):` | 0, 1, 2… |
| Números entre dos valores | `for i in range(1, 11):` | 1, 2, …, 10 |
| Números de x en x | `for i in range(0, 20, 5):` | 0, 5, 10, 15 |
| Las letras de un texto | `for letra in palabra:` | cada carácter |
| Los elementos de una lista | `for nota in notas:` | cada elemento, sea número o texto |
| Las posiciones de una lista | `for i in range(len(notas)):` | 0, 1, 2… |
| Posición y elemento a la vez | `for i, nota in enumerate(notas):` | `i` la posición, `nota` el elemento |
| Dos listas a la vez | `for dia, temp in zip(dias, temps):` | un elemento de cada lista |
| Al revés | `for letra in reversed(palabra):` | del último al primero |

---

## 6. Sentencias de salto: `break` y `continue`

Sirven dentro de `while` y de `for`.

| Sentencia | Qué hace |
|---|---|
| `break` | **Sale del bucle** inmediatamente. El programa sigue en la primera línea de después del bucle. |
| `continue` | **Salta el resto de esta vuelta** y pasa a la siguiente. |

```python
# break: busca el primer múltiplo de 7 entre 50 y 100
for numero in range(50, 101):
    if numero % 7 == 0:
        print(f"El primero es {numero}")
        break
```

```python
# continue: muestra los números del 1 al 10 menos los múltiplos de 3
for numero in range(1, 11):
    if numero % 3 == 0:
        continue
    print(numero)
```

Úsenlos con cuidado: un bucle con muchos `break` y `continue` cuesta de seguir. Si la condición del `while` puede expresar cuándo parar, mejor.

---

## 7. ¿`while` o `for`?

| Uso | Estructura | Ejemplo |
|---|---|---|
| Sabemos cuántas veces se repite | `for` con `range` | Mostrar la tabla del 7, pedir 5 notas |
| Depende de lo que pase durante el programa | `while` | Pedir el PIN hasta que sea correcto, leer números hasta un 0 |

Todo lo que se hace con `for` se puede hacer con `while`, pero `for` es más corto y evita olvidarse de actualizar el contador:

```python
# Con while
i = 1
while i <= 10:
    print(i)
    i += 1

# Con for
for i in range(1, 11):
    print(i)
```

---

## 8. Del pseudocódigo a Python

| Pseudocódigo | Python |
|---|---|
| `Si condición Entonces … FinSi` | `if condición:` |
| `SiNo` | `else:` |
| `SiNo Si …` (Si anidados) | `elif condición:` |
| `Segun variable Hacer` | `match variable:` |
| `1:` | `case 1:` |
| `De Otro Modo:` | `case _:` |
| `Mientras condición Hacer … FinMientras` | `while condición:` |
| `Repetir … Hasta Que condición` | `while True:` … `if condición: break` |
| `Para i <- 1 Hasta 10 Hacer … FinPara` | `for i in range(1, 11):` |
| `Para i <- 10 Hasta 1 Con Paso -1` | `for i in range(10, 0, -1):` |
| `FinSi`, `FinMientras`, `FinPara`, `FinSegun` | No existen: el bloque termina con la sangría |
