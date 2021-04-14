## [Bandit #12](https://overthewire.org/wargames/bandit/bandit12.html)

https://overthewire.org/wargames/bandit/bandit12.html
> The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

``` ssh bandit7@bandit.labs.overthewire.org -p 2220 ```으로 로그인  

암호는 [전에](./bandit11.md) 찾은 ```IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR```
```
bandit11@bandit:~$ cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
The password is 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu
```

```where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions```이 뭔소리인지 몰라서 찾아보니까  
Rot13이라는 암호화 기법이 있었다. 지식이 늘었다 ㅎㅎ  
```tr```을 사용하여 13글자씩 밀어주면 원래 문자열이 나온다.  
```The password is 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu```, 즉 암호는 ```5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu```이 나온다.  
Rot13 암호화의 복호화 방법을 몰랐으면 못 풀었다... 이번 기회로 알아서 반가웠다.


#### ++저번 문제에서 꿀빨던거 생각나서 해봤는데
```
bandit11@bandit:~$ cat data.txt | rot13 --decode
-bash: rot13: command not found
```
그딴건 없었다한다...  
