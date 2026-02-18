## Infix functions
Example: multiplication `*`
## Prefix functions
Most of functions
Examples:
```haskell
ghci> succ 8
9
```
The `succ` function takes anything that has a defined successor and returns that successor.

```haskell
ghci> min 9 10  
9  
ghci> max 100 101  
101
```
The functions `min` and `max` take two things that can be put in an order (like integers!). `min` returns the one that’s lesser and `max` returns the one that’s greater.

Functions have highest precedence.
```haskell
ghci> succ 9 + max 5 4 + 1  
16  
ghci> (succ 9) + (max 5 4) + 1  
16
```

If a function takes two parameters, we can also call it as an infix function by surrounding it with backticks.
```haskell
ghci> div 92 10
9
ghci> 92 `div` 10
9
```

The apostrophe `'` does not have any special meaning.
We usually use `'` to either denote a strict version of a function (one that is not lazy) or a slightly modified version of a function or a variable.
```haskell
doubleSmallNumber' x = (if x > 100 then x else x * 2) + 1
```
