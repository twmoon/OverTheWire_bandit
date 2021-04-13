## [bandit1](https://overthewire.org/wargames/bandit/bandit1.html)

https://overthewire.org/wargames/bandit/bandit1.html
> The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.


``` ssh bandit0@bandit.labs.overthewire.org -p 2220 ```으로 로그인

 ``` ls ```로 먼저 파일 스캔 후 찾은 ```readme```를 ```cat```으로 읽기

```
bandit0@bandit:~$ ls
readme
bandit0@bandit:~$ cat readme
boJ9jbbUNNfktd78OOpsqOltutMc3MY1
```

비밀번호 ```boJ9jbbUNNfktd78OOpsqOltutMc3MY1```확보

```cat```은 리눅스에서 파일을 읽을때 가장 자주 사용하는 명령어!!!(Shout out to Dr.백)

