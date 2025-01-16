# document load와 DOMContentLoaded 차이

### TL;DR

`DOMContentLoaded`는 HTML 파일이 완전히 로딩되고 파싱됐을 때를 의미한다. <br />
css, images, subframe까지 됐다는 의미는 아니다.

`load`는 css, images, subframe을 포함해 모든 의존적인 리소스가 로딩이 완료됐을 때 불린다.

```javascript
document.addEventListener("DOMContentLoaded", function () {
  console.log("DOM fully loaded and parsed");
});

window.addEventListener("load", function () {
  console.log("Page fully loaded");
});
```

## DOMContentLoaded

이 이벤트는 DOM이 준비됐을 때, JS를 실행하기를 원한다면 유용하다.

## load

이 이벤트는 슬라이드쇼 혹은 이미지 사이즈에 따른 layout 계산이 필요할 때 유용하다.

## 차이점

- Timing <br />
  `DOMContentLoaded`는 `load`보다 이른 시간에 불린다. <br />
  모든 리소스를 로딩하는 시간 차이가 존재하기 때문이다.

- Use Cases <br />
  `DOMContentLoaded`는 DOM을 조작하거나, eventListener를 적용할 때 사용된다. <br />
  `load`는 리소스에 따른 계산이 필요할 때 사용된다.
