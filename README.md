# Nand2Computer [WIP]
My own computer architecture and assembly language.

![](./my_8bit_computer.webp)

## About this project

(Turing complete)[] is an educational game

## Instructions
| Code | Binary | Assembly | Instruction |
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
| 21 | xx01 0101 | jump \<address> | jump address |
| 22 | xx01 0110 | shl \<arg1> \<arg2> \<dest> | dest = arg1 << arg2 |
| 23 | xx01 0111 | shr \<arg1> \<arg2> \<dest> | dest = arg1 >> arg2 |
| 24 | xx01 1000 | pop \<ignored> \<ignored> \<dest> | dest = pop() |
| 25 | xx01 1001 | push \<arg1> | push(arg1) |
| 32 | xx10 0000 | je \<arg1> \<arg2> \<address> | if ( arg1 == arg2) { jump(address) } |
| 33 | xx10 0001 | jne \<arg1> \<arg2> \<address> | if ( arg1 != arg2) { jump(address) } |
| 34 | xx10 0010 | jinf \<arg1> \<arg2> \<address> | if (arg1 < arg2) { jump(address) } |
| 35 | xx10 0011 | jinfe \<arg1> \<arg2> \<address> | if (arg1 <= arg2) { jump(address) } |
| 36 | xx10 0100 | jsup \<arg1> \<arg2> \<address> | if (arg1 > arg2) { jump(address) } |
| 37 | xx10 0101 | jsupe \<arg1> \<arg2> \<address> | if (arg1 >= arg2) { jump(address) } |

## Source / Destination
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
