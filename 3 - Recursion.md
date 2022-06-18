# Recursion
It is important to note that, since we don't change the control flow of a program in Haskell, Haskell has no for or while loops (!!).

Recall also that all variables are **immutable** and **final**. This means that incrementors (`i++`) are not an option.

Therefore we have to use alternate ways for programs to repeat themselves.

One way is to use programs that call themselves -- *recursion*.

```hs
-- factorial function
-- assume it never takes a negative Int
fac :: Int -> Int
fac n
    | n <= 1    = 1
    | otherwise = n * fac (n-1)
```

# Pattern Matching
**Pattern Matching** when we define functions is when we specify specfic patterns to which some patterns of data should conform, then define the function differently for those patterns.

In making recursive functions, they're super handy for specifying _edge_ cases and _end_ conditions.

For example:

```hs
is_zero 0 = True
is_zero _ = False
```
The `_` character is a _wildcard_ -- it represents _any_ input.
Patterns _cascade_, meaning the higher patterns have _precedence_ over the lower ones. In this case: the program checks firstly if the input is `0`, and _then_ any other value.

Another example:

```hs
another_fac 0 = 1
another_fac 1 = 1
another_fac n = n * another_fac (n-1)
```

# Accumulators and Auxilliary Functions
Another way of implementing recursion is through the use of auxiliary functions and accumulators.

```hs
last_fac n = aux n 1
    -- we define the factorial of n as the 
    -- output of an auxiliary function aux
    -- being given the inputs n and 1.
    where
        aux n acc
        -- here we define the aux function's logic
            | n <= 1    = acc
            | otherwise = aux (n-1) (n*acc)
            -- Recursive call!!!
```