# REST API

RESTful한 API를 말한다. <br />
일련의 특징과 규칙 등을 지키는 API를 일컫는 말이다.

## 특징

### Uniform-Interface

API에서 자원들은 각각의 독립적인 인터페이스를 가진다. <br />
각각의 자원들이 `url 자원 식별`, `표현을 통한 자원 조작`, `Self-descriptive messages`, `HATEOAS` 구조를 가진다. <br />
독립적인 인터페이스라는 건, 서로 종속적이지 않은 인터페이스를 말한다. <br />
예를 들어, 웹 페이지를 변경했다고 해서 웹 브라우저를 업데이트하는 일이 없다.<br />
HTTP 명세가 변경되어도 웹 페이지는 잘 작동해야 하듯이 말이다.

**url 자원 식별** <br />
identification of resources를 말한다. <br />
자원은 url로 식별되어야 한다.

**표현을 통한 자원 조작** <br />
manipulation of resources through representations라고 한다. <br />
url과 `GET`, `DELETE` 등 HTTP 표준 메서드 등을 통해 자원을 조회, 삭제 등 작업을 설명할 수 있는 정보가 담겨야 한다.

**Self-descriptive messages** <br />
HTTP Header에 타입을 명시하고, 각 메시지들은 MIME types에 맞춰 표현되어야 한다. <br />
예를 들어, json을 반환한다면, `application/json`으로 명시해야 한다. <br />
MIME types는 문서, 파일 등의 특성과 형식을 나타내는 표준이다. <br />
IETF의 RFC 6838에 정의 및 표준화되어 있다. <br />
`font/ttf`, `text/plain` 등을 말한다.

**HATEOAS 구조** <br />
하이퍼 링크에 따라 다른 페이지를 보여줘야 하며, 데이터마다 어떤 URL에서 원했는지 명시해줘야 하는 것을 말한다. <br />
보통은 `href`, `links`, `link`, `url` 속성 중 하나에 해당 데이터의 URL을 담아서 표기해야 한다. <br />
`_links` 속성에 담기도 한다. 링크를 유추할 수 있는 변수명을 쓰면 된다.

### Stateless

이 규칙은 HTTP 자체가 Stateless 이기 때문에, HTTP를 이용하는 것만으로도 만족된다. <br />
그리고 이는 REST API를 제공해주는 서버는 세션을 해당 서버 쪽에 유지하지 않는다는 의미다.

### Cacheable

HTTP는 원래 캐싱이 된다. <br />
아무런 로직을 구현하지 않더라도 자동적으로 캐싱이 된다. <br />
새로고침을 하면, 304가 뜨면서 원래 있던 js와 css 이미지 등을 불러온다.

이는 HTTP 메서드 중 `GET`에 한정되며, `Cache-Control:max-age=100`이런 식으로 한정된 시간을 정할 수 있다. <br />
캐싱된 데이터가 유효한지를 판단하기 위해 `Last-modified`와 `Etag`라는 헤더값을 쓴다. <br />
`Etag`는 전달되는 값에 태그를 붙여, 캐싱되는 자원인지를 확인해주는 것이다.

`Cache-control=no-store`로 하게 되면 캐싱이 안된다.<br />
기본적으로 `Cache-control=public`이기에 캐싱이 되며, HTTP Header를 기반으로 캐싱 컨트롤을 하는 게 중요하다.

### Client-Server 구조

클라이언트와 서버가 서로 독립적인 구조를 가져야 한다. <br />
물론 이는 HTTP를 통해 가능한 구조다. <br />
서버에서 HTTP 표준만 지킨다면, 웹에서는 그에 따른 화면이 잘 나타나게 된다. <br />
서버는 그저 API를 제공하고, 그 API에 맞는 비즈니스 로직을 처리하면 된다. <br />
마찬가지로 클라이언트에서는 HTTP로 받는 로직만 잘 처리하면 된다.

### Layered System

계층 구조로 나눠져 있는 아키텍처를 뜻한다. <br />
WEB 기반 서비스를 하면 보통 이런 시스템을 구축한다.

---

## URL 규칙

자원을 표기하는 URI는 아래 6가지 규칙을 적용해야 한다.

1. 동작은 HTTP 메서드로만 하며, url에 해당 내용이 들어가면 안된다. <br />
   수정 = put, 삭제 = delete, 추가 = post, 조회 = get을 이용한다. <br />
   예를 들어, `books/delete/1` 이렇게 하면 안된다.

2. `.jpg`, `.png` 등 확장자는 표시하지 않는다.

3. 동사가 아닌 명사로만 표기해야 한다. <br />
   `유저가 책을 소유한다`는 것을 표현한다면, `유저/유저아이디/inclusion/책/책ID`로 표현한다. <br />
   `/getAllUsers` 식의 동사를 집어넣으면 안된다.

4. 계층적인 내용을 담고 있어야 한다. <br />
   `/집/아파트/전세` 이런 식으로 내려가야 한다.

5. 대문자가 아닌 소문자로만 쓰며, 너무 길면 언더바가 아니라 그냥 - 를 쓴다.

6. HTTP 응답 상태 코드를 적재적소에 활용한다.

적절히 쿼리 스트링을 혼재해서 써도 된다. <br />
검색, 페이지네이션, 정렬 등 매개 변수가 많거나 복잡하면, 쿼리 스트링을 쓰는 게 좋다.
