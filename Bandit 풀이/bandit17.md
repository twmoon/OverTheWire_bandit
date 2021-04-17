## [Bandit #17](https://overthewire.org/wargames/bandit/bandit17.html)

https://overthewire.org/wargames/bandit/bandit17.html
> The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.               

``` ssh bandit16@bandit.labs.overthewire.org -p 2220 ```으로 로그인  

암호는 [전에](./bandit16.md) 찾은 ```cluFn7wTiGryunymYOu4RcffSxQluehd```

이 문제는 약 천개의 포트 중 열려있는 포트를 찾는 문제이다.
```
