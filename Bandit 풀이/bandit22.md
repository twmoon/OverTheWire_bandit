## [Bandit #22](https://overthewire.org/wargames/bandit/bandit22.html)

https://overthewire.org/wargames/bandit/bandit22.html
> A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

``` ssh bandit21@bandit.labs.overthewire.org -p 2220 ```으로 로그인  

암호는 [전에](./bandit21.md) 찾은 ```gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr```

생소한거 투성이다. 일단 ```cron```을 찾아보니까 시간 기반 작업 스케줄러라고 한다. 윈도우 스켸줄러랑 비슷한 개념으로 받아드리면 될거같다.  
문제에서 ```/etc/cron.d/```에 파일이 있다고 하니까 들어가서 확인해보면 아래와 같이 나온다.
```
bandit21@bandit:~$ cd /etc/cron.d
bandit21@bandit:/etc/cron.d$ ls
cronjob_bandit15_root  cronjob_bandit22  cronjob_bandit24
cronjob_bandit17_root  cronjob_bandit23  cronjob_bandit25_root
bandit21@bandit:/etc/cron.d$ cat cronjob_bandit22
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```
