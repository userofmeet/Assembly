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

