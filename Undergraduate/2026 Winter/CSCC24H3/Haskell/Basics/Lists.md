Lists are a **homogeneous** data structure: They store several elements of the same type.
```haskell
ghci> lostNumbers = [4,8,15,16,23,42]  
ghci> lostNumbers  
[4,8,15,16,23,42]
```
### Concatenation operator `++`
```haskell
ghci> [1,2,3,4] ++ [9,10,11,12]  
[1,2,3,4,9,10,11,12]  
ghci> "hello" ++ " " ++ "world"  
"hello world"  
ghci> ['w','o'] ++ ['o','t']  
"woot"
```
Haskell has to walk through the whole list on the left side of `++`: Not good when the list has a large size.
### Construction operator `:`
Prepends an element to the front of the list. it runs in constant time because it only adds to the head of a linked list.
```haskell
ghci> 'A':" SMALL CAT"  
"A SMALL CAT"  
ghci> 5:[1,2,3,4,5]  
[5,1,2,3,4,5]
```
### Get an element by index `!!`
```haskell
ghci> "Steve Buscemi" !! 6  
'B'  
ghci> [9.4,33.2,96.2,11.2,23.25] !! 1  
33.2
```
### Nested list
```haskell
ghci> b = [[1,2,3,4],[5,3,3,3],[1,2,2,3,4],[1,2,3]]  
ghci> b  
[[1,2,3,4],[5,3,3,3],[1,2,2,3,4],[1,2,3]]  
ghci> b ++ [[1,1,1,1]]  
[[1,2,3,4],[5,3,3,3],[1,2,2,3,4],[1,2,3],[1,1,1,1]]  
ghci> [6,6,6]:b  
[[6,6,6],[1,2,3,4],[5,3,3,3],[1,2,2,3,4],[1,2,3]]  
ghci> b !! 2  
[1,2,2,3,4]
```
Nested lists can have different length, but they cannot have different types.
### Comparing lists
When using `<`, `<=`, `>` and `>=` to compare lists, they are compared in lexicographical order. First the heads are compared. If they are equal then the second elements are compared, etc.
### Basic functions
![[Pasted image 20260218155018.png]]
#### `head`
`head` takes a list and returns its head. The head of a list is basically its first element.
```haskell
ghci> head [5,4,3,2,1]  
5
```

Try to get the head of an empty list:
```haskell
ghci> head []  
*** Exception: Prelude.head: empty list
```
#### `tail`
`tail` takes a list and returns its tail. In other words, it chops off a list’s head.
```haskell
ghci> tail [5,4,3,2,1]  
[4,3,2,1]
```
#### `last`
`last` takes a list and returns its last element.
```haskell
ghci> last [5,4,3,2,1]  
1
```
#### `init`
```haskell
ghci> init [5,4,3,2,1]  
[5,4,3,2]
```
#### `length`
`length` takes a list and returns its length.
#### `null`
`null` checks if a list is empty. If it is, it returns `True`, otherwise it returns `False`. Use this function instead of `xs == []` (if you have a list called `xs`).
```haskell
ghci> null [1,2,3]  
False  
ghci> null []  
True
```
#### `reverse`
`reverse` reverses a list.
```haskell
ghci> reverse [5,4,3,2,1]  
[1,2,3,4,5]
```
#### `take`
`take` takes a number and a list. It extracts that many elements from the beginning of the list.
```haskell
ghci> take 3 [5,4,3,2,1]  
[5,4,3]  
ghci> take 1 [3,9,3]  
[3]  
ghci> take 5 [1,2]  
[1,2]  
ghci> take 0 [6,6,6]  
[]
```
Try to take more elements than there are in the list: returns the list
Try to take 0 elements: returns an empty list
#### `drop`
drops the number of elements from the beginning of a list.
```haskell
ghci> drop 3 [8,4,2,1,5,6]  
[1,5,6]  
ghci> drop 0 [1,2,3,4]  
[1,2,3,4]  
ghci> drop 100 [1,2,3,4]  
[]
```
#### `maximum`
returns the biggest element in the list.
```haskell
ghci> maximum [1,9,2,3,4]
9
```
#### `minimum`
returns the smallest element in the list.
```haskell
ghci> minimum [8,4,2,1,5,6]  
1
```
#### `sum`
returns the sum of the list
```haskell
ghci> sum [5,2,1,6,3,2,5,7]  
31
```
#### `product`
```haskell
ghci> product [6,2,1,2]  
24  
ghci> product [1,2,5,6,7,9,2,0]  
0
```
#### `elem`
`elem` takes a thing and a list of things and tells us if that thing is an element of the list. It’s usually called as an infix function because it’s easier to read that way.
```haskell
ghci> 4 `elem` [3,4,5,6]  
True  
ghci> 10 `elem` [3,4,5,6]  
False
```
### Texas ranges
```haskell
ghci> [1..20]  
[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20]  
ghci> ['a'..'z']  
"abcdefghijklmnopqrstuvwxyz"  
ghci> ['K'..'Z']  
"KLMNOPQRSTUVWXYZ"
```
#### Specify a step
```haskell
ghci> [2,4..20]  
[2,4,6,8,10,12,14,16,18,20]  
ghci> [3,6..20]  
[3,6,9,12,15,18]
```
#### Infinite lists
##### `cycle`
`cycle` takes a list and cycles it into an infinite list. If you just try to display the result, it will go on forever so you have to slice it off somewhere.
```haskell
ghci> take 10 (cycle [1,2,3])  
[1,2,3,1,2,3,1,2,3,1]  
ghci> take 12 (cycle "LOL ")  
"LOL LOL LOL "
```
##### `repeat`
```haskell
ghci> take 10 (repeat 5)  
[5,5,5,5,5,5,5,5,5,5]
```
#### List comprehension
```haskell
ghci> [x*2 | x <- [1..10]]  
[2,4,6,8,10,12,14,16,18,20]
```
##### Condition
```haskell
ghci> [x*2 | x <- [1..10], x*2 >= 12]  
[12,14,16,18,20]
ghci> [ x | x <- [50..100], x `mod` 7 == 3]  
[52,59,66,73,80,87,94]
```
##### Filtering
```haskell
ghci> boomBangs xs = [ if x < 10 then "BOOM!" else "BANG!" | x <- xs, odd x]
ghci> boomBangs [7..13]  
["BOOM!","BOOM!","BANG!","BANG!"]
```

```haskell
ghci> [ x | x <- [10..20], x /= 13, x /= 15, x /= 19]  
[10,11,12,14,16,17,18,20]
```

```haskell
ghci> [ x*y | x <- [2,5,10], y <- [8,10,11]]  
[16,20,22,40,50,55,80,100,110]
```

```haskell
ghci> nouns = ["hobo","frog","pope"]  
ghci> adjectives = ["lazy","grouchy","scheming"]  
ghci> [adjective ++ " " ++ noun | adjective <- adjectives, noun <- nouns]  
["lazy hobo","lazy frog","lazy pope","grouchy hobo","grouchy frog",  
"grouchy pope","scheming hobo","scheming frog","scheming pope"]
```
