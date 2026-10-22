# Chapter 2 — Python Fundamentals: Objects, Variables, and Basic I/O

## 1. Introduction

Every computer program manipulates data. Before a program can solve a mathematical problem, process a document, communicate with a database, or interact with an artificial intelligence model, it must represent information in a form that the computer can process.

Python provides a concise syntax for representing values, associating names with objects, transforming data, and exchanging information with the outside world.

This chapter introduces the fundamental elements of Python programming:

- Literals and expressions
- Variables and object references
- Variable reassignment and type conversion
- Identifiers, keywords, and naming conventions
- Built-in data types
- Strings and string operations
- Standard input and output
- Common errors and essential programming practices

These concepts form the foundation upon which more sophisticated programs are constructed. A programmer who understands them thoroughly will find subsequent topics considerably easier to master.

## 2. Literals and Expressions

### 2.1 What Is a Literal?

A **literal** is a notation that directly represents a value in source code.

Consider the following examples:

```
42
3.14159
"Hello, Python!"
True
None
```

Each expression represents a value without requiring a variable to be defined first.

Python supports several categories of literals, including numeric, string, Boolean, and special literals.

```
age = 30
price = 19.99
message = "Welcome"
is_active = True
result = None
```

Here, `30`, `19.99`, `"Welcome"`, `True`, and `None` are literals. The names on the left-hand side are identifiers used to refer to the corresponding objects.

A literal is not a variable. The literal `30` represents a value; the variable name `age` provides a name through which a program can access an object.

### 2.2 Numeric Literals

Python supports integers, floating-point numbers, and complex numbers.

**Integer literals**

```
decimal = 42
negative = -17
zero = 0
```

Integer literals can also be expressed using different number systems:

```
decimal = 42       # Decimal: base 10
binary = 0b101010  # Binary: base 2
octal = 0o52       # Octal: base 8
hexadecimal = 0x2A # Hexadecimal: base 16
```

All four variables represent the same integer value.

Underscores can improve the readability of long numeric literals:

```
population = 1_400_000_000
file_size = 2_048_576
```

The underscores are ignored when Python interprets the numbers.

**Floating-point literals**

```
pi = 3.14159
temperature = -12.5
scientific = 6.02e23
small_number = 1.5e-4
```

Scientific notation uses `e` or `E` to represent a power of ten. Thus, `6.02e23` means (6.02 \times 10^{23}).

Python's built-in `float` type normally uses IEEE 754 double-precision binary floating-point representation. Consequently, many decimal fractions cannot be represented exactly.

```
print(0.1 + 0.2)
```

Output:

```
0.30000000000000004
```

This is a consequence of binary floating-point representation, not a defect in Python's arithmetic implementation.

For calculations requiring exact decimal arithmetic, such as financial calculations, consider the `decimal.Decimal` type rather than assuming that `float` represents every decimal value exactly.

**Complex literals**

```
z = 3 + 4j

print(z.real)  # 3.0
print(z.imag)  # 4.0
```

Python uses `j` or `J` for the imaginary component of a complex number.

### 2.3 String Literals

String literals represent text and can be enclosed in single quotes, double quotes, or triple quotes.

```
single = 'Hello'
double = "Hello"
multiline = """This is a
multiline string."""
```

Single-quoted and double-quoted strings are equivalent in their basic behavior.

Triple-quoted strings can span multiple lines and are commonly used for multiline text and documentation strings.

### 2.4 Boolean and Special Literals

Python has two Boolean literals:

```
True
False
```

Their capitalization is significant. `true`, `false`, `TRUE`, and `FALSE` are not Python Boolean literals.

Python also defines the special literal:

```
None
```

`None` represents the absence of a value or the lack of a meaningful result. It is not equivalent to zero, an empty string, or `False`.

```
result = None
```

The object represented by `None` has the type `NoneType`.

### 2.5 Expressions

An **expression** is a combination of literals, names, operators, and function calls that Python evaluates to produce a value.

```
10 + 20
price * quantity
"Hello, " + "world!"
len("Python")
```

Expressions can be assigned to variables:

```
subtotal = 19.99 * 3
```

They can also be nested:

```
total = (10 + 20) * 2
```

Parentheses make the intended order of evaluation explicit. Although Python defines operator precedence, explicit grouping often improves readability.

A statement, by contrast, performs an action. An assignment such as `total = 100` is a statement, while `100` is a literal and `10 + 20` is an expression.

## 3. Variables and Object References

### 3.1 What Is a Variable?

A variable is a name associated with an object in a program's execution environment.

In Python, assignment binds a name to an object. It does not require the programmer to declare the variable's type in advance.

```
age = 30
name = "Alice"
height = 1.72
```

The assignment operator `=` binds each name to the object produced by the expression on its right-hand side.

Unlike Java, Python does not require declarations such as:

```
int age = 30;
String name = "Alice";
```

The following Python code is valid:

