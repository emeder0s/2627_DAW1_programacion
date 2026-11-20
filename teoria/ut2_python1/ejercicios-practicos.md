# Ejercicios prácticos de Python

## Normas

- **Sin IA y sin copiar código.** Piensen ustedes la solución: pueden hacer antes el pseudocódigo o pensarla directamente en Python.
- **La salida tiene que ser exactamente igual que la del ejemplo:** los mismos mensajes, escritos igual y en el mismo orden. En los ejemplos, lo que escribe el usuario va justo después de cada pregunta.
- **Un archivo por ejercicio**, con nombres en `snake_case`: `ejercicio_01.py`, `ejercicio_02.py`…
- Cuando un ejercicio dice que **no se puede usar** una función, no vale usarla.
- Prueben cada programa con los datos del ejemplo **y con otros distintos**, sobre todo con los casos límite.

---

## Bloque 1. Decisiones con varias condiciones

### Ejercicio 1. Días del mes

Pide un mes (del 1 al 12) y un año, y muestra cuántos días tiene ese mes. Febrero tiene 29 días si el año es bisiesto y 28 si no lo es.

Un año es **bisiesto** si es divisible entre 4 y no entre 100, o si es divisible entre 400. Por ejemplo, 2024 y 2000 son bisiestos, pero 1900 no.

Si el mes no está entre 1 y 12, muestra `Mes no válido`.

```
Mes (1-12): 2
Año: 2024
El mes 2 de 2024 tiene 29 días
```

```
Mes (1-12): 2
Año: 1900
El mes 2 de 1900 tiene 28 días
```

---

### Ejercicio 2. ¿Es un triángulo?

Pide la longitud de tres lados y di si pueden formar un triángulo. Si pueden, di de qué tipo es:

- **Equilátero:** los tres lados son iguales.
- **Isósceles:** dos lados son iguales.
- **Escaleno:** los tres lados son distintos.

Tres lados forman un triángulo solo si **cada lado es menor que la suma de los otros dos**.

```
Lado 1: 3
Lado 2: 4
Lado 3: 5
Forman un triángulo escaleno
```

```
Lado 1: 1
Lado 2: 2
Lado 3: 5
No forman un triángulo
```

---

### Ejercicio 3. Ordenar tres números

Pide tres números enteros y muéstralos ordenados de menor a mayor.

**No se puede usar** `max`, `min` ni `sorted`.

```
Primer número: 7
Segundo número: 2
Tercer número: 5
Ordenados: 2, 5, 7
```

---

### Ejercicio 4. El parking

Un parking cobra así:

- La **primera hora**, o menos, cuesta **2 €**.
- A partir de ahí, cada **media hora** cuesta **0,80 €**. Una media hora empezada se cobra entera: 10 minutos se cobran como media hora.
- Como **máximo** se pagan **15 €**.

Pide la hora y los minutos de entrada y de salida (del mismo día), y muestra cuánto tiempo ha estado el coche y cuánto hay que pagar, con dos decimales.

```
Hora de entrada: 9
Minutos de entrada: 15
Hora de salida: 11
Minutos de salida: 50
Tiempo: 2 h 35 min
A pagar: 5.20 €
```

```
Hora de entrada: 8
Minutos de entrada: 0
Hora de salida: 20
Minutos de salida: 0
Tiempo: 12 h 0 min
A pagar: 15.00 €
```

---

### Ejercicio 5. Sumar tiempo a un reloj

Pide una hora (horas, minutos y segundos) y una cantidad de segundos que sumar, y muestra la hora resultante en formato `hh:mm:ss`. Si se pasa de las 23:59:59, el reloj vuelve a empezar desde las 00:00:00.

**Pista:** en una f-string, `{numero:02d}` muestra el número con dos cifras, con un cero delante si hace falta: `7` se muestra como `07`.

```
Horas: 23
Minutos: 59
Segundos: 30
Segundos que sumar: 45
Nueva hora: 00:00:15
```

---

## Bloque 2. Bucles

