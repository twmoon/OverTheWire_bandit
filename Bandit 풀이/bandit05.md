## [Bandit #05](https://overthewire.org/wargames/bandit/bandit5.html)

https://overthewire.org/wargames/bandit/bandit5.html
> The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.


``` ssh bandit4@bandit.labs.overthewire.org -p 2220 ```으로 로그인  

암호는 [전에](./bandit04.md) 찾은 ```pIwrPrtPN36QITSp3EQaw936yaFoFgAB```

```
bandit4@bandit:~$ ls
inhere
bandit4@bandit:~$ cd inhere/
bandit4@bandit:~/inhere$ ls
-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
bandit4@bandit:~/inhere$ file ./*
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
bandit4@bandit:~/inhere$ cat ./-file07
koReBOKuIDDepwhWk7jZC0RTdopnAYKh
```

```ls```로 **inhere**파일 찾아서 ```cd```로 마운트한 후 ```ls```시 10개의 파일이 나옴  
문제에서  only human-readable file 이라고 했으니까 ```file```로 파일의 종류을 확인함  
**-file07**만 아스키 코드로 작성 된 문서이기 떄문에 ```cat ./-file07```로 암호 GET!!

```cat -file07```안됨 --> 2번 참고