```
value = 100
value = "one hundred"
```

The name `value` first refers to an integer object and subsequently refers to a string object.

This is possible because Python uses dynamic typing: types belong to objects, while names can be rebound to objects of different types.

### 3.2 Assignment Does Not Mean Mathematical Equality

The symbol `=` represents assignment in Python, not a test of equality.

```
x = 10
x = x + 5

print(x)  # 15
```

The second statement evaluates the expression `x + 5` using the current value associated with `x`, then binds `x` to the resulting object.

To compare two values, use `==`:

```
print(10 == 10)  # True
print(10 == 20)  # False
```

Confusing `=` with `==` is a basic error that can undermine program logic.

### 3.3 Names and Objects

Consider the following code:

```
x = 100
y = x

x = 200

print(x)  # 200
print(y)  # 100
```

Initially, both names refer to the integer object representing `100`. The final assignment rebinds `x`; it does not modify the integer object or automatically change `y`.

A useful mental model is that names are labels attached to objects, rather than boxes that permanently contain values of a declared type.

The analogy has limits: Python's actual execution model involves namespaces, object identity, references, and implementation-specific memory management. Nevertheless, it is useful for understanding assignment.

### 3.4 Object Identity and Equality

Python distinguishes between object identity and value equality.

- `==` tests whether two objects compare equal in value.
- `is` tests whether two references identify the same object.

```
a = [1, 2, 3]
b = [1, 2, 3]
c = a

print(a == b)  # True
print(a is b)  # False
print(a is c)  # True
```

The lists `a` and `b` contain equal values but are distinct objects. The names `a` and `c` refer to the same list.

Use `is` when identity is the intended question, particularly when checking for `None`:

```
result = None

if result is None:
    print("No result is available.")
```

Do not use `is` as a general substitute for `==`. Object interning and implementation optimizations can make identity behavior appear surprising for certain immutable objects.

### 3.5 Mutable and Immutable Objects

Objects differ in whether their contents can be changed after creation.

**Immutable types** include:

- `int`
- `float`
- `bool`
- `complex`
- `str`
- `tuple` (with an important qualification: its elements may themselves be mutable)
- `frozenset`
- `bytes`

**Mutable types** include:

- `list`
- `dict`
- `set`
- `bytearray`

Consider an immutable object:

```
x = 10
x += 1
```

The integer object is not modified in place. The operation produces the value `11`, and the name `x` is rebound accordingly.

Now consider a mutable object:

```
numbers = [1, 2, 3]
alias = numbers

numbers.append(4)

print(alias)  # [1, 2, 3, 4]
```

Both names refer to the same list. Mutating that list makes the change observable through either name.

This distinction is important when passing data to functions, copying collections, and diagnosing unexpected changes in program state.

### 3.6 Multiple Assignment

Python allows several names to be bound in one statement:

```
x, y, z = 10, 20, 30
```

The right-hand side is evaluated, and the resulting values are unpacked into the targets on the left.

The number of targets must match the number of unpacked values:

```
a, b = 1, 2
```

The following statement raises `ValueError` because the number of values does not match the number of targets:

```
a, b = 1, 2, 3
```

Python also supports chained assignment:

```
a = b = c = 0
```

All three names are bound to the same resulting object. For immutable integers, this is usually unremarkable; with mutable objects, it can be significant:

```
a = b = []

a.append(1)

print(a)  # [1]
print(b)  # [1]
```

Only one list was created. Both names refer to it.

### 3.7 Swapping Variables

Python supports swapping values without a temporary variable:

```
a = 10
b = 20

a, b = b, a

print(a)  # 20
print(b)  # 10
```

This works through iterable unpacking. It is not a special-purpose swapping operator.

## 4. Variable Reassignment and Type Conversion

The phrase *variable transformation* can refer to several distinct operations. They should not be confused: rebinding a name, modifying an object, and converting a value are different processes.

### 4.1 Reassignment

Reassignment changes the object associated with a name.

```
value = 10
value = 3.14
value = "Python"
```

No explicit declaration is required when the name is rebound to a different type.

This flexibility is convenient, but it also places responsibility on the programmer to maintain consistent program logic. Reusing a name for unrelated kinds of values can make code harder to understand and debug.

### 4.2 Augmented Assignment

Augmented assignment combines an operation with assignment.

```
x = 10

x += 5
x -= 2
x *= 3
x /= 2

print(x)  # 19.5
```

Common augmented assignment operators include:

| Operator | General meaning               |
| -------- | ----------------------------- |
| `+=`     | Addition and assignment       |
| `-=`     | Subtraction and assignment    |
| `*=`     | Multiplication and assignment |
| `/=`     | True division and assignment  |
| `//=`    | Floor division and assignment |
| `%=`     | Remainder and assignment      |
| `**=`    | Exponentiation and assignment |

For immutable numeric objects, augmented assignment typically produces a new value and rebinds the name. For mutable objects, an in-place modification may occur.

