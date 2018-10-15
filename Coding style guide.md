# Coding style guide for pdx-robotics (first proposal)

Based on [Mozilla's coding style](https://developer.mozilla.org/en-US/docs/Mozilla/Developer_guide/Coding_Style). Simplified to make it more beginner friendly.

# Table of contents

- [Coding style guide for pdx-robotics (first proposal)](#coding-style-guide-for-pdx-robotics-(first-proposal))
- [Table of contents](#table-of-contents)
- [Formatting](#formatting)
  - [Whitespace](#whitespace)
  - [Line length](#line-length)
  - [Indentation](#indentation)
  - [Control structures](#control-structures)
  - [C++ classes](#c++-classes)
  - [Methods and functions](#methods-and-functions)
  - [Declarations](#declarations)
  - [Operators](#operators)
  - [Literals](#literals)
- [General practices](#general-practices)
- [C/C++ practices](#c/c++-practices)

# Formatting

## Whitespace

No tabs. No whitespace at the end of a line.

Unix-style linebreaks ("`\n`"), not Windows-style ("`\r\n`").

## Line length

80 characters or less (for opening 2 files side-by-side on 13" laptops).

## Indentation

Two spaces per logic level, or four spaces in Python code.

Note that class visibility and `goto` labels do not consume a logic level, but `switch case` labels do. See examples below.

## Control structures

Use [Allman bracing style](https://en.wikipedia.org/wiki/Indentation_style#Allman_style): left and right braces in their own lines, with no extra indentation.

Note: Class and function definitions are not control structures; left brace goes by itself on the second line and without extra indentation, generally in C++.

Always brace controlled statements, even a single-line consequent of `if else else`. This is redundant, typically, but it avoids dangling else bugs, so it's safer at scale than fine-tuning.

Examples:

```C++
if (...)
{
}
else if (...)
{
}
else
{
}

while (...)
{
}

do
{
}
while (...);

for (...; ...; ...)
{
}

switch (...)
{
  case 1:
  {
    // When you need to declare a variable in a switch, put the block in braces.
    int var;
    break;
  }
  case 2:
    ...
    break;
  default:
    break;
}
```

Control keywords `if`, `for`, `while`, and `switch` are always followed by a space to distinguish them from function calls, which have no trailing space.
`else` should only ever be followed by { or `if`; i.e., other control keywords are not allowed and should be placed inside braces.

## C++ classes

```C++
class MyClass: public A
{
public:
  MyClass(int var, int var2):
    var(var),
    var2(var2)
  {
     ...
  }

  // Tiny constructors and destructors can be written on a single line.
  MyClass(){...}

  // Special member functions, like constructors, that have default bodies
  // should use '= default' annotation instead.
  MyClass() = default;

  // Unless it's a copy or move constructor or you have a specific reason to allow
  // implicit conversions, mark all single-argument constructors explicit.
  explicit MyClass(OtherClass arg)
  {
    ...
  }

  // This constructor can also take a single argument, so it also needs to be marked
  // explicit.
  explicit MyClass(OtherClass arg, AnotherClass arg2 = AnotherClass())
  {
    ...
  }

  int tinyFunction(){return var;}  // Tiny functions can be written in a single line.

  int largerFunction()
  {
    ...
    ...
  }

private:
  int var;
};
```

Define classes using the style given above.

For small functions, constructors, or other braced constructs (ones that fit within the 80 character line limit), it's okay to collapse the definition to one line, as shown for `tinyFunction` above. For larger ones, use something similar to method declarations, below.

## Methods and functions

In C/C++, method names should be in camelCase. Typenames, and the names of arguments, should be separated with a single space character.

```C++
template<typename T>  // Templates on own line.
static int myFunction
(
  const std::string& str,
  std::unique_ptr<const char*>&& buffer,
  int* optionalInt = nullptr
)
{
  ...
}

int MyClass::method
(
  const std::string& str,
  std::unique_ptr<const char*>&& buffer,
  int* optionalInt = nullptr
)
{
  ...
}
```

Method declarations must use the keywords `virtual`, `override`, or `final` when applicable.

- Use `virtual` to declare virtual methods, which do not override a base class method with the same signature.
- Use `override` to declare virtual methods which do override a base class method, with the same signature, but can be further overridden in derived classes.
- Use `final` to declare virtual methods which do override a base class method, with the same signature, but can NOT be further overridden in the derived classes. This should help the person reading the code fully understand what the declaration is doing, without needing to further examine base classes.

## Declarations

In general, snuggle pointer stars with the type, not the variable name:

```C++
T* p; // GOOD
T *p; // BAD
T* p, * q; // OOPS put these on separate lines
```

Multiple pointers should be declared on separate lines.

## Operators

In C++, when breaking lines containing overlong expressions, binary operators must be left on their original lines if the line break happens around the operator. The second line should be indented in once.

```C++
int addABunchOfInts(int a, int b, int c)
{
  //                                                          80th column here v
  return a + b + c + a + b + c + a + b + c + a + b + c + a + b + c + a + b + c +
    a + b + c;
}
```

## Literals

Double-quoted strings (e.g. "foo") are preferred to single-quoted strings (e.g. 'foo').

# General practices

- Don't leave debug printfs or dumps lying around.

- Use Unix-style carriage returns ("`\n`"), rather than Windows/DOS ones ("`\r\n`"). You can convert patches, with DOS newlines to Unix via the 'dos2unix' utility, or your favorite text editor.

- Use two spaces for indentation.

- When fixing a problem, check to see if the problem occurs elsewhere in the same file, and fix it everywhere if possible.

- End the file with a newline. Make sure your patches don't contain files with the text "no newline at end of file" in them.

- Declare local variables at the top of their scopes (excluding `for` loops).


# C/C++ practices

- Have you checked for compiler warnings? Warnings often point to real bugs.

- In C++ code, use `nullptr` for pointers if possible. In C code, using `NULL` or `0` is allowed.

- For checking if a `std` container has no items, don't use `size()`, instead use `empty()`.

- Do not use multiple inheritance (see [Dimond problem](https://en.wikipedia.org/wiki/Multiple_inheritance#The_diamond_problem)).

- Do not initialize variables with `nsFoo aFoo(bFoo)` (see [Most vexing parse](https://en.wikipedia.org/wiki/Most_vexing_parse)).

  - Exception for constructors:
    ```C++
    MyClass(int foo): foo(foo){}
    ```

- Include guards are in all caps followed by `_H`. For example, TheRobot.h's guard is `THEROBOT_H`.

  Use the following exact form for include guards. GCC, and clang, recognize this idiom and avoid re-reading headers that use it. To avoid confusing GCC's and clang's header optimization, do not include any code before or after the include guards (comments and whitespace are OK). Do not combine any other preprocessor checks in the `#ifndef <guard>` expression.

  ```C++
  #ifndef THEROBOT_H
  #define THEROBOT_H
  //... All code ...
  #endif
  ```

