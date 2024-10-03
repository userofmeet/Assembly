## Sample
### Code
``` Assembly
org 0000h
ljmp main

org 0040h
main:
mov r0,#00h
mov tl0,#3ch
mov th0,#5dh
mov tmod,#01h
mov ie,#82h
setb tr0
here: cjne r0,#20h,here //done by MCU, parrellel timers generates delay
cpl p1.0
mov r0,#00h
sjmp here

org 000bh
inc r0
mov tl0,#3ch
mov th0,#5dh
reti
end
```
### Output
![image](https://github.com/user-attachments/assets/68303199-652c-413c-836b-b0a63493bd5c)


### Code
``` Assembly
ORG 0000H
SJMP MAIN

ORG 0030H
MAIN: MOV R0, #00H
MOV TL0, #3CH
MOV TH0, #5CH
MOV TMOD, #01H
MOV IE, #82H
SETB TR0
THERE:
HERE: CJNE R0, #100, HERE
CPL P1.0
MOV R0, #00H
SJMP HERE

ORG 000BH
INC R0
MOV R1, #20H
MOV TL0, #3CH
MOV TH0, #5CH
DJNZ R1, THERE
RETI
END
```
