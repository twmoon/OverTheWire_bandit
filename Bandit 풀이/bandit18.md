## [Bandit #18](https://overthewire.org/wargames/bandit/bandit18.html)

https://overthewire.org/wargames/bandit/bandit18.html
> There are 2 files in the homedirectory: **passwords.old and passwords.new.** The password for the next level is in **passwords.new** and is the only line that has been changed between **passwords.old and passwords.new**
>> **NOTE: if you have solved this level and see ‘Byebye!’ when trying to log into bandit18, this is related to the next level, bandit19**

``` ssh bandit17@bandit.labs.overthewire.org -p 2220 ```으로 로그인  

암호는 [전에](./bandit17.md) 찾은 ```xLYVMN9WE5zQ5vHacb0sZEVqbrp7nBTn```
```
bandit17@bandit:~$ ls
passwords.new  passwords.old
```
 두 개의 파일을 볼 수 있다.  
 문제에서 2개의 파일 중에 ```passwords.new``` 파일에 비밀번호가 있는것을 알 수 있다
 ```diff```명령어를 사용하여 찾아보면
```bandit17@bandit:~$ diff passwords.old passwords.new
42c42
< w0Yfolrc5bwjS4qw5mq1nnQi6mF03bii
---
> kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
```

윗줄은 ```passwords.old```파일이고 아랫줄은 ```passwords.new```파일이다.
따라서 암호는 ```kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd```이다.
