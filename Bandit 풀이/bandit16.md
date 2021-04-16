## [Bandit #16](https://overthewire.org/wargames/bandit/bandit16.html)

https://overthewire.org/wargames/bandit/bandit16.html
> The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.
>> **Helpful note: Getting “HEARTBEATING” and “Read R BLOCK”? Use -ign_eof and read the “CONNECTED COMMANDS” section in the manpage. Next to ‘R’ and ‘Q’, the ‘B’ command also works in this version of that command…**

``` ssh bandit15@bandit.labs.overthewire.org -p 2220 ```으로 로그인  

암호는 [전에](./bandit15.md) 찾은 ```BfMYroe26WYalil77FoDi9qh59eK5xNr```

SSL암호화에 관해 구글링을 해보았다. ([참조](https://www.lesstif.com/software-architect/openssl-command-tip-7635159.html))   
```openssl```이라는 커맨드를 통해 ssl 암호화로 접속 할 수있다고 찾았다.
```
bandit15@bandit:~$ openssl s_client -connect localhost:30001
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
MIICBjCCAW+gAwIBAgIEfftLGTANBgkqhkiG9w0BAQUFADAUMRIwEAYDVQQDDAls
b2NhbGhvc3QwHhcNMjEwNDEzMDgzODA3WhcNMjIwNDEzMDgzODA3WjAUMRIwEAYD
VQQDDAlsb2NhbGhvc3QwgZ8wDQYJKoZIhvcNAQEBBQADgY0AMIGJAoGBAMLfXBVa
jVKDHlA3U+S0hBMJMJlfue3xKECpmx1Ajp4/khUuWwvPB7+wLjqasBO2WfFYJzcq
z9t7FfAPIlYjgvOTQs5X4vQ1aGzanvnNn+1VknpOnFAJQBSFq6ZD3ipWrhwm9XZq
8CgFhTGp9IPthZp8Y0B7OgobhlMtXD/zLaTbAgMBAAGjZTBjMBQGA1UdEQQNMAuC
CWxvY2FsaG9zdDBLBglghkgBhvhCAQ0EPhY8QXV0b21hdGljYWxseSBnZW5lcmF0
ZWQgYnkgTmNhdC4gU2VlIGh0dHBzOi8vbm1hcC5vcmcvbmNhdC8uMA0GCSqGSIb3
DQEBBQUAA4GBAMFH9rsZovwnb5k71/MpyCnXEwGlIhixUu6qfi1kiFvhJ6lJCvaO
weOYxV4oJy1OEB0LSEAQOnSPfzC8dDasijFcdVhuIGGPuQ2GZ05nCiiIZUNnrMRB
0z2RuRxgxMVjOvcSIJyvwyjVH4jY4I434fMyldePLxO1POLd1cxoKNTO
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
    Session-ID: 7969D949AE5429A55202DFF3C7165F7538394FA0F10B07FEA35D29229E18C54A
    Session-ID-ctx:
    Master-Key: 1DB89CE610C35B1A9BE23CF786FF5C2B89B75A2A3C4BEDFA25B5CD908DAC21B2B4008E315C1D2853C4F1A45596723AB4
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - f2 5b 83 7e f0 ca 58 ca-aa f3 8f 83 b9 65 d5 23   .[.~..X......e.#
    0010 - 3b b5 0b 7c 48 f4 e2 f9-93 cd 48 35 e1 60 d2 45   ;..|H.....H5.`.E
    0020 - e8 e5 4b 13 19 e3 7f 97-73 40 c0 a0 18 bb be 45   ..K.....s@.....E
    0030 - 39 81 42 ea 9f ee d6 1c-42 df 86 27 39 41 fb 62   9.B.....B..'9A.b
    0040 - 14 83 31 14 65 95 2d 0a-a4 43 6c 88 b0 05 5d 4c   ..1.e.-..Cl...]L
    0050 - 81 e0 1c 70 cb 40 b6 89-6b 26 67 55 47 d6 d5 fb   ...p.@..k&gUG...
    0060 - 16 db 80 1a b5 c7 ae ba-a4 d4 86 62 58 36 10 fa   ...........bX6..
    0070 - 5e ec 24 69 d5 81 97 c3-8c 26 36 9d 89 ed 0e 4b   ^.$i.....&6....K
    0080 - 57 9c 26 ed de 52 33 7d-18 9a 26 33 4b 39 d5 49   W.&..R3}..&3K9.I
    0090 - a1 6f 31 74 30 9a 87 40-d7 2e b1 30 11 a0 c5 4f   .o1t0..@...0...O

    Start Time: 1618581262
    Timeout   : 7200 (sec)
    Verify return code: 18 (self signed certificate)
    Extended master secret: yes
---
BfMYroe26WYalil77FoDi9qh59eK5xNr
Correct!
cluFn7wTiGryunymYOu4RcffSxQluehd

closed
```
암호는 ```cluFn7wTiGryunymYOu4RcffSxQluehd```로 해결된것을 볼 수 있다.

#### ++다 풀고 helpful note 내용이 궁금해서 구글링 좀 해보니까 [다른 사람](https://websecurity.tistory.com/101)은 오류가 나는것을 볼 수 있었다  
```-ign_eof```는 대충 파일의 끝에 도달해도(EOF) 무시(ignore)하라는 커맨드라고들 한다. 
