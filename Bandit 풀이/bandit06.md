## [Bandit #06](https://overthewire.org/wargames/bandit/bandit6.html)

https://overthewire.org/wargames/bandit/bandit6.html
> The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:
> >human-readable  
> >1033 bytes in size  
> >not executable  
 

``` ssh bandit5@bandit.labs.overthewire.org -p 2220 ```으로 로그인  

암호는 전에 찾은 ```koReBOKuIDDepwhWk7jZC0RTdopnAYKh```

```
bandit5@bandit:~$ ls
inhere
bandit5@bandit:~$ cd inhere/
bandit5@bandit:~/inhere$ ls
maybehere00  maybehere02  maybehere04  maybehere06  maybehere08  maybehere10  maybehere12  maybehere14  maybehere16  maybehere18
maybehere01  maybehere03  maybehere05  maybehere07  maybehere09  maybehere11  maybehere13  maybehere15  maybehere17  maybehere19
bandit5@bandit:~/inhere$ find -readable -size 1033c
./maybehere07/.file2
bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
DXjZPULLxYr17uwoI01bNLQbtFemEgo7
```

앞 문제들과 같이 ```ls```로 **inhere**파일 찾아서 ```cd```로 마운트한 후 ```ls```시 20개의 폴더가 나옴  
문제에서 1033 bytes in size 라는 조건과 human-readable 이라는 조건을 주었기 때문에 ```find```를 활용해서  
```find -readable -size 1033c```라는 명령어로 조건에 부합하는 ```./maybehere07/.file2```라는 파일을 찾을 수 있었음  
```cat ./maybehere07/.file2```으로 암호를 가져오면 CLEAR!!

#### ++ 파일 안에 뭐가 있는지 궁금해서 모든 하위 폴더를 열어주는 ```ls -arl ./*```를 이용해서 열어보니까

