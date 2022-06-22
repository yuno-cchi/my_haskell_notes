# Exercises on Lists

### Exercise #1: `elem`
```hs
my_elem :: (Eq a) => a -> [a] -> Bool
```
> (more on `Eq` soon!)

Create a function `my_elem` that returns:
- `True` if an element `my_element` is in a given list
- `False` otherwise

### Solution:
<details>
    <summary>(Open to reveal answer)</summary>
    
    my_elem _ [] = False
    my_elem a (head:tail)
        | a == head = True
        | otherwise = False

</details>
<br>
<br>

### Exercise #2: `nub`
```hs
my_nub :: (Eq a) => [a] -> [a]
```
Create a function `my_nub` that takes a list,
and then returns a copy of it _without_ any duplicate elements. _Which_ of the duplicates is preserved, if any, is irrelevant. 
> **Tip:** You may use the `elem` function from Exercise #1.

### Solution:
<details>
    <summary>(Open to reveal answer)</summary>

    ```
    my_nub [] = []
    my_nub (head:tail)
        | not(x `elem` xs) = x : my_nub xs
        | otherwise        = my_nub xs
    ```
</details>
<br>
<br>

### Exercise #3: `isAsc`
```hs
isAsc :: [Int] -> Bool
```
Create a function `isAsc` that takes a list of
`Int`s that returns:
- `True` if the list is in **ascending order**
- `False` otherwise

### Solution:
<details>
    <summary>(Open to reveal answer)</summary>

    isAsc [] = True
    isAsc [x] = True
    isAsc (x:y:xs)
        | x <= y    = isAsc xs
        | otherwise = False
  
</details>
