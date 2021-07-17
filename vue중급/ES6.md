### ES6란?
- 최신 Front-End Framework인 React, Angular, Vue에서 권고하는 언어 형식
- var -> const/let

### Babel?
- ES6의 문법을 각 브라우저의 호환 가능한 ES5로 변환하는 컴파일러
- [Babel 온라인 에디터 링크](https://babeljs.io/repl/#?browsers=defaults%2C%20not%20ie%2011%2C%20not%20ie_mob%2011&build=&builtIns=false&corejs=3.6&spec=false&loose=false&code_lz=Q&debug=false&forceAllTransforms=false&shippedProposals=false&circleciRepo=&evaluate=false&fileSize=false&timeTravel=false&sourceType=module&lineWrap=true&presets=env%2Creact%2Cstage-2&prettier=false&targets=&version=7.14.7&externalPlugins=)

### Const & let
: 새로운 변수 선언 방식
- 블록`{ }` 단위로 변수의 범위가 제한되어있음. 
- `const` : 한번 선언한 값에 대해서 변경할 수 없음(상수)
  - 객체나 배열 내부는 변경 가능!
```
  const a = {};
  a.num = 10;
  console.log(a);    // {num: 10}
  
  const a = [];
  a.push(20);
  console.log(a);     // [20]
```
- `let` : 한번 선언한 값에 대해서 다시 선언할 수 없음.
```
const a = 10;
a = 20;       <- 에러!!!

let a = 10;
let a = 20;   <- 에러!!!
a = 30;
```

### ES5 특징
- __변수의 Scope__: `{ }`에 상관 없이 scope 설정됨.
```
var sum = 0;
for(var i = 1; i <= 6; i++) {
  sum = sum + i;
}
console.log(sum); // 15
console.log(i); // 6
```
- __Hoisting__: 선언한 함수와 변수를 해석기가 가장 상단에 있는 것처럼 인식
```
function willBeOveridden() {
  return 10;
}
willBeOverridden();  5
function willBeOverridden() { 
  return 5;
}
```

### Arrow Function(화살표함수)
- 함수를 정의할 때 `function` 사용하지 않고 `=>`로 대체
- 콜백 함수의 문법 간결화
```
//ES5
var sum = function(a, b) {
  return a+b;
};

//ES6
var sum = (a, b) => {
  return a+b;
}
```

### Enhanced Object Literals - 향상된 객체 리터럴
- 객체의 메서드를 사용할 때 `function` 예약어 생략하고 생성 가능
```
var dictionary = {
  // ES5
  lookup: function() {
    console.log("");
  };
  
  // ES6
  lookup() {
    console.log("");
  }
};
```
- 객체의 속성명과 값 명이 동일할 때 아래와 같이 축약 가능
```
var figures = 10;
var dictionary = {
  //figures: figures;
  figures
};
```
### Modules - 자바스크립트 모듈화 방법
- Modules: 특정 기능을 수행하는 한 단위
- 호출되기 전까지는 코드 실행과 동작을 하지 않는 특징이 있음.
- `default` export
  - 한 개의 파일에서 하나밖에 export 되지 않는다.
