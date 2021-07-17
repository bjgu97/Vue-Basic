### props
: 부모에서 자식으로 데이터 전달하기 위해 사용 (상위 컴포넌트 -> 하위 컴포넌드)
- 하위 컴포넌트
```
var ChildComponent = {
  props: ['프롭스 속성 명']
}
```
- 상위 컴포넌트
```
<div id="app">
  <child-component v-bind:프롭스속성명 = "상위컴포넌트의 data 속성"> </child-component>
</div>
```
### emit
: 자식이 부모에게 데이터 전달ㄹ하기 위해 이벤트 발생시키는 것.
- 하위 컴포넌트
```
this.$emit("이벤트명");
```
- 상위 컴포넌트
```
<div id="app">
  <child-component v-on:이벤트명 = "상위컴포넌트의 실행할 메서드명 또는 연산"> </child-component>
</div>
```
