# Variable Definition
Variables in Haskell are defined in expressions.
```hs
foo = "bar"
num = "12"
```
Variable types are inferred, but variables can be explicitly types like this:
```hs
-- strings in Haskell are lists of Chars
foo = "bar" :: [Char]
num = 12 :: Int
```
Data type documentation is available [here](https://www.haskell.org/onlinereport/haskell2010/haskellch6.html)

# Function Definition
Functions in Haskell are defined like this:
```hs
fnName arg1 arg2 ... arg_n = <expr>
```
The function is named, the arguments are listed, and is equated to an expression that describes how the output of the function is obtained from the input(s). (Like functions in Math!)

No return statements or parentheses needed.

```hs
-- function that returns True if x is 
-- between min and max (inclusive)
in_range min max x = 
    x >= min && x <= max

-- logical and mathematical operators are the same as in most languages, btw
```

# First-Class Functions
Functions in Haskell are **first-class**, meaning they can be treated like any other variable.

This means that they can (and should) be typed, like this:

```hs
-- fnDefiniion.hs
in_range :: Int -> Int -> Int -> Bool
in_range min max x = 
    x >= min && x <= max

main :: IO()
main = do
    print(in_range 3 5 4)
```
```
> runghc ./fnDefinition.hs
True
```

# `let` Bindings
In Haskell we use the `let` keyword during function declaration to create ***local*** variables/functions to use when we define the function's logic in an `in` clause.

```hs
-- Haskell is whitespace sesitive!
new_in_range min max x = 
    let is_in_lower_bound = min <= x
        is_in_upper_bound = max <= x
    in
        is_in_lower_bound && is_in_upper_bound
```

# Conditionals and Guards
Conditional fuctions in Haskell looks something like this:
```hs
another_in_range min max x =
    if (min <= x && max >= x) then True
    else False
```
Guards are essentially Boolean expressisons with a function body. They're indicated by pipes (The `|` character). If the guard evaluates to `True` then the corresponding function body is used. If not, the next guard is checked. There must be one `otherwise` guard at the end of the function to declare what the function returns if all other guards fail.

```hs
-- a tab or four spaces
-- and then a pipe
-- also note: the equals signs are with the guards
again_an_in_range min max x
    | x < min   = False
    | x > max   = False
    | otherwise = True
-- you can align the = signs for better readablity
```

# `where` bindings
Similar to `let/in` bindings.
```hs
last_in_range min max x
    | not_in_upper_bound = False
    | not_in_lower_bound = False
    | otherwise = True
    where
        not_in_upperbound = x > max
        not_in_lowerbound = x < min
    -- indent it again!
```
# Infix notation
```hs
add a b =
    a+b
```
Functions with two arguments can be called like this:
```
ghci > 10 `add` 20
30
```

