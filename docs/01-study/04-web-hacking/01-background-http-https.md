---
layout: default
title: Background HTTP/HTTPS
parent: Web Hacking
grand_parent: Study
nav_order: 1
mathjax: true
mermaid: true
permalink: /docs/web-hacking/01
---

# Background: HTTP/HTTPS
{: .no_toc }

<details markdown="block">
  <summary>
	Table of contents
  </summary>
{: .fs-3 .text-delta }
- TOC
{:toc}
</details>

---

## 1. 들어가며

### 인코딩

- 컴퓨터의 모든 데이터는 0과 1로 구성된다.

- 인코딩(Encoding): 문자나 기호를 0과 1로 만드는 것

##### 인코딩 표준 종류

- 아스키(Ascii)

	- 7-bit 데이터에 대한 인코딩 표준

	- 알파벳, 특수 문자 등을 표현할 수 있다.

- 유니코드(Unicode)

	- 32-bit 데이터에 대한 인코딩 표준

	- $2^{32}$, 약 42억 개의 정보를 표현할 수 있다.

	- 모든 언어의 문자를 Uni, 하나의 표준으로 인코딩한다.

##### 인코딩 역할

- 인코딩을 이용하면 일상 정보를 컴퓨터에 저장하고 표현할 수 있다.

- 네트워크를 이용하면 인코딩한 정보를 쉽게 교환할 수 있다.

### 통신 프로토콜

- 요청(Request): 클라이언트가 웹에게 특정 리소스를 지정하여 제공해달라고 요청하는 것

- 응답(Response): 요청를 이해하고 대응되는 동작을 통해 클라이언트에게 리소스를 반환하는 것

- 프로토콜(Protocol): 규격화된 상호작용에 적용되는 약속

- 컴퓨터 통신 프로토콜은 각 통신 주체가 교환하는 데이터를 명확히 해석할 수 있도록 문법(syntax)를 포함한다.

	- 문법에 어긋나는메시지는 잘못 전송된 것으로 취급하여 무시된다.

##### 표준 통신 프로토콜

- TCP/IP: 네트워크 통신의 기초

- HTTP: 웹 애플리케이션이 사용

- FTP: 파일 전송에 사용

## 2. HTTP

### HTTP

- HTTP(Hyper Text Transfer Protocol): 서버와 클라이언트의 데이터 교환을 요청(Request)과 응답(Response) 형식으로 정의한 프로토콜

	- 팀 버너스 리(Team Berners-Lee)와 그의 팀이 제정한 이후, 현대 웹 서비스의 바탕이 되는 프로토콜로 자리 잡았다.

##### HTTP의 기본 메커니즘

- HTTP의 기본 메커니즘은 클라이언트가 서버에게 요청하면, 서버가 응답하는 것이다.

- 웹 서버는 HTTP 서버를 HTTP 서비스 포트에 대기시킨다.

	- 이 포트는 일반적으로 TCP/80 또는 TCP/8080이다.

- 클라이언트가 서비스 포트에 HTTP 요청을 전송하면, 이를 해석하여 적절한 응답을 반환한다.

##### Request example

```
Get /index.html HTTP/1.1
Host: dreamhack.io
Connection: keep-alive
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.88 Safari/537.36
```

- `GET`: HTTP Method

- `/index.html`: Request URL

- `HTTP/1.1`: HTTP Version

- `Host: dreamhack.io ...`: Request Header

##### Response example

```
HTTP/1.1 200 OK
Server: Apache/2.4.29 (Ubuntu)
Content-Length: 61
Connection: Keep-Alive
Content-Type: text/html

<!doctype html>
<html>
<head>
</head>
<body>
</body>
</html>
```

- `HTTP/1.1`: HTTP Version

- `200 OK`: Return Code

- `Server: Apache/2.4.29 (Ubuntu) ...`: Response Header

- `<!doctype html> ...`: Response Body

##### 네트워크 포트와 서비스 포트

- 네트워크 포트(Network Port): 네트워크에서 서버와 클라이언트가 정보를 교환하는 추상화된 장소

	- 네트워크를 설명하는 맥락에서는 편의상 네트워크를 생략하고 포트라고 부르기도 한다.

- 서비스 포트(Service Port): 네트워크 포트 중에서 특정 서비스가 점유하고 있는 포트

	- ex) HTTP가 80번 포트를 점유하고 있다면 HTTP의 서비스 포트는 80번 포트이다.

- 전송 계층(Transport Layer)

	- 포트로 데이터를 교환하는 방식은 전송 계층(Transport Layer)의 프로토콜을 따른다.

	- ex) TCP, UDP

		- TCP로 데이터를 전송하려는 서비스에 UDP 클라이언트가 접근하면, 데이터가 교환되지 않는다. 반대도 마찬가지.

		- 그래서 서비스 포트를 표기할 때 서비스가 사용하는 전송 계층 프로토콜을 같지 표기하기도 한다.