```
numbers = [1, 2]
numbers += [3]

print(numbers)  # [1, 2, 3]
```

The precise behavior depends on the type's implementation of the relevant operations. Augmented assignment should not be assumed to behave identically to an ordinary assignment in every situation.

### 4.3 Explicit Type Conversion

Python provides built-in constructors that can convert certain values to other types.

```
int("123")       # 123
float("3.14")    # 3.14
str(123)         # '123'
bool(1)          # True
list("abc")      # ['a', 'b', 'c']
```

Conversion is not always possible. For example:

```
int("hello")
```

This raises `ValueError` because `"hello"` does not represent a valid integer in the expected format.

The constructor `int()` can also convert a floating-point number by truncating its fractional part toward zero:

```
int(3.9)    # 3
int(-3.9)   # -3
```

It does not round to the nearest integer.

If rounding is intended, use `round()` with an understanding of its behavior:

```
round(3.7)  # 4
round(2.5)  # 2
```

Python's built-in `round()` uses ties-to-even rounding for exact halfway cases, rather than always rounding halves upward. Binary floating-point representation can also affect which values are treated as exact halfway cases.

### 4.4 Numeric Conversion and Division

Python distinguishes true division from floor division.

```
print(7 / 2)   # 3.5
print(7 // 2)  # 3
```

The `/` operator performs true division. The `//` operator performs floor division, rounding the mathematical quotient downward toward negative infinity.

```
print(-7 // 2)  # -4
```

This differs from truncation toward zero. In Java, integer division truncates toward zero; Python's floor division has different behavior for negative operands.

The remainder operator is related to floor division:

```
print(7 % 2)    # 1
print(-7 % 2)   # 1
```

Python's modulo result is consistent with the divisor's sign for nonzero divisors. This is another detail worth remembering when porting numerical code from Java.

### 4.5 Type Checking

The built-in `type()` function reports an object's type:

```
value = 42

print(type(value))  # <class 'int'>
```

The `isinstance()` function tests whether an object is an instance of a specified type or its subclasses:

```
print(isinstance(42, int))    # True
print(isinstance("42", int))  # False
```

Prefer `isinstance()` when checking compatibility with a type hierarchy.

One notable detail is that `bool` is a subclass of `int`:

```
print(isinstance(True, int))  # True
print(True + 1)               # 2
```

Although this behavior is intentional, Boolean values should not casually be treated as ordinary integers in application logic.

## 5. Identifiers, Keywords, and Naming Conventions

### 5.1 Identifiers

An **identifier** is a name used to identify a program element, such as a variable, function, class, or module.

Valid examples include:

```
age = 30
user_name = "Alice"
_private_value = 10
count2 = 5
```

Python identifiers can contain Unicode characters, but conventional Python code generally uses English words and ASCII letters for maintainability and compatibility.

### 5.2 Identifier Rules

Python identifiers follow these rules:

1. An identifier may contain letters, underscores (`_`), and digits.
2. It must not begin with a digit.
3. It must not be a reserved keyword.
4. Identifiers are case-sensitive.
5. Spaces and punctuation such as hyphens are not permitted within an ordinary identifier.

Examples:

```
user_name = "Alice"  # Valid
_user_name = "Alice" # Valid
user2 = "Alice"      # Valid
```

Invalid examples:

```
2user = "Alice"      # SyntaxError
user-name = "Alice"  # Parsed as subtraction
class = "Python"     # SyntaxError: reserved keyword
```

The last example fails because `class` is a Python keyword.

### 5.3 Case Sensitivity

Python distinguishes between uppercase and lowercase letters.

```
name = "Alice"
Name = "Bob"

print(name)  # Alice
print(Name)  # Bob
```

These are separate identifiers. Consistent capitalization is therefore essential.

### 5.4 Keywords

Keywords have predefined grammatical meanings and cannot be used as ordinary identifiers.

Examples include:

```
False  None  True  and  as  assert  async  await
break  class  continue  def  del  elif  else
except  finally  for  from  global  if  import
in  is  lambda  nonlocal  not  or  pass  raise
return  try  while  with  yield
```

The complete keyword set depends on the Python version. To inspect the keywords recognized by the interpreter:

```
import keyword

print(keyword.kwlist)
print(keyword.iskeyword("class"))  # True
```

Python also has *soft keywords*, which act as keywords only in particular syntactic contexts. Their status and availability can vary by version.

### 5.5 Naming Conventions

Python's standard style recommendations are documented in PEP 8.

| Element       | Conventional style    | Example             |
| ------------- | --------------------- | ------------------- |
| Variable      | `snake_case`          | `user_name`         |
| Function      | `snake_case`          | `calculate_total()` |
| Class         | `PascalCase`          | `UserAccount`       |
| Constant      | `UPPER_SNAKE_CASE`    | `MAX_RETRIES`       |
| Module        | Short, lowercase name | `file_utils`        |
| Internal name | Leading underscore    | `_cache`            |

