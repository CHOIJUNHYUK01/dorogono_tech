# HTTP DEEP DIVE

HTTP 요청이라는 기술은 1.0부터 시작해, 지금 3까지 많은 발전을 했다.

## HTTP/1.0

수명이 짧은 연결이라고 한다. <br />
HTTP 요청은 자체 요청에서 완료가 된다. <br />
각 HTTP 요청당 TCP 핸드셰이크가 발생되며, 기본적으로 한 연결당 하나의 요청만 처리한다. <br />
한 번 연결할 때마다 TCP 연결을 계속하니, RTT가 늘어나는 문제점이 있다.

이를 해결하기 위해 `HTTP/1.1`이 나온다.

## HTTP/1.1

HTTP/1.0의 단점을 보완한 프로토콜이다.

1. keep-alive default <br />
   매번 데이터를 요청할 때마다 TCP 요청을 하지 않는다. <br />
   한 번 연결을 해놓고, 계속 데이터를 받을 수 있게 만들었다. <br />
   `keep-alive` 옵션을 기본 옵션으로 하면서 가능해졌다.

   `keep-alive header` <br />
   TCP 연결을 유지하는 것을 알려주는 헤더다. <br />
   연결 유지 시간인 `timeout`과 최대 요청 수, `max`를 정할 수 있다. <br />
   참고로 Node.js에서는 `timeout` 시간만 지정할 수 있다.

2. 호스트 헤더 <br />
   HTTP/1.0은 서버가 하나의 호스트만 가진다고 가정한다. <br />
   그래서 헤더에 호스트를 포함하지 않는다. <br />
   이 때문에 HTTP/1.0은 하나의 IP에 하나의 호스트만 가질 수 있었다.

   그러나 사실 서버는 여러 호스트를 가질 수 있다. <br />
   이런 유연성을 위해 HTTP/1.1은 헤더에 특정 호스트를 포함할 수 있게 변경했다. <br />
   항상 호스트를 포함해서 요청하도록 바꼈다.

3. 대역폭 최적화 <br />
   HTTP/1.0의 경우, 어떤 파일을 다운로드 받다가 연결이 끊기면 다시 다운로드가 불가능했다. <br />
   이를 다시 다운로드 받을 수 있게 바꼈다.

   예를 들어, HTTP/1.0에서는 10KB 파일을 다운로드 받는다고 해보자. <br />
   이때 5KB까지만 받고, 다시 다운로드가 불가능했다. <br />
   이를 HTTP/1.1에서는 `Range:bytes=5000-`라는 헤더를 추가해서 다운로드 재개 요청을 할 수 있게 바꼈다.

---

## 요청을 줄이기 위한 기술

HTTP/1.1로 발전했음에도 서버 요청을 할 때마다 RTT는 계속 증가한다. <br />
그래서 이 요청을 줄이기 위한 여러 기술이 있다.

대표적으로 이미지 스프라이트, 코드 압축, Base64 인코딩 기술을 같이 쓰게 됐다. <br />
참고로 HTTP 버전이 올라간 뒤에도 이러한 기술들을 같이 쓴다.

### 이미지 스프라이트

수많은 이미지를 하나의 이미지로 만든다. <br />
하나의 이미지만 다운받아놓고, 이를 통해 수많은 이미지를 다운받는 듯한 효과를 낸다.

### 코드 압축

코드를 압축해서 서빙한다.

### 이미지 Base64 인코딩

이미지 파일을 64진법으로 이뤄진 문자열로 인코딩해서 이미지 서버에 대한 HTTP 요청을 할 필요가 없이 만드는 것이다. <br />
하지만 Base64 인코딩을 할 경우, 파일 크기가 37퍼센트 크기가 더 커지는 단점이 있다.

### HTTP/1.1의 고질적인 문제 : HOL

위의 시도들을 시도해도, `HOL`과 무거운 헤더를 가지는 문제점이 있었고, 이를 해결하지 못했다.

- HOL : Head Of Line Blicking <br />
  네트워크에서 같은 큐에 있는 패킷이 그 첫번째 패킷에 의해 지연될 때 발생하는 성능저하 현상

---

## HTTP/2

구글이 HTTP/1.1의 한계를 극복하기 위해 SPDY 프로토콜을 개발했다. <br />
이후 이를 기반으로 HTTP/2 프로토콜을 만들었다.

### 바이너리 포맷 계층

