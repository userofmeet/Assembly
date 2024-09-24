## Instructions to transfer the value 10H to internal RAM location 8H, external ram location 0008H and 0100H.
## Assembly code
``` assembly
ORG 0000H
MOV 08H, #10H
MOV A, #10H
MOV DPTR, #0008H
MOVX @DPTR, A
MOV DPTR, #0100H
MOVX @DPTR, A
END
```
## Write an instruction or a set of instructions to transfer a byte from internal RAM location 7H to external RAM location 0007H, 0010H and 0100H.
## Assembly code
``` Assembly
ORG 0000H
MOV A, 07H
MOV DPTR, #0007H
MOVX @DPTR, A
MOV DPTR, #0010H
MOVX @DPTR, A
MOV DPTR, #0100H
MOVX @DPTR, A
END
```

## Inverse of the above program
## Assembly code
``` Assembly
ORG 0000H
MOV DPTR, #07H
MOVX A, @DPTR
MOV 07H, A
MOV DPTR, #10H
MOVX A, @DPTR
MOV 07H, A
MOV DPTR, #0100H
MOVX A, @DPTR
MOV 07H, A
END
```

## Write a program to transfer byte from code memory to internal RAM and external RAM.
## Assembly code
``` Assembly
ORG 0000H
MOV DPTR, #1000H
MOVC A, @A+DPTR
MOV 07H, A
MOV DPTR, #0100H
MOVX @DPTR, A
END
```

## Write a program to transfer byte from external RAM to external ROM.
## Assembly code
``` Assembly
ORG 0000H
MOV DPTR, #0007H
MOVX A, @DPTR
MOV DPTR, #0066H
MOVX @DPTR, A
END
```
