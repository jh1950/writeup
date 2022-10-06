## Programming - Programming 1

### 문제
![Programming 1](/img/programming-1-0.png)  
플래그 형식이 주어진다.

### 풀이
파일을 다운받고 열어보면  
![problem.txt](/img/programming-1-1.png)  
문제가 나온다. 계산기를 쓰던 코딩을 하던 하면 될 것 같다.

파이썬 코드 작성 후  
```python
#!/usr/bin/env python3

a, b, c = 1598, 4987, 4565
p1 = a**2 + b + b*c

a, b, c = 94, 326548, 156487
p2 = (b+c)*a

a, b, c = 9487, 45896, 10624
p3 = a*b*c*100

print('2ndCTF{' + f'{p1}_{p2}_{p3}' + '}')
```
실행하면  
![python code - result](/img/programming-1-3.png)  
끝
