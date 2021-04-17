## [Bandit #17](https://overthewire.org/wargames/bandit/bandit17.html)

https://overthewire.org/wargames/bandit/bandit17.html
> The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.               

``` ssh bandit16@bandit.labs.overthewire.org -p 2220 ```으로 로그인  

암호는 [전에](./bandit16.md) 찾은 ```cluFn7wTiGryunymYOu4RcffSxQluehd```

이 문제는 약 천개의 포트 중 열려있는 포트를 찾는 문제이다.
```nmap```명령어를 이용하여 포트를 스캔하면 해결될 거 같다. 
```
bandit16@bandit:~$ nmap -p localhost 31000-32000

Starting Nmap 7.40 ( https://nmap.org ) at 2021-04-17 15:14 CEST
Found no matches for the service mask 'localhost' and your specified protocols
QUITTING!
bandit16@bandit:~$ nmap localhost -p 31000-32000

Starting Nmap 7.40 ( https://nmap.org ) at 2021-04-17 15:14 CEST
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00034s latency).
Not shown: 996 closed ports
PORT      STATE SERVICE
31046/tcp open  unknown
31518/tcp open  unknown
31691/tcp open  unknown
31790/tcp open  unknown
31960/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 0.08 seconds
```

보면 총 5개의 포트가 열려있는 것을 볼 수 있다.  
이제 남은건 5개의 포트에 암호를 해봐도 되지만 문제에서 ssl을 사용하는 포트를 찾으라 했으니  
```nc```를 이용하여 간단한 문자를 보내보면
```
bandit16@bandit:~$ echo ?? | nc localhost 31046
??
^C
bandit16@bandit:~$ echo ?? | nc localhost 31518
^C
bandit16@bandit:~$ echo ?? | nc localhost 31691
??
^C
bandit16@bandit:~$ echo ?? | nc localhost 31790
^C
bandit16@bandit:~$ echo ?? | nc localhost 31960
??
^C
```