애플리케이션 계층과 전송 계층 사이에 바이너리 포맷 계층을 추가한다. <br />
HTTP/1.0은 일반 텍스트 메시지를 전송하고, 줄바꿈으로 데이터를 나눴다. <br />
HTTP/2는 0과 1로 이뤄진 바이너리 데이터로 변경해서 더 작은 메시지가 프레임으로 캡슐화되어 전송된다.

HTTP/2는 TLS를 선택적으로 쓸 수 있다. 즉, TLS가 없는 HTTP/2도 있다. <br />

- h2c는 TLS를 사용하지 않고, TCP 연결 위에서 직접 HTTP/2를 사용하는 것을 의미한다. <br />
  개발 환겨에서의 디버깅이나 로컬 테스트를 위해 암호화된 연결을 설정할 필요가 없으므로, <br />
  개발자들이 편리하게 테스트를 할 수 있고, 암호화에 관련된 오버헤드가 없다는 장점이 있다.

- h2는 TLS가 장착된 HTTP/2를 부른다. <br />
  브라우저에서는 HTTPS가 없는 HTTP/2는 지원하지 않기 때문에 브라우저에서는 h2만 허용된다.

### 멀티플렉싱

단일 TCP 연결의 여러 스트림에서 여러 HTTP 요청과 응답을 비동기적으로 보낼 수 있다. <br />
이를 통해 HOL을 해결한다.

HTTP/1.1에서는 병렬 요청을 하려면, 다중 TCP 연결을 통해 하고, 일반적으로는 TCP 연결 하나당 병렬 요청은 불가능했다. <br />
이를 HTTP/2에서 리소스를 작은 프레임으로 나누고, 스트림으로 프레임을 전달한다. <br />
각각의 프레임은 스트림 ID, 해당 청크의 크기를 나타내는 프레임이 추가됐다. <br />
그래서 작게 나눠 다운로드가 되더라도, 결과적으로 응답 데이터에서는 올바른 순서로 재조립할 수 있게 된다.

### 서버 푸시

서버가 리소스를 클라이언트에 푸시할 수 있다. <br />
요청된 html 파일과 함께 다른 개체를 별도로 보낼 수 있다. <br />
만약 요청한 html에 css가 포함되어있다면, 별도 요청없이 같이 보낼 수 있다.

### 헤더 압축

HTTP/1.1에서는 무거운 헤더가 있었지만, 이를 허프만 인코딩 압축 방법 등으로 압축했다. <br />
똑같은 서버에서 2개의 이미지를 준다고 했을 때, 중복되는 헤더는 제외하고 보낸다. <br />
그리고 공통 필드로 헤더를 재구성해서 중복되지 않는 헤더값만 허프만 인코딩 압축 방법으로 압축하고 전송한다.

- 허프만 인코딩 <br />
  문자열을 문자 단위로 쪼개 빈도수를 세어 빈도가 높은 정보는 적은 비트수를 사용해 표현한다. <br />
  빈도가 낮은 정보는 비트 수를 많이 사용해 전체 데이터 표현에 필요한 비트양을 줄이는 알고리즘이다.

### 우선 순위

서버에서 원하는 순서대로 우선 순위를 정해 리소스를 전달한다.

---

## HTTP/3

HTTP/2는 여전히 TCP를 사용하기에, 초기 연결에 대한 RTT로 인한 지연시간 문제가 있었다. <br />
이를 해결한 버전이다.

QUIC(Quick UDP Internet Connections)라는 계층 위에서 돌아간다. <br />
TCP 기반이 아닌, UDP 기반으로 돌아간다. <br />
HTTP/2에서 장점이었던 멀티플랙싱 등을 갖고 있고, 초기 연결 설정 시에 지연 시간 감소라는 특성을 지닌다.

HTTP/2의 경우, 3-RTT가 필요했다면, QUIC은 1-RTT만 필요하다는 장점이 있다. <br />
HTTP/2는 클라이언트와 서버 간의 연결을 맺어 세션을 만드는데 필요한 핸드 셰이크, 암호화 통신을 구축하기 위한 TLS 핸드셰이크가 각각 필요했다. <br />
그러나 HTTP/3는 TLS로 암호화 통신을 구축할 때 사용한 단 한 번의 핸드셰이크를 활용해 클라이언트와 서버간의 연결, 암호화 통신 등 모두 다 구축한다. <br />
이를 통해 1-RTT만에 모든 연결을 성립할 수 있다.

전송된 패킷이 손실됐다면, 수신 측에서 에러를 검출하고 수정하는 방식이다. <br />
열악한 네트워크 환경에서도 낮은 패킷 손실률을 자랑하는 순방향 오류 수정 매커니즘(FEC, Forward Error Correction) 특징을 가진다.
