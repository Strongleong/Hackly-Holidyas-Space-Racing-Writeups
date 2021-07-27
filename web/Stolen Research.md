# Stolen Research

## Challenge information:
  A malicious actor has broken into our research centre and has stolen some important information. 
  Help us investigate their confiscated laptop memory dump! 
  Note: if you need to crack passwords during this challenge, all potential passwords apear in rockyou-75.txt. 
  Note 2: the pcap is only relevant for the last subtask. 
  Note 2: do NOT attempt to brute-force rockyou-75.txt against the flag submission - it will get your IP banned.

## Files:    
  - memdump.vmem.7z
  - stolen.pcapng 

### Flag 1 [25 points]:
####   Kernel release

####   Desription:
  What sort of OS and kernel is the actor using? Give us the kernel release version (the output of the 'uname -r' command).

####   Solution:
  After grepping strings with "windows" and "linux" keywords, I finally thought that the actor was using Kali Linux. I asked my teammate with Kali to run the command "uname -r" and the result was correct!
  
  **FLAG: 5.10.0-kali8-amd64**

### Flag 2 [125 points]:
####   Tooling

####   Desription:
  Hope you made a good custom profile in the meantime... 
  The attacker is using some tooling for reconaissance purposes. 
  Give us the parent process ID, process ID, and tool name (not the process name) in the following format: PPID_PID_NAME

#### Solution

  For this we will use the tool "Volatility". It is a very great tool for exploring memory dumps. It needs to have a profile with the exact OS and kernel version as the computer from the dumped memory.
  Let's check bash history.

```        
strongleong@WIN-U8I7TONIUR7:~$ vol.py --profile Linux5_10_0-kali8-amd64x64 -f memdump.vmem linux_bash
Volatility Foundation Volatility Framework 2.6.1
WARNING : volatility.debug    : Overlay structure cpuinfo_x86 not present in vtypes
WARNING : volatility.debug    : Overlay structure cpuinfo_x86 not present in vtypes
Pid      Name                 Command Time                   Command
-------- -------------------- ------------------------------ -------
    1058 bash                 2021-07-01 10:32:09 UTC+0000   exit
    1058 bash                 2021-07-01 10:32:09 UTC+0000   bash
    1058 bash                 2021-07-01 10:32:09 UTC+0000   history
    1058 bash                 2021-07-01 10:32:09 UTC+0000   sudo reboot
    1058 bash                 2021-07-01 10:32:09 UTC+0000   history
    1058 bash                 2021-07-01 10:32:09 UTC+0000   sudo reboot
    1058 bash                 2021-07-01 10:32:09 UTC+0000   id
    1058 bash                 2021-07-01 10:32:09 UTC+0000   passwd
    1058 bash                 2021-07-01 10:32:09 UTC+0000   exit
    1058 bash                 2021-07-01 10:32:29 UTC+0000   maltego
    1254 bash                 2021-07-01 10:33:50 UTC+0000   passwd
```        

  Maltego... Interesting...
  There is no maltego in powershell list. So maybe it is in the static environment variables?

