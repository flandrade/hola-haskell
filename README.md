<a href="https://www.haskell.org">
  <img src="https://github.com/flandrade/hola-haskell/blob/master/img/haskell.png?raw=true" alt="Haskell" align="right"  width="120" />
</a>

# Hola Haskell

Introducción a programación functional con Haskell. Presentación realizada los días 28 y 29 de abril de 2016 en Cuenca, Ecuador. Puedes revisar la presentación [aquí](https://github.com/flandrade/hola-haskell/blob/master/slides.pdf).

## Temas

- Haskell es funcional.
- Haskell es puro.
  - Inmutabilidad.
  - Sin efectos secundarios.
  - Transparencia referencial.
- Evaluación perezosa.
- Tipificación estática.
- Funciones de orden superior.

## Hola, Haskell

```haskell
holaHaskell :: IO ()
holaHaskell = putStrLn "Hola, Haskell"
```

## Haskell es funcional 

### Haskell es funcional, no es imperatvo.

Factorial en C: 

```c 
int factorial(int n) {
  int result = 1;
  for (int i = 1; i <= n; ++i)
    result *= i;
  return result;
```

Factorial en Haskell: 

```haskell
factorial :: Int -> Int
factorial 0 = 1
factorial n = n * factorial (n-1)
````

### Evaluación de expresiones

```c
int sum(int n){
	int result = 0;
	for(int i=1; i<=n; i++)
	  result += i
	return result
}
```

Sumar números de 1 a n en Haskell:

```haskell
sum [1.. n]
```

## Haskell es puro

### Inmutabilidad

En Haskell: 

```
x :: Int
x = 5

suma :: Int -> Int
suma n = n + x

x = 0

```

Error: 

```
    Multiple declarations of 'x'
    Declared at: suma.hs:2:1
                 suma.hs:7:1
Failed, modules loaded: none.
```

### Haskell no tiene efectos secundarios

En Haskell: 

```haskell
count :: [a] -> Int
```

- Funciones sólo pueden calcular y retornar valores. 
- Funciones garantizan integridad.

### Transparencia referencial

En C: 

```c 
int global = 5;

int suma (int n){
  return (n + global);
}

int main(){
  int resultado;
  
  // resultado = 6
  resultado = suma(1); 
  
  global = 0;
  
  // resultado = 1
  resultado = suma(1); 

}
``` 

En Haskell: 

```haskell
x :: Int
x = 5

suma :: Int -> Int
suma n = n + x
```

Resultado: 
```
> suma 1
6
> suma 1
6
```

- Si una función es llamada dos veces con los mismos parámetros, obtendremos siempre el mismo resultado.

## Evaluación perezosa

En Haskell: 

```haskell
square :: Int -> Int
square x = x * x
```

Resultado:
```
> square (1 + 2)
=> (1 + 2) * (1 + 2)
=> 3 * (1+2)
=> 3 * 3
=> 9
```

- Haskell no calculará resultados hasta que se vea realmente forzado a hacerlo. 

Primeros 5 números de una lista infinita: 

```
> take 5 [1..]
[1,2,3,4,5]
```

-  Es posible trabajar con estructura de datos infinitos. 

## Tipificado estáticamente 

Haskell es un lenguaje tipificado estáticamente.

```
> printString 5
```

Resultado: 

```
<interactive>:18:13:
No instance for (Num String) arising from the literal '5'
In the first argument of 'printString', namely '5'
In the expression: printString 5
In an equation for 'i'’: it = printString 5
```

- Haskell verifica que el tipo de dato declarado coincide con el tipo inferido (en tiempo de compilación). 

## Funciones de orden superior

Funciones pueden tomar funciones como parámetros y devolver funciones como resultado.

### Función `map`

```haskell
map :: (a -> b) -> [a] -> [b]
map _ [] = []
map f (x:xs) = f x : map f xs
``` 

Resultado: 

```
> map (+3) [0,1,2,3,4,5]
[3,4,5,6,7,8]
```

### Función `filter`

```haskell
filter :: (a -> Bool) -> [a] -> [a]
filter _ [] = []
filter p (x:xs)
    | p x       = x : filter p xs
    | otherwise = filter p xs
```

Resultado: 

```
> filter even [1,2,3,4,5,6]
[2,4,6]
> filter (>3) [1,2,3,4,5,6]
[4,5,6]
```

## Bibliografía 

- Lipovača, Miran. [Learn You a Haskell for Great Good!](http://learnyouahaskell.com/)
- Allen, Christopher and Moronuki, Julie. [Haskell programming from first principles](http://haskellbook.com/index.html).

## Licencia
MIT

