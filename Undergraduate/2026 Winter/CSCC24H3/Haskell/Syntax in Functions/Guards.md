```haskell
densityTell :: (RealFloat a) => a -> String  
densityTell density  
	| density < 1.2 = "Wow! You're going for a ride in the sky!"  
	| density <= 1000.0 = "Have fun swimming, but watch out for sharks!"  
	| otherwise   = "If it's sink or swim, you're going to sink."
```
Like if-else statement

```haskell
densityTell :: (RealFloat a) => a -> a -> String  
densityTell mass volume  
	| mass / volume < 1.2 = "Wow! You're going for a ride in the sky!" 
    | mass / volume <= 1000.0 = "Have fun swimming, but watch out for sharks!"  
    | otherwise   = "If it's sink or swim, you're going to sink."
```
`otherwise` catches everything.

**Note that there is no `=` right after the function name and its parameters, before the first guard. Many newbies get syntax errors because they sometimes put it there.**