Example:

```
MAX_RETRIES = 3

def calculate_total(price, quantity):
    return price * quantity

class ShoppingCart:
    pass
```

Python does not enforce constant immutability through uppercase naming. `MAX_RETRIES` is still an ordinary name that can be rebound; the capitalization communicates programmer intent.

A single leading underscore conventionally signals that a name is intended for internal use. It does not create a strict access restriction.

Double leading underscores have special behavior inside class definitions, where name mangling is applied in certain cases. They should not be used indiscriminately as a substitute for access modifiers.

### 5.6 Avoid Shadowing Built-in Names

Avoid naming variables after commonly used built-in functions or types.

Poor practice:

```
list = [1, 2, 3]
str = "hello"
sum = 100
```

These assignments hide the corresponding built-in names in the current namespace. Subsequent attempts to call `list()`, `str()`, or `sum()` may fail or behave unexpectedly.

Prefer:

```
numbers = [1, 2, 3]
message = "hello"
total = 100
```

Naming is not merely cosmetic. Clear names reduce the cognitive burden of understanding and maintaining a program.

## 6. Built-in Data Types

Python is dynamically typed, but it is not untyped. Objects have types, and those types determine the operations the objects support.

The following table summarizes the principal built-in data types.

| Category            | Type        | Example             |
| ------------------- | ----------- | ------------------- |
| Integer             | `int`       | `42`                |
| Floating-point      | `float`     | `3.14`              |
| Complex number      | `complex`   | `2 + 3j`            |
| Boolean             | `bool`      | `True`              |
| Text                | `str`       | `"Python"`          |
| List                | `list`      | `[1, 2, 3]`         |
| Tuple               | `tuple`     | `(1, 2, 3)`         |
| Range               | `range`     | `range(5)`          |
| Dictionary          | `dict`      | `{"name": "Alice"}` |
| Set                 | `set`       | `{1, 2, 3}`         |
| Immutable set       | `frozenset` | `frozenset({1, 2})` |
| Binary data         | `bytes`     | `b"ABC"`            |
| Mutable binary data | `bytearray` | `bytearray(b"ABC")` |
| Null-like value     | `NoneType`  | `None`              |

This chapter focuses on scalar values and strings. Lists, tuples, dictionaries, sets, and other collection types will receive more detailed treatment in a dedicated chapter.

### 6.1 Dynamic Typing and Strong Typing

Python uses dynamic typing: the type associated with a name can change when the name is rebound.

```
value = 10
value = "ten"
```

Python is also commonly described as strongly typed. In general, it does not silently combine incompatible types merely because an operation might appear convenient.

```
"10" + 5
```

This raises `TypeError`. Python does not automatically interpret the string `"10"` as the integer `10` for this operation.

Explicit conversion is required:

```
int("10") + 5  # 15
```

Dynamic typing and strong typing describe different properties. Dynamic typing concerns when types are associated with values and checked; strong typing concerns how strictly operations respect type distinctions. The terminology is not perfectly uniform across all programming-language theory, but this distinction is useful in practical Python development.

### 6.2 Truth Values

Python has the Boolean values `True` and `False`. Many other objects can also be evaluated in a Boolean context.

Common false values include:

```
False
None
0
0.0
""
[]
()
{}
set()
```

Most other objects are truthy, including nonempty strings and collections.

```
if "Python":
    print("This string is truthy.")

if not "":
    print("An empty string is falsy.")
```

The `bool()` function explicitly evaluates an object's truth value:

```
bool(0)        # False
bool(1)        # True
bool("")       # False
bool("False")  # True
```

The final example is particularly important: the string `"False"` is nonempty, so it is truthy. Its textual meaning does not determine its Boolean value.

Custom objects can define their truth behavior through special methods such as `__bool__()` or `__len__()`. If neither supplies a falsy result, instances are ordinarily truthy.

### 6.3 The Importance of `None`

`None` is a singleton object commonly used to represent the absence of a value.

```
result = None

if result is None:
    print("The result has not been provided.")
```

A function that does not explicitly return a value returns `None`:

```
def log_message(message):
    print(message)

result = log_message("System started")

print(result)  # None
```

The function performs an action but does not return a meaningful result.

Remember that `None`, `False`, `0`, and `""` are distinct values, even though all are falsy in Boolean contexts.

## 7. Strings

### 7.1 Definition

A string is an immutable sequence of Unicode code points represented by Python's built-in `str` type.

```
language = "Python"
message = 'Learning Python is worthwhile.'
```

Strings are used to represent names, messages, source code, file contents, and other textual data.

### 7.2 Quotation Marks

Single and double quotes can both delimit strings.

```
message1 = "It's a programming language."
message2 = 'He said, "Hello."'
```

This flexibility reduces the need for escaping quotation marks.

Triple quotes are useful for multiline text:

