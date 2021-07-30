# Kioptrix-level4-Walk-Through

# enumeration 

![image](https://user-images.githubusercontent.com/52453415/127605225-c5054e85-8d02-458b-8bbb-37e8ae47a1dd.png)

![image](https://user-images.githubusercontent.com/52453415/127605274-9f9c06a5-6e78-46aa-a1f3-cd138a9b67d3.png)

no services are vulnarable so i'll move on 



# i won't take the   brute forcing apporch, not now , iam not disperate yet :D 

# web server 

![image](https://user-images.githubusercontent.com/52453415/127604688-341539bf-9046-4c59-849f-2c688cbaabf7.png)

user Admin

pass 'or'1'='1'--

sql error , seems to be injectable 

so i've used burbsuit to take the post data to be injected and with aid of sqlmap  any thing could be usfull so dump every thing ,


![image](https://user-images.githubusercontent.com/52453415/127605081-d87fbfe8-a23d-4fea-a98d-714ecbc5826b.png)

first thing to find is credential and some interestig tables :D 

![image](https://user-images.githubusercontent.com/52453415/127605400-72ddc29e-bfea-4dfe-a8dd-86bf75860bbe.png)

![image](https://user-images.githubusercontent.com/52453415/127605668-8739f0d4-66d8-4dcd-8357-1f6302fa8a82.png)


using robert's credentials we got very limited ssh shell 

![image](https://user-images.githubusercontent.com/52453415/127606289-03c7e5dc-badb-4616-9239-7bcdb09e9e17.png)

i get kicked if i tried any other commands 

but when i write sudo , there is a python error happens

![image](https://user-images.githubusercontent.com/52453415/127606740-c32a8ac0-89bf-4bb3-be0b-2ebe1e4bce60.png)

so i'am in some sort of python environment that acts like a shell (LShell)  and using the kshell 

i've searched the internet for this and i learned that 

![image](https://user-images.githubusercontent.com/52453415/127610173-5f06c27f-8678-40a7-8a60-25edeb169b8c.png)


so i've searched for vulnarabilities on this LSHELL and i've found this  this 


https://www.exploit-db.com/exploits/39632

run the exploit and w've escaped the very limited shell to less limited robert shell

![image](https://user-images.githubusercontent.com/52453415/127615126-6fe7ff5b-34a2-4fdd-9768-52f0e8dd2f45.png)


navigate to root , it's  preimitted and there is a flag !!!!!!!!!!

![image](https://user-images.githubusercontent.com/52453415/127617379-c0ce7fec-4803-4c1c-b46b-b4eac98f0287.png)

![image](https://user-images.githubusercontent.com/52453415/127617461-6cd1f526-7f08-4727-9503-eca5b236770c.png)

i've got the flag before i get the root access , any way 



#  priv Esc

i've navigated to lshell directory and tried  to change the restictation from the conf file but i've failled 

![image](https://user-images.githubusercontent.com/52453415/127621161-cb0c2cfd-c73b-40c0-bce5-09aba09aba82.png)

couldn't get .ssh keys also 

![image](https://user-images.githubusercontent.com/52453415/127621757-26f50203-a383-4e0d-a7bf-d50d9dc835ff.png)


i've moved to sql dierctory 

ls 

![image](https://user-images.githubusercontent.com/52453415/127605962-4e46ac48-8947-49c9-8418-3af26115a92e.png)

Awosome we've got the root credential

![image](https://user-images.githubusercontent.com/52453415/127606019-2d537514-7ed8-4f2b-aeb0-052e2d53322a.png)


so what else we need to get root shell ? since the sql running as a root we need to find a system level function 

remember that tabel ?? like i siad any thing can  be usfull

![image](https://user-images.githubusercontent.com/52453415/127660741-48311092-391f-4657-a0a3-e5d925a4d8e0.png)

searchig the web i've learned that this function is what we looking for 

![image](https://user-images.githubusercontent.com/52453415/127665638-c156de44-9434-4190-bb09-5057efb54361.png)

using the function 

mysql> use mysql;

select sys_exec('chmod u+s /bin/bash');


![image](https://user-images.githubusercontent.com/52453415/127665696-2f7cdaac-69ab-49cf-9922-b5ab4d08bc47.png)

exit 

now check if it worked 

![image](https://user-images.githubusercontent.com/52453415/127665908-b47820a3-f32a-4c9b-b987-b8d5ef5322c3.png)

it did :D 

no need to search for the flag we already found it before 
