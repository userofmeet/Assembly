## Write a program to prove that 3CE7H+3B8DH = 7874
### Code
``` Assembly
ORG 0000H
MOV A, #0E7H
ADDC A, #8DH
MOV 42H, A
MOV A, #3CH
ADDC A, #3BH
MOV 41H, A
END
```
### Results
![image](https://github.com/user-attachments/assets/052998c0-f206-4256-b76d-1dbe3944b144)

## Prove that 9C+64=100 and AC=1,P=0
### Code
``` Assembly
ORG 0000H
MOV A, #9CH
ADDC A, #64H
END
```
## Results
![image](https://github.com/user-attachments/assets/27bff5ae-b14b-4525-95dc-026c0cec1d16)

## Addition of two 32 bit numbers
### Code
``` Assembly
ORG 0000H
MOV A, #01H
ADDC A, #0EEH
MOV 53H, A
MOV A, #00H
ADDC A, #0EEH
MOV 52H, A
MOV A, #00H
ADDC A, #0EEH
MOV 51H, A
MOV A, #10H
ADDC A, #0FH
MOV 50H, A
END
```
## Results
![image](https://github.com/user-attachments/assets/a1402d28-5764-4843-a8c2-e8d5f234b5ec)

## Subtraction of two 32 bit numbers
### Code
``` Assembly
ORG 0000H
MOV A, #01H
SUBB A, #0EEH
MOV 53H, A
MOV A, #00H
SUBB A, #0EEH
MOV 52H, A
MOV A, #00H
SUBB A, #0EEH
MOV 51H, A
MOV A, #10H
SUBB A, #0FH
MOV 50H, A
END
```
## Results
![image](https://github.com/user-attachments/assets/c882cd7d-cdb6-42d3-bfae-9b581606b0f0)

## Program for reversing the elements of an array
### Code
``` Assembly
ORG 0000H
MOV R0, #50H
MOV R1, #74H
MOV R2, #10D
NEXT: MOV A, @R0
MOV @R1, A
INC R0
DEC R1
DJNZ R2, NEXT
END
```
### Results
![image](https://github.com/user-attachments/assets/dfc8b0c6-f4a1-408d-b939-790d0cb1a8de)

## Program to count number of positive negative and zero elements of an array 
### Code
``` Assembly
ORG 0000H
MOV R0, #30h
MOV R1, #10
MOV R2, #00H //Zero Counter
MOV R3, #00H //Postive Counter
MOV R4, #00H //Negative Counter
NEXT: MOV A, @R0
CLR C
JZ ZERO
RLC A
JC NEG
INC R3
SJMP SKIP
NEG: INC R4
SJMP SKIP
ZERO: INC R2
SKIP: INC R0
DJNZ R1, NEXT
END
```
### Results
#### Input
![image](https://github.com/user-attachments/assets/ca897f45-b01b-4543-a4d8-93c0cd85703e)
### Verification
![image](https://github.com/user-attachments/assets/52fbac05-8144-419c-a4f8-39c1f9608aab)


## Program for some signed addtions 
### Code
``` Assembly
ORG 0000H
MOV A, #-01
ADD A, #27
MOV R0, A
MOV A, #100
ADD A, #50
MOV R1, A
MOV A, #45
ADD A, #75
MOV R2, A
MOV A, #-30
ADD A, #-50
MOV R3, A
MOV A, #-70
ADD A, #-70
MOV R4, A
END
```
### Results
![image](https://github.com/user-attachments/assets/6d6a690e-98d6-448a-b78d-b94816602fb5)

## Program for Mul, Div and DAA of two numbers
### Code
```  Assembly
ORG 0000H     
MOV A, #05H
MOV B, #03H
MUL AB   
MOV R0, A         
MOV R1, B        
MOV A, #0CH         
MOV B, #04H         
DIV AB             
MOV R2, A
MOV R3, B           
MOV A, #25H         
ADD A, #0AAH         
DA A                
MOV R4, A          
END                
```
### Results
![image](https://github.com/user-attachments/assets/5bc37c91-d927-4af5-8582-4c914843fc62)
