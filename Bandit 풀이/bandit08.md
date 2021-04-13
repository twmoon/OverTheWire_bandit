## [Bandit #08](https://overthewire.org/wargames/bandit/bandit8.html)

https://overthewire.org/wargames/bandit/bandit8.html
> The password for the next level is stored in the file data.txt next to the word millionth

``` ssh bandit7@bandit.labs.overthewire.org -p 2220 ```으로 로그인  

암호는 [전에](./bandit07.md) 찾은 ```HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs```

```
bandit7@bandit:~$ ls
data.txt
```
### 방법1) VI EDITOR 사용  
```vi data```를 통해 VI 에디터로 data.txt에 접근한 후 ```/millionth```를 입력해 ```millionth```를 검색한다.  
검색된 ```millionth``` 옆에 암호 ``cvX2JJa4CFALtqS87jk27qwqGhBM9plV``를 확인한 후 ```:q!```로 VI 에디터 종료!!
--> 그냥 생각나는 방법대로 풀었는데 불편함... --> 방법 2 추천

### 방법2) ``grep`` 명령어 사용 **---> 강추**
```
bandit7@bandit:~$ grep millionth data.txt
millionth       cvX2JJa4CFALtqS87jk27qwqGhBM9plV
```
```grep [OPTION] [PATTERN] [FILE]```을 통해 파일에서 특정 문자열을 검색해 낼 수 있다!!!  
따라서 ```grep millionth data.txt```를 통해서  
```millionth```에 매칭된 암호 ```cvX2JJa4CFALtqS87jk27qwqGhBM9plV```를 알아낼 수 있다!!