### Ejercicio 6. Las cifras de un número

Pide un número entero positivo y muestra cuántas cifras tiene, cuánto suman sus cifras y cuál es la cifra mayor.

**No se puede usar** `str` ni `len`: hay que sacar las cifras con `//` y `%`.

**Pista:** `n % 10` es la última cifra de `n`, y `n // 10` es el número sin esa última cifra.

```
Número: 40725
Tiene 5 cifras
Suman 18
La mayor es 7
```

---

### Ejercicio 7. Tabla de temperaturas

Pide un valor inicial, un valor final y un paso, y muestra una tabla con la conversión de grados Celsius a Fahrenheit. El valor final se incluye.

La fórmula es: **F = C × 9 / 5 + 32**.

Las columnas tienen que quedar alineadas a la derecha: la de Celsius ocupa 5 caracteres y la de Fahrenheit, 8, con un decimal.

**Pista:** en una f-string, `{valor:>5}` ocupa 5 caracteres alineado a la derecha, y `{valor:>8.1f}` ocupa 8 caracteres con un decimal.

```
Desde: 0
Hasta: 40
Paso: 10
   °C      °F
    0    32.0
   10    50.0
   20    68.0
   30    86.0
   40   104.0
```

---

### Ejercicio 8. ¿Es primo?

Un número es **primo** si es mayor que 1 y solo se puede dividir exactamente entre 1 y entre sí mismo. Por ejemplo, 7 es primo, pero 21 no, porque se puede dividir entre 3 y entre 7.

**Parte 1.** Pide un número y di si es primo.

**Parte 2.** Después, muestra todos los números primos desde 2 hasta ese número.

```
Número: 29
29 es primo
Primos hasta 29: 2 3 5 7 11 13 17 19 23 29
```

```
Número: 21
21 no es primo
Primos hasta 21: 2 3 5 7 11 13 17 19
```

---

### Ejercicio 9. De decimal a binario

Pide un número entero positivo y muéstralo en binario.

**No se puede usar** `bin`.

**Cómo se pasa a binario:** se divide el número entre 2 y se apunta el resto; luego se divide el cociente entre 2 y se apunta el resto; y así hasta que el cociente sea 0. El número en binario son los restos **leídos al revés**, del último al primero.

```
13 ÷ 2 = 6, resto 1
 6 ÷ 2 = 3, resto 0
 3 ÷ 2 = 1, resto 1
 1 ÷ 2 = 0, resto 1      →  13 en binario es 1101
```

```
Número: 13
13 en binario es 1101
```

---

### Ejercicio 10. La conjetura de Collatz

Pide un número entero positivo y aplícale estas reglas una y otra vez hasta llegar a 1:

- Si el número es **par**, se divide entre 2.
- Si es **impar**, se multiplica por 3 y se le suma 1.

Muestra todos los números de la secuencia en una línea y, al final, cuántos pasos han hecho falta.

Nadie ha conseguido demostrar que con cualquier número se llega siempre a 1, pero se ha comprobado con todos los números que se han probado.

```
Número: 6
6 3 10 5 16 8 4 2 1
Pasos: 8
```

---

### Ejercicio 11. Figuras con asteriscos

Pide una altura y dibuja estas tres figuras. Háganlas en orden: no pasen a la siguiente hasta que la anterior funcione.

```
Altura: 4
Triángulo:
*
**
***
****
Pirámide:
   *
  ***
 *****
*******
Rombo:
   *
  ***
 *****
*******
 *****
  ***
   *
```

Fíjense en cuántos espacios y cuántos asteriscos hay en cada fila de la pirámide, y busquen la relación con el número de fila.

---

## Bloque 3. Retos

Para que el ordenador elija un número al azar, se usan estas dos líneas:

```python
import random
numero = random.randint(1, 100)     # un número entero entre 1 y 100, los dos incluidos
```

`import random` va **al principio** del programa.

### Ejercicio 12. Adivina el número

