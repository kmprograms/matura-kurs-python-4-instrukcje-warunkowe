[Polski](README.md) · **English**

---

# Matura computer science, extended level - Python course, part 4. "Conditional statements"

> ### 🎬 Video walkthrough
> A full step-by-step walkthrough of this part of the course is available on my YouTube channel:
> **[Link to the YouTube video](https://youtu.be/VbAC_1ebf8I)**
>
> In the video I review logical conditions and show the `not` operator, interval notation and lazy evaluation. Then I cover the `if`, `if ... else` and `if ... elif ... else` statements, the conditional expression, the `match` statement and the `min`, `max` and `abs` functions.

---

## Description

Code for the fourth part of a Python course that prepares students for the Polish Matura exam in computer science at the extended level.

In the earlier parts of the course I showed how to store different kinds of data in variables and how to perform calculations on them. This part covers conditional statements, that is, making decisions in a program. The program performs different operations depending on the value stored in a variable.

The repository also contains the files from the previous parts of the course. The code discussed in this video is in the file `app-4-instrukcje-warunkowe.py`.

The next part of the course covers loops.

## Requirements

- Python 3.10 or newer, because the file `app-4-instrukcje-warunkowe.py` uses the `match` statement
- No external dependencies, only the standard library is used

## Running

```bash
git clone https://github.com/kmprograms/matura-kurs-python-4-instrukcje-warunkowe
cd matura-kurs-python-4-instrukcje-warunkowe
python app-4-instrukcje-warunkowe.py
```

You run the other files the same way, passing the name of the chosen file. None of the programs requires keyboard input, because the `input` fragment in the file `app-3-pozyskiwanie-danych-systemy-liczbowe-float.py` is commented out.

## Project structure

| File | Description |
| --- | --- |
| `app-1-pierwszy-program-zmienne.py` | First program, variables and their types, formatting in f-strings, arithmetic operators, swapping variable values, the `end` and `sep` parameters of `print`, type conversion and the `+=`, `-=` and `*=` operators |
| `app-2-liczby-calkowite.py` | Operations on integers, parity and divisibility using `%`, relational operators, the `and` and `or` connectives, extracting the digits of a number and converting seconds into hours, minutes and seconds |
| `app-3-pozyskiwanie-danych-systemy-liczbowe-float.py` | Reading data with `input` (commented out), random numbers with the `random` module, numeral systems, bitwise operations and functions from the `math` module |
| `app-4-instrukcje-warunkowe.py` | Code discussed in this video: logical conditions, lazy evaluation, `if`, `if ... else`, `if ... elif ... else`, the conditional expression, `match` and `min`, `max` and `abs` |

## Topics covered and how the code works

### Logical conditions and the `not` operator

A logical condition is an expression whose value is `True` or `False`. At the beginning of the file I review the relational operators and the `and` and `or` connectives, and then add the `not` operator, which negates a logical value.

```python
a = 11
b = 12

print(a > 10)  # True
print(a == 11)  # True
print(a != 12)  # True
print(a > 0 and a < 15)  # True
print(a < 0 or a > 10)  # True
print(not (a > 10))   # False
```

The `and` operator gives `True` only when both component conditions are true. For the `or` operator it is enough that at least one of them is true. It is a good idea to put the negated expression in parentheses. In such a simple expression it is not necessary, but in a more complex condition with `and` and `or` the parentheses make it clear that the negation applies to the whole expression.

### Checking whether a number belongs to an interval

Python lets you express membership in an interval as a single expression, without joining two comparisons with `and`.

```python
c = 37
print(20 <= c <= 40)
print(not (20 <= c <= 40))
```

The first condition checks whether `c` belongs to the closed interval from 20 to 40, and gives `True`. The second one negates the whole expression, so it gives `False`. The type of interval is determined by the operators used, `<` and `<=`.

### Lazy evaluation

```python
# Leniwe obliczanie
d = 5
print(d != 0 and 10 / d > 1)
```

Python evaluates such an expression from left to right. When `d` is 0, the first condition gives `False`. With the `and` connective the whole condition is then certainly false, so Python does not evaluate the second part. Thanks to this, no division by zero happens, which in Python ends with an error. When `d` is 5, the first condition is true, so Python also has to evaluate the second one. `10 / 5` is 2, and 2 is greater than 1, so the result is `True`.

This behaviour brings two benefits. The value of the whole condition is determined faster, and the calculations are safer. With `and` it is worth placing further to the right the conditions that depend on earlier checks or require more computation. If a lighter condition on the left gives `False`, the heavier operations are not executed at all.

### The `if` statement

You write the statement as `if`, followed by a logical condition and a colon. Below it, indented by four spaces, you place the statements to be executed. There can be as many of them as you need. In Python, indentation is part of the syntax.

```python
e, f = 3, 25

# Jeżeli zachodzi warunek logiczny, wykonaj instrukcje
# które zapiszesz poniżej "we wcięciu"
# Jeżeli warunek nie jest prawdziwy, wtedy pomijasz ten
# fragment kodu
if e >= f:
    g = e + f
    print(f"Wersja 1 - Dodawanie: {g = }")
```

For `e = 3` and `f = 25` the condition is not met, so this fragment is skipped and nothing is printed. In the video I also check `e = 30`. Then the condition is met and a message with the sum appears.

### The `if ... else` statement

```python
# Jeżeli warunek zachodzi, wtedy wykonaj to, co pod if.
# Jeżeli warunek nie zachodzi, wtedy wykonaj to co pod else.
if e >= f:
    g = e + f
    print(f"Wersja 2 - Dodawanie: {g = }")
else:
    g = e * f
    print(f"Wersja 2 - Mnożenie: {g = }")
```

A plain `if` handles only the case in which the condition is met. The construct with `else` handles both cases. For the values in the file the condition is not met, so the `else` block runs and the program prints the product `g = 75`.

### The `if ... elif ... else` statement

You use this variant when you check many mutually exclusive conditions. These are conditions of which only one can be met. If one of them is met, the others are not. An example is checking which of four intervals a number belongs to:

- interval 1 - `[1, 10]`, closed on both sides
- interval 2 - `(10, 25)`, open on both sides
- interval 3 - `[25, 33)`, closed on the left and open on the right
- interval 4 - `[33, 48]`, closed on both sides

The intervals touch each other but have no common part. The number 10 belongs only to interval 1, and the number 33 only to interval 4.

The first version, commented out in the file, uses four separate `if` statements:

```python
# 4 osobne if - każdy z nich jest sprawdzany osobno
# if 1 <= h <= 10:
#     print(f"Liczba {h} w przedziale 1")
# if 10 < h < 25:
#     print(f"Liczba {h} w przedziale 2")
# if 25 <= h < 33:
#     print(f"Liczba {h} w przedziale 3")
# if 33 <= h <= 48:
#     print(f"Liczba {h} w przedziale 4")
```

This version gives correct results, but it is not optimal. Each `if` is checked independently, so for `h = 10` Python still performs three unnecessary checks after matching interval 1.

The better version uses the `if ... elif ... else` construct:

```python
# Kiedy masz warunki rozłączne, wtedy lepiej sprawdzać je za pomocą if ... elif ... else
if 1 <= h <= 10:
    print(f"Liczba {h} w przedziale 1")
elif 10 < h < 25:
    print(f"Liczba {h} w przedziale 2")
elif 25 <= h < 33:
    print(f"Liczba {h} w przedziale 3")
elif 33 <= h <= 48:
    print(f"Liczba {h} w przedziale 4")
else:
    print("Liczba nie należy do żadnego z przedziałów")
```

The conditions are checked one by one until one of them turns out to be true. The remaining ones are then skipped. The `else` block runs when none of the conditions is met. It is optional. Without it, the program would print nothing for a number outside the intervals.

This construct works correctly only for mutually exclusive conditions, because its purpose is to choose one of many variants. The order of the conditions matters. You place the conditions you want to check first higher up.

### Conditional expression

The conditional expression (ternary operator) is a shorter way to write simple `if ... else` constructs whose result is a value.

```python
# Wyrażenie warunkowe
i, j = 12, 40
print(i * j if i < j else i + j)
k = i * j if i < j else i + j
print(k)
```

The condition is placed between `if` and `else`. When the condition is met, the whole expression takes the value of what stands to the left of `if`, that is `i * j`. When it is not met, it takes the value of what stands to the right of `else`, that is `i + j`. You can print the result right away or assign it to a variable and use it in further calculations. For `i = 12` and `j = 40` the condition is met, so in both cases the result is 480.

### The `match` statement

The `match` statement chooses one of many cases based on the value of a variable. You describe the cases with `case`.

```python
# Instrukcja match

opcja = 31

match opcja:
    case 1:
        print("Opcja 1 - dodawanie")
    case 2 | 3:
        print("Opcja 2 - mnożenie lub dzielenie")
    case 6:
        print("Koniec")
    case _:
        print("Nie ma takiej opcji")
```

The notation `case 2 | 3` covers several values at once. `case _` runs when the value does not match any of the earlier cases. Once one case is matched, the others are skipped. A typical use is a simple menu in an application.

Many more kinds of expressions can be written after `case`. You will find the details in the Python documentation. For the Matura exam in computer science, what I show in the video is enough.

### The `min`, `max` and `abs` functions

```python
m, n, o = 12, 34, 25

najmniejsza = min(m, n, o)
print(najmniejsza)

najwieksza = max(m, n, o)
print(najwieksza)

p = -13
print(abs(p))
```

`min` returns the smallest of the given values, `max` the largest, and `abs` the absolute value. The smallest value can also be found with a series of comparisons. We will practise that approach when implementing algorithms and Matura tasks.

## Results

Running the file `app-4-instrukcje-warunkowe.py` with the values written in the code prints:

```
True
True
True
True
True
False
True
False
True
Wersja 2 - Mnożenie: g = 75
Liczba 15 w przedziale 2
480
480
Nie ma takiej opcji
12
34
13
```

In the video I also check other variable values:

| Change in the code | Result |
| --- | --- |
| `d = 0` | `False`, without evaluating `10 / d > 1` |
| `e = 30` | `Wersja 1 - Dodawanie: g = 55` and `Wersja 2 - Dodawanie: g = 55` |
| `h = 10` | `Liczba 10 w przedziale 1` |
| `h = 33` | `Liczba 33 w przedziale 4` |
| `h = 111` | `Liczba nie należy do żadnego z przedziałów` |
| `opcja = 3` | `Opcja 2 - mnożenie lub dzielenie` |

## Implementation notes

The version with four separate `if` statements is kept in the file as a comment, so that it can be compared with the `if ... elif ... else` construct.

The f-strings use the `{g = }` notation, which prints the variable name together with its value, for example `g = 75`.

The `match` statement is relatively new in Python. It was introduced in version 3.10, so older interpreters will not run the file `app-4-instrukcje-warunkowe.py`.

In the video I call `print`, `min`, `max` and `abs` statements, because the concept of a function has not been introduced yet. In fact they are built-in functions. I will cover them in more detail later in the course.