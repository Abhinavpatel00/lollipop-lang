# lollipop-lang
a basic stack based turing complete programming language made for fun 

documentation will be available soon

if you want to know how to it works you may want to learn more about computer memory and hardware details meanwhile checkout this [stack based](https://en.wikipedia.org/wiki/Stack-oriented_programming) 


# Lollipop Lang Documentation

**Lollipop**, is a stack-based programming language. This implies that to perform any operation, a value must be placed onto the stack. Imagine it as a physical stack of objects. Typically, operations will extract their arguments from the top of the stack or pop values from it. They may also return values to be pushed back onto the stack.

## A Simple Example
Consider this example in Lollipop:

```lollipop
68 1 + #
```

This basic Lollipop program adds two numbers together and then displays the sum on the console.

### Expected Output:
```
69
```

Now, let's delve into how it works step by step:

| Step | Code | Description            |
|------|------|------------------------|
| 1    | 68   | Pushes a value onto the stack.|
| 2    | 1    | Pushes another value onto the stack.|
| 3    | +    | The `+` symbol pops the two most recent values from the stack, adds them, and pushes the sum back onto the stack.|
| 4    | #    | The `#` symbol pops a value from the stack and prints it to the console.|

Stack breakdown by step:

0. []
1. [68]
2. [68][1]
3. [69]
4. []

In Lollipop, the same stack-based principles  followed. It's essential to grasp the concept of the stack to effectively work with Lollipop. Happy coding with Lollipop!

# Hello, World! in Lollipop

In Lollipop, string literals supported, which makes printing a string to the console just as simple as using the `dump_s` command with the "_s" suffix to indicate a string format.

Here's how you would print "Hello, World!" in Lollipop:

```lollipop
"Hello, World!\n" dump_s
```

As you can see, Lollipop also supports some escaped characters within strings. Specifically, you can use `\n` for a new line, `\r` for a carriage return, and `\t` for a tab.

Additionally, you can dump single characters using their ASCII code. For example, to output a newline character (ASCII code 10), you can use the `dump_c` command:

```lollipop
10 dump_c
```

### Expected Output:
```
Hello, World!
```

# Conditional Branching in Lollipop

Lollipop allows you to implement conditional branching . Let's examine a slightly more complex example program in Lollipop:

```lollipop
500 80 - 420 = if
  69 #
else
  420 #
endif
```

This program first evaluates `500 - 80`, then checks if that result is equal to 420. If true, it prints 69; otherwise, it prints 420.

### Expected Output:
```
69
```

Now, let's break down how it works step by step:

| Step | Code         | Description |
| ---- | ------------ | ----------- |
| 1    | `500 80 -`   | Push two values onto the stack, subtract them, and push the result onto the stack. |
| 2    | `420`        | Push 420 onto the stack. |
| 3    | `=`          | Use the equality comparison operator. It pops two values off the stack, compares them, and pushes back a 1 if they are equal or a 0 if they aren't. |
| 4    | `if`         | Pop the condition just pushed onto the stack; jump to `else` or `endif` if it is false, or fall through to the next instruction if it's true. |
| 5    | `69 #`       | Push a value onto the stack, then dump it to console output. |
| 6    | `else`       | Label to jump to if the `if` condition is false. |
| 7    | `420 #`      | This would push a value onto the stack and then dump it to console output; however, it is jumped over due to the `if` condition evaluating to true. |
| 8    | `endif`      | Label to jump to if the `if` condition is false, and no `else` label is present, or if the `if` condition is true, and an `else` label is present. |


# Loops in Lollipop

In Lollipop, you can also implement loops , Let's examine an example program that prints every whole number from 1 to 30 on separate lines:

```lollipop
1
while dup 30 <= do
  dup #    // Print loop counter without destroying it
  10 dump_c  // Print a newline character
  1 +         // Increment loop counter
endwhile
```

This program will produce the expected output, displaying numbers from 1 to 30, each on a new line.

Now, let's break down how this program works step by step:

| Step | Code          | Description |
| ---- | ------------- | ----------- |
| 1    | `1`           | Push 1 onto the stack to initialize the loop counter. |
| 2    | `while`       | Generate an address to jump to upon reaching `endwhile`. |
| 3    | `dup 30 <=`   | Push a boolean condition onto the stack comparing whether the last item on the stack (duplicated) is less than or equal to 30. |
| 4    | `do`          | Pop the condition just pushed onto the stack; jump just past `endwhile` (step 7) if it is zero, or fall through to the next instruction if it's true. |
| 5    | `dup #`       | Duplicate the top-most value onto the stack, then dump the duplicate to the console output. This prints the current loop counter, which is on the stack. |
| 6    | `10 dump_c`   | Print a newline character. |
| 7    | `1 +`         | Add 1 to the top-most value on the stack. This increments the loop counter. |
| 8    | `endwhile`    | Upon reaching this label, jump back to `while` (step 2) and continue execution from there. |

# Definitions in Lollipop

In Lollipop, we have definitions for stack notation, operators, and keywords. Here's how they are structured in Lollipop:

## Stack Notation
In Lollipop, stack items are enclosed in square brackets. The arrow `->` represents the transformation from the state of the stack before an operation to the state of the stack after the operation. Here are some examples:

- No effect on the stack: `[] -> []`
- Pushing a value 'a' onto the stack: `[] -> [a]`
- Summing two values on the stack: `[a][b] -> [a + b]`

## Operators
Operators in Lollipop manipulate values on the stack. The following table provides a list of operators, their stack notations, and brief descriptions:

| Operator | Stack Notation | Description |
|----------|----------------|-------------|
| `#`      | `[a] -> []`    | Print value on top of the stack as an unsigned integer. |
| `+`      | `[a][b] -> [a + b]` | Sum two elements on top of the stack. |
| `-`      | `[a][b] -> [a - b]` | Subtract two elements on top of the stack. |
| `*`      | `[a][b] -> [a * b]` | Multiply two elements on top of the stack. |
| `/`      | `[a][b] -> [a / b]` | Divide two elements on top of the stack, pushing the quotient. |
| `%`      | `[a][b] -> [a % b]` | Divide two elements on top of the stack, pushing the remainder. |
| `=`      | `[a][b] -> [a == b]` | Compare if the top two elements of the stack are equal. |
| `>`      | `[a][b] -> [a > b]` | Compare if the top element is greater than the one below. |
| `<`      | `[a][b] -> [a < b]` | Compare if the top element is less than the one below. |
| `>=`     | `[a][b] -> [a >= b]` | Compare if the top element is greater than or equal to the one below. |
| `<=`     | `[a][b] -> [a <= b]` | Compare if the top element is less than or equal to the one below. |
| `<<`     | `[a][b] -> [a << b]` | Shift bits of 'a' left by 'b' bits. |
| `>>`     | `[a][b] -> [a >> b]` | Shift bits of 'a' right by 'b' bits. |
| `&&`     | `[a][b] -> [a && b]` | Perform a bitwise AND on the top two elements of the stack. |
| `||`     | `[a][b] -> [a || b]` | Perform a bitwise OR on the top two elements of the stack. |

## Keywords
Lollipop features various keywords that control program flow and perform specific actions. Here are some essential Lollipop keywords:

- `if`: Jump to `else` or `endif` only if the popped value is equal to zero.
- `else`: Inside this block is what will be executed if the `if` condition is false.
- `endif`: A required block-ending symbol for the `if` keyword.
- `do`: Jumps just past `endwhile` if the popped value is zero.
- `while`: Generates a label for `endwhile` to jump to.
- `endwhile`: Generates a label for `do` to jump to upon a false condition.
- `dup`: Duplicates the top item on the stack.
- `twodup`: Duplicates two items on the top of the stack.
- `drop`: Deletes the top-most item from the stack.
- `swap`: Pushes two popped values back in reverse order.
- `over`: Pushes the stack item below the top onto the top.
- `dump`: Equivalent to the `#` operator; pops a value and prints it as an unsigned integer.
- `dump_c`: Pops a value off the stack and prints it formatted as a character.
- `dump_s`: Pops a value off the stack and prints it formatted as a string.

These keywords, along with operators, allow you to create simple programs and control the flow of your code in Lollipop.

## 'while', 'do', and 'endwhile' - Looping
In Lollipop, you can create loops using the `while`, `do`, and `endwhile` keywords. These keywords allow you to control the flow of your program by repeating a block of code based on a specified condition.

- `while`: The `while` keyword generates a label for the `endwhile` keyword to jump to unconditionally. It serves as the beginning of a loop.
- `do`: The `do` keyword is used within the loop. If the item on top of the stack is zero, it jumps just past `endwhile`, effectively stopping the loop.
- `endwhile`: The `endwhile` keyword is a necessary block-ending symbol for the `while` keyword, marking the end of a loop.

Here's an example of how to use these keywords to create a simple loop that prints numbers from 1 to 5:

```plaintext
1            // initialize loop counter
while dup 5 <= do
  dup dump   // print loop counter
  10 dump_c  // print newline
  1 +        // increment loop counter
endwhile
```

In this example, the loop starts with a counter initialized to 1. The `while` keyword generates the loop label, and `dup 5 <= do` checks whether the counter is less than or equal to 5. The loop continues as long as this condition is met. Inside the loop, `dup dump` prints the loop counter, `10 dump_c` prints a newline character, and `1 +` increments the counter. Finally, the loop is terminated with `endwhile`.

The output of this code will be:

```plaintext
1
2
3
4
5
```

## 'dup', 'twodup', 'drop', 'swap', 'over', and 'dump' - Stack Operations
Lollipop provides various stack operations to manipulate the items on the stack. Here are some of the key stack operations:

- `dup`: Duplicates the item at the top of the stack. For example, `[a] -> [a][a]`.

- `twodup`: Duplicates the top two items of the stack. For example, `[a][b] -> [a][b][a][b]`.

- `drop`: Deletes the item at the top of the stack, leaving no reference to it. This is useful for managing memory and avoiding stack validation warnings. For example, `[a] -> []`.

- `swap`: Swaps the positions of the top-most item and the item below it on the stack. For example, `[a][b] -> [b][a]`.

- `over`: Pushes the item below the top of the stack onto the top, effectively duplicating it. For example, `[a][b] -> [a][b][a]`.

- `dump`: Prints the item at the top of the stack to the standard output. You can specify the print format by using the `#` operator or related keywords, such as `dump_c` for characters and `dump_s` for strings.

These stack operations allow you to manage the stack efficiently and perform various manipulations on its contents.

## 'mem', 'store', and 'load' - Memory Manipulation
Lollipop provides memory-related operations to allocate, store, and retrieve data from memory. Here's an overview of these operations:

- `mem`: The `mem` keyword pushes the address of the memory allocated at runtime onto the stack. This memory can be used for various purposes, such as string-building and creating variables.

- `store`: The `store` keyword allows you to store a value at a specific address in the allocated memory. You need to specify the size of the value (byte, word, double word, or quad word) using the `store<x>` format.

- `load`: The `load` keyword retrieves a value from a given memory address and pushes it onto the stack. Like `store`, you also need to specify the size of the value to be loaded.

These memory operations are helpful for working with dynamic data and managing memory in your Lollipop programs.

## 'shl', 'shr', 'and', and 'or' - Bitwise Operators
Lollipop provides bitwise operators to manipulate binary data:

- `shl`: The `shl` keyword shifts the bits of 'a' left by 'b' bits. For example, `[a][b] -> [a << b]`.

- `shr`: The `shr` keyword shifts the bits of 'a' right by 'b' bits. For example, `[a][b] -> [a >> b]`.

- `and`: The `and` keyword performs a bitwise AND operation on two values, 'a' and 'b'. For example, `[a][b] -> [a && b]`.

- `or`: The `or` keyword performs a bitwise OR operation on two values, 'a' and 'b'. For example, `[a][b] -> [a || b]`.

These bitwise operators allow you to work with binary data and perform operations such as shifting and logical comparisons.

## 'mod' - Operator
The `mod` operator calculates the result of the modulo operation. It pops two values from the stack, 'a' and 'b', and pushes the remainder when 'a' is divided by 'b'. For example, `[a][b] -> [a % b]`.

These operations provide you with a wide range of capabilities for manipulating data and controlling program flow in Lollipop.
