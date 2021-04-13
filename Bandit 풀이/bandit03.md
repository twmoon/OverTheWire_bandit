## [Bandit #03](https://overthewire.org/wargames/bandit/bandit3.html)

https://overthewire.org/wargames/bandit/bandit3.html
> The password for the next level is stored in a file called spaces in this filename located in the home directory


``` ssh bandit2@bandit.labs.overthewire.org -p 2220 ```으로 로그인  

암호는 전에 찾은 ```CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9```

```
bandit2@bandit:~$ ls
spaces in this filename
bandit2@bandit:~$ cat "./spaces in this filename"
UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
```

처음에 ```ls```로 시작한 후 문자열이라고 생각해서 ```cat ./"spac``` 이 상태에서 TAB 키를 눌렀더니  
```cat ./"./spaces in this filename"```이 되었고 수정해서 ```cat "./spaces in this filename"```으로 파일을 읽었다.  

리눅스에서 공백을 포함한 파일 디렉토리는 ```" "```로 감싸면 인식이 된다!! (탭키 짱짱)
