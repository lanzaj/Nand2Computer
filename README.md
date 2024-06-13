# Nand2Computer
My own computer architecture and assembly language.

![](img/my_8bit_computer.webp)

color | purpose
---|---
pink | opcode
orange | arg1
yellow | arg2
green | dest
violet | result value
cyan | instruction pointer

<img src="img/circuit_annotated.PNG" height="400">

## About this project

[Turing complete](https://turingcomplete.game) is an educational game about computer science. You start with NAND gates, you build other gates like OR, AND, NOT, XOR... Then components and finally a turing complete architecture with its own assembly.
I am curently ranked [251/85k](https://turingcomplete.game/leaderboard) on the leaderboard of Turing complete.

## Instructions

An instruction is divided into up to four distinct parts, each encoded with one byte (uint8 ranging from 0 to 255):
```asm
Opcode <arg1> <arg2> <dest>
```
Here is the list of opcodes :

| Opcode | Binary | Assembly | Instruction |
|---|---|---|---|
| 0 | xx00 0000 | add \<arg1> \<arg2> \<dest> | dest = arg1 + arg2 |
| 1 | xx00 0001 | minus \<arg1> \<arg2> \<dest> | dest = arg1 - arg2 |
| 2 | xx00 0010 | and \<arg1> \<arg2> \<dest> | dest = arg1 & arg2 |
| 3 | xx00 0011 | or \<arg1> \<arg2> \<dest> | dest = arg1 \| arg2 |
| 4 | xx00 0100 | not \<arg1> \<ignored> \<dest> | dest = !arg1 |
| 5 | xx00 0101 | xor \<arg1> \<arg2> \<dest> | dest = arg1 ^ arg2 |
| 6 | xx00 0110 | multiply \<arg1> \<arg2> \<dest> | dest = arg1 * arg2 |
| 7 | xx00 0111 | div \<arg1> \<arg2> \<dest> | dest = arg1 / arg2 |
| 16 | xx01 0000 | modulo \<arg1> \<arg2> \<dest> | dest = arg1 % arg2 |
| 17 | xx01 0001 | mov \<arg1> \<ignored> \<dest> | dest = arg1 |
| 18 | xx01 0010 | inc \<arg1> \<ignored> \<dest> | dest = arg1 + 1 |
| 19 | xx01 0011 | call \<function> | function() |
| 20 | xx01 0100 | ret | return |
| 21 | xx01 0101 | jump \<address> | jump(address) |
| 22 | xx01 0110 | shl \<arg1> \<arg2> \<dest> | dest = arg1 << arg2 |
| 23 | xx01 0111 | shr \<arg1> \<arg2> \<dest> | dest = arg1 >> arg2 |
| 24 | xx01 1000 | pop \<ignored> \<ignored> \<dest> | dest = pop(), pop the stack into dest |
| 25 | xx01 1001 | push \<arg1> | push arg1 in the stack|
| 32 | xx10 0000 | je \<arg1> \<arg2> \<address> | if ( arg1 == arg2) { jump(address) } |
| 33 | xx10 0001 | jne \<arg1> \<arg2> \<address> | if ( arg1 != arg2) { jump(address) } |
| 34 | xx10 0010 | jinf \<arg1> \<arg2> \<address> | if (arg1 < arg2) { jump(address) } |
| 35 | xx10 0011 | jinfe \<arg1> \<arg2> \<address> | if (arg1 <= arg2) { jump(address) } |
| 36 | xx10 0100 | jsup \<arg1> \<arg2> \<address> | if (arg1 > arg2) { jump(address) } |
| 37 | xx10 0101 | jsupe \<arg1> \<arg2> \<address> | if (arg1 >= arg2) { jump(address) } |

Here are more details on how functions operate

special instruction | details
---|---
`call <function>` | push in the stack the value of the current instruction pointer and jump to the address of the function
`ret` | pop the value of the instruction pointer when the funcion was called and jump to it

### Source / Destination
There are 9 different sources or destinations possible :
| Code | Binary | Assembly | Source / Destination |
|---|---|---|---|
| 0 | 0000 0000 | reg0 | register 0 |
| 1 | 0000 0001 | reg1 | register 1 |
| 2 | 0000 0010 | reg2 | register 2 |
| 3 | 0000 0011 | reg3 | register 3 |
| 4 | 0000 0100 | reg4 | register 4 |
| 5 | 0000 0101 | ramIndex | index of ram |
| 6 | 0000 0110 | addr | instruction pointer |
| 7 | 0000 0111 | stdin / stdout | input / output |
| 8 | 0000 1000 | ram | ram[ramIndex] |

<img src="img/register_annotated.PNG" height="400">

example: an instruction to add `reg0` and `reg1` and store the result in `reg2`
```asm
add reg0 reg1 reg2
```
The first two bits of the opcode indicate whether `<arg1>` and `<arg2>` are:
 - Literal values (uint8) if encoded with 1 
- Codes for a register, input, output, or RAM if encoded with 0

| Opcode | arg1 | arg2 |
|---|---|---|
|00xx xxxx| memory code | memory code |
|01xx xxxx| memory code | uint8 value|
|10xx xxxx| uint8 value| memory code|
|11xx xxxx| uint8 value| uint8 value|

To modify the first two bits we will use `int1` and `int2`

| binary | asm |
|---|---|
|1000 0000| int1 |
|0100 0000| int2 |

So to add 1 and 2 into reg0, the correct instruction is :
```asm
add|int1|int2 1 2 reg0
``` 
