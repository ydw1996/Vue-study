# Vue.js 시작하기

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
