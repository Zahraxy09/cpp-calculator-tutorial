# cpp-calculator-tutorial
A beginner-friendly C++ tutorial: build a console calculator with +, -, *, / operations. Covers switch, loops, input validation, and error handling.


# Building a Simple Calculator in C++ — A Beginner's Guide

> A step-by-step educational article covering the four basic arithmetic operations using core C++ concepts.

---

## Table of Contents

1. [Introduction](#introduction)
2. [Prerequisites](#prerequisites)
3. [Project Structure](#project-structure)
4. [Concepts Used](#concepts-used)
5. [The Code](#the-code)
6. [Code Walkthrough](#code-walkthrough)
7. [Sample Output](#sample-output)
8. [How to Compile and Run](#how-to-compile-and-run)
9. [Possible Improvements](#possible-improvements)
10. [Conclusion](#conclusion)

---

## Introduction

A calculator is one of the most classic beginner projects in any programming language. In this article, we will build a **console-based calculator in C++** that supports the four fundamental arithmetic operations:

- ➕ Addition
- ➖ Subtraction
- ✖️ Multiplication
- ➗ Division

By the end of this tutorial, you will understand how to:
- Accept user input in C++
- Use conditional logic (`if/else` and `switch`)
- Handle edge cases such as division by zero
- Structure a small C++ program cleanly

This is a great starting point if you are new to C++ or want to solidify your understanding of the language fundamentals.

---

## Prerequisites

To follow this tutorial, you should have:

- Basic knowledge of what a variable is
- A C++ compiler installed (e.g., **g++**, **clang++**, or **MSVC**)
- A terminal or IDE (VS Code, CLion, Code::Blocks, etc.)

No prior C++ experience is strictly required — every concept is explained as we go.

---

## Project Structure

```
cpp-calculator/
│
└── calculator.cpp      ← The only file we need
```

This is a single-file project. No external libraries, no build system — just pure C++.

---

## Concepts Used

| Concept | Purpose |
|---|---|
| `#include <iostream>` | Input/output operations |
| `cin`, `cout` | Reading input and printing output |
| `double` | Storing decimal numbers |
| `char` | Storing the operator symbol |
| `switch` statement | Branching based on the operator |
| `do-while` loop | Repeating the calculator until the user quits |
| Error handling | Catching division by zero |

---

## The Code

```cpp
/*
 * ============================================================
 *  Simple C++ Calculator — Four Basic Arithmetic Operations
 *  Author  : Your Name
 *  License : MIT
 * ============================================================
 *
 *  Supported operations:
 *    +  Addition
 *    -  Subtraction
 *    *  Multiplication
 *    /  Division
 *
 *  The program loops until the user enters 'q' to quit.
 * ============================================================
 */

#include <iostream>   // std::cin, std::cout
#include <limits>     // std::numeric_limits (used for input clearing)

int main() {

    double number1 = 0.0;   // First operand
    double number2 = 0.0;   // Second operand
    char   op      = ' ';   // Operator character entered by the user
    char   again   = 'y';   // Loop-control variable

    std::cout << "=========================================\n";
    std::cout << "     Simple C++ Calculator\n";
    std::cout << "=========================================\n";
    std::cout << " Operations: +  -  *  /\n";
    std::cout << " Type 'q' as the operator to quit.\n";
    std::cout << "=========================================\n\n";

    do {
        // ----- Step 1: Get the first number -----
        std::cout << "Enter first number  : ";
        std::cin  >> number1;

        // Check if the input is a valid number
        if (std::cin.fail()) {
            std::cout << "[Error] Invalid input. Please enter a numeric value.\n\n";
            std::cin.clear();                                              // Clear the error flag
            std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n'); // Discard bad input
            continue;
        }

        // ----- Step 2: Get the operator -----
        std::cout << "Enter operator (+, -, *, /) or 'q' to quit: ";
        std::cin  >> op;

        // Allow the user to quit mid-way
        if (op == 'q' || op == 'Q') {
            std::cout << "\nGoodbye! Thanks for using the calculator.\n";
            break;
        }

        // Validate the operator
        if (op != '+' && op != '-' && op != '*' && op != '/') {
            std::cout << "[Error] Unknown operator '" << op << "'. Use +, -, *, or /.\n\n";
            continue;
        }

        // ----- Step 3: Get the second number -----
        std::cout << "Enter second number : ";
        std::cin  >> number2;

        if (std::cin.fail()) {
            std::cout << "[Error] Invalid input. Please enter a numeric value.\n\n";
            std::cin.clear();
            std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
            continue;
        }

        // ----- Step 4: Perform the calculation -----
        double result = 0.0;
        bool   valid  = true;   // Used to skip output if an error occurs

        switch (op) {

            case '+':
                result = number1 + number2;
                break;

            case '-':
                result = number1 - number2;
                break;

            case '*':
                result = number1 * number2;
                break;

            case '/':
                // Guard against division by zero
                if (number2 == 0.0) {
                    std::cout << "[Error] Division by zero is undefined.\n";
                    valid = false;
                } else {
                    result = number1 / number2;
                }
                break;
        }

        // ----- Step 5: Display the result -----
        if (valid) {
            std::cout << "-----------------------------------------\n";
            std::cout << " Result: "
                      << number1 << " " << op << " " << number2
                      << " = " << result << "\n";
            std::cout << "-----------------------------------------\n";
        }

        // ----- Step 6: Ask if the user wants another calculation -----
        std::cout << "\nCalculate again? (y/n): ";
        std::cin  >> again;
        std::cout << "\n";

    } while (again == 'y' || again == 'Y');

    std::cout << "\nSession ended. Goodbye!\n";
    return 0;
}
```

---

## Code Walkthrough

### 1. Headers

```cpp
#include <iostream>
#include <limits>
```

- `iostream` provides `std::cin` (standard input) and `std::cout` (standard output).
- `limits` provides `std::numeric_limits`, which we use to safely clear invalid input from the buffer.

---

### 2. Variables

```cpp
double number1 = 0.0;
double number2 = 0.0;
char   op      = ' ';
char   again   = 'y';
```

- We use `double` (64-bit floating-point) instead of `int` so the calculator handles decimal numbers like `3.14` or `0.5`.
- `op` is a `char` (single character) to store the arithmetic operator the user types.

---

### 3. The `do-while` Loop

```cpp
do {
    // ... calculator logic ...
} while (again == 'y' || again == 'Y');
```

A `do-while` loop **always executes at least once** before checking the condition. This is perfect for a calculator — we always want to perform at least one calculation before asking "again?".

---

### 4. Input Validation

```cpp
if (std::cin.fail()) {
    std::cin.clear();
    std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
    continue;
}
```

When the user types letters instead of numbers, `cin` enters a **fail state**. We:
1. `clear()` — reset the error flag.
2. `ignore(...)` — discard all remaining characters in the input buffer.
3. `continue` — jump back to the top of the loop.

---

### 5. The `switch` Statement

```cpp
switch (op) {
    case '+': result = number1 + number2; break;
    case '-': result = number1 - number2; break;
    case '*': result = number1 * number2; break;
    case '/': /* ... */ break;
}
```

`switch` is cleaner than a long chain of `if/else if` when branching on a single character or integer value. Each `case` must end with `break` to prevent **fall-through** (accidentally executing the next case).

---

### 6. Division by Zero

```cpp
if (number2 == 0.0) {
    std::cout << "[Error] Division by zero is undefined.\n";
    valid = false;
} else {
    result = number1 / number2;
}
```

Dividing by zero is mathematically undefined. Without this check, C++ would produce `inf` or trigger undefined behavior. We set a `valid` flag to `false` so the result line is skipped entirely.

---

## Sample Output

```
=========================================
     Simple C++ Calculator
=========================================
 Operations: +  -  *  /
 Type 'q' as the operator to quit.
=========================================

Enter first number  : 15
Enter operator (+, -, *, /) or 'q' to quit: /
Enter second number : 4
-----------------------------------------
 Result: 15 / 4 = 3.75
-----------------------------------------

Calculate again? (y/n): y

Enter first number  : 10
Enter operator (+, -, *, /) or 'q' to quit: /
Enter second number : 0
[Error] Division by zero is undefined.

Calculate again? (y/n): n

Session ended. Goodbye!
```

---

## How to Compile and Run

### Using g++ (Linux / macOS / Windows with MinGW)

```bash
# Step 1 — Compile
g++ -std=c++17 -Wall -o calculator calculator.cpp

# Step 2 — Run
./calculator          # Linux / macOS
calculator.exe        # Windows
```

### Using clang++

```bash
clang++ -std=c++17 -Wall -o calculator calculator.cpp
./calculator
```

### Using an IDE

If you are using **VS Code**, **CLion**, or **Code::Blocks**:
1. Create a new C++ project.
2. Replace the default `main.cpp` content with the code above.
3. Click **Build** and then **Run**.

> **Flag notes**
> - `-std=c++17` — use the C++17 standard (safe default for all modern compilers).
> - `-Wall` — enable all common warnings (helps catch bugs early).
> - `-o calculator` — name the output executable `calculator`.

---

## Possible Improvements

Once you are comfortable with this version, here are ideas to extend it:

| Feature | Concept to learn |
|---|---|
| Add modulus `%` operator | Integer division & casting |
| Support parentheses `(2+3)*4` | Expression parsing, recursion |
| History of past calculations | `std::vector`, file I/O |
| Save results to a `.txt` file | `std::ofstream` |
| GUI calculator | Qt or wxWidgets framework |
| Unit tests | Google Test (gtest) |

---

## Conclusion

In this tutorial we built a fully functional console calculator in C++ from scratch. Along the way we covered:

- **Variables and data types** (`double`, `char`)
- **User input and output** (`cin`, `cout`)
- **Control flow** (`switch`, `do-while`, `continue`, `break`)
- **Error handling** for invalid input and division by zero

This project may look small, but it exercises almost every fundamental building block of C++. Mastering these concepts will make the jump to more complex programs much smoother.

---

## License

This project is released under the [MIT License](LICENSE). Feel free to use, modify, and distribute it.

---

*Happy coding! If you found this helpful, consider giving the repository a ⭐ on GitHub.*
