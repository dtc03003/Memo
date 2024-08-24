매번 CRA(Create React App)을 사용해서 React를 생성해왔지만 Vite가 최신 기술을 기반으로 하여 매우 빠르다는 얘기를 듣고 찾아보았다.

![](https://velog.velcdn.com/images/dtc03003/post/5c98fd07-0c79-411c-a916-4cbb4412fd06/image.gif)

# 📚 vite란?

> Vite(비트)는 프랑스어로 `빠르다`라는 뜻을 가진 단어로, 차세대 프론트엔드 개발도구이다. 빠르고 간결한 모던 웹 프로젝트 개발 경험에 초점을 맞춰 탄생한 빌드 도구

<br/>

---

<br/>

## 📕 Vite를 사용해야하는 이유

<br/>

### 📖 Native ESM

Vite의 가장 큰 특징은 `Native ESM`을 사용한다.

> `ESM`이란?

- 자바스크립트에서 `모듈화`를 지원하는 표준화된 시스템, ES6부터 도입되었다.

Webpack과 같은 전통적인 번들 기반 방식에서는 모든 소스 코드를 분석하고 이를 하나 또는 여러개의 번들 파일로 묶는 과정이 필요했다.
이 번들링 과정은 시간과 리소스를 소모하며 큰 프로젝트일 수록 이 과정이 오래걸렸다.

![](https://velog.velcdn.com/images/dtc03003/post/3a4e26b6-b66d-41b8-a60f-3cd33a801d42/image.png)

`Native ESM`을 사용하는 Vite는 이런 번들링 과정을 건너 뛴다.

소스 파일을 변경하지 않고 그대로 브라우저로 전달하며 브라우저는 이 파일들을 Native ESM 방식으로 직접 가져와 실행한다.

![](https://velog.velcdn.com/images/dtc03003/post/e6854005-3380-4fb6-a6f4-e5df996271c3/image.png)

<br/>

### 📖 모듈별 요청과 로딩

기존 방식에서는 첫 페이지 로드 시점에서 브라우저는 전체코드를 한 번에 다운로드를 했어야했지만

Vite에서는 브라우저는 필요한 파일을 개별적으로 요청한다.

예를 들어 `main.js`가 `app.js`와 `utill.js`를 import 한다면

브라우저는 `main.js`를 처음에 요청한 후 이 파일에 필요한 `app.js`와 `utill.js`를 추가로 요청한다.

이 과정은 브라우저가 모듈을 동적으로 로드하도록 허용하여 필요한 모듈만 즉시 로드하고 실행할 수 있게 해준다.

<br/>

### 📖 HMR

또한 `HMR`을 지원한다.

> HMR이란?

- 개발 도중 코드를 수정할 때 `수정된 부분만` 브라우저에 즉시 반영하여
  전체 페이지를 새로고침하지 않고도 변경 사항을 적용할 수 있게 해주는 기능

개발하면서 소스코드를 수정하면 vite는 수정된 모듈과 관련된 부분만 교체하고 브라우저에 전달한다.

Native ESM을 이용하기 때문에 프로젝트 사이즈가 크더라도 HMR 시간에 영향을 주지 않아서 매우 빠르게 진행이 된다.

<br/>

---

<br/>

## 📕 Vite 시작하기

```
npm create vite@latest
```

```
# npm 6.x
npm create vite@latest [프로젝트명] --template react-ts

# npm 7+,
npm create vite@latest [프로젝트명] -- --template react-ts
```

![](https://velog.velcdn.com/images/dtc03003/post/7bbcb5c1-c046-4251-b364-3141033ef22b/image.png)

와 TypeScript 설정만 해주면 생성 끝이다.

```
npm i

npm run dev
```

![](https://velog.velcdn.com/images/dtc03003/post/ec1d595a-8e39-4c4d-b99e-f4c7f50528e4/image.png)

![](https://velog.velcdn.com/images/dtc03003/post/66f52abe-8094-40e7-adbe-fb8f7cde83c4/image.png)

이제 Vite를 시작할 수 있게되었다.

<br/>

---

<br/>

## 📕 출처

> https://ko.vitejs.dev/
> https://analogcode.tistory.com/39
