## [Bandit #19](https://overthewire.org/wargames/bandit/bandit19.html)

https://overthewire.org/wargames/bandit/bandit19.html
> The password for the next level is stored in a file **readme** in the homedirectory. Unfortunately, someone has modified **.bashrc** to log you out when you log in with SSH.

``` ssh bandit18@bandit.labs.overthewire.org -p 2220 ```으로 로그인  

암호는 [전에](./bandit17.md) 찾은 ```kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd```
```
$ ssh bandit18@bandit.labs.overthewire.org -p 2220
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit18@bandit.labs.overthewire.org's password:
Linux bandit.otw.local 5.4.8 x86_64 GNU/Linux

(중략)

Enjoy your stay!

Byebye !
Connection to bandit.labs.overthewire.org closed.
```
Enjoy your stay! 라면서 바로 다음 줄에 byebye라고 나가라고한다....  
문제에서 ```someone has modified .bashrc to log you out when you log in with SSH.```라고 한다.  
```.bashrc```는 bashrc 파일은 bash가 수행될 때 실행되는 함수를 제어하는 지역적인 시스템 설정과 관련된 파일이다.([검색](https://coding-chobo.tistory.com/72#:~:text=bashrc%20%ED%8C%8C%EC%9D%BC%EC%9D%80%20bash%EA%B0%80,%EC%84%A4%EC%A0%95%EA%B3%BC%20%EA%B4%80%EB%A0%A8%EB%90%9C%20%ED%8C%8C%EC%9D%BC%EC%9E%85%EB%8B%88%EB%8B%A4.&text=%2D%20%2Fetc%2Fbashrc-,%3A%20%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EC%A0%84%EC%97%AD(%EB%AA%A8%EB%93%A0%20%EC%82%AC%EC%9A%A9%EC%9E%90)%EC%97%90%20%EB%8C%80%ED%95%9C%20%ED%99%98%EA%B2%BD%EC%84%A4%EC%A0%95%20%ED%8C%8C%EC%9D%BC,%EB%A7%88%EB%8B%A4%20%EB%82%B4%EC%9A%A9%EC%9D%84%20%EC%9D%BD%EC%96%B4%EB%93%A4%EC%9E%84.))
```.bashrc```에서 ssh를 통한 접속을 막는거 같은데 접속은 가능하니까 꺼지기 전에 ```cat readme```를 하면 될거 같다.  
무조건 ssh 접속으로만 밴딧 서버에 접속 가능하니까 ssh말고 다른 방식으로 접속은 힘들거 같다. 
```
$ ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit18@bandit.labs.overthewire.org's password:
IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x
```
암호는 ```IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x```이다.