```
bandit5@bandit:~/inhere$ ls -arl ./*
./maybehere19:
total 76
-rwxr-x---  1 root bandit5 2307 May  7  2020 spaces file3
-rw-r-----  1 root bandit5 8785 May  7  2020 spaces file2
-rwxr-x---  1 root bandit5 7186 May  7  2020 spaces file1
-rwxr-x---  1 root bandit5  494 May  7  2020 .file3
-rwxr-x---  1 root bandit5 7965 May  7  2020 -file3
-rw-r-----  1 root bandit5 4740 May  7  2020 .file2
-rw-r-----  1 root bandit5 5594 May  7  2020 -file2
-rwxr-x---  1 root bandit5 7209 May  7  2020 .file1
-rwxr-x---  1 root bandit5 6302 May  7  2020 -file1
drwxr-x--- 22 root bandit5 4096 May  7  2020 ..
drwxr-x---  2 root bandit5 4096 May  7  2020 .

./maybehere18:
total 68
-rwxr-x---  1 root bandit5 7040 May  7  2020 spaces file3
-rw-r-----  1 root bandit5 6348 May  7  2020 spaces file2
-rwxr-x---  1 root bandit5 7334 May  7  2020 spaces file1
-rwxr-x---  1 root bandit5  154 May  7  2020 .file3
-rwxr-x---  1 root bandit5 2306 May  7  2020 -file3
-rw-r-----  1 root bandit5 2084 May  7  2020 .file2
-rw-r-----  1 root bandit5   77 May  7  2020 -file2
-rwxr-x---  1 root bandit5 5702 May  7  2020 .file1
-rwxr-x---  1 root bandit5 9697 May  7  2020 -file1
drwxr-x--- 22 root bandit5 4096 May  7  2020 ..
drwxr-x---  2 root bandit5 4096 May  7  2020 .

./maybehere17:
total 72
-rwxr-x---  1 root bandit5 6381 May  7  2020 spaces file3
-rw-r-----  1 root bandit5 3387 May  7  2020 spaces file2
-rwxr-x---  1 root bandit5 8361 May  7  2020 spaces file1
-rwxr-x---  1 root bandit5 5094 May  7  2020 .file3
-rwxr-x---  1 root bandit5 4422 May  7  2020 -file3
-rw-r-----  1 root bandit5 8341 May  7  2020 .file2
-rw-r-----  1 root bandit5 1791 May  7  2020 -file2
-rwxr-x---  1 root bandit5  895 May  7  2020 .file1
-rwxr-x---  1 root bandit5 1133 May  7  2020 -file1
drwxr-x--- 22 root bandit5 4096 May  7  2020 ..
drwxr-x---  2 root bandit5 4096 May  7  2020 .

./maybehere16:
total 80
-rwxr-x---  1 root bandit5 7509 May  7  2020 spaces file3
-rw-r-----  1 root bandit5 3146 May  7  2020 spaces file2
-rwxr-x---  1 root bandit5 9773 May  7  2020 spaces file1
-rwxr-x---  1 root bandit5 1148 May  7  2020 .file3
-rwxr-x---  1 root bandit5 8085 May  7  2020 -file3
-rw-r-----  1 root bandit5 8472 May  7  2020 .file2
-rw-r-----  1 root bandit5 5301 May  7  2020 -file2
-rwxr-x---  1 root bandit5 5426 May  7  2020 .file1
-rwxr-x---  1 root bandit5 4277 May  7  2020 -file1
drwxr-x--- 22 root bandit5 4096 May  7  2020 ..
drwxr-x---  2 root bandit5 4096 May  7  2020 .

./maybehere15:
total 64
-rwxr-x---  1 root bandit5 1637 May  7  2020 spaces file3
-rw-r-----  1 root bandit5   51 May  7  2020 spaces file2
-rwxr-x---  1 root bandit5 1623 May  7  2020 spaces file1
-rwxr-x---  1 root bandit5  742 May  7  2020 .file3
-rwxr-x---  1 root bandit5 6299 May  7  2020 -file3
-rw-r-----  1 root bandit5  279 May  7  2020 .file2
-rw-r-----  1 root bandit5 9499 May  7  2020 -file2
-rwxr-x---  1 root bandit5 2159 May  7  2020 .file1
-rwxr-x---  1 root bandit5 8794 May  7  2020 -file1
drwxr-x--- 22 root bandit5 4096 May  7  2020 ..
drwxr-x---  2 root bandit5 4096 May  7  2020 .

./maybehere14:
total 60
-rwxr-x---  1 root bandit5  376 May  7  2020 spaces file3
-rw-r-----  1 root bandit5  871 May  7  2020 spaces file2
-rwxr-x---  1 root bandit5 1382 May  7  2020 spaces file1
-rwxr-x---  1 root bandit5 4821 May  7  2020 .file3
-rwxr-x---  1 root bandit5 3756 May  7  2020 -file3
-rw-r-----  1 root bandit5 1503 May  7  2020 .file2
-rw-r-----  1 root bandit5 8351 May  7  2020 -file2
-rwxr-x---  1 root bandit5 3427 May  7  2020 .file1
-rwxr-x---  1 root bandit5 4282 May  7  2020 -file1
drwxr-x--- 22 root bandit5 4096 May  7  2020 ..
drwxr-x---  2 root bandit5 4096 May  7  2020 .

./maybehere13:
total 64
-rwxr-x---  1 root bandit5 4389 May  7  2020 spaces file3
-rw-r-----  1 root bandit5  952 May  7  2020 spaces file2
-rwxr-x---  1 root bandit5 3952 May  7  2020 spaces file1
-rwxr-x---  1 root bandit5 6965 May  7  2020 .file3
-rwxr-x---  1 root bandit5 3014 May  7  2020 -file3
-rw-r-----  1 root bandit5 8952 May  7  2020 .file2
-rw-r-----  1 root bandit5 1423 May  7  2020 -file2
-rwxr-x---  1 root bandit5 5258 May  7  2020 .file1
-rwxr-x---  1 root bandit5 1359 May  7  2020 -file1
drwxr-x--- 22 root bandit5 4096 May  7  2020 ..
drwxr-x---  2 root bandit5 4096 May  7  2020 .

./maybehere12:
total 72
-rwxr-x---  1 root bandit5 1639 May  7  2020 spaces file3
-rw-r-----  1 root bandit5 2460 May  7  2020 spaces file2
-rwxr-x---  1 root bandit5 2157 May  7  2020 spaces file1
-rwxr-x---  1 root bandit5 1022 May  7  2020 .file3
-rwxr-x---  1 root bandit5 9076 May  7  2020 -file3
-rw-r-----  1 root bandit5 8244 May  7  2020 .file2
-rw-r-----  1 root bandit5  251 May  7  2020 -file2
-rwxr-x---  1 root bandit5 5815 May  7  2020 .file1
-rwxr-x---  1 root bandit5 9678 May  7  2020 -file1
drwxr-x--- 22 root bandit5 4096 May  7  2020 ..
drwxr-x---  2 root bandit5 4096 May  7  2020 .

./maybehere11:
total 72
-rwxr-x---  1 root bandit5 8845 May  7  2020 spaces file3
-rw-r-----  1 root bandit5  503 May  7  2020 spaces file2
-rwxr-x---  1 root bandit5 3147 May  7  2020 spaces file1
-rwxr-x---  1 root bandit5 8261 May  7  2020 .file3
-rwxr-x---  1 root bandit5 8854 May  7  2020 -file3
-rw-r-----  1 root bandit5 2501 May  7  2020 .file2
-rw-r-----  1 root bandit5 4559 May  7  2020 -file2
-rwxr-x---  1 root bandit5  452 May  7  2020 .file1
-rwxr-x---  1 root bandit5 1211 May  7  2020 -file1
drwxr-x--- 22 root bandit5 4096 May  7  2020 ..
drwxr-x---  2 root bandit5 4096 May  7  2020 .

./maybehere10:
total 56
-rwxr-x---  1 root bandit5 2155 May  7  2020 spaces file3
-rw-r-----  1 root bandit5 3570 May  7  2020 spaces file2
-rwxr-x---  1 root bandit5 8269 May  7  2020 spaces file1
-rwxr-x---  1 root bandit5 2961 May  7  2020 .file3
-rwxr-x---  1 root bandit5 1237 May  7  2020 -file3
-rw-r-----  1 root bandit5   99 May  7  2020 .file2
-rw-r-----  1 root bandit5 1991 May  7  2020 -file2
-rwxr-x---  1 root bandit5 7092 May  7  2020 .file1
-rwxr-x---  1 root bandit5 1052 May  7  2020 -file1
drwxr-x--- 22 root bandit5 4096 May  7  2020 ..
drwxr-x---  2 root bandit5 4096 May  7  2020 .

./maybehere09:
total 76
-rwxr-x---  1 root bandit5 7569 May  7  2020 spaces file3
-rw-r-----  1 root bandit5 8716 May  7  2020 spaces file2
-rwxr-x---  1 root bandit5 5301 May  7  2020 spaces file1
-rwxr-x---  1 root bandit5 3798 May  7  2020 .file3
-rwxr-x---  1 root bandit5 7961 May  7  2020 -file3
-rw-r-----  1 root bandit5 8517 May  7  2020 .file2
-rw-r-----  1 root bandit5  774 May  7  2020 -file2
-rwxr-x---  1 root bandit5 6763 May  7  2020 .file1
-rwxr-x---  1 root bandit5 3628 May  7  2020 -file1
drwxr-x--- 22 root bandit5 4096 May  7  2020 ..
drwxr-x---  2 root bandit5 4096 May  7  2020 .

./maybehere08:
total 56
-rwxr-x---  1 root bandit5 9138 May  7  2020 spaces file3
-rw-r-----  1 root bandit5 3693 May  7  2020 spaces file2
-rwxr-x---  1 root bandit5  215 May  7  2020 spaces file1
-rwxr-x---  1 root bandit5 2217 May  7  2020 .file3
-rwxr-x---  1 root bandit5 2650 May  7  2020 -file3
-rw-r-----  1 root bandit5  747 May  7  2020 .file2
-rw-r-----  1 root bandit5 3825 May  7  2020 -file2
-rwxr-x---  1 root bandit5 8169 May  7  2020 .file1
-rwxr-x---  1 root bandit5 1077 May  7  2020 -file1
drwxr-x--- 22 root bandit5 4096 May  7  2020 ..
drwxr-x---  2 root bandit5 4096 May  7  2020 .

./maybehere07:
total 56
-rwxr-x---  1 root bandit5 1022 May  7  2020 spaces file3
-rw-r-----  1 root bandit5 9064 May  7  2020 spaces file2
-rwxr-x---  1 root bandit5 4130 May  7  2020 spaces file1
-rwxr-x---  1 root bandit5 1997 May  7  2020 .file3
-rwxr-x---  1 root bandit5 3362 May  7  2020 -file3
-rw-r-----  1 root bandit5 1033 May  7  2020 .file2
-rw-r-----  1 root bandit5 2488 May  7  2020 -file2
-rwxr-x---  1 root bandit5 3065 May  7  2020 .file1
-rwxr-x---  1 root bandit5 3663 May  7  2020 -file1
drwxr-x--- 22 root bandit5 4096 May  7  2020 ..
drwxr-x---  2 root bandit5 4096 May  7  2020 .

./maybehere06:
total 64
-rwxr-x---  1 root bandit5 8065 May  7  2020 spaces file3
-rw-r-----  1 root bandit5 4251 May  7  2020 spaces file2
-rwxr-x---  1 root bandit5 4073 May  7  2020 spaces file1
-rwxr-x---  1 root bandit5 2418 May  7  2020 .file3
-rwxr-x---  1 root bandit5 3443 May  7  2020 -file3
-rw-r-----  1 root bandit5 8976 May  7  2020 .file2
-rw-r-----  1 root bandit5 1076 May  7  2020 -file2
-rwxr-x---  1 root bandit5 1271 May  7  2020 .file1
-rwxr-x---  1 root bandit5 5731 May  7  2020 -file1
drwxr-x--- 22 root bandit5 4096 May  7  2020 ..
drwxr-x---  2 root bandit5 4096 May  7  2020 .

./maybehere05:
total 64
-rwxr-x---  1 root bandit5 8585 May  7  2020 spaces file3
-rw-r-----  1 root bandit5 2420 May  7  2020 spaces file2
-rwxr-x---  1 root bandit5  880 May  7  2020 spaces file1
-rwxr-x---  1 root bandit5 4585 May  7  2020 .file3
-rwxr-x---  1 root bandit5 2572 May  7  2020 -file3
-rw-r-----  1 root bandit5 5917 May  7  2020 .file2
-rw-r-----  1 root bandit5 5959 May  7  2020 -file2
-rwxr-x---  1 root bandit5 3201 May  7  2020 .file1
-rwxr-x---  1 root bandit5 2346 May  7  2020 -file1
drwxr-x--- 22 root bandit5 4096 May  7  2020 ..
drwxr-x---  2 root bandit5 4096 May  7  2020 .

./maybehere04:
total 60
-rwxr-x---  1 root bandit5 6002 May  7  2020 spaces file3
-rw-r-----  1 root bandit5 2491 May  7  2020 spaces file2
-rwxr-x---  1 root bandit5 5532 May  7  2020 spaces file1
-rwxr-x---  1 root bandit5  142 May  7  2020 .file3
-rwxr-x---  1 root bandit5 2117 May  7  2020 -file3
-rw-r-----  1 root bandit5 6144 May  7  2020 .file2
-rw-r-----  1 root bandit5 2619 May  7  2020 -file2
-rwxr-x---  1 root bandit5 2440 May  7  2020 .file1
-rwxr-x---  1 root bandit5 4410 May  7  2020 -file1
drwxr-x--- 22 root bandit5 4096 May  7  2020 ..
drwxr-x---  2 root bandit5 4096 May  7  2020 .

./maybehere03:
total 80
-rwxr-x---  1 root bandit5 9234 May  7  2020 spaces file3
-rw-r-----  1 root bandit5 3385 May  7  2020 spaces file2
-rwxr-x---  1 root bandit5 2190 May  7  2020 spaces file1
-rwxr-x---  1 root bandit5 2282 May  7  2020 .file3
-rwxr-x---  1 root bandit5 8275 May  7  2020 -file3
-rw-r-----  1 root bandit5 8880 May  7  2020 .file2
-rw-r-----  1 root bandit5 6595 May  7  2020 -file2
-rwxr-x---  1 root bandit5 9769 May  7  2020 .file1
-rwxr-x---  1 root bandit5  315 May  7  2020 -file1
drwxr-x--- 22 root bandit5 4096 May  7  2020 ..
drwxr-x---  2 root bandit5 4096 May  7  2020 .

./maybehere02:
total 68
-rwxr-x---  1 root bandit5 2275 May  7  2020 spaces file3
-rw-r-----  1 root bandit5 8488 May  7  2020 spaces file2
-rwxr-x---  1 root bandit5 6746 May  7  2020 spaces file1
-rwxr-x---  1 root bandit5 7953 May  7  2020 .file3
-rwxr-x---  1 root bandit5 4932 May  7  2020 -file3
-rw-r-----  1 root bandit5 2577 May  7  2020 .file2
-rw-r-----  1 root bandit5 3511 May  7  2020 -file2
-rwxr-x---  1 root bandit5 6351 May  7  2020 .file1
-rwxr-x---  1 root bandit5 3801 May  7  2020 -file1
drwxr-x--- 22 root bandit5 4096 May  7  2020 ..
drwxr-x---  2 root bandit5 4096 May  7  2020 .

./maybehere01:
total 80
-rwxr-x---  1 root bandit5 8834 May  7  2020 spaces file3
-rw-r-----  1 root bandit5 4543 May  7  2020 spaces file2
-rwxr-x---  1 root bandit5 4139 May  7  2020 spaces file1
-rwxr-x---  1 root bandit5 3792 May  7  2020 .file3
-rwxr-x---  1 root bandit5 9641 May  7  2020 -file3
-rw-r-----  1 root bandit5 3070 May  7  2020 .file2
-rw-r-----  1 root bandit5  288 May  7  2020 -file2
-rwxr-x---  1 root bandit5 8944 May  7  2020 .file1
-rwxr-x---  1 root bandit5 6028 May  7  2020 -file1
drwxr-x--- 22 root bandit5 4096 May  7  2020 ..
drwxr-x---  2 root bandit5 4096 May  7  2020 .

./maybehere00:
total 72
-rwxr-x---  1 root bandit5 1915 May  7  2020 spaces file3
-rw-r-----  1 root bandit5 6850 May  7  2020 spaces file2
-rwxr-x---  1 root bandit5 6118 May  7  2020 spaces file1
-rwxr-x---  1 root bandit5 4802 May  7  2020 .file3
-rwxr-x---  1 root bandit5 7378 May  7  2020 -file3
-rw-r-----  1 root bandit5 7836 May  7  2020 .file2
-rw-r-----  1 root bandit5 9388 May  7  2020 -file2
-rwxr-x---  1 root bandit5  551 May  7  2020 .file1
-rwxr-x---  1 root bandit5 1039 May  7  2020 -file1
drwxr-x--- 22 root bandit5 4096 May  7  2020 ..
drwxr-x---  2 root bandit5 4096 May  7  2020 .
```
지옥도가 펼쳐졌다.... 이럴때 ```clear```쓰거나 **Crtl + L** 쓰면 편----안 해진다 
