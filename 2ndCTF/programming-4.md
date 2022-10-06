## Programming - Programming 4

### 문제
![Programming 4](/img/programming-4-0.png)  
소수 = 약수가 1과 자기 자신밖에 없는 수

### 풀이
코드 작성  
```python
#!/usr/bin/env python3

def f_cus(i):
    for j in range(2, int(i**1/2)+1):
        if i%j==0: return False
    return True

c = []
for i in range(2, 90001):
    if f_cus(i): c.append(i)

print( len(c) )
```

코드 실행 결과  
![Python code - Result](/img/programming-4-2.png)
