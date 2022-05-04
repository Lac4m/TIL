# HTTP란?

## HTTP란?

HyperText Transfer Protocol의 약자로, 하이퍼텍스트 문서를 교환하기 위하여 사용된 TP. 웹 서버와 클라이언트 간의 통신을 위함. 웹에서만 사용하는 protocol으로 TCP/IP 기반으로 한 지점에서 다른 지점 (서버/클라이언트)로 요청과 응답을 전송한다.

<br> 

## HTTP의 특징

- HTTP 메세지는 HTTP 서버와 HTTP 클라이언트에 의해 해석된다
- TCP/IP를 이용하는 application protocol
- HTTP는 연결 상태를 유지하지 않는 비연결성 protocol (complemented by cookie and session)
- HTTP는 연결을 유지하지 않는 protocol이므로 request/response로 동작

client가 어떠한 서비스를 url 또는 다른 것을 통해 request 하면 서버에서는 요청사항에 따른 결과를 response

- request: client -> server
- response: server -> client

HTML 문서 뿐만 아니라 Plain text, JSON data, XML 등의 정보도 주고 받을 수 있으며, client가 보통 정보 형태를 명시.