El ordenador piensa un número del 1 al 100 y el jugador tiene **7 intentos** para adivinarlo. Después de cada intento fallido, el programa dice si el número secreto es mayor o menor. Al final, dice si ha acertado y en cuántos intentos o, si ha perdido, cuál era el número.

**Consejo:** mientras lo prueban, pongan un número fijo, por ejemplo `secreto = 65`, para saber si el programa responde bien. Cuando funcione, cámbienlo por el número al azar.

```
Intento 1: 50
Es mayor
Intento 2: 75
Es menor
Intento 3: 62
Es mayor
Intento 4: 68
Es menor
Intento 5: 65
¡Acertaste en 5 intentos!
```

Si se gastan los 7 intentos sin acertar, la última línea es:

```
Has perdido. El número era 65
```

---

### Ejercicio 13. Carrera de dados

Dos jugadores tiran un dado por turnos. Cada uno suma los puntos que saca, pero **si sale un 1, pierde todos sus puntos** y vuelve a 0. Gana el primero que llegue a **20 puntos o más**.

Antes de cada tirada, el programa espera a que el jugador pulse Intro. Para eso se puede usar `input` sin guardar lo que devuelve.

Como el dado es al azar, la partida siempre será distinta, pero los mensajes tienen que ser como estos:

```
Jugador 1, pulsa Intro para tirar
Sale un 6. Jugador 1: 6 puntos
Jugador 2, pulsa Intro para tirar
Sale un 4. Jugador 2: 4 puntos
Jugador 1, pulsa Intro para tirar
Sale un 1. Jugador 1: 0 puntos
Jugador 2, pulsa Intro para tirar
Sale un 6. Jugador 2: 10 puntos
Jugador 1, pulsa Intro para tirar
Sale un 5. Jugador 1: 5 puntos
Jugador 2, pulsa Intro para tirar
Sale un 5. Jugador 2: 15 puntos
Jugador 1, pulsa Intro para tirar
Sale un 3. Jugador 1: 8 puntos
Jugador 2, pulsa Intro para tirar
Sale un 6. Jugador 2: 21 puntos
¡Gana el jugador 2!
```

---

### Ejercicio 14. Conversor de unidades

Muestra un menú y repítelo hasta que el usuario elija salir:

- **1:** kilómetros a millas (1 km = 0.621371 millas).
- **2:** millas a kilómetros.
- **3:** grados Celsius a Fahrenheit (F = C × 9 / 5 + 32).
- **0:** salir.

Las distancias se muestran con dos decimales y la temperatura con uno. Si se escribe una distancia negativa, muestra `La distancia no puede ser negativa`. Si la opción no existe, muestra `Opción no válida`.

Usen `match` para el menú.

```
1. Kilómetros a millas
2. Millas a kilómetros
3. Celsius a Fahrenheit
0. Salir
Opción: 1
Kilómetros: 10
10.0 km son 6.21 millas
1. Kilómetros a millas
2. Millas a kilómetros
3. Celsius a Fahrenheit
0. Salir
Opción: 5
Opción no válida
1. Kilómetros a millas
2. Millas a kilómetros
3. Celsius a Fahrenheit
0. Salir
Opción: 0
¡Hasta luego!
```

---

### Ejercicio 15. El número de la suerte

Pide una fecha de nacimiento en formato `dd/mm/aaaa` y calcula el **número de la suerte**: se suman todas las cifras de la fecha y, si el resultado tiene más de una cifra, se vuelven a sumar sus cifras, y así hasta que quede una sola. Muestra cada suma.

La fecha se lee como texto: hay que recorrerla carácter a carácter, saltarse las barras y convertir cada cifra a número.

```
Fecha de nacimiento (dd/mm/aaaa): 15/08/2004
1+5+0+8+2+0+0+4 = 20
2+0 = 2
Tu número de la suerte es 2
```

```
Fecha de nacimiento (dd/mm/aaaa): 29/12/1999
2+9+1+2+1+9+9+9 = 42
4+2 = 6
Tu número de la suerte es 6
```
