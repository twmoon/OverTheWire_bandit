## [Bandit #11](https://overthewire.org/wargames/bandit/bandit11.html)

https://overthewire.org/wargames/bandit/bandit11.html
> The password for the next level is stored in the file data.txt, which contains base64 encoded data

``` ssh bandit10@bandit.labs.overthewire.org -p 2220 ```으로 로그인  

암호는 [전에](./bandit10.md) 찾은 ```truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk```

```
bandit10@bandit:~$ cat data.txt
VGhlIHBhc3N3b3JkIGlzIElGdWt3S0dzRlc4TU9xM0lSRnFyeEUxaHhUTkViVVBSCg==
bandit10@bandit:~$ cat data.txt | base64 --decode
The password is IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR
```

```cat data.txt```명령어로 파일을 열어보면 의미없는 문자열이 보인다.  
문제에서 base64로 인코딩된 문자열이라고 하니까 ```base64 --decode```명령으로 디코딩해주면  
```The password is IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR```, 즉 암호는 ```IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR```이다.
