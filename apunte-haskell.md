# Apunte: primeros pasos en Haskell

- [Apunte: primeros pasos en Haskell](#apunte-primeros-pasos-en-haskell)
- [Introducción](#introducción)
- [Herramientas para desarrollar](#herramientas-para-desarrollar)
  - [Instalación de un editor de texto](#instalación-de-un-editor-de-texto)
  - [Instalación de un intérprete de Haskell](#instalación-de-un-intérprete-de-haskell)
- [Lenguaje Haskell](#lenguaje-haskell)
  - [Tipos de datos básicos](#tipos-de-datos-básicos)
  - [Operaciones sobre tipos de datos básicos](#operaciones-sobre-tipos-de-datos-básicos)
    - [Operaciones sobre Int](#operaciones-sobre-int)
    - [Operaciones sobre Bool](#operaciones-sobre-bool)
    - [Operaciones sobre Char y String](#operaciones-sobre-char-y-string)
    - [Operaciones genéricas de comparación](#operaciones-genéricas-de-comparación)
  - [Estructuras de datos básicas](#estructuras-de-datos-básicas)
    - [Operaciones sobre tuplas](#operaciones-sobre-tuplas)
    - [Operaciones sobre listas](#operaciones-sobre-listas)
      - [Operaciones que generan listas](#operaciones-que-generan-listas)
      - [Operaciones inspectoras sobre listas](#operaciones-inspectoras-sobre-listas)
      - [Operaciones adicionales sobre listas](#operaciones-adicionales-sobre-listas)
  - [Definiciones de constantes y funciones](#definiciones-de-constantes-y-funciones)
    - [Declaraciones de tipos de definiciones](#declaraciones-de-tipos-de-definiciones)
    - [Alternativa condicional](#alternativa-condicional)
- [Preguntas frecuentes](#preguntas-frecuentes)
  - [¿Cómo puedo seguir la ejecución de un programa?](#cómo-puedo-seguir-la-ejecución-de-un-programa)
  - [Comparado con otros lenguajes de programación a los que estoy acostumbrado (como Javascript, Python, Java, Gobstones, etc.), ¿Por qué en Haskell los paréntesis se utilizan de forma diferente?](#comparado-con-otros-lenguajes-de-programación-a-los-que-estoy-acostumbrado-como-javascript-python-java-gobstones-etc-por-qué-en-haskell-los-paréntesis-se-utilizan-de-forma-diferente)

# Introducción

Haskell es un lenguaje de programación funcional. Su principal característica radica en que los programas están constituidos de una serie de definiciones de constantes y funciones, y la ejecución de un programa consistente simplemente de evaluar una expresión.

En esta materia utilizaremos Haskell durante la primera parte.

# Herramientas para desarrollar

## Instalación de un editor de texto

Antes de arrancar a programar, tendrás que contar con un editor de texto moderno. Recomendamos [VSCode](https://code.visualstudio.com/) o [Sublime Text](https://www.sublimetext.com/).

## Instalación de un intérprete de Haskell

Para poder evaluar programas Haskell utilizaremos un
[intérprete](https://es.wikipedia.org/wiki/Int%C3%A9rprete_(inform%C3%A1tica)). En esta materia recomendamos usar [WinHugs](https://www.haskell.org/hugs/downloads/2006-05/WinHugs-May2006.exe) (en Windows), o [Hugs](https://howtoinstall.co/es/ubuntu/xenial/hugs) (en Linux). En el caso de Windows, recomendamos *ejecutar como administrador* el instalador de WinHugs.

Si tenés Mac, o alguna distribución de Linux que no ofrece Hugs, te recomendamos utilizar GHCi, pero vía [stack](https://docs.haskellstack.org/en/stable/README/). Una vez instalada esa herramienta, podés cargar desde la consola un programa mediante el comando `stack ghci <archivo>`.

# Lenguaje Haskell

## Tipos de datos básicos

En esta materia utilizaremos frecuentemente los siguientes tipos básicos de Haskell:
- **Int**, que representa a los números enteros, como `1`, `-1`, `2`, `0`, `5`, etc.
- **Bool**, que representa los valores de verdad. Sus posibles valores son `True` y `False`.
- **String**, que representa cadenas de caracteres, y se escriben entre comillas dobles. Ejemplo: `"hola"`, `"auto"`, `"casa"`.
- **Char**, que representa a los caracteres individuales, y se escriben entre comillas simples. Ejemplo: `'a'`, `'b'`, `'c'`, etc. Como veremos más adelante, los **String** son listas de **Char**.

Cabe destacar que existen otros tipos (como `Float`, que representa números racionales), pero que no vamos a utilizar.

## Operaciones sobre tipos de datos básicos

Los tipos básicos cuentan con operaciones ya definidas. A continuación enumeramos las que utilizaremos en la materia.

### Operaciones sobre Int

Para los números enteros contamos con las operaciones `+` (suma), `-` (resta), `*` (multiplicación) y `div` (división entera).

Ejemplos:
```
Hugs> 1 + 1
2
Hugs> 2 * 3
6
Hugs> 6 - 5
1
Hugs> div 10 2
5
```

### Operaciones sobre Bool

Para los booleanos contamos con las operaciones `&&` (conjunción), `||` (disyunción) y `not` (negación).

```
Hugs> True && False
False
Hugs> False || True
True
Hugs> not True
False
Hugs> not (True || True)
False
```

### Operaciones sobre Char y String

Las únicas operaciones interesantes sobre `Char` son `succ` y `pred`, que, siguiendo un orden basado en [ASCII](https://elcodigoascii.com.ar/), nos dan el siguiente o anterior `Char`.

Para `String`, dado que son listas de `Char`, utilizaremos las mismas funciones sobre listas, descritas más adelante.

### Operaciones genéricas de comparación

A todos los tipos ya descritos, podemos aplicarles las operaciones de comparación usuales: `==` (igualdad), `/=` (desigualdad), `<` (menor), `>` (mayor), `<=` (menor o igual), `>=` (mayor o igual).

## Estructuras de datos básicas

Además, utilizaremos dos estructuras de datos que vienen con Haskell:
- **Tuplas**, que usaremos para armar pares entre distintos tipos de expresiones. Ejemplos: `(1,2)`, `("Jorge", 32)`, `(True, 10)`, etc. Notar que *los tipos de las componentes de las tuplas NO son necesariamente iguales*, aunque pueden serlo.
- **Listas**, que utilizaremos para listar una serie de elementos. Ejemplos: `[1,2,3]`, `[True, False]`, `['c','a','s','a']` (que equivale a `"casa"`). Notar que *los elementos que componen una lista deben ser de un mismo tipo* (no podemos formar listas de diferentes tipos de expresiones).

### Operaciones sobre tuplas

Existen solamente dos operaciones posibles `fst` y `snd`.

Ejemplos:
```
Hugs> fst (1, True)
1
Hugs> snd (32, "Jorge")
"Jorge"
```

### Operaciones sobre listas

#### Operaciones que generan listas

La operación principal para generar listas de elementos será `:`, y que llamamos *cons*. Dicha operación toma primero un elemento y luego una lista, y *forma una nueva lista* con dicho elemento agregado al principio.

Ejemplos:
```
Hugs> 10 : [25,30]
[10,25,30]
Hugs> True : []
[True]
Hugs> 1 : 2 : 3 : []
[1,2,3]
Hugs> 'c' : "asa"
"casa"
```

Recordar que en Haskell las operaciones NO pueden modificar las expresiones tomadas por parámetro, dado que son inmutables, por lo que siempre devuelven nuevas expresiones.

Más adelante también veremos que esta operación es de alguna manera especial, y nos ayudará a definir funciones sobre listas.

Por otra parte también contamos con `++`, que llamamos *append*. Dicha operación toma dos listas, y las concatena respetando el orden de los argumentos.

Ejemplos:
```
Hugs> [1,2,3] ++ [4,5,6]
[1,2,3,4,5,6]
Hugs> [True, False] ++ []
[True,False]
Hugs> "ca" ++ "sa"
"casa"
```

#### Operaciones inspectoras sobre listas

Existen otras operaciones que nos devuelven información sobre una lista. Las principales son las siguientes:
- `null`, que dada una lista nos indica si se encuentra vacía
- `head`, que dada una lista nos devuelve su primer elemento
- `tail`, que dada una lista nos retorna la lista sin su primer elemento

Ejemplos:
```
Hugs> null []
True
Hugs> null [1,2,3]
False
Hugs> head [1,2,3]
1
Hugs> tail [1,2,3]
[2,3]
```

#### Operaciones adicionales sobre listas

Existen más operaciones sobre listas que ya vienen con Haskell. Entre éstas, utilizaremos generalmente las siguientes:
- `length`, que toma una lista y devuelve su tamaño.
- `minimum` y `maximum`, que toman listas y nos devuelve el mínimo o máximo elemento respectivamente.
- `last`, que toma una lista y nos devuelve el último elemento
- etc.

## Definiciones de constantes y funciones

Como dijimos anteriormente, el código fuente de un programa Haskell consiste de una **serie de definiciones de constantes y funciones**. La extensión de los archivos debe ser `.hs`.

Por ejemplo, el siguiente puede ser un archivo llamado `main.hs`
```
-- Esta es una función que toma un número y devuelve su siguiente
sucesor :: Int -> Int
sucesor x = x + 1

-- Esta es una función que toma un número y devuelve su doble
doble :: Int -> Int
doble x = x * 2

-- Esta es una función que toma dos números y devuelve el menor
minimo :: Int -> Int -> Int
minimo x y = 
  if x < y
     then x
     else y

-- Esta es una constante, que equivale a 10
diez :: Int
diez = 10
```

Que si cargamos en el intérprete, nos permitirá ejecutar lo siguiente
```
Hugs> minimo (sucesor 20) (doble 2 + diez)
14
```

### Declaraciones de tipos de definiciones

Como podrás observar en el ejemplo anterior, indicamos qué tipo de parámetro aceptamos y qué tipo de expresión devuelve cada función definida.

Por ejemplo, `sucesor` toma un `Int` y devuelve un `Int`. Eso se indica de la siguiente manera `sucesor :: Int -> Int`, antes de comenzar con la definición de la función.

En el caso de la función `minimo`, toma dos `Int` para devolver un `Int`, y por eso anotamos `minimo :: Int -> Int -> Int`. Puede observarse que la cantidad de flechas en esa declaración coincide con la cantidad de parámetros.

### Alternativa condicional

Como también habrás podido notar, en la función `minimo` utilizamos una alternativa condicional.

La forma de la alternativa condicional es la siguiente:
```
if <expresión booleana>
   then <expresión de algún tipo>
   else <expresión del mismo tipo que la rama anterior>
```

Cabe aclarar que en Haskell *la alternativa condicional es una expresión*, por lo que no podemos omitir la rama `else`. En otras palabras, simplemente elije entre una expresión u otra analizando el valor resultante de evaluar una expresión booleana.

# Preguntas frecuentes

## ¿Cómo puedo seguir la ejecución de un programa?

A esta altura habrás notado que el flujo de ejecución de un programa Haskell es ligeramente más abstracto que el de los programas immperativos, dado que simplemente nos importa el valor resultante de evaluar una expresión, y no exactamente cómo dicha expresión fue evaluada.

Si te encontrás necesitando pensar cómo el intérprete evalúa una expresión dada, podés pensar que lo hace como vos cuando necesitás resolver una cuenta matemática. Es decir, utiliza las definiciones dadas para poder reducir lo máximo posible la expresión, y así obtener un valor resultante (algo que ya no puede seguir evaluando).

Siguiente el ejemplo `minimo (sucesor 20) (doble 2 + diez)`, podemos pensar en posibles pasos de evaluación, que no necesariamente son los mismos que hará el intérprete, pero que nos pueden ayudar a razonar cómo llegar a un resultado:

```
minimo (sucesor 20) (doble 2 + diez)
-> (se aplica la definicion de sucesor)
minimo 21 (doble 2 + diez)
-> (se aplica la definición de doble)
minimo 21 (4 + diez)
-> (se aplica la definicion de diez)
minimo 21 (4 + 10)
-> (se realiza una suma)
minimo 21 14
-> (se aplica la definicion de minimo)
14
```

Como podrás observar, podríamos haber elegido otros caminos, y llegado al mismo resultado. Si bien esto no siempre es así, y en programas más complejos existirán caminos que pueden resultar en un error, en esta materia no nos interesará profundizar en este aspecto, y evaluaremos expresiones siguiendo los pasos que más nos convengan.

## Comparado con otros lenguajes de programación a los que estoy acostumbrado (como Javascript, Python, Java, Gobstones, etc.), ¿Por qué en Haskell los paréntesis se utilizan de forma diferente?

Seguramente estés acostumbrado a que los paréntesis se utilizan para agrupar los argumentos de los llamados a funciones, como en Gobstones el caso de `PonerN(10, Rojo)`.

En Haskell los valores se pasan separados por espacios, y los paréntesis se utilizan para agrupar expresiones de la misma forma que en matemática.

Por ejemplo, si tenemos la expresión `1 + 2 * 3`, sabemos que existe una predencia entre los operadores, y que los paréntesis, si los explicitaramos, serían `1 + (2 * 3)`. Si quisiéramos realizar la suma entre 1 y 2, y luego multiplicar, utilizaríamos los paréntesis de esta manera: `(1 + 2) * 3`.

De forma similar, en la expresión `sucesor (doble 20)`, utilizamos paréntesis, no para aplicar un parámetro a `sucesor`, sino para asociar primero la función `doble` con su argumento `20`. Si no hiciéramos esto, y escribiésemos `sucesor doble 20`, Haskell interpretaría que los términos `doble` como `20` son argumento de `sucesor`, informando un error de tipos.