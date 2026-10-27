# Chapter 2 — Fundamentals of Python — Values, Variables, and Basic I/O

## 2.1 Introduction

Every program manipulates data. Before a program can process a file, communicate with a server, analyze a dataset, or interact with an artificial intelligence model, it must represent information in a form that the computer can work with.

Python provides a concise and expressive system for representing data, assigning names to objects, converting between types, processing text, and communicating with users.

This chapter introduces these fundamental mechanisms:

- Literals and values
- Variables and variable reassignment
- Identifiers and naming conventions
- Built-in data types
- Type conversion and type inspection
- Strings and basic string operations
- Standard input and output
- Object references, mutability, and identity
- Comments, whitespace, and basic formatting conventions

These concepts form the foundation for subsequent topics, including operators, control flow, collections, functions, and object-oriented programming.

## 2.2 Literals and Values

### 2.2.1 What Is a Literal?

A **literal** is a notation used directly in source code to represent a value.

Consider the following examples:

```
42
3.14159
"Python"
True
None
```

Each expression represents a value of a particular type.

A literal is not the same thing as a variable. A literal appe0ars directly in the source code, whereas a variable provides a name through which a value or object can be accessed.

For example:

```python
# Example 2.1: Basic Literals

print(42)
print(3.14159)
print("Python")
print(True)
print(None)
```

Output:

```
42
3.14159
Python
True
None
```

Python supports several categories of literals.

| Category                | Examples                       | Description                               |
| ----------------------- | ------------------------------ | ----------------------------------------- |
| Integer literals        | `0`, `42`, `-17`               | Whole-number values                       |
| Floating-point literals | `3.14`, `-0.5`, `2.0`          | Approximate real-number values            |
| String literals         | `"Python"`, `'Hello'`          | Text                                      |
| Boolean literals        | `True`, `False`                | Truth values                              |
| Special literal         | `None`                         | Represents the absence of a value         |
| Collection literals     | `[1, 2]`, `(1, 2)`, `{"a": 1}` | Construct lists, tuples, and dictionaries |

The underscore character can improve the readability of long numeric literals.

```python
# Example 2.2: Readable Numeric Literals

population = 1_400_000_000
file_size = 2_048_576

print(population)
print(file_size)
```

Output:

```
1400000000
2048576
```

Underscores in numeric literals are separators for human readers. They do not change the represented numeric value.

Python also supports integer literals in hexadecimal, binary, and octal notation:

```python
# Example 2.3: Integer Number Systems

decimal_number = 42
binary_number = 0b101010
octal_number = 0o52
hexadecimal_number = 0x2A

print(decimal_number)
print(binary_number)
print(octal_number)
print(hexadecimal_number)
```

Output:

```
42
42
42
42
```

The prefixes are:

- `0b` or `0B`: binary
- `0o` or `0O`: octal
- `0x` or `0X`: hexadecimal

All four literals represent the same integer.

### 2.2.2 Expressions and Values

An expression is a combination of literals, variables, operators, and function calls that Python evaluates to produce a result.

For example:

```python
# Example 2.4: Expressions Produce Values

result = 10 + 5 * 2

print(result)
print(10 > 5)
print("Py" + "thon")
```

Output:

```
20
True
Python
```

The expression `10 + 5 * 2` evaluates to `20` because multiplication has higher precedence than addition.

The expression `"Py" + "thon"` evaluates to a new string containing `Python`.

Understanding the distinction between a literal and an expression is important. `42` is an integer literal, while `40 + 2` is an expression whose result is the integer `42`.

### 2.2.3 Numeric Precision

Python integers can represent arbitrarily large integers, subject to available memory.

Floating-point numbers, however, generally use binary floating-point arithmetic and cannot represent every decimal fraction exactly.

```python
# Example 2.5: Floating-Point Precision

print(0.1 + 0.2)
print(0.1 + 0.2 == 0.3)
```

Typical output:

```
0.30000000000000004
False
```

This result is not a random malfunction. Many decimal fractions have no exact finite representation in binary floating-point format.

When comparing floating-point results, a tolerance is often more appropriate than exact equality.

```python
# Example 2.6: Comparing Floating-Point Values

result = 0.1 + 0.2
expected = 0.3
tolerance = 1e-9

print(abs(result - expected) < tolerance)
```

Output:

```
True
```

For financial calculations requiring exact decimal arithmetic, Python provides the `decimal` module. It should be introduced when the application requires decimal arithmetic with controlled precision.

## 2.3 Variables and Assignment

### 2.3.1 What Is a Variable?

A **variable** is a name bound to an object.

In Python, assignment does not declare a fixed memory container with a permanently established type. Instead, it binds a name to an object.

```python
# Example 2.7: Creating Variables

name = "Alice"
age = 25
height = 1.68
is_student = True

print(name)
print(age)
print(height)
print(is_student)
```

Output:

```
Alice
25
1.68
True
```

The assignment operator `=` binds the name on its left to the object produced by the expression on its right.

For example:

```
age = 25
```

This statement binds `age` to the integer object representing `25`.

It does not mean that `age` is a special integer-shaped container that can never refer to anything else.

### 2.3.2 Assignment Is Not Mathematical Equality

In mathematics, an equals sign generally expresses equality. In Python, `=` is an assignment operator.

```python
# Example 2.8: Assignment and Equality

number = 10
number = number + 5

print(number)
print(number == 15)
```

Output:

```
15
True
```

The statement

```
number = number + 5
```

is valid Python because the right-hand expression is evaluated first. Its result is then bound to the name `number`.

By contrast, `==` tests equality.

```
number == 15
```

This expression evaluates to `True` if the value referred to by `number` compares equal to `15`.