- 포트의 개수는 운영체제에서 정의하기 나름이나, 현대의 윈도우나 리눅스, 맥 운영체제는 0번부터 65535번까지, 총 65536개의 같은 수의 네트워크 포트를 사용한다.

- 포트 중 0번부터 1023번 포트는 잘 알려진 포트(Well-known port) 또는 특권 포트(Privileged port)라고 한다.

	- 각 포트 번호에 유명한 서비스가 등록되어 있다.

	- 22번 포트에는 SSH, 80에는 HTTP, 443에는 HTTPS가 할당되어 있다.

	- 잘 알려진 포트에 서비스를 실행하려면 관리자 권한이 필요하다.

	- 따라서 클라이언트는 이 대역에서 실행 중인 서비스들은 관리자의 것이라고 신뢰할 수 있다.

### HTTP 메시지

- HTTP 메시지에는 클라이언트가 전송하는 HTTP 요청, 서버가 반환하는 HTTP 응답이 있다.

- HTTP 요청과 응답은 기능과 세부 구조에서는 차이가 있지만, 크게 보면 이들은 HTTP 헤드와 바디로 구성된다는 공통점이 있다.

##### HTTP 헤드

- 각 줄은 CRLF로 구분되며, 첫 줄은 시작 줄(Start-line), 나머지 줄은 헤더(Header)라고 부른다. 헤더의 끝은 CRLF 한 줄로 나타낸다.

- 시작 줄의 역할은 요청과 응답에서 차이가 있다.

- 헤더는 필드와 값으로 구성되며 HTTP 메시지 또는 바디의 속성을 나타낸다.

- 하나의 HTTP 메시지에는 0개 이상의 헤더가 있을 수 있다.

##### HTTP 바디

- 헤드의 끝을 나타내는 CRLF 뒤, 모든 줄을 말한다.

- 클라이언트나 서버에게 전송하려는 데이터가 바디에 담긴다.

<center markdown="block">
![http-message](/assets/web-hacking/2-1-http-message.png)

HTTP 메시지 구조
</center>

### HTTP 요청

- HTTP 요청: 서버에게 특정 동작을 요구하는 메시지

- 서버는 해당 동작이 실현 가능한지, 클라이언트가 그러한 동작을 요청한 권한이 있는지 등을 검토하고, 적절한 때만 이를 처리한다.

##### 시작 줄

- HTTP 요청의 시작 줄은 메소드(Method), 요청 URI(Request-URI), HTTP 버전으로 구성된다.

	- 각각은 띄어쓰기로 구분한다.

- 메소드(Method): URI가 가리키는 리소스를 대상으로, 서버가 수행하길 바라는 동작을 나타낸다.

- 요청 URI: 메소드의 대상

- HTTP 버전: 클라이언트가 사용하는 HTTP 프로토콜 버전

