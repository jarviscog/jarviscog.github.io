---
title: 'NAND to Tetris'
date: 2024-03-13T17:55:09-04:00
draft: false
tags: ["Projects"]
hideToc: false
---

[NAND to Tetris](https://www.nand2tetris.org/) is a challenge where you set out to create a computer from the ground up. Split into 12 projects, you scale the layers of abstraction through the logic gates, ALU circuits, and the Assembler to a complete operating system.  
Each project took an afternoon to complete, with some of the trickier ones taking an afternoon day.


## Projects 1-6

The first set of projects work with the lowest-level hardware of a computer, starting out by building NAND, AND, MUX circuits.
Comprehensive descriptions are included for each circuit, which can be very useful.
Things start to get interesting around Project 3, where the registers, program counter, and RAM are built.

<!-- Notes from school compared to notes from nand to tetris -->

Project 4 jumps forward to give a taste of assembly language. This is so in Project 5 you have an idea of what you are going to be building (the assembler), and I think this is definitely the best way to go about teaching this, and is way more straightforward than the way I was taught in school.

{{< figure src="/images/nand-school-slide.jpg" title="A sample slide from my Computer Organization class...">}}
{{< figure src="/images/nand-og-slide.jpg" title="A slide from the book included with NAND to Tetris. Much better">}}


Project 6 deals solely with the assembler, and leads straight into the Virtual machine that is built in Projects 7-8.
If you want a real-life example of how this is useful, check out the work being done on [RISC-V](https://domipheus.com/blog/designing-a-risc-v-cpu-in-vhdl-part-22-doom-as-a-benchmark-and-adding-cache-to-rpu/)

## Projects 7-8
Projects 7 and 8 dealt with creating an interpreter for the Jack language. This involved creating a symbol table, where each variable can be stored, and creating things such as the function call stack. This is definitely where I had the most fun.

## Projects 9-12
Once the Virtual machine was done, I decided to take a break. I will come back to finish this at some point, but you know how these things go...


That's all for now. I would highly recommend completing at least the first 3 projects to get a feel for the challenge. You can check out my attempt [here](https://github.com/jarviscog/nand-to-tetris).
