## [Bandit #13](https://overthewire.org/wargames/bandit/bandit13.html)

https://overthewire.org/wargames/bandit/bandit13.html
> The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!)

``` ssh bandit12@bandit.labs.overthewire.org -p 2220 ```으로 로그인  

암호는 [전에](./bandit12.md) 찾은 ```5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu```

~~아 이게 뭐지??? 이거 안배운건데......~~  
일단 침착하고 문제에 명시된 권한이 있는 디렉토리를 만들고 ```data.txt```파일을 복사했다
```
bandit12@bandit:~$ mkdir /tmp/13
bandit12@bandit:~$ cp data.txt /tmp/13
bandit12@bandit:~$ cd /tmp/13
```
그리고 흔들리는 멘탈을 붙잡고 구글링 시작   
첫 번째로 ```xxd -r```명령어를 통해 헥스덤프 파일을 바이너리 파일로 복원해보았다  
```
bandit12@bandit:/tmp/13$ xxd -r data.txt > 13
bandit12@bandit:/tmp/13$ cat 13
P▒^data2.bin=▒▒BZh91AY&SY▒O▒▒▒▒ڞOv▒▒▒}?▒▒}▒▒^▒▒▒▒▒▒▒▒▒ߣ▒▒;▒▒▒▒4▒▒h▒F▒F▒▒4LM
                                                                           @▒▒z▒▒FM▒▒C▒hF▒C@▒4@f▒▒h
                                                                                                   ▒▒i▒hP4hh▒=C%▒>X,▒k▒▒▒1▒▒GY▒▒
▒J▒쌑Oϊ▒▒{RBp▒Qix▒Y▒Z!d▒▒j▒(▒搿ݳ▒▒/▒▒A▒#▒A▒▒0P▒▒v▒▒`▒"3▒

                                          ▒▒d▒bX?▒▒z▒▒2▒▒<▒▒A ▒n}
5(3A▒▒
      wO▒R▒▒▒▒6▒XS{▒
▒▒9?L▒P▒yB▒▒=z▒m?▒L▒Nt*▒7{qP▒▒̜▒%"▒w9▒qm4▒▒ N3▒6▒▒▒K▒▒H䋑[▒▒}!
                                                             d▒▒3A4$▒M~▒\ɠJ▒C▒kUƦ\▒▒▒\▒FSN▒▒&=▒[▒▒q     \)▒$:▒▒H▒t&/▒(▒▒▒▒]▒▒BB9<s ▒▒h=
```

이젠 이렇게 깨진 문자가 익숙하다 ㅎㅎ  
```file```명령어를 통해 ```13```의 정체를 알아보았다
```
bandit12@bandit:/tmp/13$ file 13
13: gzip compressed data, was "data2.bin", last modified: Thu May  7 18:14:30 2020, max compression, from Unix
```

```13```파일이 gzip파일인것과 ```data2.bin```이라는 파일이 압축된 것도 알아냈다.  
따라서 ```13```파일 이름을 ```data2.bin.gz```로 바꿔준주고 압축 해제를 진행한다.
```
bandit12@bandit:/tmp/13$ mv 13 data2.bin.gz
bandit12@bandit:/tmp/13$ gzip -d data2.bin.gz
bandit12@bandit:/tmp/13$ ls
data2.bin
```

```data2.bin```파일을 압축해제하는데 성공!!  
```file```명령어로 파일의 정체를 보면
```
bandit12@bandit:/tmp/13$ file data2.bin
data2.bin: bzip2 compressed data, block size = 900k
```

bzip2로 압축된 파일인것을 볼 수 있다.  
다시 이름을 ```data3.bin.bz2```으로 바꾸고 압축을 풀어주고 ```file```로 확인하면
```
bandit12@bandit:/tmp/13$ mv data2.bin data3.bin.bz2
bandit12@bandit:/tmp/13$ bunzip2 data3.bin.bz2
bandit12@bandit:/tmp/13$ ls
data3.bin
bandit12@bandit:/tmp/13$ file data3.bin
data3.bin: gzip compressed data, was "data4.bin", last modified: Thu May  7 18:14:30 2020, max compression, from Unix
```

이제 무슨 문제인지 슬슬 감이 온다. 이렇게 아스키 코드로 된 파일이 나올때 까지 압축 풀어가면서 해결하는 문제일거 같다.
다시 ```data4.bin.gz```로 이름 바꾸고 풀어보고 정보를 보자
```
bandit12@bandit:/tmp/13$ gzip -d data4.bin.gz
bandit12@bandit:/tmp/13$ file data4.bin
data4.bin: POSIX tar archive (GNU)
```

이번엔 tar파일이다. 위 방법대로 이름 변경하고 다시 압축 풀어주고 정보를 보면
```
bandit12@bandit:/tmp/13$ tar -xvf data5.bin.tar
data5.bin
bandit12@bandit:/tmp/13$ file data5.bin
data5.bin: POSIX tar archive (GNU)
```

이번에도 tar파일이다. 이제 슬슬 손이 아프지만 다시 위에 방법대로 그대로 다시 하면
```
bandit12@bandit:/tmp/13$ tar -xvf data6.bin.tar
data6.bin
bandit12@bandit:/tmp/13$ file data6.bin
data6.bin: bzip2 compressed data, block size = 900k
```

이 문제는 지식을 시험한다기보단 인내력을 시험하는 문제인거 같다. (위에서 ```xxd -r```찾아본건 안비밀)  
인내력을 시험하는 방향으로 생각하면 디게 잘 만든 문제같다.  
헛소리는 여기까지 하고 이어서 풀어보면
```
bandit12@bandit:/tmp/13$ mv data6.bin data7.bin.bz2
bandit12@bandit:/tmp/13$ bunzip2 data7.bin.bz2
bandit12@bandit:/tmp/13$ file data7.bin
data7.bin: POSIX tar archive (GNU)
```

이 문제의 목적 중 한가지는 확실하다. 나를 반디집으로 만드려는거 말이다...  
반디집 쓰세요 여러분... 윈도우 만만세...  (유료광고 미포함)
```
bandit12@bandit:/tmp/13$ mv data7.bin data8.bin.tar
bandit12@bandit:/tmp/13$ tar -xvf data8.bin.tar
data8.bin
bandit12@bandit:/tmp/13$ file data8.bin
data8.bin: gzip compressed data, was "data9.bin", last modified: Thu May  7 18:14:30 2020, max compression, from Unix
```

이거 진짜 언제끝나지??? 이게 그 나루토에서 본 무한 쭈꾸요미인가 뭐시기 그거인가...  
```
bandit12@bandit:/tmp/13$ mv data8.bin data9.bin.gz
bandit12@bandit:/tmp/13$ gzip -d data9.bin.gz
bandit12@bandit:/tmp/13$ file data9.bin
data9.bin: ASCII text
```
왐ㄴ오ㅟ멀옴ㅇㄴㄹ;ㅓㅗㄻㄴ;ㅓㅗ랴ㅐㅁ  
#### 드디어 아스키 텍스트 파일 찾았다!!!!!!!!!
폭죽 피유우우웅 뻐어어엉뻥 드럼 두구두구두구  
```
bandit12@bandit:/tmp/13$ cat data9.bin
The password is 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL
```

결국 찾은 암호는 ```8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL```였다!!!
끝~!!