The two operators serve different purposes:

| Operator | Meaning               |
| -------- | --------------------- |
| `=`      | Assignment            |
| `==`     | Equality comparison   |
| `!=`     | Inequality comparison |

Confusing assignment with equality is a common beginner error. The distinction remains important even for experienced programmers.

### 2.3.3 Multiple Assignment

Python allows multiple names to be assigned in a single statement.

```python
# Example 2.9: Multiple Assignment

x, y, z = 10, 20, 30

print(x)
print(y)
print(z)
```

Output:

```
10
20
30
```

The number of target names must match the number of values in an unpacking assignment, unless a starred target is used.

Python also permits assigning the same object reference to several names:

```python
# Example 2.10: Assigning One Value to Multiple Names

x = y = z = 100

print(x, y, z)
```

Output:

```
100 100 100
```

All three names refer to the same integer object. Since integers are immutable, this sharing does not introduce the mutable-aliasing problems discussed later in this chapter.

### 2.3.4 Swapping Variables

Python supports swapping two variables without a temporary variable.

```python
# Example 2.11: Swapping Two Variables

a = 10
b = 20

a, b = b, a

print(a)
print(b)
```

Output:

```
20
10
```

Python evaluates the right-hand side before completing the assignments to the targets. This makes the operation concise and avoids the need for a temporary variable.

## 2.4 Variable Reassignment and Object References

### 2.4.1 Reassignment

A name can be rebound to a different object.

```python
# Example 2.12: Variable Reassignment

value = 10
print(value)

value = 20
print(value)

value = "Python"
print(value)
```

Output:

```
10
20
Python
```

The name `value` first refers to an integer, then to another integer, and finally to a string.

Python does not require the name to retain its original type.

This behavior is a consequence of Python's dynamic type system. Objects have types; names are not permanently declared to have those types.

### 2.4.2 Dynamic Typing

Python is a dynamically typed language.

The type of an object is determined at runtime, and a name can be rebound to objects of different types.

Java, by contrast, is statically typed. A variable declared as `int` cannot subsequently be assigned a `String`.

Java:

```java
int value = 10;
value = 20;

// value = "Python"; // Compilation error
```

Python:

```python
# Example 2.13: Dynamic Typing

value = 10
value = 20
value = "Python"

print(value)
print(type(value))
```

Output:

```
Python
<class 'str'>
```

Dynamic typing can make experimentation and rapid development convenient. It also means that some type-related errors may only become apparent when the relevant code executes.

Static typing can detect many incompatible assignments before execution. Python offers optional type annotations to support static analysis, but ordinary Python annotations do not automatically enforce types at runtime.

### 2.4.3 Names, Objects, and References

Python's object model is best understood in terms of names and objects.

Consider the following example:

```python
# Example 2.14: Two Names Referring to One Object

first = [1, 2, 3]
second = first

print(first)
print(second)
```

Output:

```
[1, 2, 3]
[1, 2, 3]
```

The assignment

```
second = first
```

does not create a new list. It binds `second` to the same list object already referenced by `first`.

Python provides the `is` operator to test **object identity**: whether two references point to the same object.

```python
# Example 2.15: Testing Object Identity

first = [1, 2, 3]
second = first
third = [1, 2, 3]

print(first is second)
print(first is third)
```

Output:

```
True
False
```

`first is second` evaluates to `True` because both names refer to the same list object.

`first is third` evaluates to `False` because `third` refers to a separate list object, even though that list contains the same elements.

This distinction can be summarized as follows:

- `==` tests whether two objects compare equal in value.
- `is` tests whether two references identify the same object.

For example:

```python
# Example 2.16: Equality Versus Identity

first = [1, 2, 3]
second = [1, 2, 3]

print(first == second)
print(first is second)
```

Output:

```
True
False
```

The lists have equal contents, but they are distinct objects.

Returning to the original example, modifying the list through one name affects what is observed through the other.

```python
# Example 2.17: Shared Mutable Objects

first = [1, 2, 3]
second = first

second.append(4)

print(first)
print(second)
print(first is second)
```

Output:

```
[1, 2, 3, 4]
[1, 2, 3, 4]
True
```

Both names refer to the same mutable object. Consequently, modifying the list through `second` also changes the list observed through `first`.

This is a fundamental distinction between rebinding a name and modifying an object.

Rebinding changes which object a name refers to. Mutation changes the state of an existing mutable object.

A useful mental model is to think of names as labels attached to objects rather than independent containers. Moving one label does not move the object to which another label is attached.

### 2.4.4 Reassignment Does Not Necessarily Modify an Object

Consider the following example:

```python
# Example 2.18: Rebinding Versus Mutation

first = [1, 2, 3]
second = first

first = [4, 5, 6]

print(first)
print(second)
print(first is second)
```

Output:

```
[4, 5, 6]
[1, 2, 3]
False
```

The statement

```
first = [4, 5, 6]
```

creates a new list and binds `first` to it. It does not alter the original list.

`second` continues to refer to the original object.

Think of names as labels attached to objects rather than boxes into which objects must permanently fit. Moving a label does not move the object to which another label is attached.

### 2.4.5 Copying Mutable Objects

If two names must refer to independent lists, create a copy.

```python
# Example 2.19: Copying a List

original = [1, 2, 3]
copied = original.copy()

copied.append(4)

print(original)
print(copied)
print(original is copied)
```

Output:

```
[1, 2, 3]
[1, 2, 3, 4]
False
```

The `copy()` method creates a shallow copy. The new list is a different list object, but references to nested objects are copied rather than recursively duplicating those objects.

Deep copying is available through the `copy` module when independent copies of nested structures are required.

