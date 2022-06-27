# Partial Function Application & Currying
**Partial Function Application** is the result of *"Currying."*

It is a principle that tells us: that a function typed like this:
```hs
f :: a -> b -> c -> d
```
can essentially be broken down into functions, type-defined like:
```
f :: a -> (b -> (c -> d)) 
```
i.e. to say, it takes a single argument, that returns a function,
that returns a single argument, etc.

Essentially,
> Functions that have multiple arguments **DO NOT EXIST!**
> Every function either returns another fuction, or an end result.

This *currying* can be used to rewrite functions. e.g.:

```hs
add :: Int -> Int -> Int
-- the following three definitions are equivalent and valid
add x y = x+y 
add x = (\y -> x+y)
add = (\x -> (\y -> x+y))
```

We take special note of the last definition:
```hs
add = (\x -> (\y -> x+y))
```
What if we took this function add applied just *one* argument?
```
ghci> add 1
```

For a normal, imperative programming language, we could quite
easily conclude that this function would cause the program to
throw an error, as there the program would probably have been
defined to have _2_ arguments, but is only supplied with 1.
But in Haskell, this isn't true, as every single function, 
implicitly, is a function that takes _1_ argument, and then 
returns a function...

```
ghci> add 1
\y -> 1 + y
```
So what we get is a new function!

It's type, of course, is `Int -> Int`.

This is what is known as **Currying**.

# Currying
Currying is a way for us to change the behcaiour a function, and
generate new functions from old functions, and is done all the
time in functional programming.

For example, let's define a function called `doubleList`, using
`map`:
```
-- map :: (a -> b) -> [a] -> [b]
doubleList = map (\x -> 2*x) 
```
`doubleList` now therefore a function that takes a list and returns
a list.
```hs
-- doubleList :: [a] -> [b]
```

```
ghci> doubeList [1,2,3]
[2,4,6]
```
