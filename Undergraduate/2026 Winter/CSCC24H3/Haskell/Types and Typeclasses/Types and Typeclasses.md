# Types
- Haskell has a static type system: The type of every expression is known at compile time -> safer code.
- Type inference

`:t` command: examine the types of expressions
```haskell
ghci> :t 'a'  
'a' :: Char  
ghci> :t True  
True :: Bool  
ghci> :t "HELLO!"  
"HELLO!" :: [Char]  
ghci> :t (True, 'a')  
(True, 'a') :: (Bool, Char)  
ghci> :t 4 == 5  
4 == 5 :: Bool
```
\[Char\] denotes a list of characters. (List elements can have only one type.)
(Bool, Char) denotes a tuple. (Tuple elements can have multiple types)

```haskell
removeNonUppercase :: [Char] -> [Char]  
removeNonUppercase st = [ c | c <- st, c `elem` ['A'..'Z']]
```
Functions have types
Explicit type declaration: This is a good practice except writing very short functions.
Note: It's clearer to write `removeNonUppercase :: String -> String` since `[Char]` is synonymous with `String`.

```haskell
addThree :: Int -> Int -> Int -> Int  
addThree x y z = x + y + z
```
`->` has no special distinction between the parameters and the return type: The return type is the last item in the declaration, and the parameters are the first three.
## Common types
## `Int`
Stands for integer (whole number)
Range: $[-2147483648, 2147483647]$
## `Integer`
Stands for integer but is not bounded.
`Int` is more efficient than `Integer`.
## `Float`
A real floating point with single precision
## `Double`
A real floating point with double the precision
## `Bool`
A boolean type: Have only two values `True` and `False`.
## `Char`
Represents a character. 
Denoted by single quotes.
A list of characters is a string.
## Type variables
```haskell
ghci> :t head  
head :: [a] -> a
ghci> :t fst
fst :: (a, b) -> a
```
This means `a` can be any type. (like generics)
Functions that have type variables are called **polymorphic functions**.
Usually give them names of a, b, c, d, ...
# Typeclasses 101
A typeclass is a sort of interface that defines some behavior. If a type is a part of a typeclass, that means that it supports and implements the behavior the typeclass describes.

```haskell
ghci> :t (==)  
(==) :: (Eq a) => a -> a -> Bool
```
The equality function takes any two values that are of the same type and returns a `Bool`. The type of those two values must be a member of the `Eq` class (this was the class constraint).

Everything before the `=>` symbol is called a **class constraint**.
## Basic typeclasses
### `Eq`
Used for types that support equality testing.
The functions its members implement are `==` and `/=`.
```haskell
ghci> 5 == 5  
True  
ghci> 5 /= 5  
False  
ghci> 'a' == 'a'  
True  
ghci> "Ho Ho" == "Ho Ho"  
True  
ghci> 3.432 == 3.432  
True
```
### `Ord`
Used for types that have an ordering.

```haskell
ghci> :t (>)  
(>) :: (Ord a) => a -> a -> Bool
```
`Ord` covers all the standard comparing functions such as `>`, `<`, `>=`, and `<=`.

```haskell
ghci> "Abrakadabra" < "Zebra"  
True  
ghci> "Abrakadabra" `compare` "Zebra"  
LT  
ghci> 5 >= 2  
True  
ghci> 5 `compare` 3  
GT
```
The `compare` function takes two `Ord` members of the same type and returns an ordering. `Ordering` is a type that can be `GT`, `LT`, or `EQ`, meaning greater than, lesser than, and equal, respectively.
### Show
Can be presented as strings.
All types covered so far except for functions are parts of `Show`.
```haskell
ghci> show 3  
"3"  
ghci> show 5.334  
"5.334"  
ghci> show True  
"True"
```
### Read
The opposite typeclass of `Show`
The `read` function takes a string and returns a type which is a member of `Read`.
```haskell
ghci> read "True" || False  
True  
ghci> read "8.2" + 3.8  
12.0  
ghci> read "5" - 2  
3  
ghci> read "[1,2,3,4]" ++ [3]  
[1,2,3,4,3]
```

```haskell
ghci> read "4"  
<interactive>:1:0:  
	Ambiguous type variable `a' in the constraint:  
    `Read a' arising from a use of `read' at <interactive>:1:0-7  
    Probable fix: add a type signature that fixes these type variable(s)
```
GHCI does not know exactly which type in the `Read` class.
Need to use explicit annotations:
```haskell
ghci> read "5" :: Int  
5  
ghci> read "5" :: Float  
5.0  
ghci> (read "5" :: Float) * 4  
20.0  
ghci> read "[1,2,3,4]" :: [Int]  
[1,2,3,4]  
ghci> read "(3, 'a')" :: (Int, Char)  
(3, 'a')
```
### Enum
Sequentially ordered types (Can be enumerated)
Have defined successors and predecessors. (Get with the `succ` and `pred` functions.)
Types in the class: `()`, `Bool`, `Char`, `Ordering`, `Int`, `Integer`, `Float` and `Double`.
### Bounded
Have an upper and a lower bound.
Use `minBound` and `maxBound` to get lower and upper bounds.
```haskell
ghci> minBound :: Int  
-2147483648  
ghci> maxBound :: Char  
'\1114111'  
ghci> maxBound :: Bool  
True  
ghci> minBound :: Bool  
False
```
### Num
Includes real numbers and integral numbers.
### Integral
Includes only integral (whole) numbers: `Int` and `Integer`.
### Floating
Includes only floating point numbers: `Float` and `Double`.