The distinction between shallow and deep copying becomes important when working with nested collections, configuration objects, and complex application state.

## 2.5 Identifiers and Naming Conventions

### 2.5.1 What Is an Identifier?

An **identifier** is a name used to identify a program element, such as a variable, function, class, or module.

Examples:

```
user_name = "Alice"
total_price = 99.99
MAX_RETRIES = 3
```

Here, `user_name`, `total_price`, and `MAX_RETRIES` are identifiers.

Python identifiers must follow specific lexical rules.

An identifier may contain:

- Letters, including many Unicode letters
- Digits, except as the first character
- Underscores

An identifier cannot begin with a digit, and ordinary identifiers cannot contain spaces or punctuation such as hyphens.

Valid identifiers:

```python
# Example 2.20: Valid Identifiers

name = "Alice"
user_name = "Bob"
age2 = 30
_private_value = 100
```

Invalid identifiers include:

```py
# Example 2.21: Invalid Identifiers

# 2age = 30
# user-name = "Alice"
# user name = "Alice"
```

These lines are commented out because they would cause syntax errors if executed as written.

An identifier must also not be a reserved keyword.

For example, `class`, `if`, `for`, and `return` have special grammatical meanings in Python and cannot be used as ordinary variable names.

### 2.5.2 Case Sensitivity

Python is case-sensitive.

```python
# Example 2.22: Case-Sensitive Identifiers

name = "Alice"
Name = "Bob"
NAME = "Charlie"

print(name)
print(Name)
print(NAME)
```

Output:

```
Alice
Bob
Charlie
```

The three names are distinct identifiers.

Consistent capitalization is therefore important for readability and correctness.

### 2.5.3 Naming Conventions

Python has established naming conventions, commonly documented in PEP 8.

| Element                       | Convention         | Example             |
| ----------------------------- | ------------------ | ------------------- |
| Variables                     | `snake_case`       | `user_name`         |
| Functions                     | `snake_case`       | `calculate_total()` |
| Classes                       | `PascalCase`       | `BankAccount`       |
| Constants                     | `UPPER_SNAKE_CASE` | `MAX_RETRIES`       |
| Internal implementation names | Leading underscore | `_internal_value`   |

A leading underscore commonly indicates that a name is intended for internal use. It does not make the name inaccessible.

Python does not enforce constants merely because their names use uppercase letters. `MAX_RETRIES` can still be reassigned. Uppercase naming is a convention that communicates intent.

Double leading underscores have a special role in class definitions: they can trigger name mangling. This topic belongs to object-oriented programming rather than basic variable naming.

### 2.5.4 Keywords and Built-in Names

Keywords have syntactic significance. Built-in names, such as `print`, `str`, and `list`, are different: they are ordinary names provided by Python's built-in namespace.

You should avoid using built-in names as variable names.

```python
# Example 2.23: Avoid Shadowing Built-in Names

# Avoid:
# list = [1, 2, 3]
# str = "Python"

numbers = [1, 2, 3]
text = "Python"

print(numbers)
print(text)
```

If you bind the name `list` to a variable, then `list(...)` may no longer call the built-in list constructor within that scope.

This is called **shadowing** a name. It can produce confusing errors that are entirely avoidable through sensible naming.

To inspect Python's keywords:

```python
# Example 2.24: Inspecting Python Keywords

import keyword

print(keyword.kwlist)
print(keyword.iskeyword("class"))
print(keyword.iskeyword("variable"))
```

The exact keyword list can vary between Python versions.

## 2.6 Built-in Data Types

### 2.6.1 Overview

Python objects have types. A type determines which operations an object supports and how those operations behave.

The following table summarizes several essential built-in types.

| Type        | Example             | Description                        | Mutable? |
| ----------- | ------------------- | ---------------------------------- | -------- |
| `int`       | `42`                | Integer                            | No       |
| `float`     | `3.14`              | Floating-point number              | No       |
| `complex`   | `2 + 3j`            | Complex number                     | No       |
| `bool`      | `True`              | Boolean value                      | No       |
| `str`       | `"Python"`          | Text                               | No       |
| `list`      | `[1, 2, 3]`         | Ordered sequence                   | Yes      |
| `tuple`     | `(1, 2, 3)`         | Ordered sequence                   | No       |
| `range`     | `range(5)`          | Arithmetic progression of integers | No       |
| `dict`      | `{"name": "Alice"}` | Mapping of keys to values          | Yes      |
| `set`       | `{1, 2, 3}`         | Collection of distinct elements    | Yes      |
| `frozenset` | `frozenset({1, 2})` | Immutable set                      | No       |
| `bytes`     | `b"ABC"`            | Immutable byte sequence            | No       |
| `bytearray` | `bytearray(b"ABC")` | Mutable byte sequence              | Yes      |
| `NoneType`  | `None`              | Type of the `None` object          | No       |

This chapter focuses primarily on numeric types, booleans, strings, and `None`. Collections are introduced here only where needed to explain references and mutability.

### 2.6.2 Integers: `int`

The `int` type represents integers.

```python
# Example 2.25: Integer Operations

a = 10
b = 3

print(a + b)
print(a - b)
print(a * b)
print(a // b)
print(a % b)
print(a ** b)
```

Output:

```
13
7
30
3
1
1000
```

The operators demonstrate:

- `+`: addition
- `-`: subtraction
- `*`: multiplication
- `//`: floor division
- `%`: remainder
- `**`: exponentiation

Floor division rounds the mathematical quotient down toward negative infinity. It does not always behave like integer division in Java, which truncates toward zero.

For example:

```python
# Example 2.26: Floor Division with Negative Numbers

print(7 // 3)
print(-7 // 3)
print(7 % 3)
print(-7 % 3)
```

