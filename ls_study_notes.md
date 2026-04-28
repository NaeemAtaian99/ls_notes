# PY100 Book Notes: Basic Operations

## 1. Arithmetic Operations

- **Key Vocabulary**:
    - **Float Division (`/`)**: Always returns a float, even with two integers. `10 / 5` is `2.0`.
    - **Integer Division (`//`)**: Always rounds *down* (floor division). `17 // 5` is `3`. `(-17) // 5` is `-4`.
    - **Modulo (`%`)**: Returns the remainder of a division. `17 % 5` is `2`.
        - **Common Use**: Checking for even/odd. `number % 2 == 0`.

(Reference: [Arithmetic Operations](https://launchschool.com/books/python/read/basic_ops#arithmeticoperations))

## 2. Floating-Point Imprecision

- **The "Gotcha"**: Computers can't store some decimals precisely in binary. This means `0.1 + 0.2 == 0.3` is **`False`**.
- **Best Practice**: **Never use floats for money.**
- **Solutions**:
    1.  **Use Integers**: Store currency in its smallest unit (e.g., store `$45.99` as the integer `4599`).
    2.  **Use `Decimal` type**: When you need exact decimal math.
        - **Crucial Detail**: Always create `Decimal` objects from strings to preserve precision: `Decimal('0.1')`. Creating from a float `Decimal(0.1)` inherits the original imprecision.

(Reference: [Floating Point Imprecision](https://launchschool.com/books/python/read/basic_ops#floatingpointimprecision))

## 3. Comparison Operators

- **Key Idea**: All comparison operators (`==`, `!=`, `<`, `>`, etc.) return a boolean: `True` or `False`.
- **The "Surprise" (Lexicographical Comparison)**: Strings are compared character by character, from left to right. Python stops as soon as it finds a difference.
- **Examples**:
    - `'3' > '24'` is `True` because the first character `'3'` is greater than `'2'`.
    - `'a' > 'Z'` is `True` because all lowercase letters are "greater than" all uppercase letters.
    - `'abc' < 'abcdef'` is `True` because when two strings are identical up to the length of the shorter one, the shorter one is considered "less than".

(Reference: [Ordered Comparisons](https://launchschool.com/books/python/read/basic_ops#orderedcomparisons))

## 4. String Concatenation

- **The "Gotcha"**: The `+` operator joins strings. It does not perform math on strings that look like numbers.
    - `'1' + '2'` results in `'12'`, not `3`.

(Reference: [String Concatenation](https://launchschool.com/books/python/read/basic_ops#stringconcatenation))

## 5. Type Coercion (Converting Types)

- **Key Vocabulary**:
    - **Explicit Coercion**: You manually convert a type using a function like `int()`, `float()`, or `str()`.
        - **When to use**: When Python can't guess your intent. E.g., `int('5') + 10`.
    - **Implicit Coercion**: Python automatically converts a type.
        - **When it happens**: In mixed-type math, like `5 + 3.5`. Python promotes the integer `5` to a float `5.0` to avoid losing precision.
- **Best Practice**: Rely on Python's implicit coercion for mixed `int`/`float` math. Don't write `float(5) + 3.5`; it's unnecessary.

(Reference: [Coercion](https://launchschool.com/books/python/read/basic_ops#coercion))

## 6. `str()` vs. `repr()`

- **Core Idea**: Two different ways to get a string representation of an object.
- **`str()`**:
    - **Purpose**: Create a clean, "human-readable" string for users.
    - **Behavior**: This is what `print()` uses by default. It can hide type information.
- **`repr()`**:
    - **Purpose**: Create an "unambiguous" string for developers to debug.
    - **Behavior**: The goal is to show a string that could be used in code to recreate the object. It reveals the type.
- **Best Practice**: **Use `repr()` when debugging** to clearly distinguish between data types.

- **The Killer Example**:
  ```python
    num = 123
  str_num = '123'

  print(str(num))      # Outputs: 123
  print(str(str_num))  # Outputs: 123  <-- Ambiguous!

  print(repr(num))     # Outputs: 123
  print(repr(str_num)) # Outputs: '123' <-- Unambiguous! The quotes reveal it's a string.