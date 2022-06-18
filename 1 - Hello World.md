# Haskell
```
             _   _           _        _ _ 
   ::@@     | | | |         | |      | | |
    ::@@====| |_| | __ _ ___| | _____| | |
   ::@@@@   |  _  |/ _` / __| |/ / _ \ | |
  ::@@  @@==| | | | (_| \__ \   <  __/ | |
 ::@@    @@ \_| |_/\__,_|___/_|\_\___|_|_|

```

Haskell is a **statically typed** general purpose **functional** programming language first developed in 1987, named after logician Haskell Curry.

It has seen use in a wide variety of server-side applications, such as the Hasura API platform and spam filtering on Facebook, and also compilers for languages such as `Elm` and `PureScript`.

# Functional Programming
Functional programming is a programming paradigm based on [lambda calculus](https://en.wikipedia.org/wiki/Lambda_calculus) which means a function always produces the same output given the same input.

Data is also immutable: it _cannot_ be changed (in place).

This is as opposed to the Object-Oriented Programming paradigm like in languages such as Java, in which the code can modify the input, which can procuce side-effects that will change the behaviour of an application.

This makes code significantly easier to test, debug and refactor.

# More on Haskell
Haskell (and most other functional programming languages) are **declarative**, as opposed to imperative, meaning we describe the logic of a computation instead of its control flow.

Haskell also uses **lazy evaluation** meaning statement are evaluated if and when they need to be.

# Running Haskell
After installling the [Glasgow Haskell Compiler \(GHC\)](https://www.haskell.org/ghc/):
- `ghc` compiles Haskell code into an executable.
- `ghci` opens the GHC interactive environment
- `runghc` runs Haskell code as if it were a script

You are now ready to start learning Haskell!
```haskell
-- hello_world.hs
-- comments start with double dashes, btw

main :: IO()
main = putStrLn "Hello, World!"
```
```
> runghc ./hello_world.hs
Hello, World!
```