```
description = """Python is a general-purpose language.
It supports several programming paradigms.
Its syntax emphasizes readability."""
```

Triple-quoted strings preserve embedded newline characters. They are also commonly used for docstrings, which document modules, classes, and functions.

### 7.3 Escape Sequences

Escape sequences represent characters that cannot conveniently be written directly within a string literal.

| Sequence     | Meaning                                                      |
| ------------ | ------------------------------------------------------------ |
| `\n`         | Newline                                                      |
| `\t`         | Horizontal tab                                               |
| `\\`         | Backslash                                                    |
| `\'`         | Single quotation mark                                        |
| `\"`         | Double quotation mark                                        |
| `\r`         | Carriage return                                              |
| `\b`         | Backspace                                                    |
| `\xhh`       | Character specified by a hexadecimal code point value in the range `00`–`FF` |
| `\uXXXX`     | Unicode code point using four hexadecimal digits             |
| `\UXXXXXXXX` | Unicode code point using eight hexadecimal digits            |

Example:

```
text = "First line\nSecond line"
print(text)
```

Output:

```
First line
Second line
```

A backslash can also introduce a Unicode escape:

```
copyright_symbol = "\u00A9"
print(copyright_symbol)  # ©
```

Raw string literals suppress most backslash escape processing:

```
path = r"C:\Users\Alice\Documents"
print(path)
```

Raw strings are especially useful for regular expressions and Windows-style paths. However, a raw string literal cannot end with an odd number of backslashes, because the final backslash would escape the closing quotation mark.

### 7.4 String Concatenation and Repetition

The `+` operator concatenates strings:

```
first = "Hello"
second = "World"

message = first + ", " + second + "!"
print(message)
```

Output:

```
Hello, World!
```

The `*` operator repeats a string when combined with an integer:

```
print("Python " * 3)
```

Output:

```
Python Python Python
```

Concatenating a string and an integer directly raises `TypeError`:

```
age = 30

# print("Age: " + age)  # TypeError
print("Age: " + str(age))
```

For mixed text and values, formatted strings are generally preferable.

### 7.5 String Immutability

Strings are immutable. Their individual characters cannot be changed in place.

```
word = "Python"

# word[0] = "J"  # TypeError
```

To obtain modified text, create a new string:

```
word = "J" + word[1:]

print(word)  # Jython
```

This operation does not mutate the original string object. The resulting string is assigned to `word`.

### 7.6 Indexing

Python strings use zero-based indexing.

```
language = "Python"

print(language[0])   # P
print(language[1])   # y
print(language[-1])  # n
print(language[-2])  # o
```

Positive indexes count from the beginning, while negative indexes count from the end.

An index outside the valid range raises `IndexError`:

```
language = "Python"

# print(language[10])  # IndexError
```

### 7.7 Slicing

Slicing extracts a subsequence of a string.

The general form is:

```
string[start:stop:step]
```

The `start` index is included, while the `stop` index is excluded.

```
text = "Python Programming"

print(text[0:6])   # Python
print(text[7:])    # Programming
print(text[:6])    # Python
print(text[::2])   # Every second character
print(text[::-1])  # Reversed string
```

Omitted boundaries use defaults appropriate to the direction of traversal. A zero step is invalid and raises `ValueError`.

Slicing is particularly useful for extracting prefixes, suffixes, and substrings without manually constructing loops.

### 7.8 String Length

The built-in `len()` function returns the number of elements in a string. For `str`, these elements are Unicode code points, not necessarily user-perceived characters.

```
text = "Python"

print(len(text))  # 6
```

For many ordinary English strings, the distinction is invisible. However, some visible characters consist of multiple Unicode code points, such as certain emoji and letters combined with diacritical marks.

Therefore, `len()` does not always equal the number of characters a person perceives on screen.

### 7.9 Common String Methods

Strings provide methods for common text-processing operations.

```
text = "  Hello, Python!  "

print(text.lower())                  # Lowercase
print(text.upper())                  # Uppercase
print(text.strip())                  # Remove surrounding whitespace
print(text.replace("Python", "Java"))
print(text.startswith("  Hello"))    # True
print(text.endswith("  "))           # True
```

Additional methods include:

```
"hello world".title()
"hello world".capitalize()
"apple,banana,cherry".split(",")
"-".join(["2026", "10", "22"])
"python".find("th")
"python".count("o")
"12345".isdigit()
"python".isalpha()
"hello123".isalnum()
```

Important distinctions:

- `strip()` removes leading and trailing characters according to its argument; without an argument, it removes surrounding whitespace.
- `replace()` returns a new string.
- `split()` divides a string into a list of substrings.
- `join()` combines an iterable of strings using the receiving string as a separator.
- `find()` returns `-1` when the requested substring is not found.
- `index()` behaves similarly to `find()`, but raises `ValueError` when the substring is absent.

These methods do not modify the original string.

### 7.10 String Formatting

