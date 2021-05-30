## [Bandit #23](https://overthewire.org/wargames/bandit/bandit23.html)

https://overthewire.org/wargames/bandit/bandit23.html
> A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.
>> NOTE: Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.

``` ssh bandit22@bandit.labs.overthewire.org -p 2220 ```으로 로그인  

암호는 [전에](./bandit22.md) 찾은 ```Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI```

전 문제와 같이 기본적인 과정을 쭉해보면
```
bandit22@bandit:~$ cd /etc/cron.d
bandit22@bandit:/etc/cron.d$ ls
cronjob_bandit15_root  cronjob_bandit17_root  cronjob_bandit22  cronjob_bandit23  cronjob_bandit24  cronjob_bandit25_root
bandit22@bandit:/etc/cron.d$ file cronjob_bandit23
cronjob_bandit23: ASCII text
bandit22@bandit:/etc/cron.d$ cat cronjob_bandit23
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
bandit22@bandit:/etc/cron.d$ file /usr/bin/cronjob_bandit23.sh
/usr/bin/cronjob_bandit23.sh: Bourne-Again shell script, ASCII text executable
```
```
bandit22@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit23.sh
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```
순차적으로 해석해보면 ```myname```에 ```$whoami```값을 넘겨준다  
여기서 ```whoami```는 현재 유저 이름이므로 ```bandit23```이다.
