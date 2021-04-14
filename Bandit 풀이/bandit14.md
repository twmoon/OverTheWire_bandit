## [Bandit #14](https://overthewire.org/wargames/bandit/bandit14.html)

https://overthewire.org/wargames/bandit/bandit14.html
> The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on

``` ssh bandit13bandit.labs.overthewire.org -p 2220 ```으로 로그인  

암호는 [전에 ~~(눈물겨움 주의)~~ ](./bandit13.md) 찾은 ```8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL```

산 넘어 산이라더니 이번엔 아에 비밀번호를 안 알려준다고 문제에서 명시를 해놨다....  

일단 ```private SSH key```를 찾아보도록 하겠다.
```
bandit13@bandit:~$ ls
sshkey.private
```

```ls```를 하니까 ```sshkey.private```이라는 뭔가 ```private SSH key```과 연관있어 보이는 파일이 있었다.  
```cat sshkey.private```해보면
```
bandit13@bandit:~$ cat sshkey.private
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEAxkkOE83W2cOT7IWhFc9aPaaQmQDdgzuXCv+ppZHa++buSkN+
gg0tcr7Fw8NLGa5+Uzec2rEg0WmeevB13AIoYp0MZyETq46t+jk9puNwZwIt9XgB
ZufGtZEwWbFWw/vVLNwOXBe4UWStGRWzgPpEeSv5Tb1VjLZIBdGphTIK22Amz6Zb
ThMsiMnyJafEwJ/T8PQO3myS91vUHEuoOMAzoUID4kN0MEZ3+XahyK0HJVq68KsV
ObefXG1vvA3GAJ29kxJaqvRfgYnqZryWN7w3CHjNU4c/2Jkp+n8L0SnxaNA+WYA7
jiPyTF0is8uzMlYQ4l1Lzh/8/MpvhCQF8r22dwIDAQABAoIBAQC6dWBjhyEOzjeA
J3j/RWmap9M5zfJ/wb2bfidNpwbB8rsJ4sZIDZQ7XuIh4LfygoAQSS+bBw3RXvzE
pvJt3SmU8hIDuLsCjL1VnBY5pY7Bju8g8aR/3FyjyNAqx/TLfzlLYfOu7i9Jet67
xAh0tONG/u8FB5I3LAI2Vp6OviwvdWeC4nOxCthldpuPKNLA8rmMMVRTKQ+7T2VS
nXmwYckKUcUgzoVSpiNZaS0zUDypdpy2+tRH3MQa5kqN1YKjvF8RC47woOYCktsD
o3FFpGNFec9Taa3Msy+DfQQhHKZFKIL3bJDONtmrVvtYK40/yeU4aZ/HA2DQzwhe
ol1AfiEhAoGBAOnVjosBkm7sblK+n4IEwPxs8sOmhPnTDUy5WGrpSCrXOmsVIBUf
laL3ZGLx3xCIwtCnEucB9DvN2HZkupc/h6hTKUYLqXuyLD8njTrbRhLgbC9QrKrS
M1F2fSTxVqPtZDlDMwjNR04xHA/fKh8bXXyTMqOHNJTHHNhbh3McdURjAoGBANkU
1hqfnw7+aXncJ9bjysr1ZWbqOE5Nd8AFgfwaKuGTTVX2NsUQnCMWdOp+wFak40JH
PKWkJNdBG+ex0H9JNQsTK3X5PBMAS8AfX0GrKeuwKWA6erytVTqjOfLYcdp5+z9s
8DtVCxDuVsM+i4X8UqIGOlvGbtKEVokHPFXP1q/dAoGAcHg5YX7WEehCgCYTzpO+
xysX8ScM2qS6xuZ3MqUWAxUWkh7NGZvhe0sGy9iOdANzwKw7mUUFViaCMR/t54W1
GC83sOs3D7n5Mj8x3NdO8xFit7dT9a245TvaoYQ7KgmqpSg/ScKCw4c3eiLava+J
3btnJeSIU+8ZXq9XjPRpKwUCgYA7z6LiOQKxNeXH3qHXcnHok855maUj5fJNpPbY
iDkyZ8ySF8GlcFsky8Yw6fWCqfG3zDrohJ5l9JmEsBh7SadkwsZhvecQcS9t4vby
9/8X4jS0P8ibfcKS4nBP+dT81kkkg5Z5MohXBORA7VWx+ACohcDEkprsQ+w32xeD
qT1EvQKBgQDKm8ws2ByvSUVs9GjTilCajFqLJ0eVYzRPaY6f++Gv/UVfAPV4c+S0
kAWpXbv5tbkkzbS0eaLPTKgLzavXtQoTtKwrjpolHKIHUz6Wu+n4abfAIRFubOdN
/+aLoRQ0yBDRbdXMsZN/jvY44eM+xRLdRVyMmdPtP8belRi2E2aEzA==
-----END RSA PRIVATE KEY-----
```

