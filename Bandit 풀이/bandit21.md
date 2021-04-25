## [Bandit #21](https://overthewire.org/wargames/bandit/bandit21.html)

https://overthewire.org/wargames/bandit/bandit21.html
> There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

``` ssh bandit20@bandit.labs.overthewire.org -p 2220 ```으로 로그인  

암호는 [전에](./bandit20.md) 찾은 ```GbKksEFF4yrVs6il55v6gwY5aVje5f0j```
```
bandit20@bandit:~$ ./suconnect
Usage: ./suconnect <portnumber>
This program will connect to the given port on localhost using TCP. If it receives the correct password from the other side, the next password is transmitted back.
```
```suconnect``` 파일을 실행 시켜보면 사용법이 나온다. 따라서 ```nc -l```로 새로운 포트를 열어두고 다른 터미널로 그 포트로 ```suconnect``` 로 접속하면 해결 될 거 같다
```
bandit20@bandit:~$ nc -l 40000
```
```
bandit20@bandit:~$ ./suconnect 40000
Could not connect
```
??? 오류나 나서 찾아보았는데 그냥 내께 이상한거 같다... 다른 사람들은 다 잘 되는데....
일단 [검색 결과](https://blog.do9.kr/236) 암호는 ```gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr```이다. 내일 다시 해봐야겠다...
