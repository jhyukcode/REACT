# React 프로젝트 구성 가이드

## 목차

1. [React 설치](#1-react-설치)  
2. [디자인 적용 - antd / 반응형 / 최적화](#2-디자인-적용---antd--반응형--최적화-렌더링)  
3. [Redux](#3-redux)  
4. [Saga](#4-saga)  
5. [기타 도구 - 스크롤링, Faker Dummy 등](#5-etc---스크롤링-faker-dummy)

---

## 1. React 설치

### 1-1. Node & NPM 확인

```bash
node -v
npm -v
```

```bash
mkdir front
cd front
```

### 1-2. React vs Vue

- React: 단방향 데이터 흐름
- Vue: 양방향 데이터 바인딩

### 1-3. Next.js 초기 설정

```bash
npm init
npm i next@13.4.13
npm i react@18.3.1 react-dom@18.3.1
```

`package.json` 예시:

```json
"author": "kjh",
"scripts": {
  "dev": "next"
}
```

서버 실행:

```bash
npm run dev
```

### 1-4. 기본 페이지 생성

```js
// pages/index.js
import React from "react";

const Home = () => {
  return <div>Hello, next</div>;
};
export default Home;
```

추가 페이지 예시:

- pages/profile.js → http://localhost:3000/profile  
- pages/signup.js → http://localhost:3000/signup

### 1-5. 크롬 확장 프로그램

- React Developer Tools  
- Redux DevTools

---

## 2. 디자인 적용 - antd / 반응형 / 최적화 렌더링

### 2-1. 프로젝트 구조

```
[front]
├── package.json
├── pages/
│   ├── index.js
│   ├── profile.js
│   └── signup.js
├── components/
├── hooks/
├── store/
├── reducers/
└── sagas/
```

### 2-2. AppLayout 컴포넌트 생성

```bash
npm i --save prop-types
```

### 2-3. Ant Design + styled-components + 아이콘

```bash
npm install --save antd@4
npm install --save styled-components@5
npm install --save @ant-design/icons@5
```

공식 사이트: https://4x.ant.design

### 2-4. 반응형 디자인

- 24 컬럼 그리드 시스템
- 디바이스별 크기: `xs`, `sm`, `md`
- `gutter` 속성: 컬럼 간 간격

```html
<a href="https://company.com" target="_blank" rel="noreferrer noopener">
  Company
</a>
```

- `noreferrer`: referrer 정보 숨김  
- `noopener`: 새 탭에서 열린 페이지가 원본을 제어하지 못하게 함

### 2-5. 로그인 / 프로필 컴포넌트

- components/LoginForm.js  
- components/Profile.js  
- AppLayout.js 내에서 조건부 렌더링

### 2-6. Hook과 비구조화 할당

```js
const [a, b] = [1, 2];
```

### 2-7. 화살표 함수 주의

```js
const user1 = () => { return { name: 'name', age: 3 }; };
const user2 = () => ({ name: 'name', age: 3 }); // 자동 반환
```

```js
const test1 = num.filter((n) => { return n % 2 === 0; });
const test2 = num.filter((n) => n % 2 === 0);
```

### 2-8. 리렌더링 최적화

- `useMemo` 활용
- 객체 비교는 주소값 기준

```js
let obj1 = {};
let obj2 = {};
console.log(obj1 === obj2); // false
```

### 2-9. 공통 스타일 적용

- `_app.js`에서 `antd.css`, styled-components import

---

## 3. Redux

### 3-1. 설치

```bash
npm i redux@4.0.5
npm i react-redux@8.0.5
npm i next-redux-wrapper@8.1.0
npm i redux-devtools-extension
```

### 3-2. 데이터 흐름 구조

```
[Component]
   ↓
[Dispatch]
   ↓
[Reducer]
   ↓
[Store]
   ↓
[Component]
```

### 3-3. 전개 연산자 예시

```js
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
const arr = [...arr1, ...arr2];

const obj1 = { a: 1, b: 2 };
const obj2 = { c: 3, d: 4 };
const obj = { ...obj1, ...obj2 };
```

### 3-4. 이미지 캐러셀 (react-slick)

```bash
npm i react-slick
```

공식: https://www.npmjs.com/package/react-slick

---

## 4. Saga

### 4-1. redux-saga란?

- Redux 미들웨어
- 비동기 액션 제어
- generator 함수 기반

### 4-2. 설치

```bash
npm i redux-saga@1.1.3
npm i axios
```

### 4-3. generator 함수 기본

```js
function* gen() {
  console.log(1);
  yield;
  console.log(2);
  yield;
  console.log(3);
  yield;
}

const g = gen();
g.next(); // 1
g.next(); // 2
g.next(); // 3
```

### 4-4. 무한 반복 generator

```js
let i = 0;
function* infiniteGen() {
  while (true) {
    yield i++;
  }
}

const g = infiniteGen();
g.next(); // { value: 0 }
g.next(); // { value: 1 }
```

---

## 5. etc - 스크롤링, faker dummy..

### 5-1. ESLint 설정

```bash
npm i -D babel-eslint@10.1.0 eslint-config-airbnb@18.1.0 eslint-plugin-import@2.20.2
npm i -D eslint-plugin-react-hooks@4.0.4
npm i -D eslint-plugin-jsx-a11y@6.2.3 --legacy-peer-deps
```

### 5-2. 아이디 생성 - shortid

```bash
npm i shortid@2.2.15 --legacy-peer-deps
```

### 5-3. 상태 불변성 관리 - immer

```bash
npm i immer@9.0.19 --legacy-peer-deps
```

### 5-4. 더미 데이터 생성 - faker

```bash
npm install --save-dev @faker-js/faker --legacy-peer-deps
```