```sshkey.private```파일이 ssh 개인키 파일인것을 알 수 있었다. 따라서 암호 없이도 로그인에 성공할 수 있다는 것이다. 무야호~~  
패스워드가 있는 ```/etc/bandit_pass```로 들어가보면  
```
bandit13@bandit:~$ cd /etc/bandit_pass
bandit13@bandit:/etc/bandit_pass$ ls -al
total 144
drwxr-xr-x  2 root     root     4096 May  7  2020 .
drwxr-xr-x 87 root     root     4096 May 14  2020 ..
-r--------  1 bandit0  bandit0     8 May  7  2020 bandit0
-r--------  1 bandit1  bandit1    33 May  7  2020 bandit1
-r--------  1 bandit10 bandit10   33 May  7  2020 bandit10
-r--------  1 bandit11 bandit11   33 May  7  2020 bandit11
-r--------  1 bandit12 bandit12   33 May  7  2020 bandit12
-r--------  1 bandit13 bandit13   33 May  7  2020 bandit13
-r--------  1 bandit14 bandit14   33 May  7  2020 bandit14
-r--------  1 bandit15 bandit15   33 May  7  2020 bandit15
-r--------  1 bandit16 bandit16   33 May  7  2020 bandit16
-r--------  1 bandit17 bandit17   33 May  7  2020 bandit17
-r--------  1 bandit18 bandit18   33 May  7  2020 bandit18
-r--------  1 bandit19 bandit19   33 May  7  2020 bandit19
-r--------  1 bandit2  bandit2    33 May  7  2020 bandit2
-r--------  1 bandit20 bandit20   33 May  7  2020 bandit20
-r--------  1 bandit21 bandit21   33 May  7  2020 bandit21
-r--------  1 bandit22 bandit22   33 May  7  2020 bandit22
-r--------  1 bandit23 bandit23   33 May  7  2020 bandit23
-r--------  1 bandit24 bandit24   33 May  7  2020 bandit24
-r--------  1 bandit25 bandit25   33 May  7  2020 bandit25
-r--------  1 bandit26 bandit26   33 May  7  2020 bandit26
-r--------  1 bandit27 bandit27   33 May  7  2020 bandit27
-r--------  1 bandit28 bandit28   33 May  7  2020 bandit28
-r--------  1 bandit29 bandit29   33 May  7  2020 bandit29
-r--------  1 bandit3  bandit3    33 May  7  2020 bandit3
-r--------  1 bandit30 bandit30   33 May  7  2020 bandit30
-r--------  1 bandit31 bandit31   33 May  7  2020 bandit31
-r--------  1 bandit32 bandit32   33 May  7  2020 bandit32
-r--------  1 bandit33 bandit33   33 May  7  2020 bandit33
-r--------  1 bandit4  bandit4    33 May  7  2020 bandit4
-r--------  1 bandit5  bandit5    33 May  7  2020 bandit5
-r--------  1 bandit6  bandit6    33 May  7  2020 bandit6
-r--------  1 bandit7  bandit7    33 May  7  2020 bandit7
-r--------  1 bandit8  bandit8    33 May  7  2020 bandit8
-r--------  1 bandit9  bandit9    33 May  7  2020 bandit9
bandit13@bandit:/etc/bandit_pass$ cat bandit13
8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL
bandit13@bandit:/etc/bandit_pass$ cat bandit14
cat: bandit14: Permission denied
```

권한을 보면 모든 파일은 소유자 본인의 파일만 읽을수 있다고 보여진다.   
따라서 ```cat bandit13```은 성공적으로 읽을 수 있지만 ```cat bandit14```는 권한 오류가 발생한다.  

따라서 우리는 암호를 알기위해 bandit14로 로그인할 필요가 있다.  
전에 얻어두었던 ```sshkey.private```를 이용하여 bandit14에 로그인해보면
```
bandit13@bandit:~$ ssh -i sshkey.private bandit14@localhost
Could not create directory '/home/bandit13/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit13/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

Linux bandit.otw.local 5.4.8 x86_64 GNU/Linux
생략(로그인 할때 나오는 상투적인 페이지)
```

이러면 성공적으로 bandit14에 로그인할 수 있다.
이제 남은건 암호 파일에 접근해서 값을 알아내는 것이다.
```
bandit14@bandit:~$ cd /etc/bandit_pass/
bandit14@bandit:/etc/bandit_pass$ cat bandit14
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
```
짜잔 암호는 ```4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e```이였습니다.

#### 궁금해서 ```ssh -i sshkey.private bandit15@localhost```로 접근해 보니까 
```
bandit13@bandit:~$ ssh -i sshkey.private bandit15@localhost
Could not create directory '/home/bandit13/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit13/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit15@localhost's password:
```

암호를 입력하라고 나온다... ```sshkey.private```은 bnadit14용 개인키인데...
너무 당연한건데 너무 큰 기대를 품어서 살짝 실망했다.