String formatting inserts values into textual templates. Python offers several approaches.

**F-strings**

Formatted string literals, commonly called f-strings, are usually the clearest choice for modern Python code.

```
name = "Alice"
age = 30

message = f"My name is {name}, and I am {age} years old."
print(message)
```

Expressions can appear inside the braces:

```
x = 10
y = 20

print(f"The sum is {x + y}.")
```

Formatting specifications control the representation of values:

```
price = 19.9876
ratio = 0.875
large_number = 1234567

print(f"Price: {price:.2f}")
print(f"Ratio: {ratio:.1%}")
print(f"Number: {large_number:,}")
```

Output:

```
Price: 19.99
Ratio: 87.5%
Number: 1,234,567
```

Common formatting specifications include:

| Specification | Meaning                                                      |
| ------------- | ------------------------------------------------------------ |
| `:.2f`        | Fixed-point number with two decimal places                   |
| `:.3e`        | Scientific notation with three digits after the decimal point |
| `:%`          | Percentage representation                                    |
| `:,`          | Thousands separator                                          |
| `:>10`        | Right-align within a field of width 10                       |
| `:<10`        | Left-align within a field of width 10                        |
| `:^10`        | Center within a field of width 10                            |
| `:04d`        | Integer formatted with a minimum width of four, padded with zeros |

Example:

```
number = 42

print(f"{number:04d}")  # 0042
print(f"{'Python':^12}")  # Centered text
```

**The** `**format()**` **method**

```
message = "Hello, {}!".format("Python")
print(message)
```

Named and positional fields are also supported:

```
message = "{name} scored {score} points.".format(
    name="Alice",
    score=95
)
```

**The** `**%**` **operator**

Older Python code may use printf-style formatting:

```
name = "Alice"
score = 95

message = "%s scored %d points." % (name, score)
```

This style remains relevant when maintaining legacy code, but f-strings are generally preferable for straightforward formatting in modern Python.

### 7.11 Unicode and Text Encoding

Python strings represent Unicode text. A `str` object is not itself a sequence of UTF-8 bytes.

Encoding converts text into bytes; decoding converts bytes into text.

```
text = "Hello, 世界"

encoded = text.encode("utf-8")
decoded = encoded.decode("utf-8")

print(encoded)
print(decoded)
```

The first result is a `bytes` object, while the second is a `str`.

When reading or writing text files, specify the encoding explicitly when appropriate:

```
with open("message.txt", "w", encoding="utf-8") as file:
    file.write("Hello, 世界")
```

Confusing text with its encoded byte representation can cause data corruption or decoding errors, especially when handling files, network protocols, and external systems.

## 8. Standard Input and Output

Programs often need to receive information from users and display results. Python provides built-in functions for these basic operations.

### 8.1 The `print()` Function

The `print()` function writes textual representations of objects to a text stream, normally standard output.

```
print("Hello, Python!")
print(42)
print(3.14)
```

Multiple arguments are separated by a space by default:

```
print("Python", "is", "powerful")
```

Output:

```
Python is powerful
```

The principal parameters are:

```
print(*objects, sep=" ", end="\n", file=None, flush=False)
```

- `objects`: The objects to display.
- `sep`: The separator inserted between objects.
- `end`: The text appended after the final object.
- `file`: The destination text stream; standard output is used by default.
- `flush`: Whether to force the stream to flush immediately.

Examples:

```
print("2026", "10", "22", sep="-")
print("Hello", end=" ")
print("World")
```

Output:

```
2026-10-22
Hello World
```

By default, `print()` ends with a newline. Setting `end=""` suppresses that newline.

The `flush` parameter can be useful when output must become visible immediately, such as in progress reporting or interactive applications. Its practical effect depends on the output stream.

### 8.2 Printing Variables and Objects

`print()` can display several values in one call:

```
name = "Alice"
age = 30

print("Name:", name)
print("Age:", age)
```

Python obtains a textual representation of each object. The representation used by `print()` is generally based on `str()`, which may differ from the representation produced by `repr()`.

```
text = "Hello\nWorld"

print(str(text))
print(repr(text))
```

Output:

```
Hello
World
'Hello\nWorld'
```

`str()` is intended to provide a readable textual representation. `repr()` aims to provide an informative representation useful for debugging and inspection; for some types, it may resemble valid source syntax.

### 8.3 The `input()` Function

The `input()` function reads a line of text from standard input.

```
name = input("Enter your name: ")

print(f"Hello, {name}!")
```

The optional prompt is displayed without automatically adding a newline. The function then waits for a line of input.

**Crucially,** `**input()**` **returns a string.** It does not automatically infer whether the user entered a number, a Boolean value, or some other type.

```
age = input("Enter your age: ")

print(type(age))  # <class 'str'>
```

If the user enters `30`, the value stored in `age` is `"30"`, not the integer `30`.

This behavior is intentional: text input has no inherent type until the program interprets it.

