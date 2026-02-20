Separate function bodies for different patterns.

```haskell
lucky :: (Integral a) => a -> String  
lucky 7 = "LUCKY NUMBER SEVEN!"  
lucky x = "Sorry, you're out of luck, pal!"
```
 The patterns will be checked from top to bottom, and the corresponding function body will be used when it conforms to a pattern.
 
```haskell
sayMe :: (Integral a) => a -> String  
sayMe 1 = "One!"  
sayMe 2 = "Two!"  
sayMe 3 = "Three!"  
sayMe 4 = "Four!"  
sayMe 5 = "Five!"  
sayMe x = "Not between 1 and 5"
```
Prevent a convoluted if-then-else tree with pattern matching.

```haskell
factorial :: (Integral a) => a -> a
factorial 0 = 1
factorial n = n * factorial (n - 1)
```
Recursively define a function.

```haskell
charName :: Char -> String  
charName 'a' = "Albert"  
charName 'b' = "Broseph"  
charName 'c' = "Cecil"
```
```haskell
ghci> charName 'a'  
"Albert"  
ghci> charName 'b'  
"Broseph"  
ghci> charName 'h'  
"*** Exception: tut.hs:(53,0)-(55,21): Non-exhaustive patterns in function charName
```
Always include a catch-all pattern so the program does not crash if we get some unexpected input.

```haskell
addVectors :: (Num a) => (a, a) -> (a, a) -> (a, a)
addVectors a b = (fst a + fst b, snd a + snd b)
```
A better way (Using pattern matching):
```haskell
addVectors :: (Num a) => (a, a) -> (a, a) -> (a, a)  
addVectors (x1, y1) (x2, y2) = (x1 + x2, y1 + y2)
```
Easier to read and prevent functions like `fst` and `snd`.

```haskell
first :: (a, b, c) -> a  
first (x, _, _) = x  

second :: (a, b, c) -> b  
second (_, y, _) = y  

third :: (a, b, c) -> c  
third (_, _, z) = z
```
`_` means we don't care what that part is.
# Pattern matching in lists
```haskell
ghci> let xs = [(1,3), (4,3), (2,4), (5,3), (5,6), (3,1)]  
ghci> [a+b | (a,b) <- xs]  
[4,7,6,8,11,4]
```

## `x:xs` pattern
```haskell
head' :: [a] -> a  
head' [] = error "Can't call head on an empty list, dummy!"  
head' (x:_) = x
```
`error` function: Take a string and generate a runtime error.

```haskell
tell :: (Show a) => [a] -> String  
tell [] = "The list is empty"  
tell (x:[]) = "The list has one element: " ++ show x  
tell (x:y:[]) = "The list has two elements: " ++ show x ++ " and " ++ show y  
tell (x:y:_) = "This list is long. The first two elements are: " ++ show x ++ " and " ++ show y
```
Note that `(x:[])` and `(x:y:[])` could be rewritten as `[x]` and `[x,y]`, but `(x:y:_)` cannot be rewritten.
## patterns
```haskell
capital :: String -> String
capital "" = "Empty string, whoops!"
capital all@(x:xs) = "The first letter of " ++ all ++ " is " ++ [x]
```
```haskell
ghci> capital "Dracula"  
"The first letter of Dracula is D"
```