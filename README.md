# Island

The Island programming language is a an experimental project for a uniformly design programming language.

The main features of the language include:

* Prefix notation
* Multiple dispatch
* Higher-order functions
* Uniformity and simplicity

### Examples

The following examples illustrate some of the decisions made in designing the syntax of the language.

#### Factorial

```python
def fac { |n|
    if [eq n 0] [ return 1 ]
    mul n (call fac (sub n 1))
}

say (call fac 10)    #=> 3628800
```

#### Fibonacci

```python
def fib { |n|
    if [lt n 2] [ return n ]
    add (call fib (sub n 1)) (call fib (sub n 2))
}

say (call fib 12)    #=> 144
```

#### `while`-loop

Multimethod: `while(Expr, Expr)`

```python
def n 10
while [gt n 0] [
    say n
    sub! n 1
]
```

#### `foreach`-loop

Multimethod: `for(Range, Block)`

```python
for (range 1 10) { |n|
    say n
}
```

#### `for(;;)`-loop

Multimethod: `for(Expr, Expr, Expr, Expr)`

```python
for [def n 1] [lt n 10] [add! n 1] [
    say n
]
```

#### Bernoulli numbers (recursive)

```python
def bern_helper { |n k|
    mul (call binomial n k) (div (call bernoulli_number k) (add (sub n k) 1))
}

def bern_diff { |n k d|
    if [lt n k] [ return d ]
    call bern_diff n (add k 1) (sub d (call bern_helper (add n 1) k))
}

def bernoulli_number { |n|
    if [one? n] [ return (div 1 2) ]
    if [odd? n] [ return 0         ]
    if [gt n 0] [ call bern_diff (sub n 1) 0 1]
    return 1
}

for (range 0 25) { |i|
    def num (call bernoulli_number i)
    unless [zero? num] [
        printf "B(%2d) = %20s / %s\n" i (nu num) (de num)
    ]
}
```