### 8.4 Converting Input

Convert input explicitly when a numeric value is required.

```
age = int(input("Enter your age: "))
print(f"Next year, you will be {age + 1}.")
```

For floating-point input:

```
price = float(input("Enter the price: "))
print(f"The price is {price:.2f}.")
```

The conversion can fail if the input is not in the expected format.

For example, entering `thirty` when an integer is expected causes `ValueError`.

Programs that interact with untrusted or unpredictable input should validate the data and handle conversion errors rather than assuming that every user supplies valid input.

### 8.5 A Complete Input–Process–Output Example

```
# Read input
name = input("Enter your name: ")
age_text = input("Enter your age: ")

# Convert and process
age = int(age_text)
next_year_age = age + 1

# Display output
print(f"Hello, {name}.")
print(f"Next year, you will be {next_year_age}.")
```

This example follows the familiar input–process–output model:

1. Input: receive data from the user.
2. Processing: convert the age and calculate the result.
3. Output: present the result in a readable format.

The model is simple, but it applies equally to much larger programs, from command-line utilities to services that process data for machine-learning systems.

### 8.6 Basic Input Validation

A more robust program anticipates invalid input.

```
age_text = input("Enter your age: ")

try:
    age = int(age_text)

    if age < 0:
        print("Age cannot be negative.")
    else:
        print(f"Your age is {age}.")

except ValueError:
    print("Please enter a valid integer.")
```

This example introduces `try` and `except`, which handle exceptions raised during execution. Exception handling will be examined systematically in a later chapter.

The essential principle is that data received from an external source should be treated as unverified until its validity has been established.

### 8.7 Standard Streams

Command-line programs conventionally use three standard streams:

- **Standard input (**`**stdin**`**)**: Usually receives keyboard input or piped input.
- **Standard output (**`**stdout**`**)**: Usually displays normal program output.
- **Standard error (**`**stderr**`**)**: Usually displays diagnostic messages and errors.

Python exposes these streams through the `sys` module.

```
import sys

print("Normal output", file=sys.stdout)
print("Diagnostic message", file=sys.stderr)
```

Separating ordinary output from diagnostic output makes programs easier to automate and integrate into shell pipelines.

The streams do not necessarily correspond to a physical keyboard or terminal. Their actual destinations depend on the execution environment and how the process is launched.

## 9. Common Errors and Misconceptions

The following mistakes occur frequently among beginners and are also useful targets for basic technical interviews.

### 9.1 Confusing Assignment with Equality

Incorrect interpretation:

```
x = 10
```

This assigns a value; it does not test whether `x` equals `10`.

Use `==` for equality comparisons.

### 9.2 Assuming `input()` Returns a Number

```
age = input("Age: ")
```

Even if the user enters `30`, `age` is a string.

Convert it explicitly with `int()` or another suitable conversion function.

### 9.3 Mixing Incompatible Types

```
# "Age: " + 30
```

This raises `TypeError`.

Use explicit conversion or an f-string:

```
age = 30
print(f"Age: {age}")
```

### 9.4 Confusing `==` and `is`

```
a = [1, 2]
b = [1, 2]

print(a == b)  # True
print(a is b)  # False
```

Value equality and object identity are separate concepts.

### 9.5 Assuming Strings Are Mutable

```
word = "Python"

# word[0] = "J"
```

This raises `TypeError`. Create a new string instead.

### 9.6 Assuming `int()` Rounds

```
int(4.9)  # 4
```

Conversion truncates toward zero. Use an appropriate rounding function when rounding is required.

### 9.7 Assuming All Falsy Values Are Equivalent

```
bool(None)  # False
bool(0)     # False
bool("")    # False
```

These values are all falsy, but they represent different things. The correct choice depends on the meaning of the data.

### 9.8 Reusing Built-in Names

Avoid assigning application data to names such as `list`, `str`, `type`, and `input`. Doing so can obscure or disable access to the corresponding built-in functions or types within the relevant namespace.

### 9.9 Treating Floating-Point Values as Exact Decimals

```
0.1 + 0.2 == 0.3  # False
```

For approximate numerical calculations, use an appropriate tolerance or `math.isclose()` when exact equality is not suitable. For exact decimal arithmetic, choose a decimal representation designed for that purpose.

## 10. Practical Exercises

Complete these exercises without consulting a solution first. The objective is not merely to produce correct output, but to understand why the code behaves as it does.

### Exercise 1: Literals and Types

Create variables representing an integer, a floating-point number, a complex number, a Boolean, a string, and `None`.

Print each value and its type using `type()`.

### Exercise 2: Reassignment

Write a program that assigns an integer to a variable, reassigns a string to the same variable, and prints the variable after each assignment.

Explain why Python permits this behavior.

### Exercise 3: Assignment and Identity

Create two independent lists containing the same values. Compare them using `==` and `is`.

