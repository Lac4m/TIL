# DNS란?

> DNS(Domain Name System)은 호스트의 도메인 이름을 호스트의 네트워크 주소로 바꾸거나 그 반대의 변환을 수행할 수 있도록 하기 위해 개발 된 것.

Domain Name(DN) examples: naver.com, google.com...

<br>

## DNS 작동원리

1. 웹 브라우저에 www.naver.com을 입력하면 먼저 Local DNS에 "www.naver.com"이라는 hostname에 대한 IP 주소를 질의하여 Local DNS에 없으면 다른 DNS name 서버 정보(Root DNS 정보)를 받음

> Root DNS는 인터넷의 DNS의 루트 존이다. 루트 존의 레코드의 요청에 직접 응답하고 적절한 최상위 도메인에 대해 권한이 있는 서버 목록을 반환함으로써 요청에 응답한다.

2. Root DNS 서버에 "www.naver.com" 질의

3. Root DNS 서버로부터 "com 도메인"을 관리하는 TLD(Top-Level Domain) 이름 서버(.com을 관리하는 서버) 정보 전달 받음

4. TLD에 "www.naver.com" 질의

5. TLD에서 "name.com" 관리하는 DNS 정보 전달

6. "naver.com" 도메인을 관리하는 DNS 서버에 "www.naver.com" 호스트네임에 대한 IP 주소 질의

7. Local DNS 서버에 "www.naver.com"에 대한 IP 주소 "222.122.195.6" 응답

8. Local DNS 서버는 "www.naver.com"에 대한 IP 주소를 캐싱하고 IP 주소 정보 전달

> Caching은 일시적인 특징이 있는 데이터 하위 집합을 저장하는 고속 데이터 스토리지 계층. 이후 해당 데이터에 대한 요청이 있을 경우 데이터의 기본 스토리지 위치에 엑세스할 때보다 더 빠르게 요청을 처리할 수 있다. 주기억장치와 CPU 사이에 위치.

> DomainName은 넓게는 네트워크 상에서 컴퓨터를 식별하는 호스트명, 좁은 의미에서는 도메인 레지스트리에서 등록된 이름. ex. naver.com

> HostName, NodeName은 서브도메인을 사용할때 각 서비스를 구분하기 위한 고유 이름. ex. mail.naver.com, comic.naver.com에서의 mail, comic

출처: https://velog.io/@goban/DNS%EC%99%80-%EC%9E%91%EB%8F%99%EC%9B%90%EB%A6%AC