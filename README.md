# Vue.js 강의1

[Vue.js 시작하기 인프런 강의](https://inf.run/RxKK)와 [Vue 3 시작하기 인프런 강의](https://inf.run/kRHp) 리포지토리입니다.

![인프런 Vue 3 시작하기 강의 썸네일](https://cdn.inflearn.com/public/courses/332010/cover/fffd02eb-685e-44ab-aa0d-6788349338c5/332010-eng.png)

## 인스턴스

[Vue 인스턴스 공식문서](https://v2.vuejs.org/v2/guide/instance.html)

- 생성: new Vue()로 인스턴스를 생성
- 데이터: data 옵션에 애플리케이션의 상태(데이터)를 정의
- 메소드: methods 옵션에 동작(함수)을 정의
- 라이프사이클 훅: created, mounted 등의 훅을 사용해 특정 시점에 실행되는 코드를 작성할 수 있음

```jsx
new Vue({
  el: '#app',
  data: {
    message: 'Hello, Vue!',
  },

  methods: {
    reverseMessage() {
      this.message = this.message
        .split('')
        .reverse()
        .join('');
    },
  },

  created() {
    console.log('Vue 인스턴스가 생성되었습니다.');
  },
});
```

## 뷰 컴포넌트

[Vue 컴포넌트 공식문서](https://ko.vuejs.org/guide/essentials/component-basics)

- Vue 컴포넌트는 재사용 가능한 UI 요소를 정의하는 방법
- 컴포넌트는 HTML, CSS, JavaScript를 하나로 묶어 독립적인 블록

### 1. 컴포넌트 정의

```jsx
Vue.component('my-component', {
  template: '<div>Hello, this is my component!</div>',
});
```

### 2. 컴포넌트 사용

```jsx
<div id="app">
  <my-component></my-component>
</div>
```

### 3. 데이터와 메소드 사용

```jsx
Vue.component('counter-component', {
  data() {
    return { count: 0 };
  },
  template: '<button @click="count++">{{ count }}</button>',
});
```

### 4. 부모-자식 간 데이터 전달 (Props)와 이벤트 (Events)

```jsx
// 자식 컴포넌트에서 Props 사용
Vue.component('child-component', {
  props: ['message'],
  template: '<p>{{ message }}</p>',
});

// 자식 컴포넌트에서 이벤트 발생
Vue.component('button-counter', {
  data() {
    return { count: 0 };
  },
  template:
    '<button @click="increment">{{ count }}</button>',
  methods: {
    increment() {
      this.count++;
      this.$emit('increment');
    },
  },
});
```

### 5. 같은 레벨 컴포넌트간 데이터 전달

```jsx
<div id="app">
  <!-- num 데이터를 app-header 컴포넌트로 전달 -->
  <app-header v-bind:propsdata="num"></app-header>

  <!-- app-content에서 발생한 이벤트를 deliverNum 메서드로 처리 -->
  <app-content v-on:pass="deliverNum"></app-content>
</div>
```

- app-header 컴포넌트는 부모 컴포넌트로부터 num 데이터를 props로 전달받아 화면에 표시
- app-content 컴포넌트는 버튼을 클릭했을 때 pass 이벤트를 발생시키며, 이 이벤트는 부모 컴포넌트의 deliverNum 메소드에서 처리

#### 데이터 흐름 요약

- 데이터 초기화: 부모 컴포넌트는 num을 0으로 초기화
- 데이터 전달 (props): 부모 컴포넌트는 이 num 값을 app-header 컴포넌트로 전달
- 이벤트 발생 (emit): 사용자가 app-content 컴포넌트의 버튼을 클릭하면 pass 이벤트가 발생하고, 10이 부모 컴포넌트로 전달
- 이벤트 처리: 부모 컴포넌트는 deliverNum 메서드를 통해 전달된 10 값을 num에 저장하고, 이 값은 다시 app-header 컴포넌트로 전달됩니다.

## 라우터

[뷰 라우터 공식문서](https://v3.router.vuejs.org/kr/guide/#html)

- 페이지 간의 이동을 관리하는 공식 라이브러리
- 라우팅을 통해 사용자가 다른 URL로 이동할 때마다 다른 컴포넌트를 렌더링하거나 특정 동작을 수행

#### Vue Router

1. 라우트(Route): URL 경로와 컴포넌트를 매핑하는 설정
2. 라우트 뷰(`router-view`): 현재 활성화된 라우트의 컴포넌트를 렌더링 하는 표시자
3. 라우트 링크(`router-link`): 사용자가 클릭하여 라우트를 변경할 수 있는 링크 컴포넌트

```jsx
<div id="app">
  <div>
    <router-link to="/login">Login</router-link>
    <router-link to="/main">Main</router-link>
  </div>
  <router-view></router-view>
</div>
```

```jsx
var LoginComponent = {
  template: '<div>login</div>',
};
var MainComponent = {
  template: '<div>main</div>',
};

var router = new VueRouter({
  // 페이지의 라우팅 정보
  routes: [
    // 로그인 페이지 정보
    {
      path: '/login',
      component: LoginComponent,
    },
    // 메인 페이지 정보
    {
      path: '/main',
      component: MainComponent,
    },
  ],
});

new Vue({
  el: '#app',
  router: router,
});
```

#### Vue Router의 주요 기능

1. 라우트 정의: URL 경로와 컴포넌트를 연결하여 특정 URL에 어떤 컴포넌트를 표시할지 설정합니다.
2. 동적 라우트:URL의 변수 부분(`:id`등)을 사용해 동적인 페이지를 처리. 예: `/user/:id`
3. 네비게이션 가드: 라우트 전환 시 특정 작업(예: 인증확인)을 실행함
4. 프로그램적 네비게이션: 코드에서 `this.$router.push()`를 사용해 URL을 변경하며 페이지 전환

5. 라우터 모드

- 해시 모드: URL에 해시(`#`)를 사용. 예:`/#/home`
- 히스토리 모드: 깔끔한 URL사용. 예: `/home`