Then assign one list to a third variable and repeat the comparisons. Explain every result.

### Exercise 4: Numeric Conversion

Ask the user to enter two numbers. Convert the inputs to floating-point values and print their sum, difference, product, and quotient.

Consider how the program should behave when the second number is zero or when an input is invalid.

### Exercise 5: String Processing

Ask the user to enter a sentence. Print:

- The original sentence
- The sentence in uppercase
- The sentence in lowercase
- The number of code points in the string
- The sentence with surrounding whitespace removed
- The sentence in reverse order

Explain why the reverse operation does not necessarily reverse every user-perceived character correctly.

### Exercise 6: Formatted Output

Ask the user for a product name, price, and quantity. Calculate the total price and display a formatted receipt.

Requirements:

- Display the product name.
- Format the unit price to two decimal places.
- Display the quantity as an integer.
- Format the total to two decimal places.

### Exercise 7: Naming and Keywords

Write down five valid Python identifiers and five invalid ones. For each invalid identifier, explain which naming rule it violates.

Use the `keyword` module to verify whether a proposed name is a reserved keyword.

### Exercise 8: Debugging

Identify and correct the errors in the following program:

```
name = input("Enter your name: ")
age = input("Enter your age: ")

print("Hello, " + name)
print("Next year, you will be " + age + 1)
```

Explain the type of error that occurs and why it occurs.

### Exercise 9: Boolean Semantics

Predict the result of each expression before executing it:

```
bool("False")
bool("0")
bool(0)
bool([])
bool([0])
True + True
```

Explain why the textual contents of a string do not determine its truth value.

### Exercise 10: Mini Project — Personal Profile

Write a command-line program that collects a user's name, age, and height.

The program should:

1. Read the three values.
2. Convert age and height to suitable numeric types.
3. Display the information in a readable format.
4. Calculate the user's age next year.
5. Handle invalid numeric input gracefully.

Use meaningful variable names, f-strings, and consistent formatting.

## 11. Interview Review

Before proceeding to the next chapter, make sure you can answer the following questions precisely.

1. What is a literal, and how does it differ from a variable?
2. What does Python actually do when executing an assignment statement?
3. Why can a Python name refer to objects of different types at different times?
4. What is the difference between object identity and value equality?
5. What is the difference between mutable and immutable objects?
6. Why can modifying a list through one variable affect another variable?
7. What is the difference between `=` and `==`?
8. What is the difference between `is` and `==`?
9. Why is `bool` considered a subclass of `int`?
10. What is the difference between dynamic typing and strong typing?
11. What rules govern valid Python identifiers?
12. What is the difference between a keyword and a naming convention?
13. Why should built-in names such as `list` and `str` not be reused carelessly?
14. What is the difference between `/` and `//` in Python?
15. How does Python's `int()` behave when converting a floating-point value?
16. Why can `0.1 + 0.2` produce a value that differs from `0.3`?
17. Why are strings immutable?
18. What is the difference between string indexing and slicing?
19. What does `len()` count in a Python string?
20. What is the difference between `str()` and `repr()`?
21. What is the difference between encoding and decoding?
22. Why does `input()` return a string?
23. How should a program handle invalid numeric input?
24. What are `stdin`, `stdout`, and `stderr`?
25. Why are f-strings useful, and how do formatting specifications work?

A satisfactory understanding requires more than memorizing definitions. You should be able to predict the output of short programs, explain the underlying semantics, identify incorrect assumptions, and write small programs that apply the concepts correctly.

## 12. Summary

This chapter established the basic model of Python data and execution.

Literals represent values directly. Variables are names bound to objects, and assignment can bind a name to a different object without requiring a declaration of its type. Objects have types, and those types determine the operations they support. Mutable objects can be changed in place, whereas immutable objects cannot.

Identifiers follow syntactic rules, while naming conventions improve readability and maintainability. Python's built-in types represent numerical values, Boolean values, text, collections, binary data, and the absence of a value.

Strings are immutable Unicode sequences that support indexing, slicing, concatenation, and formatting. The `input()` and `print()` functions provide basic mechanisms for interacting with users and text streams. Because external input arrives as text, conversion and validation are necessary whenever a program expects another type.

These fundamentals may appear elementary, but they are not disposable preliminaries. Errors involving object references, type conversion, mutable data, and string handling can propagate into larger applications, where they become considerably more expensive to diagnose.

A reliable Python programmer does not merely recognize the syntax. The programmer understands what the syntax means.

### Further Reading

- Python Documentation — Built-in Types: https://docs.python.org/3/library/stdtypes.html
- Python Documentation — Built-in Functions: https://docs.python.org/3/library/functions.html
- Python Documentation — Lexical Analysis: https://docs.python.org/3/reference/lexical_analysis.html
- Python Documentation — Expressions: https://docs.python.org/3/reference/expressions.html
- PEP 8 — Style Guide for Python Code: https://peps.python.org/pep-0008/