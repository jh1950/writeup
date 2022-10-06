## Web - file upload

### 문제
![Web - file upload](/img/file-upload-0.png)  
파일 업로드 취약점을 이용해 플래그를 알아내야 한다.

### 풀이
![Upload Page](/img/file-upload-1.png)  
여기도 귀여운 너구리 한 마리가 반겨준다..  
그리고 URL을 보면 해당 사이트가 PHP를 사용하는 것을 알 수 있다.

PHP로 웹셸을 작성 후  
![Webshell Code](/img/file-upload-2.png)  
파일을 올리면

![Uplaod Path](/img/file-upload-3.png)  
친절하게도 파일이 업로드된 위치를 알려준다. ..?

이제 위 경로로 접속하면  
![Webshell](/img/file-upload-4.png)  
웹셸을 사용할 수 있다.

![Webshell - ls -lhA ../](/img/file-upload-5.png)  
`flag`라는 이름을 가진 파일을 찾았다.

이제 저 파일을 읽기만 하면 된다.  
![Webshell - cat ../flag](/img/file-upload-6.png)  
`flag` 파일의 위치를 브라우저로 접속해도 된다.