```        
strongleong@WIN-U8I7TONIUR7:~$ vol.py --profile Linux5_10_0-kali8-amd64x64 -f memdump.vmem linux_psenv | grep maltego
Volatility Foundation Volatility Framework 2.6.1
WARNING : volatility.debug    : Overlay structure cpuinfo_x86 not present in vtypes
WARNING : volatility.debug    : Overlay structure cpuinfo_x86 not present in vtypes
bash              1082   LESS_TERMCAP_se= POWERSHELL_TELEMETRY_OPTOUT=1 LANGUAGE= USER=invictus LESS_TERMCAP_ue= XDG_SEAT=seat0 SSH_AGENT_PID=795 XDG_SESSION_TYPE=x11 SHLVL=1 HOME=/home/invictus OLDPWD=/home/invictus DESKTOP_SESSION=lightdm-xsession PANEL_GDK_CORE_DEVICE_EVENTS=0 GTK_MODULES=gail:atk-bridge XDG_SEAT_PATH=/org/freedesktop/DisplayManager/Seat0 LESS_TERMCAP_so= COLORTERM=truecolor COMMAND_NOT_FOUND_INSTALL_PROMPT=1 QT_QPA_PLATFORMTHEME=qt5ct LOGNAME=invictus WINDOWID=0 LESS_TERMCAP_us= QT_AUTO_SCREEN_SCALE_FACTOR=0 _=/usr/bin/maltego XDG_SESSION_CLASS=user COLORFGBG=15;0 TERM=xterm-256color XDG_SESSION_ID=2 PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/local/games:/usr/games SESSION_MANAGER=local/kali:@/tmp/.ICE-unix/746,unix/kali:/tmp/.ICE-unix/746 GDM_LANG=en_US.utf8 XDG_SESSION_PATH=/org/freedesktop/DisplayManager/Session0 XDG_MENU_PREFIX=xfce- XDG_RUNTIME_DIR=/run/user/1001 DISPLAY=:0.0 LANG=en_US.UTF-8 XDG_CURRENT_DESKTOP=XFCE XDG_SESSION_DESKTOP=lightdm-xsession XAUTHORITY=/home/invictus/.Xauthority SSH_AUTH_SOCK=/tmp/ssh-TGNtdMlzIDN5/agent.746 XDG_GREETER_DATA_DIR=/var/lib/lightdm/data/invictus SHELL=/bin/bash QT_ACCESSIBILITY=1 GDMSESSION=lightdm-xsession LESS_TERMCAP_mb= LESS_TERMCAP_md= XDG_VTNR=7 PWD=/usr/share/maltego/bin LESS_TERMCAP_me= XDG_CONFIG_DIRS=/etc/xdg XDG_DATA_DIRS=/usr/share/xfce4:/usr/local/share/:/usr/share/:/usr/share
java              1208   SHELL=/bin/bash SESSION_MANAGER=local/kali:@/tmp/.ICE-unix/746,unix/kali:/tmp/.ICE-unix/746 WINDOWID=0 QT_ACCESSIBILITY=1 COLORTERM=truecolor XDG_CONFIG_DIRS=/etc/xdg XDG_SESSION_PATH=/org/freedesktop/DisplayManager/Session0 XDG_MENU_PREFIX=xfce- LANGUAGE= LESS_TERMCAP_se= LESS_TERMCAP_so= POWERSHELL_TELEMETRY_OPTOUT=1 SSH_AUTH_SOCK=/tmp/ssh-TGNtdMlzIDN5/agent.746 DESKTOP_SESSION=lightdm-xsession SSH_AGENT_PID=795 GTK_MODULES=gail:atk-bridge XDG_SEAT=seat0 PWD=/usr/share/maltego/bin XDG_SESSION_DESKTOP=lightdm-xsession LOGNAME=invictus QT_QPA_PLATFORMTHEME=qt5ct XDG_SESSION_TYPE=x11 PANEL_GDK_CORE_DEVICE_EVENTS=0 XAUTHORITY=/home/invictus/.Xauthority J2D_PIXMAPS=shared XDG_GREETER_DATA_DIR=/var/lib/lightdm/data/invictus COMMAND_NOT_FOUND_INSTALL_PROMPT=1 GDM_LANG=en_US.utf8 HOME=/home/invictus LANG=en_US.UTF-8 XDG_CURRENT_DESKTOP=XFCE XDG_SEAT_PATH=/org/freedesktop/DisplayManager/Seat0 XDG_SESSION_CLASS=user TERM=xterm-256color LESS_TERMCAP_mb= LESS_TERMCAP_me= LESS_TERMCAP_md= USER=invictus COLORFGBG=15;0 DISPLAY=:0.0 SHLVL=1 LESS_TERMCAP_ue= LESS_TERMCAP_us= XDG_VTNR=7 XDG_SESSION_ID=2 XDG_RUNTIME_DIR=/run/user/1001 QT_AUTO_SCREEN_SCALE_FACTOR=0 XDG_DATA_DIRS=/usr/share/xfce4:/usr/local/share/:/usr/share/:/usr/share PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/local/games:/usr/games GDMSESSION=lightdm-xsession OLDPWD=/home/invictus _=/usr/lib/jvm/default-java/bin/java
```        
        

  So we need to find a java process. Hmm..
        
  What is Maltego's PPID?

```        
strongleong@WIN-U8I7TONIUR7:~$ vol.py --profile Linux5_10_0-kali8-amd64x64 -f memdump.vmem linux_pstree 
Volatility Foundation Volatility Framework 2.6.1
WARNING : volatility.debug    : Overlay structure cpuinfo_x86 not present in vtypes
WARNING : volatility.debug    : Overlay structure cpuinfo_x86 not present in vtypes
..................
...bash              1082            1001
....java             1208            1001
..................
```
        

  There it is. PPID: 1082. PID: 1208. NAME: maltego.

  **FLAG: 1082_1208_maltego.**

### Flag 3 [100 points]
####   Password of the actor

####   Desription:
  What is the password of the actor?

####   Solution:
  So now we will dump the full filesystem ```vol.py --profile Linux5_10_0-kali8-amd64x64 -f memdump.vmem linux_recover_filesystem -D dump``` and check the shadow file:
  
```
strongleong@WIN-U8I7TONIUR7:~/dump$ cat etc/shadow
root:!:18777:0:99999:7:::
..........................
invictus:$y$j9T$i6GkFortXamhKHY0bpTN.0$FLCqzsvVB1ZnfpffqSuvdLgzwLJvkmz6.aHfyoo11NB:18808:0:99999:7:::
```

Ok, it is unusual hash. $y means yescrypt encryption. So we can crack it with johntheripper and we get:
```
strongleong@WIN-U8I7TONIUR7:~$ john --format=crypt -w=rockyou-75.txt hash
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Press 'q' or Ctrl-C to abort, almost any other key for status
security1        (?)
1g 0:00:04:16 100% 0.003897g/s 104.3p/s 104.3c/s 104.3C/s 020585..pimp10
Use the "--show" option to display all of the cracked passwords reliably
Session completed
```

  **Flag: security1**