> [표준 문서](https://www.w3.org/Protocols/rfc2616/rfc2616-sec5.html)

##### HTTP Method

> [참고](http://www.ktword.co.kr/test/view/view.php?no=3791)

- HTTP 표준에 정의된 메소드는 9가지가 있다.

1. `GET`: 리소스 취득

	- URL(URI) 형식으로 웹서버의 리소스를 요청한다.

2. `HEAD`: 메시지 헤더(문서 정보) 취득

	- GET과 비슷하나, 실제 문서를 요청하는 것이 아니라, 문서 정보를 요청한다.

3. `POST`: 내용 전송 (파일 전송도 가능)

	- 클라이언트에서 서버로 정보를 전송한다.

		- 요청 데이터를 HTTP 바디에 담아 웹서버로 전송한다.

	- 이때, 요청 데이터의 HTTP 헤더에 아래와 같이 설정한다.

		```
		Conten-Type:application/x-www-form-urlencoded
		```

		- 이는 해당 개체가 폼으로 전송하는 데이터 임을 알리는 HTTP 헤더 형식이다.

	- 만일 요청된 리소스가 새롭게 작성된 또다른 것이라면, 서버는 HTTP 헤더 항목 중 `Location:`에 새롭게 작성된 리소스에 대한 URL 정보를 포함시켜 응답하게 된다.

4. `PUT`: 내용 갱신 위주 (파일 전송도 가능)

	- POST처럼 정보를 서버로 전송하는 것으로 형식을 동일하지만, 갱신 위주이다.

		- 갱신된 리소스에 대한 주소 정보를 보내지 않아도 됨다. 서버측은 클라이언트 측이 제시한 URI를 그대로 사용하는 것으로 간주한다.

	- PUT은 클라이언트측이 서버측 구현에 관여하는 것이므로, 통상 보다 세밀한 POST를 더 많이 쓴다.

5. `DELETE`: 파일 삭제

	- 웹 리소스를 제거한다.

6. `OPTIONS`: 웹 서버측 제공 메서드에 대한 질의

	- 가능한 메소드 옵션에 대해 질의한다.

		- 이 경우 응답 메시지에 HTTP 헤더 항목 중 'Allow: GET, POST, HEAD`처럼 보내게 된다.

7. `TRACE`: (거의 사용 안함)

	- 요청 리소스가 수신되는 경로를 보여준다.

8. `CONNECT`: (거의 사용 안함)

	- 프록시 서버와 같은 중간 서버 경유한다.

- 보안상의 이유로 대부분의 웹서버가 GET, POST 2개 또는 OPTIONS 포함 3개만을 허용하는 경우가 일반적이다.

### HTTP 응답

- HTTP 응답: HTTP 요청에 대한 결과를 반환하는 메시지

- 요청을 수행했는지, 하지 않았는지, 안 했다면 이유는 무엇인지와 같은 상태 정보(Status), 그리고 클라이언트에게 전송할 리소스가 응답에 포함된다.

##### 시작 줄

- HTTP 응답의 시작 줄은 HTTP 버전, 상태 코드(Status Code), 처리 사유(Reason Phrase)로 구선된다.

	- 각각은 띄어쓰기로 구분된다.

- HTTP 버전: 서버에서 사용하는 HTTP 프로토콜의 버전을 나타낸다.

- 상태 코드: 요청에 대한 처리 결과를 세 자릿수로 나타낸다.

	- HTTP 표준인 RFC 2616은 대략 40여개의 상태 코드를 정의하고 있는데, 각각은 첫번째 자리수에 따라 5개의 클래스로 분류된다.

- 처리 사유: 상태 코드가 발생한 이유를 짧게 기술한 것

|상태 코드|설명|대표 예시|
|-|-|-|
|1xx|요청을 제대로 받았고, 처리가 진행 중임| |
|2xx|요청이 제대로 처리됨|- 200: 성공|
|3xx|요청을 처리하려면, 클라이언트가 추가 동작을 취해야 함.|- 302: 다른 URL로 갈 것|
|4xx|클라이언트가 잘못된 요청을 보내어 처리에 실패함|- 400: 요청이 문법에 맞지 않음<br> - 403: 클라이언트가 리소스에 요청할 권한이 없음<br>- 404: 리소스가 없음|
|5xx|클라이언트의 요청은 유효하지만, 서버에 에러가 발생하여 처리에 실패함|- 500: 요청을 처리하다가 에러가 발생함<br>- 503: 서버가 과부하로 인해 요청을 처리할 수 없음|

> [표준 문서](https://www.w3.org/Protocols/rfc2616/rfc2616-sec6.html)

## 3. HTTPS

### HTTPS

- HTTP의 응답과 요청은 평문으로 전달된다.

	- 중요한 정보가 유출될 수 있다.

- HTTPS(HTTP over Secure socket layer)는 TLS(Transport Layer Security) 프로토콜을 도입하여 HTTP의 문제점을 보완한다.

- TLS는 서버와 클라이언트 사이에 오가는 모든 HTTP 메시지를 암호화한다.

- 공격자가 중간에 메시지를 탈취하더라도 이를 해석하는 것은 불가능하며, 결과적으로 HTTP 통신이 도청과 변조로부터 보호된다.

- 현재 개발되는 서비스들은 규모에 상관없이 HTTPS를 사용하는 추세이다.

- 웹 서버의 URL이 `http://`로 시작되면 HTTP, `https://로 시작되면 HTTPS 프로토콜을 사용한다.

## 키워드

- HTTP(HyperText Transfer Protocol): 웹 서버와 클라이언트가 리소스를 교환하기 위해 사용하는 프로토콜. 클라이언트가 요청하면, 서버가 응답하는 방식

- HTTP 메시지: HTTP 서버와 클라이언트가 교환하는 데이터. 헤드와 바디로 구성되며 각 줄은 CRLF로 구분됨

	- 헤드: 메시지에 대한 정보. 헤드의 끝에는 CRLF가 한 줄 있음

	- 바디: 클라이언트가 서버에게, 또는 서버가 클라이언트에게 전달할 데이터

- HTTP 요청(Request): 클라이언트가 서버에게 특정 동작을 요청하는 메시지

	- 메소드(Method): 요청 URI가 가리키는 리소스에 대해, 서버가 수행했으면 하는 동작을 지정함

	- 요청 URI(Request-URI): 메소드의 대상이 되는 리소스를 지정

- HTTP 응답(Response): 요청을 처리한 결과 및 이유, 그리고 클라이언트에 전송할 웹 리소스를 포함하는 메시지

	- 상태 코드(Status Code): 요청을 처리한 결과

	- 처리 사유(Reason Phrase): 상태 코드가 발생한 이유

- HTTPS(HTTP on Secure socket layer): TLS를 이용하여 HTTP의 약점을 보완한 프로토콜

