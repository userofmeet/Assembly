## Sample
### Code
``` Assembly
org 0000h
ljmp main
org 000bh
inc r0
mov tl0,#3ch
mov th0,#5dh
cpl p1.0
reti
org 0100h
main: mov r0,#00h
mov tl0,#3ch
mov th0,#5dh
mov tmod,#01h
mov ie,#82h
setb tr0
here: cjne r0,#20h,here //done by MCU, parrellel timers generates delay
mov r0,#00h
sjmp here
end
```
### Output
![image](https://github.com/user-attachments/assets/d1aebeed-e747-4420-b359-31b7243b4ad8)


## Write a delay routine of 0.5ms, which is called 100 times which in turn is called 20 times.
### Code
``` Assembly
org 0000h 
ljmp 0300h
org 000bh 
inc r0 
clr tr0
mov tl0,#0ch 
mov th0,#0feh 
clr tf0
setb tr0
reti
org 0300h
mov r0,#00h 
mov tl0,#0ch 
mov th0,#0feh 
mov tmod,#01h 
mov ie,#82h 
setb tr0 
here1:mov r1,#100
here: cjne r0,#20,here  
mov r0,#00h 
djnz r1,here
cpl p1.0 
sjmp here1 
end
```
### Output
![image](https://github.com/user-attachments/assets/5e4c16c6-a9a5-4300-aad8-5a75b54f9c68)

## Every time you push the button the accumulator is incremented by one and the content is transferred to an external memory location
### Code
``` Assembly
ORG 0000H        
LJMP MAIN
ORG 0003H        
INC A
MOVX @DPTR, A
RETI
ORG 0100H
MAIN:
CLR A
MOV IE, #81H     
MOV DPTR, #300H    
SETB TCON.0
HERE: SJMP HERE
END
```
### Outputs
![image](https://github.com/user-attachments/assets/4d057904-1047-4b87-baac-fe760d789b8e)
![image](https://github.com/user-attachments/assets/0d82ed6f-d064-4590-8cb3-106e8752a4a3)

## Every time you push the button the accumulator is incremented by one and the content is transferred to an external memory location, also check the debounce this time

### Code
``` Assembly
ORG 0000H        
LJMP MAIN
ORG 0003H        
ACALL DEBOUNCE
INC A
MOVX @DPTR, A
RETI
ORG 0100H
MAIN:
CLR A
MOV IE, #81H     
MOV DPTR, #300H    
SETB TCON.0
YO: SJMP YO
DEBOUNCE: 
MOV R2, #20
AGAIN: MOV R3, #250
HERE: NOP
NOP 
DJNZ R3, HERE
DJNZ R2, AGAIN // 4 x 250 x 1 x 20 = 20ms + 3 x 0.02 = 20.06ms
RET
END
```
### Output
![image](https://github.com/user-attachments/assets/7e959591-725c-4caf-82fe-e92f20dde07c)
![image](https://github.com/user-attachments/assets/5dd2b720-7c01-4162-b1bf-76663c7157f6)
