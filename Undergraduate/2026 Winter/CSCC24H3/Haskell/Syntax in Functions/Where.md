```haskell
densityTell :: (RealFloat a) => a -> a -> String  
densityTell mass volume  
    | mass / volume < 1.2 = "Wow! You're going for a ride in the sky!" 
    | mass / volume <= 1000.0 = "Have fun swimming, but watch out for sharks!"  
    | otherwise   = "If it's sink or swim, you're going to sink."
```
Repeat `mass / volume` twice.
Fix: Using `where`
```haskell
densityTell :: (RealFloat a) => a -> a -> String
densityTell mass volume
    | mass / volume < 1.2 = "Wow! You're going for a ride in the sky!"
    | mass / volume <= 1000.0 = "Have fun swimming, but watch out for sharks!"
    | otherwise   = "If it's sink or swim, you're going to sink."
    where density = mass / volume
```

Multiple expressions after `where`:
```haskell
densityTell :: (RealFloat a) => a -> a -> String
densityTell mass volume
    | mass / volume < air = "Wow! You're going for a ride in the sky!"
    | mass / volume <= water = "Have fun swimming, but watch out for sharks!"
    | otherwise   = "If it's sink or swim, you're going to sink."
    where density = mass / volume
		  air = 1.2
		  water = 1000.0
```

Pattern matching after `where`:
```haskell
densityTell :: (RealFloat a) => a -> a -> String
densityTell mass volume
    | mass / volume < air = "Wow! You're going for a ride in the sky!"
    | mass / volume <= water = "Have fun swimming, but watch out for sharks!"
    | otherwise   = "If it's sink or swim, you're going to sink."
    where density = mass / volume
		  (air, water) = (1.2, 1000.0)
```
```haskell
initials :: String -> String -> String  
initials firstname lastname = [f] ++ ". " ++ [l] ++ "."  
	where (f:_) = firstname  
          (l:_) = lastname
```

Functions after `where`
```haskell
calcDensities :: (RealFloat a) => [(a, a)] -> [a]  
calcDensities xs = [density m v | (m, v) <- xs]  
	where density mass volume = mass / volume
```