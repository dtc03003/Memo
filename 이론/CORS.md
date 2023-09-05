# 📚 CORS

## 📕 CORS란?

![](https://velog.velcdn.com/images/dtc03003/post/927fab4c-c5dd-472a-90a3-feb49959a1a4/image.png)

> `CORS(Cross-Origin Resource Sharing)` 직역하면 `교차 출처 리소스 공유 정책`  
> 즉 출처가 다른 자원들을 공유한다는 뜻으로, 한 출처에 있는 자원에서 다른 출처에 있는 자원에 접근하도록 하는 개념

<br/>

### 📖 출처(Origin)란?

사이트를 접속할때 `URL`이라는 문자열을 통해 접근한다. 하나의 문자열 같아 보여도, 사실은 여러 개의 구성 요소로 이루어져있다.

![](https://velog.velcdn.com/images/dtc03003/post/3842c1e7-3b42-47b9-a341-dd63b7c6d134/image.png)

-   `Protocol` : http, https
-   `Host`: 사이트 도메인
-   `Port`: 포트 번호(생략 가능)
-   `Path`: 사이트 내부 경로
-   `Query string` : 요청의 key와 value값
-   `Fragment` : 해시태그

이 중 `출처(Origin)`는 URL의 `프로토콜`, `호스트`, `포트` 이 3가지로 정의 된다.  
즉 어떤 URL이 같은 출처인지를 판단하려면 URL의 `프로토콜`, `호스트`, `포트`가 모두 같은지 확인하면 된다.

<br/>

### 📖 SOP(Same-Origin-Policy)란?

CORS를 알아보기 전에 그 배경이 되는 `SOP`에 대해 먼저 알아볼 필요가 있다.  
`SOP`는 "동일한 출처 사이에서만 리소스를 공유할 수 있다는 규칙"을 가지고 있다.

![](https://velog.velcdn.com/images/dtc03003/post/bb0bcce2-3d73-448e-8191-9a6aed3ab31d/image.png)

모든 처리가 같은 도메인 내에서 일어난다는 것 이다. 따라서 애초에 브라우저에서 다른 오리진으로 요청을 보낼 필요가 없었다. Ajax 를 통해 제한적으로 보낸다 하더라도, 같은 도메인 내에서 호출하므로 큰 문제가 없었다.

오히려 그 당시에는 다른 출처로 요청을 보내는 것을 악의적인 행위(CSRF, XSS 등)로 간주하는 것이 자연스러웠고, 따라서 출처가 다른 곳으로 요청하는 것 자체를 브라우저 차원에서 막았던 것 이었다. 하지만 시대의 흐름에 따라 웹 기술로 할 수 있는 것들이 많아졌고, 자연스럽게 다른 출처로 요청을 하고 응답을 받아오는 수요가 증가했다.

-   CSRF - 사용자가 자신의 의지와는 무관하게 공격자가 의도한 행위를 특정 웹사이트에 요청하게 하는 공격

<br/>

### 📖 CORS(Cross-Origin Resource Sharing)

이처럼 `교차 출처 리소스 공유(Cross-Origin Resource Sharing)`는 단어 그대로 다른 출처의 리소스 공유에 대한 허용/비허용 정책이다.

보안이 중요하지만 개발을 하다 보면 기능상 어쩔 수 없이 다른 출처 간의 상호작용을 해야 하는 케이스도 있다. 따라서 이와 같은 예외 사항을 두기 위해 CORS 정책을 허용하는 리소스에 한해 다른 출처라도 받아들인다는 것이다.

<br/>

---

<br/>

## 📕 CORS 기본 동작 살펴보기

1. 클라이언트에서 HTTP요청의 헤더에 Origin을 담아 전달
    - 기본적으로 웹은 HTTP 프로토콜을 이용하여 서버에 요청을 보내게 되는데,
    - 이때 브라우저는 요청 헤더에 Origin 이라는 필드에 출처를 함께 담아 보내게 된다.

![](https://velog.velcdn.com/images/dtc03003/post/999d63aa-7e0b-4070-9c00-0632a180c8cd/image.png)

2. 서버는 응답헤더에 `Access-Control-Allow-Origin`을 담아 클라이언트로 전달한다.
    - 이후 서버가 이 요청에 대한 응답을 할 때 응답 헤더에 `Access-Control-Allow-Origin`이라는 필드를 추가하고 값으로 `이 리소스를 접근하는 것이 허용된 출처 URL`을 보낸다.

![](https://velog.velcdn.com/images/dtc03003/post/8e0b9ffd-84b1-437f-80a6-34dbe37bcc48/image.png)

3. 클라이언트에서 Origin과 서버가 보내준 `Access-Control_Allow-Origin`을 비교한다.
    - 이후 응답을 받은 브라우저는 자신이 보냈던 요청의 Origin과 서버가 보내준 응답의 `Access-Control_Allow-Origin`을 비교해본 후 차단할지 말지를 결정
    - 만약 유효하지 않다면 그 응답을 사용하지 않고 버린다. (이때 CORS에러가 발생한다.)
    - 위와 같이 둘다 http://localhost:3000이기 때문에 다른출처의 리소스를 문제없이 가져온다.

<br/>

### 📖 CORS 해결책은 서버의 허용이 필요

-   서버에서 `Access-Control_Allow-Origin` 헤더에 허용할 출처를 기재해서 클라이언트에 응답하면 되는 것이다.

<br/>

---

<br/>

## 📕 CORS를 해결하는 방법

### 📖 Chrome 확장 프로그램 이용

Chrome에서는 CORS 문제를 해결하기 위한 [확장 프로그램]을 제공한다.

![](https://velog.velcdn.com/images/dtc03003/post/c60c22c4-a3d0-4a9d-8c69-ac5553e2d781/image.png)

브라우저 오른쪽 상단에서 확장 프로그램을 활성화 시킬 수 있다. 해당 프로그램을 활성화 시키게 되면, 로컬(localhost) 환경에서 API를 테스트 시, CORS 문제를 해결할 수 있다

<br/>

### 📖 프록시 사이트 이용하기

프록시(Proxy)란 클라이언트와 서버 사이의 중계 대리점

즉, 프론트에서 직접 서버에 리소스를 요청을 했더니 서버에서 따로 설정을 안해줘서 CORS 에러가 뜬다면, 모든 출처를 허용한 서버 대리점을 통해 요청을 하면 되는 것이다

![](https://velog.velcdn.com/images/dtc03003/post/774e5a3b-c38f-4bb8-969b-e556eb211d2e/image.png)

다만 현재 무료 프록시 서버 대여 서비스들은 모두 악용 사례 때문에 api 요청 횟수 제한을 두어 실전에서는 사용하기 무리이다. 따라서 테스트용이나 맛보기용으로 사용하되, 실전에서는 직접 프록시 서버를 구축하여 사용하여야 한다.

[heroku 프록시 서버]  
[cors proxy app 프록시 서버]  
[cors.sh 프록시 서버]

<br/>

### 📖 서버에서 Access-Control_Allow-Origin 헤더 세팅하기

직접 서버에서 HTTP헤더 설정을 통해 출처를 허용하게 설정하는 가장 정석적인 해결책

서버의 종류도 여러가지가 있으며 이를 참고할 [사이트]를 링크한다.

<br/>

---

<br/>

## 📕 출처

> https://inpa.tistory.com/entry/WEB-%F0%9F%93%9A-CORS-%F0%9F%92%AF-%EC%A0%95%EB%A6%AC-%ED%95%B4%EA%B2%B0-%EB%B0%A9%EB%B2%95-%F0%9F%91%8F#%F0%9F%93%9C_%EB%8F%99%EC%9D%BC_%EC%B6%9C%EC%B2%98_%EC%A0%95%EC%B1%85%EC%9D%B4_%ED%95%84%EC%9A%94%ED%95%9C_%EC%9D%B4%EC%9C%A0  
> https://evan-moon.github.io/2020/05/21/about-cors/  
> https://escapefromcoding.tistory.com/724

[확장 프로그램 ]: https://inpa.tistory.com/entry/WEB-%F0%9F%93%9A-CORS-%F0%9F%92%AF-%EC%A0%95%EB%A6%AC-%ED%95%B4%EA%B2%B0-%EB%B0%A9%EB%B2%95-%F0%9F%91%8F#%F0%9F%93%9C_%EB%8F%99%EC%9D%BC_%EC%B6%9C%EC%B2%98_%EC%A0%95%EC%B1%85%EC%9D%B4_%ED%95%84%EC%9A%94%ED%95%9C_%EC%9D%B4%EC%9C%A0
[heroku 프록시 서버]: http://cors-anywhere.herokuapp.com/corsdemo
[cors proxy app 프록시 서버]: https://github.com/raravel/cors-proxy
[cors.sh 프록시 서버]: https://cors.sh/
[사이트]: https://inpa.tistory.com/entry/WEB-%F0%9F%93%9A-CORS-%F0%9F%92%AF-%EC%A0%95%EB%A6%AC-%ED%95%B4%EA%B2%B0-%EB%B0%A9%EB%B2%95-%F0%9F%91%8F#3._%EC%84%9C%EB%B2%84%EC%97%90%EC%84%9C_access-control-allow-origin_%ED%97%A4%EB%8D%94_%EC%84%B8%ED%8C%85%ED%95%98%EA%B8%B0
