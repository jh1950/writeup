## Programming - Programming 2

### 문제
![Programming 2](/img/programming-2-0.png)  

### 풀이
파일 오픈  
![problem.txt](/img/programming-2-1.png)

코드 작성  
```
#!/usr/bin/env python3

list = '50 110 100 67 84 70 123 65 115 99 105 105 95 101 78 99 111 68 101 114 95 72 111 119 95 68 101 99 48 100 49 110 103 63 125'.split(' ')

for i in list:
    print( chr(int(i)), end='' )
print()
```

코드 실행 결과  
![Python code - Result](/img/programming-2-3.png)
