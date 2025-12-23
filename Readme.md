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




##
