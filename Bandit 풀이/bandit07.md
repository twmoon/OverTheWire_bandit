## [Bandit #07](https://overthewire.org/wargames/bandit/bandit7.html)

https://overthewire.org/wargames/bandit/bandit7.html
> The password for the next level is stored somewhere on the server and has all of the following properties:
>>owned by user bandit7  
>>owned by group bandit6  
>>33 bytes in size

``` ssh bandit6@bandit.labs.overthewire.org -p 2220 ```으로 로그인  

암호는 [전에](./bandit06.md) 찾은 ```DXjZPULLxYr17uwoI01bNLQbtFemEgo7```

```
bandit6@bandit:~$ ls -a
.  ..  .bash_logout  .bashrc  .profile
bbandit6@bandit:~$ find / -size 33c -user bandit7 -group bandit6 2>/dev/null
/var/lib/dpkg/info/bandit7.password
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs
```

```ls -a```로 현제 디렉토리를 탐색해도 별다른게 보이지 않으므로 ROOT 디렉토리부터 조건에 맞는 파일을 검색할 것이다.  
처음에는 ```find / -size 33c -user bandit7 -group bandit6```로 검색했으나 (검색 결과 아래)  
ROOT 디렉토리부터 모든 파일을 검색하는 것이기 때문에 수 많은 권한 오류로 에러 메세지들이 결과창을 더럽힌다.  
따라서 ```2>/dev/null```을 이용해 에러 메세지들을 날려주면 조건에 적합한 ```/var/lib/dpkg/info/bandit7.password```이 검색되고  
```cat /var/lib/dpkg/info/bandit7.password```하면 암호를 볼 수 있다!!

#### ++ ```2>/dev/null``` 자세히 뜯어보기
```0>``` -----------> 표준 입력  
```1>``` -----------> 표준 출력    
```2>``` -----------> 표준 오류  
```/dev/null``` ----> NULL 장치  
```2>/dev/null``` --> 오류 메세지를 NULL장치로 출력 --> 오류메세지 출력 안함  

#### ++ ```find / -size 33c -user bandit7 -group bandit6``` 검색 결과
```
bandit6@bandit:~$ find / -group bandit6 -user bandit7 -size 33c
find: ‘/root’: Permission denied
find: ‘/home/bandit28-git’: Permission denied
find: ‘/home/bandit30-git’: Permission denied
find: ‘/home/bandit5/inhere’: Permission denied
find: ‘/home/bandit27-git’: Permission denied
find: ‘/home/bandit29-git’: Permission denied
find: ‘/home/bandit31-git’: Permission denied
find: ‘/lost+found’: Permission denied
find: ‘/etc/ssl/private’: Permission denied
find: ‘/etc/polkit-1/localauthority’: Permission denied
find: ‘/etc/lvm/archive’: Permission denied
find: ‘/etc/lvm/backup’: Permission denied
find: ‘/sys/fs/pstore’: Permission denied
find: ‘/proc/tty/driver’: Permission denied
find: ‘/proc/12316/task/12316/fd/6’: No such file or directory
find: ‘/proc/12316/task/12316/fdinfo/6’: No such file or directory
find: ‘/proc/12316/fd/5’: No such file or directory
find: ‘/proc/12316/fdinfo/5’: No such file or directory
find: ‘/cgroup2/csessions’: Permission denied
find: ‘/boot/lost+found’: Permission denied
find: ‘/tmp’: Permission denied
find: ‘/run/lvm’: Permission denied
find: ‘/run/screen/S-bandit20’: Permission denied
find: ‘/run/shm’: Permission denied
find: ‘/run/lock/lvm’: Permission denied
find: ‘/var/spool/bandit24’: Permission denied
find: ‘/var/spool/cron/crontabs’: Permission denied
find: ‘/var/spool/rsyslog’: Permission denied
find: ‘/var/tmp’: Permission denied
find: ‘/var/lib/apt/lists/partial’: Permission denied
find: ‘/var/lib/polkit-1’: Permission denied
/var/lib/dpkg/info/bandit7.password
find: ‘/var/log’: Permission denied
find: ‘/var/cache/apt/archives/partial’: Permission denied
find: ‘/var/cache/ldconfig’: Permission denied
```
중간에 아주 자세히 보면 ```/var/lib/dpkg/info/bandit7.password```가 있긴 한데 이런거 찾을 시간이 있으면 시험 일주일 남았는데 교양 프린트 한 번 더 보는걸 추천  
