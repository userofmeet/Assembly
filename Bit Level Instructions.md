``` Assembly
mov a,30h;
clr c;
mov psw.4,c;
mov psw.3,c;
mov r0,#0ch;
mov 20h,#0eh;
mov c,acc.0;
cpl c;
mov 01h,c;
mov a,20h;
orl a,r0;
mov r0,a;
```
## Reduce the length of the above program.
### Code
``` Assembly
mov a,30h;
clr c;
ANL PSW, #0E7H
mov r0,#0ch;
mov 20h,#0eh;
mov c,acc.0;
cpl c;
mov 01h,c;
mov a,20h;
orl a,r0;
mov r0,a;
```

## Rewrite the above program so as to repeat the above operation on 10 eight-bit numbers starting from 30h.
### Code
``` Assembly
mov dptr, #30h
mov r2, #10
start: clr c
anl psw, #0e7h
movx a, @dptr
mov r0, #0ch
mov 20h, #0eh
mov c, acc.0
cpl c
mov 01h, c
orl a, r0
mov r0, a
inc dptr
djnz r2, start
```

## Implement the following function using bit level instruction. Y1 = ABC + ABC +ABC’
### Code
``` Assembly
MOV A, 20H
MOV C, 00H
ANL C, 01H
ANL C, 02H
MOV 06H, C
MOV C, 03H
ANL C, 04H
ANL C, 05H
ORL C, 06H
MOV 06H, C
MOV A, 21H
MOV C, 08H
ANL C, 09H
ANL C, 0AH
ORL C, /`06H
```

## Implement function function using bit level instruction. Y2 = AB’C + ABC’ +A’B’C’
### Code
``` Assembly
MOV A, 20H
MOV C, 00H
ANL C, /01H
ANL C, 02H
MOV 06H, C
MOV C, 03H
ANL C, 04H
ANL C, /05H
ORL C, 06H
MOV 06H, C
MOV A, 21H
MOV C, /08H
ANL C, /09H
ANL C, /0AH
ORL C, 06H
```
