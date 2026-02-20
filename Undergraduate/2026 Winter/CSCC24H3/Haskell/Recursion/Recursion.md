# Recursion
- A way of defining functions in which the function is applied inside its own definition.
- Base case & Recursive step
- Pattern matching goes great with recursion.

```haskell
maximum' :: (Ord a) => [a] -> a
maximum' [] = error "maximum of empty of list"
maximum' [x] = x
maximum' (x:xs) 
	| x > maxTail = x
	| otherwise = maxTail
	where maxTail = maximum xs
```

With function `max`
```haskell
maximum' :: (Ord a) => [a] -> a
maximum' [] = error "maximum of empty of list"
maximum' [x] = x
maximum' (x:xs) = max x (maximum' xs)
```
## A few more recursive functions
```haskell
replicate' :: (Num i, Ord i) => i -> a -> [a]
replicate' n x
	| n <= 0 = []
	| otherwise = x : (replicate' (n-1) x)
```

```haskell
take' :: (Num i, Ord i) => i -> [a] -> [a]  
take' n _  
	| n <= 0   = []  
take' _ []     = []  
take' n (x:xs) = x : take' (n-1) xs
```

```haskell
reverse' :: [a] -> [a]
reverse' [] = []
reverse' (x:xs) = reverse' xs ++ x
```

```haskell
repeat' :: a -> [a]
repeat' x = x : repeat' x
```

```haskell
zip' :: [a] -> [b] -> [(a,b)]
zip' [] _ = []
zip' _ [] = []
zip' (x:xs) (y:ys) = (x,y) : zip' xs ys
```

```haskell
elem' :: a -> [a] -> Bool
elem' a [] = False
elem' a (x:xs)
	| a == x = True
	| otherwise = elem' a xs
```

```haskell
qSort :: (Ord a) => [a] -> [a]
qSort [] = []
qSort (x:xs) =
	let smallerSorted = qSort [a | a <- xs, a <= x]
		biggerSorted = qSort [a | a <- xs, a > x]
	in smallerSorted ++ [x] ++ biggerSorted
```
```haskell
qSort :: (Ord a) => [a] -> [a]
qSort [] = []
qSort (x:xs) = smallerSorted ++ [x] ++ biggerSorted
	where smallerSorted = qSort [a | a <- xs, a <= x]
		  biggerSorted = qSort [a | a <- xs, a > x]
```
# Tail Recursion
```haskell
maximum' :: (Ord a) => [a] -> a
maximum' [] = error "maximum of empty of list"
maximum' (x:xs) = max_tail xs x
	where max_tail [] acc = acc
		  max_tail (y:ys) acc = max_tail ys (if y > acc then y else acc)
```

```haskell
replicate' :: (Num i, Ord i) => i -> a -> [a]
replicate' n x 
	| n <= 0 = []
	| otherwise = replicateTail n []
		where replicateTail 0 acc = acc
			  replicateTail n acc = replicateTail (n-1) x (x:acc)
```

```haskell
take' :: (Num i, Ord i) => i -> [a] -> [a]
take' n x
	| n <= 0 = []
	| null x = []
	| otherwise = reverse (takeTail n x [])
		where takeTail 0 _ acc = acc
			  takeTail _ [] acc = acc
			  takeTail k (y:ys) acc = takeTail (k-1) ys (y:acc)
```
# Continuation-passing-style (CPS) recursion
```haskell
reverse' :: [a] -> [a]
reverse' x = revCPS x id
	where revCPS [] k = k []
	      revCPS (y:ys) k = revCPS ys (\v -> k (y:v))
```
