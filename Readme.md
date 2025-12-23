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




##