Output:

```
2
-3
1
2
```

Python's quotient and remainder satisfy the relationship

```
a == (a // b) * b + (a % b)
```

for integer `a` and nonzero integer `b`.

For `-7` and `3`, the quotient is `-3` and the remainder is `2`.

This is a frequent source of cross-language surprises.

### 2.6.3 Floating-Point Numbers: `float`

The `float` type represents floating-point numbers.

```python
# Example 2.27: Floating-Point Values

price = 19.99
temperature = -3.5
scientific_value = 6.02e23

print(price)
print(temperature)
print(scientific_value)
print(type(price))
```

The notation `6.02e23` represents approximately `6.02 × 10²³`.

In ordinary CPython implementations on modern platforms, `float` typically uses IEEE 754 double-precision binary floating-point representation.

This provides a wide numeric range and efficient arithmetic, but decimal precision is finite.

### 2.6.4 Complex Numbers: `complex`

Python supports complex numbers, using `j` to denote the imaginary component.

```python
# Example 2.28: Complex Numbers

number = 2 + 3j

print(number)
print(number.real)
print(number.imag)
print(abs(number))
```

Output:

```
(2+3j)
2.0
3.0
3.605551275463989
```

Complex numbers are useful in scientific computing, signal processing, and mathematical applications.

### 2.6.5 Boolean Values: `bool`

The Boolean type has two values:

```
True
False
```

These values represent logical truth.

```python
# Example 2.29: Boolean Expressions

is_adult = True
has_permission = False

print(is_adult)
print(10 > 5)
print(10 == 5)
print(is_adult and has_permission)
```

Output:

```
True
True
False
False
```

Python's Boolean literals must be capitalized exactly as shown. `true` and `false` are not Python Boolean literals.

The `bool` type is a subclass of `int`.

Consequently:

```python
# Example 2.30: Booleans and Integers

print(isinstance(True, int))
print(True + True)
print(False + 10)
```

Output:

```
True
2
10
```

Although this behavior is valid Python, Boolean values should generally be used to express logical meaning rather than treated as ordinary numbers.

### 2.6.6 The Special Value `None`

`None` is a special singleton object representing the absence of a value or the lack of a meaningful result.

```python
# Example 2.31: The None Value

result = None

print(result)
print(type(result))
print(result is None)
```

Output:

```
None
<class 'NoneType'>
True
```

A function that reaches its end without an explicit `return` statement returns `None`.

```
# Example 2.30: Implicit None Return

def display_message():
    print("Hello, Python!")

result = display_message()

print(result)
```

Output:

```
Hello, Python!
None
```

The function prints a message but does not explicitly return a value.

The `None` object is distinct from:

- `0`, which is an integer
- `False`, which is a Boolean
- `""`, which is an empty string
- `[]`, which is an empty list

These values may all be falsy in a Boolean context, but they are not interchangeable.

When testing whether a value is `None`, use `is None` or `is not None`.

### 2.6.7 Inspecting Types

The built-in `type()` function reports the type of an object.

```
# Example 2.31: Inspecting Data Types

values = [
    42,
    3.14,
    2 + 3j,
    True,
    "Python",
    None
]

for value in values:
    print(value, type(value))
```

Example output:

```
42 <class 'int'>
3.14 <class 'float'>
(2+3j) <class 'complex'>
True <class 'bool'>
Python <class 'str'>
None <class 'NoneType'>
```

For checking whether an object is an instance of a type or its subclasses, `isinstance()` is often more appropriate.

```
# Example 2.32: Using isinstance()

value = 42

print(isinstance(value, int))
print(isinstance(value, str))
print(isinstance(value, (int, float)))
```

Output:

```
True
False
True
```

There is an important distinction:

- `type(value) is SomeType` checks for that exact type.
- `isinstance(value, SomeType)` also recognizes instances of subclasses.

This distinction becomes particularly important in object-oriented programming.

### 2.6.8 Mutability

An object is **mutable** if its state can be changed after creation. An immutable object cannot be changed in place.

Examples of immutable built-in types include:

- `int`
- `float`
- `complex`
- `bool`
- `str`
- `tuple`
- `bytes`

Examples of mutable built-in types include:

- `list`
- `dict`
- `set`
- `bytearray`

The immutability of a tuple does not mean every object contained in it must be immutable. A tuple can contain a reference to a mutable object.

```
# Example 2.33: A Tuple Containing a Mutable List

items = ([1, 2], "Python")

items[0].append(3)

print(items)
```

Output:

```
([1, 2, 3], 'Python')
```

The tuple's elements cannot be reassigned through ordinary item assignment, but the list referenced by its first element can still be modified.

Immutability applies to the object itself, not automatically to every object reachable through it.

## 2.7 Type Conversion

### 2.7.1 Explicit Conversion

Python provides built-in functions for converting values between compatible types.

Common conversion functions include:

| Function  | Purpose                               | Example          |
| --------- | ------------------------------------- | ---------------- |
| `int()`   | Convert to an integer where supported | `int("42")`      |
| `float()` | Convert to a floating-point number    | `float("3.14")`  |
| `str()`   | Produce a string representation       | `str(42)`        |
| `bool()`  | Evaluate truthiness                   | `bool(1)`        |
| `list()`  | Construct a list from an iterable     | `list("abc")`    |
| `tuple()` | Construct a tuple from an iterable    | `tuple([1, 2])`  |
| `set()`   | Construct a set from an iterable      | `set([1, 1, 2])` |

Example:

```
# Example 2.34: Basic Type Conversion

integer_value = int("42")
floating_value = float("3.14")
string_value = str(100)
boolean_value = bool(1)

print(integer_value, type(integer_value))
print(floating_value, type(floating_value))
print(string_value, type(string_value))
print(boolean_value, type(boolean_value))
```

