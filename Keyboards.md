# KEYBOARDS
## Program for Keyboard
### Code
``` Assembly
ORG 0000H
START: MOV R0, #00 
MOV P2, #0FFH 
MOV P1, #00H 
K1: MOV A, P2 
ANL A, #0FH 
CJNE A, #0FH, K1
LCALL DBOUN 
WAIT: MOV A, P2 
ANL A, #0FH
CJNE A, #0FH, K_IDEN 
SJMP WAIT
K_IDEN: LCALL DBOUN
MOV R4, #7FH 
MOV R2, #04 
MOV A, R4
NXT_ROW: RL A
MOV R4, A 
MOV P1, A 
MOV A, P2
ANL A, #0FH 
MOV R3, #04 
NXT_COLM: RRC A 
JNC KY_FND
INC R0
DJNZ R3, NXT_COLM
MOV A, R4
DJNZ R2, NXT_ROW
SJMP WAIT 
KY_FND: MOV A, R0 
SJMP CONTINUE
DBOUN: 
THR2: 
THR1: 
MOV R6, #10 
MOV R7, #250
NOP
NOP
DJNZ R7, THR1
DJNZ R6, THR2
RET
CONTINUE: MOV P3, A 
SJMP START

```
### Output
![image](https://github.com/user-attachments/assets/0840b9cf-ef32-49d0-88a8-4332d28866c5)
![WhatsApp Image 2024-10-18 at 08 14 51_9d2b4242](https://github.com/user-attachments/assets/586024d0-d1d2-4a95-981b-bb2dedb3c467)
![WhatsApp Image 2024-10-18 at 08 14 51_9e4099e0](https://github.com/user-attachments/assets/ff7d2c1e-be54-4327-ac1c-cf6708a3fa09)
![WhatsApp Image 2024-10-18 at 08 14 51_83df4a08](https://github.com/user-attachments/assets/1b3f03e5-6f4a-4d2d-af1c-63171a9d6409)


## 2s delay
### Code
``` Assembly
ORG 0000H
MOV TMOD, #01H
HERE: MOV R0,#40
YO: MOV TL0,#60H
MOV TH0,#3CH
SETB TR0
WAIT: JNB TF0, WAIT
CLR TR0
CLR TF0
DJNZ R0, YO
CPL P1.0
SJMP HERE
```
### Output
![image](https://github.com/user-attachments/assets/3ba22ec7-9e68-4448-986c-e1e4f48489f2)
