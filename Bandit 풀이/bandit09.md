## [Bandit #09](https://overthewire.org/wargames/bandit/bandit9.html)

https://overthewire.org/wargames/bandit/bandit9.html
> The password for the next level is stored in the file data.txt and is the only line of text that occurs only once

``` ssh bandit8@bandit.labs.overthewire.org -p 2220 ```으로 로그인  

암호는 [전에](./bandit08.md) 찾은 ```cvX2JJa4CFALtqS87jk27qwqGhBM9plV```

```
bandit8@bandit:~$ ls
data.txt
```
### 방법1) ```uniq -c```명령어 사용
```
bandit8@bandit:~$ cat data.txt | sort | uniq -c
     10 07KC3ukwX7kswl8Le9ebb3H3sOoNTsR2
     10 0efnqHY1ZTNRu4LsDX4D73DsxIQq7RuJ
     10 0N65ZPpNGkUJePzFxctCRZRXVrCbUGfm
     10 0Xo6DLyK5izRqEtBA7sW2SRmlAixWYSg
     10 10XitczY5Dz7UMoseKIeFWSzzwQrylfw
     10 1ETSsKgjfQj1cJeFzXLJWzKzza3iWcJa
                    ...
     10 ojGabNG5NJ9ppKUBXGr8lwMRRS5GuiA5
     10 TKUtQbeYnEzzYIne7BinoBx2bHFLBXzG
     10 TThRArdF2ZEXMO47TIYkyPPLtvzzLcDf
     10 tVW9iY1Ml0uHPK4usZnN8oZXbjRt2ATY
     10 U0NYdD3wHZKpfEg9qGQOLJimAJy6qxhS
     10 UASW6CQwD6MRzftu6FAfyXBK0cVvnBLP
     10 UJiCNvDNfgb3fcCj8PjjnAXHqUM63Uyj
     10 UjsVbcqKeJqdCZQCDMkzv6A9X7hLbNE4
      1 UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR
     10 UVnZvhiVQECraz5jl8U14sMVZQhjuXia
     10 V2d9umHiuPLYLIDsuHj0frOEmreCZMaA
     10 v9zaxkVAOdIOlITZY2uoCtB1fX2gmly9
     10 VkBAEWyIibVkeURZV5mowiGg6i3m7Be0
     10 w4zUWFGTUrAAh8lNkS8gH3WK2zowBEkA
     10 WBqr9xvf6mYTT5kLcTGCG6jb3ex94xWr
     10 wjNwumEX58RUQTrufHMciWz5Yx10GtTC
     10 X1JHOUkrb4KgugMXIzMWWIWvRkeZleTI
     10 XyeJdbrUJyGtdGx8cXLQST0pwu5cvpcA
     10 yo0HbSe2GM0jJNhRQLxwoPp7ayYEmRKY
     10 ySvsTwlMgnUF0n86Fgmn2TNjkSOlrV72
     10 Z9OC6DQpppreChPhwRJJV9YYTtrxNVcO
     10 zdd2ctVveROGeiS2WE3TeLZMeL5jL7iM
```
```cat data.txt```를 사용하여 출력을 후 ```sort```로 정렬을 하고 ```uniq -c```로 각 문자열별로 중복된 횟수를 확인할 수 있음  
따라서 중간에 보면 중복 횟수가 1인 ```UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR```이 암호임

### 방법2) ```uniq -u```명령어 사용  
```
bandit8@bandit:~$ cat data.txt | sort | uniq -u
UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR
```

이 방법은 찾아봐서 알아냈는데 ```uniq```명령어에서 ```-u```옵션을 사용하면 중복된 문자열을 제외하고 비중복 문자열만 보여줄 수 있음  
편하고 좋은거 같음
