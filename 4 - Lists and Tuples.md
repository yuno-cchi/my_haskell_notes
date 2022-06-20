# Lists

Lists are ordered sets of elements.
They can only have _one_ inernal type -- you cannot have a list of `int`s and `float`s, for example.

# List construction

Lists can be explicitly declared like this:
```hs
lis = [1,2,3,4,5] -- :: [Int] --(optional typing)
```

They can also be constructed:
`[]` is the **empty set** -- the set with no elements inside.

`:` is the _prepend_ operator -- it plops the item on the left to the first postion of list on the right
```
ghci> 1:[2,3,4]
[1,2,3,4]
ghci> 1:2:3:4:5:[]
[1,2,3,4,5]
ghci> 'f':'o':'o':['b','a','r'] 
foobar
```
> Recall that `String`s in Haskell are lists of `Char`s!

### Small List exercise:
Define a function `my_asc` that takes two `Int`s `m` 
and `n` as inputs,
and outputs a list of Ints that count
***up*** from m to n (m and n included).

```hs
-- my_asc.hs
my_asc :: Int -> Int -> Int
my_asc m n
    | m > n     = []
    | m == n    = [n]
    | otherwise = m : my_asc m+1 n

main :: IO()
main = do
    print(my_asc 1 9)
```
```
> runghc ./my_asc.hs
[1,2,3,4,5,6,7,8,9]
```

# The `Data.List` Module (a non-exhaustive preview)
Lists are an integral part of writing algorithms in 
Haskell so people have already written lots of useful
functions involving them -- which you can all import
using the statement:

```hs
import Data.List
```

```hs
-- head :: [a] -> a
-- takes a list and returns its first value
-- (no modification -- data is immutable)
h = head [1,2,3,4,5]
-- => 1

-- tail :: [a] -> [a]
-- takes a list and returns a copy of it without
-- its head
t = tail [1,2,3,4,5]
-- => [2,3,4,5]

-- init :: [a] -> [a]
-- takes a list and returns a copy of it without 
-- its last element
i = init [1,2,3,4,5]
-- => [1,2,3,4]

-- length :: [a] -> Int
-- takes a list and returns its length
l = length [1,2,3,4,5]
-- => 5

-- null :: [a] -> Bool
-- takes a list and returns True if its length is 0
-- return False otherwise
n0 = null []
-- => True
n1 = null [1,2,3]
-- => False
```

These two are in the standard library -- no import required:
```hs
-- and :: [Bool] -> Bool
-- or :: [Bool] -> Bool
-- these evaluate a list of Bools

a = and [True, False, True]
-- => False
o = or [True, False, True]
-- => True
```

# List Comprehension: 
We can use a list (or more than one) with some
some rules and guards to make a new list! The syntax
looks like this:
```
[ <generator> | <element> <- <list>, ... , <guard>...]
```
Examples:
```
ghci> [ 2*x | x <- [1,2,3]]
[2,4,6]
```
You can add a guard...
```
ghci> [3*x | x <- [1,2,3,4,5], x > 2]
[9,12,15]
```
Or more than one! (evaluated sequentially)
```
ghci> [2*x | x <- [1,2,3,4,5,6,7,8,9,10], x>2, (rem x 2 == 0)]
[8,12,16,20]
```
> (`mod x 2` is the modulo operator)

You can have more than one element too!
```
ghci> [x+y| x<-[1,2,3,4,5], y<-[5,4,3,2,1]]
[6,6,6,6,6]
ghci> [(x,y)| x<-[1,2], y <-['a','b']]
[(1,'a'),(1,'b'),(2,'a'),(2,'b')]
```
> These are tuples, more on them later!
> They're super handy for creating lists of permutations!

# Pattern matching with Lists
Pattern matching is a powerful tool for (recursively) iterating through a list!

```hs
-- my_sum.hs
-- function that sums the elements of a list of Ints
my_sum :: [Int] -> Int
my_sum [] = 0
my_sum (head:tail) = head + my_sum tail

main :: IO()
main = do
    print(my_sum [1,2,3,4,5,6,7,8,9,10])
```
```
> runghc ./my_sum.hs
55
```

> `(head:tail)` is just a list; but notating it this way
> let us do stuff with the first element, `head`!
> Common functional programmer notation for it is
> `(x:xs)`, though

To illustrate this function mathematically we can say: 
```
let sum({ }) = 0
let sum({a,b,...z})
  = a + sum({b,...z})
  = a + b + sum({...})
  ...
  = a + b + ... + z + sum({ })
  = a + b + ... + z + 0
  = a + b + ... + z
```

### Another example:
```hs
-- function that filters out the even numbers 
-- in a list of Ints
evens :: [Int] -> [Int]
evens [] = []       --stop condition
evens (x:xs)
    | mod x 2 == 0  = x : evens xs
    -- x even: evaluate evens of the tail and prepend the head
    | otherwise     = evens xs
    -- x odd: evaluate evens of tail
```
