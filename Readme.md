Hi , This is my learing path ..

# First learning C program to adding by Default text on opeining sudo mode 

#include  <stdio.h>

int main(int  argc , char  *argv[]){
        if(argc==2){
        printf("Knok , Knock %s\n" , argv[1]);

}
else{
        fprintf(stderr, "Usage: %s <name>\n",argv[0]);
        return 1;
}
return 0;
}

# compiling it using
gcc first.c -o first 

# running
./first janpreet

# Adding to .bashrc and .bash_profile for always start on doing sudo su 

# .bashrc
export PATH=$PATH:/home/janpreet
echo "Knock , Knock : $USER"

# .bash_profile
[ -f ~/.bashrc ] && . ~/.bashrc




## Next creating the same script using python
#!/usr/bin/python3.6

import sys

if len(sys.argv)==2:
    print("Knock Knock {0}".format(sys.argv[1]))
else:
    sys.stderr.write("Usage: {0} <name>\n".format(sys.argv[0]))


# Here shebang is used to directly run this script as python not using cmd python first.py , Drectly ./first.py




## Reversing and cracking my first code 

Here First thing is the knowlwdge of Assembly Code here as from 
https://github.com/LiveOverflow/liveoverflow_youtube/tree/master/0x05_simple_crackme_intro_assembler

Here in liscence Assembly code i analyzed it 

Dump of assembler code for function main:
   0x00000000004005bd <+0>:	push   rbp
   0x00000000004005be <+1>:	mov    rbp,rsp
   0x00000000004005c1 <+4>:	sub    rsp,0x10
   0x00000000004005c5 <+8>:	mov    DWORD PTR [rbp-0x4],edi
   0x00000000004005c8 <+11>:	mov    QWORD PTR [rbp-0x10],rsi
   0x00000000004005cc <+15>:	cmp    DWORD PTR [rbp-0x4],0x2
   0x00000000004005d0 <+19>:	jne    0x400623 <main+102>
   0x00000000004005d2 <+21>:	mov    rax,QWORD PTR [rbp-0x10]
   0x00000000004005d6 <+25>:	add    rax,0x8
   0x00000000004005da <+29>:	mov    rax,QWORD PTR [rax]
   0x00000000004005dd <+32>:	mov    rsi,rax
   0x00000000004005e0 <+35>:	mov    edi,0x4006c4
   0x00000000004005e5 <+40>:	mov    eax,0x0
   0x00000000004005ea <+45>:	call   0x400490 <printf@plt>
   0x00000000004005ef <+50>:	mov    rax,QWORD PTR [rbp-0x10]
   0x00000000004005f3 <+54>:	add    rax,0x8
   0x00000000004005f7 <+58>:	mov    rax,QWORD PTR [rax]
   0x00000000004005fa <+61>:	mov    esi,0x4006da
   0x00000000004005ff <+66>:	mov    rdi,rax
   0x0000000000400602 <+69>:	call   0x4004b0 <strcmp@plt>
   0x0000000000400607 <+74>:	test   eax,eax
   0x0000000000400609 <+76>:	jne    0x400617 <main+90>
   0x000000000040060b <+78>:	mov    edi,0x4006ea
   0x0000000000400610 <+83>:	call   0x400480 <puts@plt>
   0x0000000000400615 <+88>:	jmp    0x40062d <main+112>
   0x0000000000400617 <+90>:	mov    edi,0x4006fa
   0x000000000040061c <+95>:	call   0x400480 <puts@plt>
   0x0000000000400621 <+100>:	jmp    0x40062d <main+112>
   0x0000000000400623 <+102>:	mov    edi,0x400701
   0x0000000000400628 <+107>:	call   0x400480 <puts@plt>
   0x000000000040062d <+112>:	mov    eax,0x0
   0x0000000000400632 <+117>:	leave  
   0x0000000000400633 <+118>:	ret    


   Here i found and understood the flow o this and then disassemble it from main and undertood each step by ni cmd and implemented break points and so that i could analyze the point from where the logic gets changed and changed the ex value to 0 so that the strcmp function sets iszerovalue to 1 means it interpret y fake passwd to be true and give Access Granted 

   



##
