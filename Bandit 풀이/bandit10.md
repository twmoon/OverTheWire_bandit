## [Bandit #10](https://overthewire.org/wargames/bandit/bandit10.html)

https://overthewire.org/wargames/bandit/bandit10.html
> The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.

``` ssh bandit9@bandit.labs.overthewire.org -p 2220 ```으로 로그인  

암호는 [전에](./bandit09.md) 찾은 ```UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR```

```
bandit9@bandit:~$ cat data.txt
(깨진 문자들 파티여서 중략)
bandit9@bandit:~$ strings data.txt | grep ^=
========== the*2i"4
=:G e
========== password
bandit9@bandit:~$ strings data.txt | grep ==
========== the*2i"4
========== password
Z)========== is
&========== truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk
```
```cat data.txt```로 ```data.txt```파일을 읽어보았으나 문자들이 다 깨진걸 볼 수 있었다.  
 ```data.txt```은 바이너리 파일로 추정되기 때문에 ```strings```로 바이너리 데이터를 문자열로 변환했다.  
 ***preceded by several ‘=’ characters*** 라는 조건이 있었기에 ```grep ==```를 이용하여 암호인 ```truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk```를 찾아냈다.
