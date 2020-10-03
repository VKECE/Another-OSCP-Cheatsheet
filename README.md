# Another-OSCP-Cheatsheet
This is my personal OSCP cheatsheet that also "hopefully" would let me pass my exam. Any improvement is welcome :)

## POP3 enum
    for user in <user1> <user2> <user3>.. <userX>; do
    ( echo USER ${user}; sleep 2s; echo PASS abcd; sleep 2s; echo LIST; sleep 2s; echo quit) | nc -nvC <ip> <port>;  done
    
## Windows enumeration

    enum4linux -H <ip>		
    
    medusa -M smbnt -h <ip> -U userfile -P passfile -m GROUP:DOMAIN -v 4		
