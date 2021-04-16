## [Bandit #16](https://overthewire.org/wargames/bandit/bandit16.html)

https://overthewire.org/wargames/bandit/bandit16.html
> The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.
>> **Helpful note: Getting “HEARTBEATING” and “Read R BLOCK”? Use -ign_eof and read the “CONNECTED COMMANDS” section in the manpage. Next to ‘R’ and ‘Q’, the ‘B’ command also works in this version of that command…**

``` ssh bandit15@bandit.labs.overthewire.org -p 2220 ```으로 로그인  

암호는 [전에](./bandit15.md) 찾은 ```BfMYroe26WYalil77FoDi9qh59eK5xNr```

SSL암호화에 관해 구글링을 해보았다.  
```
