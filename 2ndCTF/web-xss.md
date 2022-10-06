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
