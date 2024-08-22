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

##
