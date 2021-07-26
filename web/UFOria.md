# UFOria

## Challenge information:
  UFOria specializes in organizing your trip to space. Get some tickets while they last!

### Flag 1 [75 points]:
####   Description:
  Can you get a valid invite code? The flag is the invite code.

####   Solution:
  So, there is 3 tours in UFOria website. And of course works only expensive one.
  
  ![изображение](https://user-images.githubusercontent.com/17177071/127030515-c1105caf-4206-49b1-a9fa-6a63aaa59560.png)

  
  
  It asks for invite code. Lets invistegate.
  
  ![изображение](https://user-images.githubusercontent.com/17177071/127030550-4f3c8d01-33aa-45f2-a4eb-3beb63a000dd.png)
  
  It calls contactus() fucnction on click. There it is:
  ```
  function contactus() {
      var code = prompt("This option is invitation only. Enter your invite code:");

      var verify = (function(code) {
          if (code.length != 12) { return false; }

          var parts = [code.substr(0,3), code.substr(4,4), code.substr(9,3)];
          if (parts.join("-") != code) { return false; }

          if (parts[0] != "UFO") { return false; }
          if (parts[1] != btoa("UFO")) { return false; }
          if (parts[2] != ("UFO".charCodeAt(0) + "UFO".charCodeAt(1) + "UFO".charCodeAt(2))) { return false; }

          return true;
      })(code);

      if (verify) {
          alert("Great, please continue the booking process by sending us an email with your invitation code.")        
      } else {
          alert("Wrong invite code.")
      }
  }
  ```
  We can tell that code is 12 characters long and consists of 3 parts delimited with dash. First part is just "UFO". 
  Second part is "UFO" encoded in base64 ("VUZP")
  Third part is sum of charcodes of UFO letters ("234")

  Invite code: "UFO-VUZP-234"
  **Flag: UFO-VUZP-234**

### Flag 2 [75 points]: 
####   Members only

####   Desription:
  Can you access the members-only area?

####   Solution:
  Let's see what in memebers page. 
  
  ![изображение](https://user-images.githubusercontent.com/17177071/127030670-cbc976b3-b0e4-4199-8576-9aa63d867acb.png)

  
  And there is login form with "I've forgotten my password." link.
  
  ![изображение](https://user-images.githubusercontent.com/17177071/127030722-7b6fcc70-0e61-4292-8dae-35fc0cc347d3.png)
  
  It is shows input for username.
  As secoond category being "osint" I think it is not SQLInjection and we must look closely to the site.
  There is name two in About page: Ben Organa (aka borgana), UFOria CEO and Elliot Talton. 
  
  ![изображение](https://user-images.githubusercontent.com/17177071/127030813-cca4b536-00fa-4b08-bdcd-1e4448413d83.png)
  
  Let's try restore borganas password. 
  Looks like he is in members databade. But we need to know what his place of birth for security question.

  There is two links in the footer: on linkedin and twitter. Twitter link is not working, so we need to do some osint in linkedid
  Tiying to find Ben Organa in linked in. No luck. Trying Elliot Talton. Bingo! He is CEO of UFOria too. 
  
  ![изображение](https://user-images.githubusercontent.com/17177071/127031020-96aefe7f-2ad9-4642-b309-0956180d7ca9.png)
  
  About page says: "I can never forget the day that we decided to establish the pillars of this company with Elliot Talton in our trip to our home town."
  So it means that his bitrh of place same with Ben. Nice.
  In Elliots posts I found this: "Visiting 's Lands Huys Café reminds me of all the sweet childhood memories".
  
  ![изображение](https://user-images.githubusercontent.com/17177071/127031119-f77cfc56-2fd0-4bee-aaaa-4cabf7cc6997.png)
  
  Checking where it is at Google maps: Marktplein 2, 9545 PH Bourtange, Netherland. 

  Trying "Bourtange" as place of bith. YES! "Your password is 'fataborgana42', please remember it this time!"

![изображение](https://user-images.githubusercontent.com/17177071/127031221-17fa7273-0d64-48a1-ab09-dd657c041b27.png)

  Loging with borgana and fataborgana42 and get the flag.
  
  ![изображение](https://user-images.githubusercontent.com/17177071/127031285-b8e8101a-b4ae-4f57-b58b-0ee006f4d302.png)


  **FLAG: CTF{fataborgana42}**
