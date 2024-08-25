## Complement the lower nibble and set the higher nibble to 1111 
### Code
``` Assembly
ORG 0000H
MOV DPTR, #00H
MOVX A, @DPTR
CPL A
ORL A, #0F0H
MOVX @DPTR, A
END
```
### Result
![image](https://github.com/user-attachments/assets/b5e4e0ed-101a-465a-a332-871397e1c1c0)

## Parity of 16 bit number
### Code
``` Assembly
ORG 0000H 
// 16 BIT NUMBER: F1F0H
MOV R0, #0F0H	// Lower Bit
MOV R1, #0F1H	// Higher Bit
MOV R2, #9
MOV R3, #00H	// Number of 1s
MOV R4, #00H	// Number of 0s
LOWER: MOV A, R0
CLR C
RLC A
JC PLUS
SJMP SKIP
PLUS: INC R3
SJMP SKIP
SKIP: MOV R0, A
DJNZ R2, LOWER
MOV R2, #9
HIGHER: MOV A, R1
CLR C
RLC A
JC INCREASE
SJMP SKIPTHIS
INCREASE: INC R3
SJMP SKIPTHIS
SKIPTHIS: MOV R1, A
DJNZ R2, HIGHER
MOV A, #10H
CLR C
SUBB A, R3
MOV R4, A
END
```
### Result
![image](https://github.com/user-attachments/assets/8a021336-3626-44b4-b896-2ca2deabb0bd)