포트 31046,31691,31960는 단순히 데이터를 돌려주는 포트 같고 나머지 포트 31518, 31790가 ssl을 사용하는 포트로 추정된다.  
ssl을 사용하는 포트 2곳에 현재 레벨의 암호 ```cluFn7wTiGryunymYOu4RcffSxQluehd```를 입력해주면
```
bandit16@bandit:~$ openssl s_client -connect localhost:31518
CONNECTED(00000003)
depth=0 CN = localhost
verify error:num=18:self signed certificate
verify return:1
depth=0 CN = localhost
verify return:1
---
Certificate chain
 0 s:/CN=localhost
   i:/CN=localhost
---
Server certificate
-----BEGIN CERTIFICATE-----
MIICBjCCAW+gAwIBAgIETAnsOzANBgkqhkiG9w0BAQUFADAUMRIwEAYDVQQDDAls
b2NhbGhvc3QwHhcNMjEwNDEzMDgzOTAyWhcNMjIwNDEzMDgzOTAyWjAUMRIwEAYD
VQQDDAlsb2NhbGhvc3QwgZ8wDQYJKoZIhvcNAQEBBQADgY0AMIGJAoGBAPdDeqD+
TfS3WqaEQFYaamXCjcRO9RB6R4tqKkkkS/E06dKfP6v8+OfuYHMc8gS5IVst5I+c
indf3oSiE1MmskmuzHlje+QKSjZEL4K+oFBD8vUr91q22NRgkdwmcGLANYpU2I2o
+CGB15a1al5UmU6apThvqFnzKOVBq634XaOFAgMBAAGjZTBjMBQGA1UdEQQNMAuC
CWxvY2FsaG9zdDBLBglghkgBhvhCAQ0EPhY8QXV0b21hdGljYWxseSBnZW5lcmF0
ZWQgYnkgTmNhdC4gU2VlIGh0dHBzOi8vbm1hcC5vcmcvbmNhdC8uMA0GCSqGSIb3
DQEBBQUAA4GBAAzuRK+BEijL+kgZ/Yo78izaPpgZr9q+NqDIHMxjtF4lDsQZVJuv
00HZ+StojQeAmJn5BRmcN3WBs9lwwcZuqr2eMk/KFJ4ZKKMaQjBGtLe/9qoMlCA2
7iv7/q1UVLCYsOfgOzIMY+UQtb4HrLenvI8F6ndraMI5AzjLJet8LfAI
-----END CERTIFICATE-----
subject=/CN=localhost
issuer=/CN=localhost
---
No client certificate CA names sent
Peer signing digest: SHA512
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 1019 bytes and written 269 bytes
Verification error: self signed certificate
---
New, TLSv1.2, Cipher is ECDHE-RSA-AES256-GCM-SHA384
Server public key is 1024 bit
Secure Renegotiation IS supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
SSL-Session:
    Protocol  : TLSv1.2
    Cipher    : ECDHE-RSA-AES256-GCM-SHA384
    Session-ID: E4342DCE59AFC3FF1310275F6B76346C57FB337B5E6D771DEB19E8A9CA61C89B
    Session-ID-ctx:
    Master-Key: 18DBA9A9C5A2AA5C3BE4BFF2EFF73ECCE96067730C7039F32AE4102D2B54F6149AFE9E34B107FA3BF21CA3D3628EE40F
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - 27 f7 c2 d1 66 25 86 f4-a5 ac ce 74 a6 68 5b 20   '...f%.....t.h[
    0010 - 7c dc 95 af 0f ce 8c 1c-a1 9e 80 9e 00 94 61 38   |.............a8
    0020 - 55 23 8f 16 0d 71 e0 a5-24 99 8e 08 2c cb e6 ed   U#...q..$...,...
    0030 - 84 ee 07 67 8e b5 09 a5-1a a0 93 3f 7d e3 3f 8d   ...g.......?}.?.
    0040 - b1 1c a1 a6 4e 27 ad 0b-d0 c4 87 fb e0 9c 3c ab   ....N'........<.
    0050 - 18 b6 8f 94 c6 8c 10 64-78 19 9b bd eb 5b 32 65   .......dx....[2e
    0060 - 72 36 c5 56 4a 06 01 5a-b7 12 41 b2 31 4e de bd   r6.VJ..Z..A.1N..
    0070 - 2d 5f 93 15 12 b0 38 11-bb 7d 0d 4a b4 70 cd 38   -_....8..}.J.p.8
    0080 - 7a 60 6c 40 32 af 1d 9c-65 c8 09 8d c5 b6 e9 f2   z`l@2...e.......
    0090 - 41 be 05 1a 3d 84 7f 28-7c e6 31 bb 74 6b 08 92   A...=..(|.1.tk..

    Start Time: 1618665779
    Timeout   : 7200 (sec)
    Verify return code: 18 (self signed certificate)
    Extended master secret: yes
---
cluFn7wTiGryunymYOu4RcffSxQluehd
cluFn7wTiGryunymYOu4RcffSxQluehd
DONE
```

포트 31518은 그냥 입력한 문자 그대로 
```
bandit16@bandit:~$ openssl s_client -connect localhost:31790
CONNECTED(00000003)
depth=0 CN = localhost
verify error:num=18:self signed certificate
verify return:1
depth=0 CN = localhost
verify return:1
---
Certificate chain
 0 s:/CN=localhost
   i:/CN=localhost
---
Server certificate
-----BEGIN CERTIFICATE-----
MIICBjCCAW+gAwIBAgIEAVEaADANBgkqhkiG9w0BAQUFADAUMRIwEAYDVQQDDAls
b2NhbGhvc3QwHhcNMjEwNDEzMDgzOTAyWhcNMjIwNDEzMDgzOTAyWjAUMRIwEAYD
VQQDDAlsb2NhbGhvc3QwgZ8wDQYJKoZIhvcNAQEBBQADgY0AMIGJAoGBAMSNMcd2
/JHQJIG6WVZ1VjJUi7NU2N/tkFLsLv7Y3slHaQAHLaC2aqILEQwYjDAhkvCogSwx
nvyWicMmNAUie9JaHNqKbRXPawKvKpr3bMgH5Gwbj/aUt18FZlzGUVJJfGzlWPkr
A2nwgzcVLkJKWR/2bV1C9gh/VqTYtUxPi7RtAgMBAAGjZTBjMBQGA1UdEQQNMAuC
CWxvY2FsaG9zdDBLBglghkgBhvhCAQ0EPhY8QXV0b21hdGljYWxseSBnZW5lcmF0
ZWQgYnkgTmNhdC4gU2VlIGh0dHBzOi8vbm1hcC5vcmcvbmNhdC8uMA0GCSqGSIb3
DQEBBQUAA4GBAGcuQr3/eWigw9h33i60xbf62wgXV8lcX6BuQ5xvOgd8eyvFIohp
usJHhSNGtdA+V0cw2qRuwWCmC/+unVvDWyC5OX2ka3XuF1Z9Z9282z+BCsuSAYHS
P3Oibv3/cEqa3kPuswuHOn2LkJmL/a/Kwwkzwfi/j9RIR/jm9FEOVlgm
-----END CERTIFICATE-----
subject=/CN=localhost
issuer=/CN=localhost
---
No client certificate CA names sent
Peer signing digest: SHA512
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 1019 bytes and written 269 bytes
Verification error: self signed certificate
---
New, TLSv1.2, Cipher is ECDHE-RSA-AES256-GCM-SHA384
Server public key is 1024 bit
Secure Renegotiation IS supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
SSL-Session:
    Protocol  : TLSv1.2
    Cipher    : ECDHE-RSA-AES256-GCM-SHA384
    Session-ID: 660A641DE1B09E72161BC63C02118170A3FDCF26474CAE8603B4C2C8E164EDAD
    Session-ID-ctx:
    Master-Key: 801E3BAEE91C6090D668AD60C57AF90F1556A3309EE7E804DDC95AB83CBFEC34F21ED61329C4265210AE47730601E786
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - 03 83 6e 86 7a 68 2a 2b-55 2d 9b 9e 6d 2f ce e5   ..n.zh*+U-..m/..
    0010 - 22 e2 5d 72 e9 7d 2e 3e-f3 8d e7 e7 fd 68 14 0d   ".]r.}.>.....h..
    0020 - c8 4b 48 8c d6 77 07 c4-c0 82 fd f6 06 f9 ac bd   .KH..w..........
    0030 - 2f 03 f1 81 e5 f5 76 18-d4 f4 b3 35 3c 4d a1 f4   /.....v....5<M..
    0040 - 3f 10 20 fc 4c f8 69 9d-26 3f fb 9b 3d 32 f8 3c   ?. .L.i.&?..=2.<
    0050 - 04 7c 72 f1 26 4f 1d 78-22 02 05 6b 29 4f 34 74   .|r.&O.x"..k)O4t
    0060 - fa cf 8d 35 93 ef 34 ba-50 da 9f fc 64 19 d0 79   ...5..4.P...d..y
    0070 - 43 4e 54 4a e4 f4 40 f9-84 cf e2 68 5d bf 78 2c   CNTJ..@....h].x,
    0080 - f9 d4 d9 b7 eb 10 1d 59-3e b3 52 1f 37 54 c7 73   .......Y>.R.7T.s
    0090 - 99 e3 85 94 5d be 21 08-63 35 c7 a7 f6 64 10 19   ....].!.c5...d..

    Start Time: 1618663585
    Timeout   : 7200 (sec)
    Verify return code: 18 (self signed certificate)
    Extended master secret: yes
