# Whitespace

[Whitespace](https://web.archive.org/web/20150717190859/http://compsoc.dur.ac.uk:80/whitespace/)
is a strange language. Its tokens are space, line-feed, and tab —
everything else is comment. It's stack based, has console i/o, and an
associative store. Yes, it's Turing complete. Yes, you'd be insane to
use it. It belongs to the venerable tradition of languages like
[Brainf*ck](https://www.muppetlabs.com/~breadbox/bf/),
[Shakespeare](http://shakespearelang.sourceforge.net/), and
[Unlambda](http://www.madore.org/~david/programs/unlambda/).

Here's [my Whitespace interpreter](./whitespace), written in Ruby. It's
nothing to be proud of, but hey, what do you expect at 4 a.m.?

I stayed up for the better part of a night writing this. Why?
Crazy, I guess.

## Whitespace-asm

Here's my [whitespace assembler](whitespace-asm), also written in Ruby.

This test program prints the alphabet: [alphabet.wsa](alphabet.wsa)

To assemble it, run whitespace-asm like this:

```sh
./whitespace-asm alphabet.wsa
```

That should generate [alphabet.ws](alphabet.ws).

Then run it:

```sh
./whitespace alphabet.ws
ABCDEFGHIJKLMNOPQRSTUVWXYZ
```

### Syntax

#### Comments

A "#" anywhere on a line starts a comment. The rest of the line is
ignored. Blank lines are ignored.

#### Labels

You can use this alternate syntax for a label if you wish:

```wsa
unsigned-number:
```

#### Opcodes

|                        | Opcode   | Operand         | Description                                                 |
| :--------------------: | -------- | --------------- | ----------------------------------------------------------- |
| **Stack Manipulation** | push     | signed-number   | Push a number onto the stack                                |
|                        | dup      |                 | Push top of stack into the stack again                      |
|                        | swap     |                 | Swap two topmost numbers on stack                           |
|                        | discard  |                 | Pop & discard number on top of stack                        |
| **Arithmetic**         | add      |                 | Pop two numbers, add, push result                           |
|                        | sub      |                 | Pop two numbers, subtract, push result                      |
|                        | mul      |                 | Pop two numbers, multiply, push result                      |
|                        | div      |                 | Pop two numbers, integer divide, push result                |
|                        | mod      |                 | Pop two numbers, modulo, push result                        |
| **Heap Access**        | store    |                 | Pop value and address; store value on heap at that address  |
|                        | retrieve |                 | Pop address; push onto stack the heap value at that address |
| **Flow Control**       | label    | unsigned-number | Target for other flow-control ops                           |
|                        | call     | unsigned-number | Call subroutine                                             |
|                        | jump     | unsigned-number | Unconditional jump                                          |
|                        | jz       | unsigned-number | Pop top of stack; jump if it's zero                         |
|                        | jn       | unsigned-number | Pop top of stack; jump if it's negative                     |
|                        | ret      |                 | Return from subroutine                                      |
|                        | exit     |                 | Exit interpreter                                            |
| **I/O**                | outchar  |                 | Pop top of stack; print it as ascii character               |
|                        | outnum   |                 | Pop top of stack; print it as decimal number                |
|                        | readchar |                 | Read character from stdin & push it onto stack              |
|                        | readnum  |                 | Read integer from stdin & push it onto stack                |

## Whitespace-disassem

Here's my [whitespace disassembler](whitespace-disassem). It's nothing
more than a cheap hack of my interpreter.

Yes, there's too much duplicated code between these three programs.
No, I'm not going to fix it tonight. Maybe tomorrow.

Content of this site is © [Wayne Conrad](mailto:wconrad@yagni.com).
All rights reserved.
