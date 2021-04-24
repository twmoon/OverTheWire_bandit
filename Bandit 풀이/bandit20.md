## [Bandit #20](https://overthewire.org/wargames/bandit/bandit20.html)

https://overthewire.org/wargames/bandit/bandit20.html
> To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

``` ssh bandit19@bandit.labs.overthewire.org -p 2220 ```으로 로그인  

암호는 [전에](./bandit19.md) 찾은 ```IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x```
```
bandit19@bandit:~$ ls -la
total 28
drwxr-xr-x  2 root     root     4096 May  7  2020 .
drwxr-xr-x 41 root     root     4096 May  7  2020 ..
-rwsr-x---  1 bandit20 bandit19 7296 May  7  2020 bandit20-do
-rw-r--r--  1 root     root      220 May 15  2017 .bash_logout
-rw-r--r--  1 root     root     3526 May 15  2017 .bashrc
-rw-r--r--  1 root     root      675 May 15  2017 .profile
```
```ls -la```로 권한을 보니까 소유자가 bandit20 인걸 알 수 있습니다.  
```bandit20-do```을 실행보면 
```
bandit19@bandit:~$ ./bandit20-do
Run a command as another user.
  Example: ./bandit20-do id
```

친절히도 뭐하는 파일인지 설명을 했다.  
```/etc/bandit_pass/```에서 암호는 조회하려면 본인으로 접속해야하는데 ```bandit20-do```를 이용하여 우회할 수 있을거 같다.

```
bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
GbKksEFF4yrVs6il55v6gwY5aVje5f0j
```
짜잔 암호는 ```GbKksEFF4yrVs6il55v6gwY5aVje5f0j```이다.
