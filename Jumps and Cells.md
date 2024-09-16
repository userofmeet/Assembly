## Sample Program Code
``` Assembly
mov r1,#00h;
mov dptr,#0000h;
movx a,@dptr;
mov r0,a; r0=04h
again: inc dptr;
movx a,@dptr;
mov r7,a; r7=13h
lcall checkbcd; SP,PC
jnb 00h,next;
inc r1;
next: djnz r0,again;
inc dptr;
mov a,r1;
movx @dptr,a;
same: sjmp same;
checkbcd: clr 00h;
mov a,r7;
anl a,#0fh; a=03h
cjne a,#09h,lowhigh;
sjmp limit;
lowhigh: jnc back;
limit: mov a,r7;
anl a,#0f0h;
swap a;
cjne a,#09h,final;

setone: setb 00h;
Back: ret;
Final: jnc back;
sjmp setone;
end;
```

### Reduced length
``` Assembly
mov r1,#00h;
movx a,@dptr;
mov r0,a; r0=04h
again: inc dptr;
movx a,@dptr;
mov r7,a; r7=13h
lcall checkbcd; SP,PC
jnb 00h,next;
inc r1;
next: djnz r0,again;
inc dptr;
mov a,r1;
movx @dptr,a;
same: sjmp same;
checkbcd: clr 00h;
mov a,r7;
anl a,#0fh; a=03h
cjne a,#09h,lowhigh;
sjmp limit;
lowhigh: jnc back;
limit: mov a,r7;
anl a,#0f0h;
swap a;
cjne a,#09h,final;

setone: setb 00h;
Back: ret;
Final: jnc back;
sjmp setone;
end;
```

### Same program using JC instruction
``` Assembly
mov r1,#00h;
mov dptr,#0000h;
movx a,@dptr;
mov r0,a; r0=04h
again: inc dptr;
movx a,@dptr;
mov r7,a; r7=13h
lcall checkbcd; SP,PC
jnb 00h,next;
inc r1;
next: djnz r0,again;
inc dptr;
mov a,r1;
movx @dptr,a;
same: sjmp same;
checkbcd: clr 00h;
mov a,r7;
anl a,#0fh; a=03h
cjne a,#09h,lowhigh;
sjmp limit;
limit: mov a,r7;
anl a,#0f0h;
swap a;
cjne a,#09h,final;
sjmp setone
setone: setb 00h;
clr c
lowhigh: jc limit
Back: ret;
Final: jc setone;
sjmp back;
end;
```

### Same program using JB instruction
``` Assembly
mov r1,#00h;
mov dptr,#0000h;
movx a,@dptr;
mov r0,a; r0=04h
again: inc dptr;
movx a,@dptr;
mov r7,a; r7=13h
lcall checkbcd; SP,PC
jb 00h,next;
inc r1;
next: djnz r0,again;
inc dptr;
mov a,r1;
movx @dptr,a;
same: sjmp same;
checkbcd: setb 00h;
mov a,r7;
anl a,#0fh; a=03h
cjne a,#09h,lowhigh;
sjmp limit;
lowhigh: jnc back
limit: mov a,r7;
anl a,#0f0h;
swap a;
cjne a,#09h,final;
clearone: clr 00h;
Back: ret;
Final: jnc back;
sjmp clearone;
end;
```

## 1. Array of BCD numbers starts from 4001h in memory. End of the array is detected by a non-BCD number
``` Assembly
MOV R1, #00H
MOV DPTR, #4000H
AGAIN:MOVX A, @DPTR
MOV R7, A
LCALL CHECKBCD
INC DPTR
JB 00H, AGAIN
SAME: SJMP SAME
CHECKBCD: CLR 00H
MOV A, R7
ANL A, #0FH
CJNE A, #09H, LOWHIGH
SJMP LIMIT
LOWHIGH: JNC BACK
LIMIT: MOV A, R7
ANL A, #0F0H
SWAP A
CJNE A, #09H, FINAL
SETONE: SETB 00H
INC R1
BACK: RET
FINAL: JNC BACK
SJMP SETONE
END
```

## Program to transfer 10 bytes from external RAM location 30H onwards to 300H onwards.
### Code
``` Assembly
ORG 0000H
MOV DPTR, #0030H
MOV R2, #10
MOV R3, #00H
MOV R4, #03H
TRANSFER: MOVX A, @DPTR
MOV R5, DPL
MOV R6, DPH
MOV DPL, R3
MOV DPH, R4
INC R3
MOVX @DPTR, A
MOV DPL, R5
MOV DPH, R6
INC DPTR
DJNZ R2, TRANSFER
```
### Results
#### Input
![image](https://github.com/user-attachments/assets/7a217808-66c2-44a4-b39c-24fec9164658)
#### Output
![image](https://github.com/user-attachments/assets/ba219fba-d570-4790-bc80-51857ca281b3)

## Program to transfer 10 bytes from internal RAM 30H onwards to external RAM 30H onwards.
### Code
``` Assembly
ORG 0000H            
MOV R0, #30H         
MOV DPTR, #30H       
MOV R2, #10
TRANSFER: MOV A, @R0        
INC R0            
MOVX @DPTR, A     
INC DPTR          
DJNZ R2, TRANSFER 
END
```
### Results
#### Input
![image](https://github.com/user-attachments/assets/f7725323-d277-4036-ab6b-00cdbbe6b993)
#### Output
![image](https://github.com/user-attachments/assets/20454d0b-377e-4806-b6b2-41c720d83b52)

## Program usig procedure to find the number of one in DPTR.
### Code
``` Assembly
ORG 0000H
MOV DPL, 50H
MOV DPH, 51H
MOV R0, #08
MOV R1, #00H
PARITY: MOV A, DPH
ACALL CAL
MOV R0, #08
MOV A, DPL
ACALL CAL
MOV A, R1
SKIP: SJMP SKIP
CAL: RLC A
JNC FURTHER
INC R1
FURTHER: DJNZ R0, CAL
RET
```
### Results
![image](https://github.com/user-attachments/assets/1126e562-6df0-431d-965b-ff2fbb02df85)
