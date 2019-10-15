Lets start with some basic concept that are present in bold in the course 

* **Machine language**: LAnguage use for the computers, very rudimentary.
* **Natural Language**: Language use by people, it is constantly evolving, new words are created every day and old one disappear. 
* **Instruction list** (IL): a complete set of know commands 

## What is a language

> I paraphrased the original information of the course since it is condense and simple

* **An Alphabet:** A set of symbols use to build a word.
* **A Lexis:**  also known as dictionary, it is a set of words available in to be use.
* **A Syntax:** A set of rules used to determine if a certain string of words make a valid sentence 
* **Semantics:** a set of rules to determining if a certain phrase make sense.

The IL o Instruction list is the alphabet for the machine, this is the simplest set of symbols that can be use to give commands to the computer.
In order to give instruction to the computer we need a intermediary language, complex enough to be human readable, simple enough so computer can follow, this languages are called **High-Level programming Language**, a program written with this language is call **source code** and a file  containing this code will be a **source file**.

## Compilation vs. Interpretation

A code or source code must be correct in many senses:

* **Alphabetically:** A program must be written in recognizable script, using recognizable character, as example Roman alphabet.
* **Lexically:** Each programming language ahas a dictionary and one must master it, although is simpler than a natural language dictionary.
* **Syntactically:** Each language has it rules and must be obeyed
* **Semantically:** The program has to make sense

Assuming the program is written correctly, now we need the computer to translate it to machine language, this transformation from **high-Level Programming Language** into **Machine Language**.

## Compilation

The source code is translate once (but this act needs to be repeated each time we modify the code) by getting a file, that contain the machine code, now the code can be distribute.

## Interpretation
We can translate the source program each time it has to be run; the program performing this kind of transformation is called an interpreter, as it interprets the code every time it is intended to be executed; it also means that you cannot just distribute the source code *as-is*, because the end-user also needs the interpreter to execute it.