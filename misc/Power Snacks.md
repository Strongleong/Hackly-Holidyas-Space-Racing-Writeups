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
**FLAG: CTF{using_your_powers_for_powershell}**

### Flag 3 [30 points]:

####   TSV

####   Description:
  In the tab-separated file "passwords.tsv" you get an overview of often-used passwords. Can you give us an overview of the number of passwords per category? Sort the result by descending count. Example excerpt given below:
  Name     Count
  ----     -----
  ..          ..
  nerdy       30
  animal      19
  ..          .. 

#### Solution:
  Lets look at the "passwords.tsv" file:
```
PS /workdir> cat ./passwords.tsv
Password        size    category        rank    note
123456  20      alphanumeric    1
password        20      security        1
12345678        18      alphanumeric    3
.............
```

  So it have 5 columns. We need only one: category. 
  There is my plan of action: first we need to get all categories and sort them. Then count categorites and save it as {Category; Count} object. Then sort this object and we all set!
  
### Script:
```
$passw = @();
foreach($line in Get-Content ./passwords.tsv)
{
	$pass = $line -split "\t";
	if ($pass[2] -eq "category")
	{
		continue
	}
	$passw += $pass[2]	
};
$passw = $passw | sort; 
$count = 0;
$name = $passw[0];
$res = @();
foreach($line in $passw)
{
	if($name -eq $line) 
	{
		$count++;
	}
	else
	{
		$res += [pscustomobject]@{Name = $name;Count = $count + 1};
		$count = 0
	};
	$name = $line;
};

$res[0].Count = $res[0].Count - 1
$res += [pscustomobject]@{Name = $name;Count = $count + 1};

$res | sort -Property @{Expression="Count";Descending=$True} |  Check
```

  **FLAG: CTF{powerful_password_filtering}**

### Flag 4 [30 points]:

####   Names

####   Description:
  Given the passwords file, supply a list of passwords from the 'names' category ordered first by ascending password length, then alphabetically. Example excerpt given below:
  ..
  scott
  steve
  albert
  alexis
  ..

####   Solution:
  It is easier then last flag. Just loop for the passwords file and if category is "names" save pass in array as {Len, Pass} object where "Len" is length of password (for simple sorting).

####   Script:
```
$passw = @();
foreach($line in Get-Content ./passwords.tsv)
{
	$pass = $line -split "\t";
	if($pass[2] -eq "names")
	{
		$passw += [pscustomobject]@{Len=$pass[0].Length;Pass=$pass[0]}
	}
};
$passw | sort -Property Len, Pass | Select-Object -ExpandProperty Pass | Check
```
  **FLAG: CTF{im_a_powershell_pro}**