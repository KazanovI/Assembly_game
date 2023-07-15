DAT SEGMENT
l0 db '0','0','0','0','0','0','0','0','0','0'
l1 db '0','0','0','0','0','0','0','0','0','0'
l2 db '0','0','0','0','0','0','0','0','0','0'
l3 db '0','0','0','0','0','0','0','0','0','0'
l4 db '0','0','0','0','0','0','0','0','0','0'
l5 db '0','0','0','0','0','0','0','0','0','0'
l6 db '0','0','0','0','0','0','0','0','0','0'
l7 db '0','0','0','0','0','0','0','0','0','0'
l8 db '0','0','0','0','0','0','0','0','0','0'
l9 db '0','0','0','0','0','0','0','0','0','0'
line db 0dh,0ah,'$'
hi db "welcome to the game$"
insert db "insert the place where you want to put the bomb in scale of 11-88 without numbers with 0 and 9 at the end$"
count db "how many bombs you would like to put in scale of 1-9?$"
bomb db "the number of bombs that i found is:$"
DAT ENDS

S SEGMENT STACK
  DB 100H DUP (0)
S ENDS

CODE SEGMENT
  ASSUME DS :DAT , SS: S ,CS: CODE
  
START :
        MOV AX ,DAT
        MOV DS , AX 
        mov dx, offset hi
        mov ah,9
        int 21h
        call shura
        call hadpes
        call shura
        mov di,0
        mov al,0
        mov dx,offset count
        mov ah,9
        int 21h
        mov ah,7
        int 21h
        sub al,48
        mov ah,0
        add di,ax
       mov al,0
knisa: mov bx,offset l0
        call shura
        mov dx, offset insert
        mov ah,9
        int 21h
        mov ah,7
        int 21h
        sub al,48
        mov ah,al
        mov al,10
        mul ah
        mov cx,ax
        mov dl,al
        mov al,0
        mov ah,7
        int 21h
        sub al,48
        mov dh,0
        add dl,al
        add bx,dx
        mov dh,'*'
        mov [bx],dh
        call shura
        call hadpes
        call shura
        dec di
        cmp di,0
        jnz knisa
        mov ch,0
        mov al,8
        mov cl,8
        mov bx,10
        mov si,1
 again: mov di,bx
        add di,si
        mov ah,[di]
        cmp ah,'*'
        jz mine
        inc si
        dec al
        cmp al,0
        jz nextline
        jmp again
nextline: add bx,10
          mov si,1
          mov al,8
          dec cl
          cmp cl,0
         jnz again 
         mov dx, offset bomb
         mov ah,9
         int 21h
         call shura
         add ch,48
         mov dl,ch
         mov ah,2
         int 21h
         call shura
         call hadpes
         call shura
         jmp sof 	             
mine:    inc ch
         sub bx,10
         dec si
         mov di,bx
         add di,si
         mov ah,[di]
         cmp ah,'*'
         jz skip1
         inc ah
         mov [di],ah
skip1:   inc si
         mov di,bx
         add di,si
         mov ah,[di]
         cmp ah,'*'
         jz skip2
         inc ah
         mov [di],ah
skip2:   inc si 
         mov di,bx
         add di,si
         mov ah,[di]
         cmp ah,'*'
         jz skip3
         inc ah
         mov [di],ah
skip3:   add bx,10
         sub si,2
         mov di,bx
         add di,si
         mov ah,[di]
         cmp ah,'*'
         jz skip4
         inc ah
         mov [di],ah
skip4:   add si,2 
         mov di,bx
         add di,si
         mov ah,[di]
         cmp ah,'*'
         jz skip5
         inc ah
         mov [di],ah
skip5:   add bx,10
         sub si,2
         mov di,bx
         add di,si
         mov ah,[di]
         cmp ah,'*'
         jz skip6
         inc ah
         mov [di],ah
skip6:   inc si
         mov di,bx
         add di,si
         mov ah,[di]
         cmp ah,'*'
         jz skip7
         inc ah
         mov [di],ah
skip7:   inc si
         mov di,bx
         add di,si
         mov ah,[di]
         cmp ah,'*'
         jz skip8
         inc ah
         mov [di],ah
skip8:   sub bx,10
         dec al
         jmp again
         
        
hadpes:  mov bx,offset l1
         mov si,8
shuv:    mov cx,8  
next:    inc bx
         mov dl,[bx]
         mov ah,2
         int 21h
         loop next
         call shura
         add bx,2
         dec si
         cmp si,0
         jne shuv 
         ret
        
shura:  mov dx,offset line
        mov ah,9
        int 21h
        ret        
        
 sof:       MOV AX ,4C00H
        INT 21H
 CODE ENDS
 END START       
        
        