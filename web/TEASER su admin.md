# TEASER: su admin

## Challenge information:
  You arrived at the launch platform of SPACE RACE. Teams around you are preparing for the event the best they can by gathering their crew and designing their flag.
  At the outset of the camp you notice the Hacky Holidays admin base, you decide to stake-out and see what's happening. 
  After a while you notice that people are only allowed to access the admin base when they show the Hacky Holidays admin flag below.

## Files:
  - admin_flag.png

### Flag 1 [50 points]:
####   Identify yourself

####   Desription:
  Open the flag designer and see if you can hack your way into the admin base.
  Note: Only the URL https://portal.hackazon.org/flagdesigner and its sub-URLs are part of the teaser challenge.


####  Solution:
  So I opened the link and I saw flag generator. After a little investigation with Firefox developer tools, in the network tab I saw that after each button a GET request is made and a special url is made with respect to the buttons pressed.
        ``` https://portal.hackazon.org/flagdesigner/api/flag/6/8/10/3/5/3/5/5.svg```

   We can assume that api has all possible flags and numbers, since in the url after /flag folder, there are the numbers of overlays and colors.
   After trying to make a flag that looks like an admin flag we can see that there is no "overlay #1" that looks like the one in admin flag. 
   The second digit is responsible for "overlay #1". There are 14 different overlays #1 shown but let's try to get 15.
        ``` /flagdesigner/api/flag/7/15/9/5/2/4/3/1.svg ```

   We get the flag now. The flag is in an image.

   **FLAG: CTF{YOU-HAZ-ADMIN-FLAG}**
