## HTTP 메시지

HTTP 메시지는 서버와 클라이언트 간에 데이터가 교환되는 방식이다. 메시지는 두 종류가 있다. 요청(*request)은* 클라이언트가 서버로 전달해서 서버의 액션이 일어나게끔 하는 메시지고, 응답(*response)은 요청*에 대한 서버의 대답이다.

HTTP 메시지는 텍스트 정보이다. 메시지는 시작줄, 헤더, 본문으로 이루어진다. 각 블록은 빈 줄(CRLF)로 구분된다.

![메시지_형식](https://user-images.githubusercontent.com/40727649/61178740-4520e180-a62e-11e9-8fda-c892da76eaf6.png)



## HTTP REQUEST

### 시작줄

Start-line. 실행해야 할 요청, 또는 요청에 대한 성공 or 실패가 기록된다. 항상 한 줄로 끝난다.  

```
<메서드> <URI> <HTTP Version>
GET www.naver.com/ HTTP/1.1
```

### 헤더

헤더는 키-밸류 쌍으로 구성한다. HTTP에 정의되어 있는 헤더를 사용하는 것을 권장한다.  
헤더는 여러 줄로 이루어져 있을 수 있다.

```
Accept : text/html
Cookie : abcdefg?expire=1234123&v=1.3
...
```

![헤더_예시](https://user-images.githubusercontent.com/40727649/61178741-48b46880-a62e-11e9-855f-91ba7ef77e1e.png)

### 본문

모든 요청에 본문이 필요한 것은 아니다. `POST, PUT`의 경우 본문이 있을 수 있지만, `GET, DELETE`의 경우 없을 수 있다.

```
POST our-generation.com/andole HTTP/1.1

Content-Type : application/json

{
	"data": "미안해 솔직하지 못한 내가"
}

```



## HTTP RESPONSE

### 시작줄

상태 줄`status line`이라고 부르기도 한다. 상태 코드를 포함한다.  

```
<HTTP Version> <Status Code> <Status Text>
HTTP/1.1 200 Ok
HTTP/1.1 302 Temporary Moved
HTTP/1.1 404 Not Found
HTTP/1.1 500 Internal Sever Error
```

### 헤더

요청 헤더와 공통으로 사용하는 헤더가 많다.   
쿠키와 관련한 `Set-cookie`, 리소스와 관련한 `Content`헤더를 자주 볼 수 있다.

```
Keep-Alive : timeout=10, max=999
Set-Cookie: csrftoken= ...
Content-type : text/html; charset=utf-8
Content-Length: 12345
```

### 본문

요청한 리소스 자체가 들어간다. `naver.com`의 `index.html`이 본문에 들어 있거나, `naver.com/main.png` 이미지 파일의 바이너리가 들어있다.

```
<html>
<head>Naver</head>
<body>
	...
</body>
</html
```



## 레퍼런스

메시지의 구조는 쉽게 이해할 수 있다. 문제는 `MIME`타입이나 `HEADER` 정보는 매우 많다.  
MDN과 같은 곳에서 치트시트를 찾아 사용하는게 좋다.

예) 엑셀 파일을 전달하려면 `MIME Type`을 뭐로 해야 하더라? -> `Content-Type : application/vnd.ms-excel`

예) 캐시를 허용하지 않으려면 헤더를 어떻게 했더라? -> `Cache-Control : no-cache`

다만 `Status Code`는 200번대 의미, 300번대 의미, 400번대 의미, 500번대 의미를 알아두는게 좋다.  
201 302 405 502는 몰라도 2xx, 3xx, 4xx, 5xx는 반드시 알아둬야 한다.
