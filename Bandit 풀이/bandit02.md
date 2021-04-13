## [Bandit #02](https://overthewire.org/wargames/bandit/bandit2.html)

https://overthewire.org/wargames/bandit/bandit2.html
> The password for the next level is stored in a file called - located in the home directory


``` ssh bandit1@bandit.labs.overthewire.org -p 2220 ```으로 로그인  

암호는 전에 찾은 ```boJ9jbbUNNfktd78OOpsqOltutMc3MY1```

```
bandit1@bandit:~$ bandit1@bandit:~$ ls
-
bandit1@bandit:~$ bandit1@bandit:~$ cat ./-
CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9
```

당연히 ```ls```로 시작한 후 ```cat ./-```로 파일 읽음  

리눅스에서 ```-```는  표준입력 기호로 다음에 입력받을 명령어를 **기다린다**  
따라서 ```cat -```는 작동하지 않고 경로를 나타내는 기호를 이용하여 ```cat ./-``` 해야지 출력된다!!
