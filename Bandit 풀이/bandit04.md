## [Bandit #04](https://overthewire.org/wargames/bandit/bandit4.html)

https://overthewire.org/wargames/bandit/bandit4.html
> The password for the next level is stored in a hidden file in the inhere directory.


``` ssh bandit3@bandit.labs.overthewire.org -p 2220 ```으로 로그인  

암호는 전에 찾은 ```UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK```

```
bandit3@bandit:~$ ls
inhere
bandit3@bandit:~$ cd inhere/
bandit3@bandit:~/inhere$ ls
bandit3@bandit:~/inhere$ ls -a
.  ..  .hidden
bandit3@bandit:~/inhere$ cat .hidden
pIwrPrtPN36QITSp3EQaw936yaFoFgAB
```

```ls```로 **inhere**파일 찾아서 ```cd```로 마운트한 후 ```ls```시 아무런 파일을 찾을 수 없음...  
따라서 숨겨진 파일까지 찾을 수 있는 ```ls -a```를 이용하여 숨겨진 파일 **.hidden**을 찾음 
```cat .hidden```으로 암호를 가져오면 끝!!

++```ls -ai```: 숨겨진 파일 포함 모든 파일의 권한까지 보여준다.  
++자세한 ls 옵션은 [https://choseongho93.tistory.com/113](https://choseongho93.tistory.com/113)
