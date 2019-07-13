## URI, URL, URN
> URI : Uniform Resources Identifier
> URN : Uniform Resources Name
> URL : Uniform Resources Location

### Resource

리소스. 자원이란 뜻이다. html 파일, 이미지 파일, 바이너리 파일 등 그야말로 자원을 의미한다. 

서로간에 의사 전달을 위해서는  **원하는 자원을 구체적으로 기술해야 한다**   


### URI

> Uniform Resource Identifier  
> 통합 자원 식별자

URI는 어떤 자원을 UNIQUE하게 구별하기 위한 주소다. 여기서 **UNIQUE** 하게 구분하는 방법이 **위치** 인지 **자원이름** 인지에 따라 URL과 URN으로 나뉜다.  
> 원하는 자원을 표시하는 방법이 `URI`이고, `URI`의 종류 중에 `URN`, `URL`이 있다.


### URN

> Uniform Resource Name
> 자원의 이름으로 식별

```
<URN> ::= "urn:" <NID> ":" <NSS>
```

URN은 위치에 상관없이 자원 그 자체로 식별하는 특징이 있다. 네이버에 있던 이미지가 다음으로 옮겨가도, URN은 **변하지 않는다**. 자원 스스로가 바뀌지 않으면 네이버에 위치하든, 다음에 위치하든 URN은 **같다**

이 장점 때문에 URN을 도입하기 위한 여러 시도가 있지만, 알다시피 URL로 이루어져 있어 이전이 쉽지 않다.

### URL

> Uniform Resource Location
> 자원의 위치로 식별

자원을 **위치** 로 식별하는 URI를 URL이라고 한다.  
PC의 파일 시스템처럼, 경로를 가진다. 
```
C://Users/our-generation/Document/SailerMoonOst.mp3

~/our-generation/Documents/SailerrMoonOst.mp3
```

어떤 자원의 **위치**가 변경되면 `URL`역시 바뀌어야 한다. 실수하기 쉬운 부분.  
보편적으로 쓰이는 `URI`이므로 `URI`와 같은 말로 쓰이기도 한다. `URN`으로 이전하기 위한 노력들이 있었지만, 오랜동안 쓰여왔기 때문에 전환이 쉽지 않다.

## URL 문법

```
<스킴> :// <사용자> : <비밀번호> @ <호스트> : <포트> / <경로> ; <파라미터> ? <질의> #. <프래그먼트>
```

**반드시** 순서를 지켜야 한다.

| 구분 |                                                                                                                        |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| 스킴                   | 어떤 프로토콜을 사용하는가? `http`, `https`,`ftp`, `rtsp`, `file` … 등등이 올 수 있다. 이어서 나오는 자원 정보가 어떤 프로토콜로 접근하는지 정의한다.                |
| 사용자 이름, 비밀번호         | 공용 자원이 아닌 경우, 몇몇 프로토콜은 계정과 비밀번호를 요구하기도 한다. 예)FTP                                                                       |
| 호스트                  | **서버** 를 뜻한다. naver.com, daum.net, google.com ...                                                                      |
| 포트                   | 서버에 접근하기 위한 포트를 정의한다. 잘 알려진 포트의 경우 생략할 수 있다. (브라우저가 스킴을 보고 자동으로 붙여준다) HTTP는 80, HTTPS는 443, FTP는 21, SFTP는 22 ...      |
| 경로                   | 호스트 내부에서 자원의 위치를 기술한다. 위에서 설명한 파일시스템과 유사한 방식이다. /baseball/kiwoom/1, /java/spring/starter ...                           |
| 파라미터                 | 자원을 정의하기 위한 키 / 밸류 조합. FTP에서는 바이너리, 텍스트 포맷이 있다. `type`파라미터가 i인 경우 바이너리를, a 인 경우 ASCII 포맷이다. `ftp://foo.org/bar;type=i` |
| 질의 (쿼리스트링)           | 자원의 형식을 구체화 하기 위해 질의를 포함할 수 있다. `naver.com/book/search?title=HTTP` 는 도서 리스트 중에서 `title`이 `HTTP` 인 것을 요청할 수 있다.         |
| 프래그먼트                | HTML 문서의 위치를 설명한다. #[TITLE]은 TITLE 섹션을 의미한다.                                                                           |



## 상대 URL

URL은 상대 URL과 절대 URL로 나눈다. 

절대 URL은 위에서 살펴본 URL 문법에 맞게 항목을 기술한 것을 말한다.
상대 URL은 URL의 일부만 기술한다. 스킴에서 포트까지를 `root` 또는 `base URL`이라고 하는데, 상대 URL은 `root` 이후 URL을 기술한다.  
> 참고)  
> `base URL`은 수동 설정할 수 있다. 예를들어 `our-generation.com/andole`은 `root`이 아니지만 `base`태그를 통해 `base URL`로 사용할 수 있다.  
> 아마도 `jekyll` 설정을 하면서 만나봤을 것이다...

```
// Absolute URL
https://github.com/andole87/some-repo

// Relative URL
// github.com에 접속
https://github.com

// github.com에 접속 중일 때
/some-repo
```



## URL 인코딩 체계

브라우저 주소창에 한글을 입력할 수 있다. 크롬의 경우 바로 구글 검색으로 넘어간다.  
하지만 `URL`에는 한글을 포함시킬 수 없다. 이스케이프된 16진수가 문자를 표현한다. 브라우저는 자동으로 디코딩해서 한글을 보여줄 뿐이다.

크롬 주소창에 "웹" 을 입력하고 엔터를 누른다. 주소창을 잘 보면

```
https://www.google.com/search?q=웹[...]
```

한글로 잘 표시될 것이다. 자, 이제 주소를 복사해서 메모장에 붙여넣어보자.

```
https://www.google.com/search?q=%EC%9B%B9&oq=%EC%9B%B9&aqs=chrome..69i57j0l3j69i61j0.610j0j9&sourceid=chrome&ie=UTF-8
```

`q=웹`이 `q=%EC%9B%B9`로 바뀐다.

URL은 US-ASCII 문자 집합으로만 표시할 수 있다. 그 외 알파벳 문자나 한글, 한자 등은 URL에서 표시할 수 없다. 이 때문에 이스케이프 문자로 다른 문자셋을 표시한다. 위에서 알 수 있듯이 유니코드 인코딩 이스케이프 문자는 `%`이다.

브라우저는 똑똑해서 이스케이프 문자를 자동 디코딩 해주지만, 실제 URL을 기술할 때는 영어 알파벳만 가능하다.

이처럼, URL에는 `들어갈 수 없는` 문자들이 있다. 

```
% / . .. # ? ; : $ , + @ & = {} | \ ~ [] ` <> "
```