Output:

```
42 <class 'int'>
3.14 <class 'float'>
100 <class 'str'>
True <class 'bool'>
```

Conversion is not always possible.

```python
# Example 2.35: Invalid Numeric Conversion

value = "Python"

# The following statement raises ValueError:
# number = int(value)

print("The string cannot be converted to an integer.")
```

The exception is `ValueError` because the string has an acceptable input type for `int()`, but its contents do not represent a valid integer literal for that conversion.

By contrast, passing an object of an unsupported type may raise `TypeError`.

### 2.7.2 Conversion Is Not Always Reversible

Converting a floating-point number to an integer discards the fractional part by truncating toward zero.

```
# Example 2.36: Converting Floats to Integers

print(int(3.9))
print(int(-3.9))
```

Output:

```
3
-3
```

This operation is not rounding.

If rounding is required, Python provides `round()`:

```
# Example 2.37: Rounding Numbers

print(round(3.9))
print(round(3.2))
print(round(2.5))
print(round(3.5))
```

Output:

```
4
3
2
4
```

Python's built-in `round()` uses ties-to-even behavior for exact halfway cases. Floating-point representation can affect whether a computed value is an exact halfway case.

This differs from the rounding behavior some developers may expect from other languages or financial applications.

### 2.7.3 Truth-Value Testing

Python allows many objects to be evaluated in a Boolean context.

The following values are falsy:

- `False`
- `None`
- Numeric zero, including `0`, `0.0`, and `0j`
- Empty strings and other empty built-in collections

Most other objects are truthy.

```
# Example 2.38: Truth Values

print(bool(0))
print(bool(1))
print(bool(""))
print(bool("Python"))
print(bool([]))
print(bool([1, 2, 3]))
print(bool(None))
```

Output:

```
False
True
False
True
False
True
False
```

An empty string is not the same as `None`. An empty list is not the same as `False`.

They merely evaluate to `False` when converted to a Boolean value.

This behavior is useful for concise conditions, but it should not replace explicit checks when the distinction between missing data, empty data, and a valid zero value matters.

## 2.8 Strings

### 2.8.1 What Is a String?

A string is an immutable sequence of Unicode code points represented by the `str` type.

Strings are used for names, messages, file paths, configuration values, user input, API responses, and many other forms of textual data.

Python supports single-quoted and double-quoted string literals.

```
# Example 2.39: Creating Strings

first_message = 'Hello'
second_message = "Python"
empty_string = ""

print(first_message)
print(second_message)
print(empty_string)
```

Single and double quotes are generally interchangeable, provided the opening and closing delimiters match.

Using the appropriate quote style can reduce the need for escape characters.

```
# Example 2.40: Choosing Quote Delimiters

message1 = "It's a beautiful day."
message2 = 'She said, "Hello."'

print(message1)
print(message2)
```

Output:

```
It's a beautiful day.
She said, "Hello."
```

### 2.8.2 Escape Sequences

Escape sequences represent special characters within string literals.

Common examples include:

| Escape sequence | Meaning                                           |
| --------------- | ------------------------------------------------- |
| `\n`            | Newline                                           |
| `\t`            | Horizontal tab                                    |
| `\\`            | Backslash                                         |
| `\'`            | Single quote                                      |
| `\"`            | Double quote                                      |
| `\r`            | Carriage return                                   |
| `\b`            | Backspace                                         |
| `\uXXXX`        | Unicode code point using four hexadecimal digits  |
| `\UXXXXXXXX`    | Unicode code point using eight hexadecimal digits |

Example:

```
# Example 2.41: Escape Sequences

text = "First line\nSecond line"
tabbed_text = "Name:\tAlice"
path_fragment = "C:\\Users\\Alice"

print(text)
print(tabbed_text)
print(path_fragment)
```

Output:

```
First line
Second line
Name:   Alice
C:\Users\Alice
```

Escape sequences are interpreted when Python parses an ordinary string literal.

### 2.8.3 Multiline Strings

Triple-quoted strings can span multiple lines.

```
# Example 2.42: Multiline Strings

message = """Python is a general-purpose language.
It supports multiple programming paradigms.
It is widely used in automation and AI."""

print(message)
```

Output:

```
Python is a general-purpose language.
It supports multiple programming paradigms.
It is widely used in automation and AI.
```

Triple quotes can be either `'''` or `"""`.

They are useful for multiline text and docstrings. A docstring is a string literal used as the documentation string of a module, class, or function.

Triple quotes do not automatically remove indentation or surrounding newline characters. If exact formatting matters, inspect the resulting string rather than assuming the delimiters normalize it.

### 2.8.4 Raw Strings

A raw string literal, prefixed with `r` or `R`, changes how backslashes are interpreted in the literal.

```
# Example 2.43: Raw Strings

normal_path = "C:\\Users\\Alice"
raw_path = r"C:\Users\Alice"

print(normal_path)
print(raw_path)
print(normal_path == raw_path)
```

Output:

```
C:\Users\Alice
C:\Users\Alice
True
```

Raw strings are useful for Windows paths and regular expressions because they reduce the need to double backslashes.

A raw string is not a separate runtime string type. The resulting object is still a `str`.

Raw string syntax also has limitations: a raw string literal cannot end with an odd number of consecutive backslashes because the final backslash would escape the closing quote.

### 2.8.5 String Concatenation

The `+` operator concatenates strings.

```
# Example 2.44: String Concatenation

first_name = "Ada"
last_name = "Lovelace"

full_name = first_name + " " + last_name

print(full_name)
```

