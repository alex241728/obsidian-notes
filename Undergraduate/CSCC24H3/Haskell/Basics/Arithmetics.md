## Simple arithmetics
```haskell
ghci> 2 + 15
17
ghci> 49 * 100  
4900  
ghci> 1892 - 1472  
420  
ghci> 5 / 2  
2.5
```
## Usual precedence rules
```haskell
ghci> (50 * 100) - 4999  
1  
ghci> 50 * 100 - 4999  
1  
ghci> 50 * (100 - 4999)  
-244950
```
### Important
```haskell
ghci> 5 * -3
<interactive>:1:1: error:
	Precedence parsing error
	cannot mix ‘*’ [infixl 7] and prefix `-' [infixl 6] in the same infix expression
ghci> 5 * (-3)
-15
```
## Boolean Algebra
```haskell
ghci> True && False  
False  
ghci> True && True  
True  
ghci> False || True  
True  
ghci> not False  
True  
ghci> not (True && True)  
False
```

```haskell
ghci> 5 == 5  
True  
ghci> 1 == 0  
False  
ghci> 5 /= 5  
False  
ghci> 5 /= 4  
True  
ghci> "hello" == "hello"  
True
```
### Important
```haskell
ghci> 5 + "llama"
<interactive>:3:1: error: [GHC-39999]
    ? No instance for ‘Num String’ arising from the literal ‘5’
    ? In the first argument of ‘(+)’, namely ‘5’
      In the expression: 5 + "llama"
      In an equation for ‘it’: it = 5 + "llama"
```
`+` expects its left and right side to be numbers.

```haskell
ghci> 5 == True
<interactive>:4:1: error: [GHC-39999]
    ? No instance for ‘Num Bool’ arising from the literal ‘5’
    ? In the first argument of ‘(==)’, namely ‘5’
      In the expression: 5 == True
      In an equation for ‘it’: it = 5 == True
```
`\==` expects its left and right side to be things that can be compared.
