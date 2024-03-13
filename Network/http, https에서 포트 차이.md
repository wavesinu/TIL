[http://naver.com](http://naver.com/)와 [https://naver.com](http://naver.com/)로 접속이 가능하나, 이 둘의 포트는 서로 다르다.

**HTTP(HyperText Transfer Protocol)**

- HTTP를 사용할 땐, **포트 80**을 사용한다.

**HTTPS(HyperText Transfer Protocol Secure)**

- HTTPS를 사용할 땐, **포트 443**을 사용한다.

즉, [http://naver.com](http://naver.com/)과 [https://naver.com](http://naver.com/)로 접속할 때는 포트가 각각 80과 443이므로 서로 다르다.

HTTPS는 SSL/TLS를 사용하여 통신 내용을 암호화하는 보안된 버전의 HTTP이기 때문에 서로 다른 포트를 사용한다.

>**확장된 관점에서의 HTTP와 HTTPS**
>
HTTP와 HTTPS의 가장 큰 차이점은 보안이다. HTTPS는 민감한 정보가 인터넷을 통해 전송될 때, 이를 암호화(대칭 키 암호화, 비대칭 키 암호화 등)하여 보호한다.
암호화를 통해 데이터가 전송되는 경로상에서 정보를 읽을 수 없도록 하기 때문에, 해커가 데이터를 가로채도 정보를 해독할 수 없다.