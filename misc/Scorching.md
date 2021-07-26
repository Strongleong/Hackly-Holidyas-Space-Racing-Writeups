# Scorching

## Challenge information
  Windows domains are hot. Scorching even. 
  Note: a domain controller is spun up on-demand. It may take a while to fully boot upon launch. 
  Verify whether it's online by checking if port 445 is open on 10.6.0.2.

## Files:    
  - hash.txt

### Flag 1 [75 points]:
####   Password

####   Desription:
  Can you find out the password for the hash in the file? It is the account for the "NAccount" user. 
  Hint: The password does not meet the password complexity policy as it is less than 8 characters and only includes letters and numbers.

####   Solution:
  The file contains NT:LM hash. With hint we can crack it with attack by mask with hashcat.
  **FLAG: H4cky21**