# CORS

`cross origin resource sharing`이다. <br />
HTTP 헤더를 기반으로 브라우저가 다른 오리진에 대한 리소스 로드를 허용할지 말지에 대한 매커니즘이다.

## 오리진

https://site.com:8080 <br />

> https = protocol <br />
> site.com = hostname <br />
> 8080 = port <br />
> hostname + port = host <br />
> protocol + host = origin

## SOP

Same-Origin Policy는 브라우저 상에서 오로지 같은 오리진끼리만 요청을 허가한다. <br />
이게 없다면, 악의적인 사이트를 방문했을 때, 내 개인 정보가 변경되거나 유출될 수 있다. <br />
즉, 악성 스크립트가 다른 오리진 서버에 요청을 보내고, 사용자의 리소스를 임의적으로 접근하는 걸 1차적으로 막아준다는 것이다.

다른 오리진끼리 요청해야 하는 순간도 있다. <br />
서비스를 만들 때, 보통 사용하는 OPEN API 등이 그 예시다. <br />
SOP을 브라우저 상에서 조금 더 유연하게 바꿔서 어떤 경우에는 다른 오리진끼리도 요청하고 응답할 수 있게 만든 매커니즘이 CORS다.

---

## preflight request와 simple request

만약 요청을 보낼 때, 다음의 메서드 타입과 헤더에 해당되지 않은 게 하나라도 포함되어 있다면, `preflight request`를 보내게 된다. <br />
반대로 다음의 메서드 타입과 헤더를 모두 가진 요청을 `simple request`라 한다.

### preflight request 과정

1. OPTIONS 메서드로 해당 서버에 원래의 요청을 보내기 전 요청을 보낸다. <br />
2. 요청을 받은 서버는 `Access-Control-*` 헤더로 응답한다. <br />
3. `Access-Control-*` 헤더에 요청한 오리진이 존재하지 않는다면, `CORS 에러`를 보낸다.

> Access-Control-Allow-Headers: Content-Type (허용된 헤더) <br />
> Access-Control-Allow-Origin: https://kundol.com (오리진 확인)<br />
> Access-Control-Allow-Methods: GET, DELETE, HEAD, OPTIONS (허용된 메서드) <br />
> Access-Control-Allow-Credentials: true || false (인증관련 헤더) <br />
> 이외에도 Access-Control-Max-Age 등이 있다.