Output:

```
Ada Lovelace
```

The `*` operator can repeat a string.

```
# Example 2.45: Repeating Strings

separator = "-" * 20

print(separator)
print("Python " * 3)
```

Output:

```
--------------------
Python Python Python
```

The `+` operator does not automatically convert arbitrary objects into strings.

For example, this expression raises `TypeError`:

```
# "Age: " + 30
```

Convert the number explicitly or use a formatted string.

```
# Example 2.46: Combining Text and Numbers

age = 30

print("Age: " + str(age))
print(f"Age: {age}")
```

Output:

```
Age: 30
Age: 30
```

### 2.8.6 String Immutability

Strings are immutable.

Once a string object has been created, its characters cannot be changed in place.

```
# Example 2.47: String Immutability

word = "Python"

# The following statement raises TypeError:
# word[0] = "J"

word = "J" + word[1:]

print(word)
```

Output:

```
Jython
```

The expression creates a new string and binds `word` to it. It does not modify the original string object.

This is different from modifying an element in a list.

### 2.8.7 String Indexing

Strings are sequences, so individual characters can be accessed using indices.

Python uses zero-based indexing.

```
# Example 2.48: String Indexing

language = "Python"

print(language[0])
print(language[1])
print(language[5])
```

Output:

```
P
y
n
```

Negative indices count from the end.

```
# Example 2.49: Negative String Indices

language = "Python"

print(language[-1])
print(language[-2])
print(language[-6])
```

Output:

```
n
o
P
```

For a string of length `n`, valid single-character indices range from `-n` through `n - 1`, inclusive.

An index outside this range raises `IndexError`.

The built-in `len()` function returns the number of Unicode code points in a string.

```
# Example 2.50: String Length

text = "Python"

print(len(text))
```

Output:

```
6
```

The number returned by `len()` is not necessarily the number of bytes used to encode the string, nor is it always the number of user-perceived characters. Some visible characters consist of multiple Unicode code points.

### 2.8.8 String Slicing

Slicing extracts a subsequence.

The general form is:

```
sequence[start:stop:step]
```

The `start` index is inclusive, while `stop` is exclusive. The `step` determines the interval between selected elements.

```
# Example 2.51: String Slicing

language = "Python"

print(language[0:2])
print(language[2:6])
print(language[:3])
print(language[3:])
print(language[::2])
print(language[::-1])
```

Output:

```
Py
thon
Pyt
hon
Pto
nohtyP
```

If omitted, `start` and `stop` use defaults determined by the direction of the step.

Slicing is particularly useful because an ordinary slice that extends beyond the sequence boundaries is adjusted automatically rather than raising `IndexError`.

For example:

```
# Example 2.52: Slicing Beyond the Boundaries

text = "Python"

print(text[0:100])
print(text[100:200])
```

Output:

```
Python
```

The second result is an empty string.

This differs from indexing, where an invalid index raises an exception.

### 2.8.9 Common String Methods

Python strings provide many useful methods.

| Method         | Purpose                                               | Example                      |
| -------------- | ----------------------------------------------------- | ---------------------------- |
| `lower()`      | Convert cased characters to lowercase                 | `"PYTHON".lower()`           |
| `upper()`      | Convert cased characters to uppercase                 | `"python".upper()`           |
| `capitalize()` | Capitalize the first character and lowercase the rest | `"hELLO".capitalize()`       |
| `title()`      | Apply title-case transformations                      | `"hello world".title()`      |
| `strip()`      | Remove leading and trailing whitespace by default     | `"  hi  ".strip()`           |
| `lstrip()`     | Remove leading whitespace by default                  | `"  hi".lstrip()`            |
| `rstrip()`     | Remove trailing whitespace by default                 | `"hi  ".rstrip()`            |
| `replace()`    | Replace occurrences of a substring                    | `"banana".replace("a", "o")` |
| `find()`       | Find a substring's first index, or return `-1`        | `"python".find("th")`        |
| `count()`      | Count non-overlapping occurrences                     | `"banana".count("a")`        |
| `startswith()` | Test a prefix                                         | `"python".startswith("py")`  |
| `endswith()`   | Test a suffix                                         | `"python".endswith("on")`    |
| `split()`      | Split a string into a list                            | `"a,b,c".split(",")`         |
| `join()`       | Join strings using a separator                        | `",".join(["a", "b"])`       |

Example:

```
# Example 2.53: Common String Methods

message = "  Hello, Python!  "

print(message.strip())
print(message.lower())
print(message.upper())
print(message.replace("Python", "World"))
print(message.find("Python"))
print("banana".count("a"))
```

Output:

```
Hello, Python!
  hello, python!  
  HELLO, PYTHON!  
  Hello, World!  
9
3
```

String methods generally return new strings rather than modifying the original string.

A common misconception concerns `strip(chars)`. When an argument is supplied, it specifies a set of characters to remove from the ends, not a literal substring to remove.

For example:

```
# Example 2.54: Understanding strip()

text = "www.example.com"

print(text.strip("w.com"))
```

The method removes matching characters from both ends until it encounters a character not present in the supplied set. It does not remove a single exact suffix.

### 2.8.10 Splitting and Joining

The `split()` method converts a string into a list of strings.

```
# Example 2.55: Splitting Strings

csv_line = "Alice,Bob,Charlie"
names = csv_line.split(",")

print(names)
print(len(names))
```

Output:

```
['Alice', 'Bob', 'Charlie']
3
```

When `split()` is called without an explicit separator, Python splits on runs of whitespace and removes leading and trailing whitespace from the result.

The `join()` method performs the opposite kind of operation: it combines an iterable of strings using a separator.

