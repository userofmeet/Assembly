## Sample Program
### Code
``` Assembly
org 0000h
mov tmod, #10h;
repeat: mov tl1, #33h;
mov th1, #0feh;
setb tr1;
wait: jnb tf1, wait;
clr tr1;
clr tf1;
cpl p2.0;
sjmp repeat;
end
```
### Output 
![image](https://github.com/user-attachments/assets/0faa21d4-b2ed-4f1f-bb75-90579e24b5d2)

## For double frequency
### Code
``` Assembly
org 0000h
mov tmod, #10h;
repeat: mov tl1, #01ah;
mov th1, #0ffh;
setb tr1;
wait: jnb tf1, wait;
clr tr1;
clr tf1;
cpl p2.0;
sjmp repeat;
end
```
### Output
![image](https://github.com/user-attachments/assets/52c0ec3b-736c-46dc-98a2-55cbb0322bd7)

## PWM with ON time of 2 ms and an OFF time of 10 ms on pin P0.0 pin
### Code
``` Assembly
org 0000h
mov tmod, #10h;
repeat: 
setb p0.0
acall delay
clr p0.0;
acall delay
acall delay
acall delay
acall delay
acall delay
sjmp repeat
delay:
setb tr1
mov tl1, #30h;
mov th1, #0f8h;
wait: jnb tf1, wait;
clr tr1;
clr tf1;
ret
end
```
### Output
![image](https://github.com/user-attachments/assets/f166b603-b795-4ef3-9118-b860f34926f9)


## Generate square wave of frequencies 2 KHz and 10 KHz on P1.0 and P1.2 respectively.
### Code
``` Assembly
ORG 0000H
MOV TMOD, #10H
AGAIN:
LCALL DELAY
CPL P1.2
LCALL DELAY
CPL P1.2
LCALL DELAY
CPL P1.2
LCALL DELAY
CPL P1.2
LCALL DELAY
CPL P1.2
CPL P1.0
SJMP AGAIN
DELAY:
MOV TL1, #01H
MOV TH1, #0FFH
SETB TR1
WAIT: JNB TF1, WAIT
CLR TR1
CLR TF1
RET
END
```
### Output
![image](https://github.com/user-attachments/assets/ae04fead-851c-421c-9d58-111ed8de3d32)

## Count external pulses applied to Timer 1 input T1 (P3.5 pin). Display continuously the count on P2 (LSByte) and P1 (MSByte).
### Code
``` Assembly
ORG 0000H
MOV TMOD, #50H
MOV TL1, #00H
MOV TH1, #00H
MOV P2, #00H
MOV P1, #00H
SETB P3.5
SETB TR1
AGAIN: MOV P2, TL1
MOV P1, TH1
SJMP AGAIN
END
```
### Output
![image](https://github.com/user-attachments/assets/5e048e9e-ebbc-49dd-bc63-7bcab8b7bf96)
