---
tags:
  - compsci
  - "#cpp"
date: 2024-09-09
source: www.learncpp.com
---
A computer’s CPU is incapable of understanding C++. Instead, CPUs are only capable of processing instructions written in **machine language** (or **machine code**). The set of all possible machine language instructions that a given CPU can understand is called an **instruction set**.

Here is a sample machine language instruction: `10110000 01100001`.

Each instruction is interpreted by the CPU into a command to do a very specific job, such as “compare these two numbers”, or “copy this number into that memory location”. Back when computers were first invented, programmers had to write programs directly in machine language, which was a very difficult and time-consuming thing to do.

First, each instruction is composed of a sequence of 1s and 0s. Each individual 0 or 1 is called a **binary digit**, or **bit** for short. The number of bits in a machine language instruction varies -- for example, some CPUs process instructions that are always 32 bits long, whereas some other CPUs (such as those from the x86 family, which you may be using) have instructions that can be a variable length.

Second, each family of compatible CPUs (e.g. x86, Arm64) has its own machine language, and this machine language is not compatible with the machine language of other CPU families. This means machine language programs written for one CPU family cannot be run on CPUs from a different family!


[[Assembly]] and machine language essentially have the same downsides.

- Assembly programs are hard to understand. While individual assembly instructions are understandable, it can be hard to deduce what a section of assembly code is actually doing. And since assembly programs require many instructions to do even simple tasks, they tend to be quite long.
- Assembly programs are not **portable**. Each CPU family has its own assembly language, which is designed to be assembled into machine language for that same CPU family. A program written in assembly language cannot be easily assembled to machine language for a different CPU family.


![[Screenshot 2024-09-09 at 9.04.45 PM.png]]



