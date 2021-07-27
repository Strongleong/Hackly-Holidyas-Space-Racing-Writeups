# Power Snacks
## Challenge Information
Are you the very best PowerShell user? Try this challenge to get better acquainted with PowerShell's functionality. You need to come up with commands that result in a specific output. You can check your output by piping the result to the "Check" function.
E.g. Get-Content words | dosomething | Check

Note: do not use any format- function before piping to the Check function. Also note that the checker may not understand all sorts of inputs. Try piping your output to the Out-String function first, or make sure your output matches more closely to the given example. Lastly, instead of write-host, use write-output to be able to pipe to the checker.

### Flag 1 [25 points]

#### 42

#### Description:
Write a script that writes out all numbers (1 per line) from 1 to 1337, inclusive. However, if the number is divisible by 42, instead, print the string "Life, the universe, and everything".

#### Solution
So what I thought of immediately here is a for loop which goes from 1 to 1337, so that our variable is less than 1337, and within that for loop, we get an if statement which says that if a number is divisible by 42, or more 
technically, if the remainder of a number while dividing by 42 is 0, then we shall print "Life, the universe, and everything", else we shall our variable i. I had to do this in powershell, of course, so I learnt some syntax too.

#### Script:
```
$(for ($i = 1; $i -le 1337; $i++) {
    if ($i % 42 -eq 0) {
      Write-output "Life, the universe, and everything"
    }
    else {
      $i
    }
}) | Check
```
**FLAG**: CTF{using_your_powers_for_powershell}
