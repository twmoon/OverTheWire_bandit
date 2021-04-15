## [Bandit #15](https://overthewire.org/wargames/bandit/bandit15.html)

https://overthewire.org/wargames/bandit/bandit15.html
> The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost

``` ssh bandit14@bandit.labs.overthewire.org -p 2220 ```으로 로그인  

암호는 [전에](./bandit14.md) 찾은 ```4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e```

이 문제는 localhost 30000포트에 14레벨의 암호를 제출하면 해결되는 문제다  
평소 열던 방식대로 ```ssh```명령어로 열어보았다.
```
bandit14@bandit:~$ ssh passscode@localhost -p 30000
ssh_exchange_identification: Connection closed by remote host
```

보안상 오류가 생긴다...   

#### 방법 1) ```nc```명령어 사용
```
bandit14@bandit:~$ nc -l 30000
```

넷캣 명령어로 포트 30000을 열어둔다  
터미널은 새로 연다음 localhost의 30000번 포트로 접속헀다
```
bandit14@bandit:~$ nc localhost 30000
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
Correct!
BfMYroe26WYalil77FoDi9qh59eK5xNr
```

포트에 접속해서 현재 로그인 중인 레벨의 암호인 ```4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e```를 입력하니까  
다음 레벨의 암호 ```BfMYroe26WYalil77FoDi9qh59eK5xNr```를 출력했다

#### 방법 2) ```talnet```명령어 사용
```
bandit14@bandit:~$ telnet localhost 30000
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
Correct!
BfMYroe26WYalil77FoDi9qh59eK5xNr
```

```telnet```으로 로컬호스트의 30000포트로 바로 접속할 수 있다.
포트에 접속해서 현재 로그인 중인 레벨의 암호인 ```4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e```를 입력하니까  
다음 레벨의 암호 ```BfMYroe26WYalil77FoDi9qh59eK5xNr```를 출력했다
