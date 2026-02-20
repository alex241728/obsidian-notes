- In Haskell, every function officially takes only one parameter.
- Functions that appear to take multiple parameters are actually **curried functions**.
	- How it works: When you call `max 4 5`, Haskell first creates a function that takes one parameter and returns either `4` or that parameter (whichever is larger). Then, `5` is applied to that new function to get the result.
	- Equivalent to `(max 4) 5`.
	- Type Signatures: The arrows in type signatures are right-associative.
		- `max :: (Ord a) => a -> a -> a` is actually `max :: (Ord a) => a -> (a -> a)`.
		- This means `max` takes an `a` and returns a function of type `a -> a`.

Calling a function with "too few" arguments does not result in an error; Instead, it returns a partially applied function.
```haskell
multThree :: (Num a) => a -> a -> a -> a  
multThree x y z = x * y * z
```
```haskell
ghci> let multTwoWithNine = multThree 9  
ghci> multTwoWithNine 2 3  
54  
ghci> let multWithEighteen = multTwoWithNine 2  
ghci> multWithEighteen 10  
180
```
This applies to infix functions
```haskell
divideByTen :: (Floating a) => a -> a  
divideByTen = (/10)
```
```haskell
isUpperAlphanum :: Char -> Bool  
isUpperAlphanum = (`elem` ['A'..'Z'])
```