```
# Example 2.56: Joining Strings

names = ["Alice", "Bob", "Charlie"]

result = " | ".join(names)

print(result)
```

Output:

```
Alice | Bob | Charlie
```

The elements supplied to `join()` must be strings. It does not automatically convert arbitrary objects.

### 2.8.11 String Formatting with f-Strings

Formatted string literals, commonly called **f-strings**, provide a convenient way to embed expressions inside strings.

```
# Example 2.57: Basic f-Strings

name = "Alice"
age = 25

message = f"My name is {name}, and I am {age} years old."

print(message)
```

Output:

```
My name is Alice, and I am 25 years old.
```

Expressions can be evaluated inside replacement fields.

```
# Example 2.58: Expressions in f-Strings

a = 10
b = 20

print(f"The sum is {a + b}.")
print(f"The product is {a * b}.")
```

Output:

```
The sum is 30.
The product is 200.
```

Format specifications control presentation.

```
# Example 2.59: Numeric Formatting

price = 19.9876
percentage = 0.875

print(f"Price: {price:.2f}")
print(f"Percentage: {percentage:.1%}")
```

Output:

```
Price: 19.99
Percentage: 87.5%
```

Here:

- `.2f` formats a number with two digits after the decimal point.
- `.1%` formats a number as a percentage with one digit after the decimal point.

F-strings are generally preferable to manually concatenating multiple strings and converted values.

Python also supports other formatting mechanisms, including `str.format()` and the older `%` formatting operator. F-strings are the recommended default for many modern Python applications.

## 2.9 Standard Input and Output

### 2.9.1 Standard Output: `print()`

The built-in `print()` function writes textual representations of its arguments to a text stream. By default, that stream is standard output.

```
# Example 2.60: Basic Output

print("Hello, Python!")
print(42)
print(3.14)
print(True)
```

Output:

```
Hello, Python!
42
3.14
True
```

`print()` can accept multiple arguments.

```
# Example 2.61: Multiple Output Arguments

name = "Alice"
age = 25

print("Name:", name, "Age:", age)
```

Output:

```
Name: Alice Age: 25
```

By default, `print()` separates arguments with a space and ends the output with a newline.

Its important parameters are:

- `sep`: the separator between arguments
- `end`: the string appended after the final argument
- `file`: the destination text stream
- `flush`: whether to flush the stream immediately

Example:

```
# Example 2.62: Customizing print()

print("Python", "Java", "Go", sep=" | ")
print("First line", end=" ")
print("Second part")
```

Output:

```
Python | Java | Go
First line Second part
```

These parameters are useful for formatting output and controlling when buffered output becomes visible.

### 2.9.2 Standard Input: `input()`

The built-in `input()` function reads a line from standard input.

It optionally displays a prompt before reading.

```
# Example 2.63: Reading User Input

name = input("Enter your name: ")

print(f"Hello, {name}!")
```

Example interaction:

```
Enter your name: Alice
Hello, Alice!
```

The prompt is displayed without automatically adding a newline before the user enters input.

Most importantly, `input()` returns a string.

Even if the user enters digits, the result is still of type `str`.

```
# Example 2.64: The Type Returned by input()

value = input("Enter a value: ")

print(value)
print(type(value))
```

If the user enters `123`, the output is:

```
123
<class 'str'>
```

This behavior must be remembered when reading numeric input.

### 2.9.3 Converting Input

To perform arithmetic on numeric input, convert it explicitly.

```
# Example 2.65: Reading an Integer

age_text = input("Enter your age: ")
age = int(age_text)

print(f"Next year, you will be {age + 1}.")
```

Example interaction:

```
Enter your age: 30
Next year, you will be 31.
```

For floating-point input:

```
# Example 2.66: Reading a Floating-Point Number

price_text = input("Enter the price: ")
price = float(price_text)

print(f"Price: {price:.2f}")
```

Example interaction:

```
Enter the price: 19.99
Price: 19.99
```

If the input does not represent a valid number, conversion may raise `ValueError`.

Production programs should handle invalid input appropriately, usually with exception handling and validation. That topic will be covered more systematically when exceptions are introduced.

### 2.9.4 A Complete Input-Process-Output Program

Most simple interactive programs follow a basic pattern:

1. Read input.
2. Convert or validate it if necessary.
3. Process the resulting values.
4. Display the result.

```
# Example 2.67: Simple Calculator

first_number = float(input("Enter the first number: "))
second_number = float(input("Enter the second number: "))

total = first_number + second_number

print(f"The sum is {total}.")
```

Example interaction:

```
Enter the first number: 12.5
Enter the second number: 7.5
The sum is 20.0.
```

This small program demonstrates several fundamental ideas together: input, type conversion, assignment, arithmetic, and formatted output.

### 2.9.5 Output to a File

The `file` parameter of `print()` can direct output to an open text file.

```
# Example 2.68: Writing Output to a File

with open("output.txt", "w", encoding="utf-8") as file:
    print("Hello, Python!", file=file)
    print("This line is stored in a file.", file=file)
```

This program creates or overwrites `output.txt` in the working directory.

The `with` statement ensures that the file is closed when the block finishes, including when an exception occurs.

File handling is an important extension of input and output, although the full subject of files, paths, encodings, and exception handling deserves its own chapter.

## 2.10 Comments, Whitespace, and Basic Code Structure

### 2.10.1 Comments

A comment begins with `#` and continues to the end of the physical line.

```
# Example 2.69: Comments

# Store the user's age.
age = 30

# Calculate the age next year.
next_year_age = age + 1

print(next_year_age)
```

Comments explain intent, assumptions, or decisions that are not obvious from the code.

They should not merely repeat what the code already states.

