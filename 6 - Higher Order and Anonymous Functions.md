# Higher Order Functions
A *higher order function* is a function that takes *another*
function as anargument. For example:

```hs
-- hof.hs
app :: (a -> b) -> a -> b
app f x = f x

add1 :: Int -> Int
add1 x = x+1

main :: IO()
main = do
  print(app add1 1)
```
```
> runghc hof.hs
2
```

We can see this in the type definition of `app`: Its first argument is a function (which takes an `a` and gives back
a `b`) and an `a`, and then gives back a `b`.

So in the example, the function app simply just returns the f of x.

# Anonymous functions 
An important part of higher order functions are anonymous functions--
we do not want to define functions with a new name every single
time in the context of using higher-order functions, so we can
simply use un-named functions, or **anonymous functions**.

An anonymous function is defined like this:
```
\<args> -> <expr>
```
With a backslash, a list of arguments, and an expression.
This is similar to how *Lambda Calculus* looks and works.

For further elaboration, what we could do is
something like this...
```
add1 = (\x -> x+1) 
```
```
(\x y z -> x+y+z) 
-- no commas!
```

```
ghci> (\x -> x+1) 1
2
ghci> (\x y z -> x+y+z) 1 2 3
6
```

# `map`
`map` is a **vital** higher-order function in typical Haskell
programs.

```hs
-- Type Definition:
-- map :: (a -> b) -> [a] -> [b]
```
`map` takes two arguments: 
 - a one argument, one return type function
 - a list
and then returns a list of the results, `map`ped one-to-one.

For example: 
```hs
-- map.hs
doubleIt :: Int -> Int
doubleIt x = 2*x

main :: IO()
main = do
  print(map doubleIt [1,2,3,4,5])
```
```
> runghc map.hs
[2,4,6,8,10]
```

```hs
-- map2.hs
isItOne :: x -> Bool
isItOne x = x == 1

main :: IO()
main = do
  print(map isItOne [1,2,3,4,5])
```
```
> runghc map2.hs
[True,False,False,False,False]
```

```
ghci> map(\(x,y) -> x+y) [(1,2),(2,3),(3,4)]
[3,5,7]
```
In this last example, we used took a list of 2-ples, mapped it
to an **anonymous function** that used **pattern matching** to
reference each element in each of the 2-ples and then **added them together**, and returned a list of each result.

# `filter`
Another **vital** HOF to know. 

```hs
-- type definition:
-- filter :: (a -> Bool) -> [a] -> [a]
```
`filter` takes a function that MUST return a `Bool`, and a list
of anything as arguments, then returns a list that has been
`filter`ed according to the function.

For example:
```
ghci> filter (x -> x `rem` 2 == 0) [1,2,3,4,5,6,7,8,9,10]
[2,4,6,8,10]
```

Bool function returns `True` with an element: Element gets put into
returned list.
