### 1) 컴포넌트 설계
- TodoHeader : 로고
- TodoInput : 할일 작성 및 추가
- TodoList : 할일 목록 및 삭제 
- TodoFooter : 할일 전체삭제

### 2) 컴포넌트 생성
- src/components 하위에 __TodoHeader.vue__, __TodoInput.vue__, __TodoList,vue__, __TodoFooter.vue__ 생성

### 3) 컴포넌트 등록
```
//////////////////
// src/App.vue  //
//////////////////

import TodoHeader from "./components/TodoHeader.vue"
import TodoInput from "./components/TodoInput.vue"
import TodoList from "./components/TodoList.vue"
import TodoFooter from "./components/TodoFooter.vue"

export default {
  components: {
    // [컴포넌트 태그명] : [컴포넌트 내용]      <- 구조 
    "TodoHeader" : TodoHeader,
    "TodoInput" : TodoInput,
    "TodoList" : TodoList,
    "TodoFooter" : TodoFooter
  }
}
```

### 4) 반응형 태그 & 파비콘 & 아이콘
#### (1) 반응형 태그(웹)
`<meta name="viewport" content="width=device-width, initial-scale=1.0">`
#### (2) 파비콘 
- https://www.favicon-generator.org/ 에서 favicon 생성
- favicon 추가
#### (3) web font
- https://fontawesome.com/v5.15/how-to-use/customizing-wordpress/snippets/setup-cdn-webfont#load-all-styles 에서 태그 갖고오기
#### (4) (Ubuntu) font 추가
- https://fonts.google.com/specimen/Ubuntu#standard-styles
```
////////////////////////
// public/index.html  //
////////////////////////

 <link rel="shortcut icon" href="src/assets/favicon.ico" type="image/x-icon">
 <link rel="icon" href="src/assets/favicon.ico" type="image/x-icon">
 <link rel="stylesheet" href="https://pro.fontawesome.com/releases/v5.10.0/css/all.css" integrity="sha384-AYmEC3Yw5cVb3ZcuHtOA93w35dYTsvhLPVnYs9eStHfGJvOvKxVfELGroGkvsg+p" crossorigin="anonymous"/>
 <link href="https://fonts.googleapis.com/css2?family=Ubuntu:wght@300&display=swap" rel="stylesheet">
```

### 5) 프로젝트 구현 
#### (1) TodoHeader 컴포넌트 구현 (template + style)
__cf)__ `<style scoped>` : 해당 component에서만 유효한 스타일 지정
  
#### (2) TodoInput 컴포넌트 구현 
- `v-model` : input에 입력된 값을 동적으로 vue instance에 매핑하는 역할. (서로 동기화) <br>

__ex)__ 
```
///////////////////////////////////
// src/components/TodoInput.vue  //
///////////////////////////////////

/// v-model 등록
<input type="text" v-model = "newTodoItem"> 

/// script 
export default {
    data: function() {
        return {
            newTodoItem: ""
        }
    }
}
```
![image](https://user-images.githubusercontent.com/86991030/125878328-a79fd1ee-6916-4070-a670-b2d619ec8f16.png) --->
![image](https://user-images.githubusercontent.com/86991030/125878340-9f4a4c88-4653-4458-b838-4e9eea8272a5.png)
- `v-on:click="addTodo"` : 버튼 클릭시 addTodo 함수 실행
```
///////////////////////////////////
// src/components/TodoInput.vue  //
///////////////////////////////////

/// 버튼 생성
<button v-on:click="addTodo"> add </button>

/// 함수 정의
export default {
    data: function() {
        return {
            newTodoItem: ""
        }
    },
    methods: {
        addTodo: function() {
            console.log(this.newTodoItem);    // this : 현재 컴포넌트(TodoInput 컴포넌트)를 의미. 
        }
    }
}
```
- `localStorage.setItem(key, value)` : 로컬 스토리지에 입력한 내용 저장
```
localStorage.setItem(this.newTodoItem, this.newTodoItem);
```

  