For example, a comment such as `# Add one to age` above `age + 1` adds little information. A comment explaining why a particular business rule requires adding one may be useful.

### 2.10.2 Whitespace

Whitespace separates tokens and can affect how code is parsed.

Python generally ignores leading and trailing spaces within expressions where they do not affect syntax, but indentation is significant in compound statements.

For example:

```
# Example 2.70: Indentation

if True:
    print("This statement belongs to the if block.")
```

The indented statement belongs to the `if` block.

Inconsistent indentation can produce `IndentationError` or alter the structure of a program.

Python code conventionally uses four spaces per indentation level. Tabs and spaces should not be mixed carelessly.

### 2.10.3 Line Length and Readability

Python permits long expressions, but readable code is easier to maintain and debug.

```
# Example 2.71: Clear Variable Names

unit_price = 19.99
quantity = 3
total_price = unit_price * quantity

print(f"Total price: {total_price:.2f}")
```

Descriptive names communicate intent without requiring a separate explanation.

PEP 8 recommends limiting most lines to 79 characters, with somewhat different guidance for comments and docstrings. Projects may adopt different conventions, but consistency is more important than mechanically obeying a number in every circumstance.

### 2.10.4 The Importance of Readability

Python emphasizes readable code. Indentation, naming, whitespace, and formatting are not decorative details; they help make program structure visible.

A program is written once but may be read many times. The person who eventually maintains it may be the original author after several months, when the reasoning behind every abbreviated name has conveniently disappeared.

## 2.11 Common Beginner Mistakes

The following mistakes are worth recognizing early.

### Mistake 1: Confusing `=` with `==`

Incorrect assumption:

```
# This is an assignment, not a comparison:
number = 10
```

Use `==` when testing equality.

### Mistake 2: Assuming `input()` Returns a Number

```
# Example 2.72: Input Type Error

# If the user enters 10:
# value = input("Enter a number: ")
# print(value + 5)  # TypeError
```

The input is a string. Convert it to the required numeric type first.

### Mistake 3: Assuming Assignment Copies an Object

```
# Example 2.73: Shared References

first = [1, 2]
second = first

second.append(3)

print(first)
```

The output is `[1, 2, 3]`, because both names refer to the same list.

### Mistake 4: Attempting to Modify a String in Place

```
# Example 2.74: Immutable Strings

word = "Python"

# word[0] = "J"  # TypeError
```

Create a new string instead.

### Mistake 5: Using `is` Instead of `==`

The `==` operator tests equality. The `is` operator tests object identity.

```python
# Example 2.75: Equality Versus Identity

first = [1, 2, 3]
second = [1, 2, 3]
third = first

print(first == second)
print(first is second)
print(first is third)
```

Output:

```
True
False
True
```

The first two lists have equal contents but are distinct objects. The third name refers to the same object as `first`.

For ordinary value comparisons, use `==`. Use `is` when identity is the intended property, especially when checking for `None`.

### Mistake 6: Assuming `int()` Rounds

```
# Example 2.76: Truncation Rather Than Rounding

print(int(4.9))
print(int(-4.9))
```

Output:

```
4
-4
```

`int()` truncates a floating-point value toward zero. It does not perform ordinary nearest-integer rounding.

### Mistake 7: Assuming an Empty Value Is `None`

```
# Example 2.77: Distinguishing Empty Values

print("" is None)
print([] is None)
print(0 is None)
```

All three expressions evaluate to `False`.

An empty string, an empty list, zero, and `None` represent different states. Choose the correct check for the problem being solved.

## 2.12 Summary

This chapter introduced the fundamental mechanisms Python uses to represent and manipulate data.

### Literals and Expressions

- Literals represent values directly in source code.
- Expressions combine literals, names, operators, and function calls to produce results.
- Python supports integer, floating-point, string, Boolean, and other literals.
- Floating-point arithmetic may produce small representation errors.

### Variables and Assignment

- A Python variable is a name bound to an object.
- Assignment uses `=`, while equality comparison uses `==`.
- A name can be rebound to an object of a different type.
- Assigning one name to another does not necessarily copy the underlying object.
- Rebinding a name and mutating an object are different operations.

### Identifiers

- Identifiers name variables, functions, classes, and other program elements.
- Identifiers are case-sensitive and must follow Python's naming rules.
- Keywords cannot be used as ordinary identifiers.
- Following naming conventions improves readability and maintainability.

### Data Types

- Python includes numeric types such as `int`, `float`, and `complex`.
- `bool` represents truth values, while `None` represents the absence of a value.
- `type()` inspects an object's type; `isinstance()` checks its relationship to a type.
- Mutable objects can change in place; immutable objects cannot.
- Type conversion may fail or lose information.

### Strings

- Strings are immutable sequences of Unicode code points.
- Strings support concatenation, repetition, indexing, slicing, and numerous methods.
- F-strings provide readable and flexible string formatting.
- String indexing and slicing use zero-based positions, with the slice's stop index excluded.

### Input and Output

- `print()` writes output to a text stream.
- `input()` reads a line and returns a string.
- Numeric input must be converted before numeric operations can be performed.
- Files can serve as input or output streams, and `with` provides reliable resource management.

### Final Perspective

The most important conceptual distinction in this chapter is the difference between a **name**, an **object**, and an **operation performed on that object**.

A name does not permanently possess a type. Assignment binds names to objects; mutation changes mutable objects; and expressions evaluate to values that can be used in subsequent operations.

Once these distinctions are clear, Python's concise syntax becomes easier to understand rather than merely easier to memorize.

The next chapter should introduce **Operators and Expressions**, covering arithmetic, comparison, logical operations, assignment operators, operator precedence, and the evaluation of compound expressions.