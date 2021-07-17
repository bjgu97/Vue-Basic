### Vuex?
: 무수히 많은 컴포넌트의 데이터를 관리하기 위한 상태 관리 패턴이자 라이브러리

### Flux?
: MVC 패턴의 목잡한 데이터 흐름 문제를 해결하는 개발 패턴 <br>
Action -> Dispatcher -> Model -> view (단방향 통신)
- __action__ : 화면에서 발생하는 이벤트, 또는 사용자의 입력
- __dispatcher__ : 데이터를 변경하는 방법, 메서드; 모델을 바꾸기 위한 역할.
- __model__ : 화면에 표시할 데이터
- __view__ : 사용자에게 비춰지는 화면

### Vuex?
- Vuex로 해결할 수 있는 문제
  1) MVC 패턴에서 발생하는 구조적 오류
  2) 컴포넌트 간 데이터 전달 명시
  3) 여러개의 컴포넌트에서 같은 데이터 업데이트 할 때 동기화 문제.
- Vuex 컨셉
  - __State__ : 컴포넌트 간에 공유하는 데이터 `data()`
  - __View__ : 데이터를 표시하는 화면 `template`
  - __Action__ : 사용자의 입력에 따라 데이터를 변경하는 `methods`
- Vuex 구조
  - 컴포넌트 -> 비동기 로직 -> 동기 로직 -> 상태
### Vuex 설치 및 시작
- `npm install vuex --save`
  - 설치한거는 `package.json`의 dependencies에서 확인 가능.
- src 폴더 밑에 `Store/store.js` 생성
```
////////////////////////////////
//     src/Store/store.js     //
////////////////////////////////

import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex); // use : Vue의 플러그인 기능. 

export const store = new Vuex.store({    // export 해줬기 때문에 store은 전역변수. 
    // ...
})


/////////////////////////
//     src/main.js     //
/////////////////////////

import { store } from './Store/store'

new Vue({
  el: '#app',
  store,
  render: h => h(App)
})
```
### Vuex 기술 요소
__1) state__ : 여러 컴포넌트에 공유되는 데이터 `data`
- 여러 컴포넌트 간에 공유할 데이터 (상태)
```
// Vue
data: {
  message: "Hello Vue.js!"
}

// Vuex
state: {
  message: "Hello Vue.js!"
}
```
```
<!-- Vue -->
{{ message }}

<!-- Vuex -->
{{ this.$store.state.message }}
```
__2) getters__ : 연산된 state에 접근하는 속성 `computed`
- state 값을 접근하는 속성이자 `computed()` 처럼 미리 연산된 값을 접근하는 속성
```
// store.js
state: {
  num: 10;
},
getters: {
  getNumber(state) {
    return state.num;
  }
}

{{ this.$store.getters.getNumber }} 
```
__3) mutations__ : state 값을 변경하는 이벤트 로직/메서드 `methods`
- _state의 값을 변경할 수 있는 유일한 방법_이자 메서드
- `commit()`로 동작한다. 
```
// store.js
state: {num: 10;}
mutations: {
  sumNumbers(state, anotherNum) {
    return state.num + anotherNum;
  }
}

// App.vue
this.$store.commit('sumNumbers', 20);
```
- `commit()` 형식 : state를 변경하기 위해 mutations를 동작시킬 때 인자(payload) 전달할 수 있음.
```
// store.js
state: {storeNum: 10 },
mutations: {
  modifyState(state, payload) {
    console.log(payload.str);
    return state.storeNum += payload.num;
  }
}

// App.vue
this.$store.commit('modifyState', {
  str: "passed from payload",
  num: 20
});
```
- ___state를 직접 변경하지 않고 mutations으로 변경하는 이유?___
  - 여러 개의 컴포넌트에서 state 값을 변경하는 경우 어느 컴포넌트에서 해당 state를 변경했는지 추적하기 어려움.
  - 특정 시점에 어떤 컴포넌트가 state에 접근하여 변경한 건지 확인하기 어렵기 때문.
  - 따라서 뷰의 반응성을 거스르지 ㅇ낳게 명시적으로 상태 변화를 수행. 반응성, 디버깅, 테스팅 혜택

__4) actions__ : 비동기 처리 로직을 선언하는 메서드 `async methods`
- 비동기 처리 로직을 선언하는 메서드. 비동기 로직을 담당하는 mutations.
- 데이터 요청, Promise, ES6 async과 같은 비동기 처리는 모두 actions에 선언.
```
// store.js
actions: {
  delayDoubleNumber(context) {      // context : actions에서 mutation에 접근하기 위한 경로
    context.commit("doubleNumber");
  }
}

// App.vue
this.$store.dispatch('delayDoubleNumber');   // dispatch : action 발생시키는 api.
```
- ___비동기 처리 로직을 actions에 선언해야 하는 이유?___
  - 언제 어느 component에서 해당 state를 호출하고, 변경했는지 확인하기 어려움.
  - 즉, state 값의 변화를 추적하기 어렵기 때문에 mutations 속성에는 동기 처리 로직만 넣어야 한다. 
 
### Vuex Helpers
### Vuex로 프로젝트 구조화 및 모듈화