---
cluFn7wTiGryunymYOu4RcffSxQluehd
Correct!
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----

closed
```

나머지 포트는 암호 ```cluFn7wTiGryunymYOu4RcffSxQluehd```를 입력하니까 익숙한 RSA PRIVATE KEY, 즉 SSH 개인키 파일을 획득했다.
쓰기 권한이 있는 ```/tmp/17```경로에 파일을 만들어 bandit17로의 로그인 인증을 시도하였다
```
bandit16@bandit:/tmp$ mkdir /tmp/17
bandit16@bandit:~$ cd /tmp/17
bandit16@bandit:/tmp/17$ vi private.txt
bandit16@bandit:/tmp/17$ ssh -i private.txt bandit17@localhost
Could not create directory '/home/bandit16/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit16/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0644 for 'private.txt' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "private.txt": bad permissions
bandit17@localhost's password: Connection to bandit.labs.overthewire.org closed by remote host.
Connection to bandit.labs.overthewire.org closed.
```
권한이 너무 열려있다면서 오류가 발생하게 된다.  
전에 [Bandit #14](./bandit14.md)에서 ```sshkey.private```파일의 권한을 비교해보면 
```
bandit13@bandit:~$ ls -l
total 4
-rw-r----- 1 bandit14 bandit13 1679 May  7  2020 sshkey.private
```
```
bandit16@bandit:/tmp/17$ ls -l
total 4
-rw-r--r-- 1 bandit16 root 1675 Apr 17 15:03 private.txt
```
본인 외에는 파일 수정을 막아야하므로 600으로 바꾸고 다시 인증 해볼거다.
```
bandit16@bandit:/tmp/17$ chmod 600 private.txt
bandit16@bandit:/tmp/17$ ls -l
total 4
-rw------- 1 bandit16 root 1675 Apr 17 15:03 private.txt
```
```
bandit16@bandit:/tmp/17$ ssh -i private.txt bandit17@localhost
Could not create directory '/home/bandit16/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit16/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

Linux bandit.otw.local 5.4.8 x86_64 GNU/Linux
생략(로그인 할때 나오는 상투적인 페이지)
```

bandit17로 성공적으로 접속하였고 이제 암호가 저장되어있는 페이지로 가서 암호를 보면 끝이다
```
bandit17@bandit:~$ cd /etc/bandit_pass/
bandit17@bandit:/etc/bandit_pass$ cat bandit17
xLYVMN9WE5zQ5vHacb0sZEVqbrp7nBTn
```
암호는 ```xLYVMN9WE5zQ5vHacb0sZEVqbrp7nBTn```이다.
