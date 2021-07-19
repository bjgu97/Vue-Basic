### axios 
- `npm install axios`
- ex:
```
////////////////////////////
//      Newsview.vue      //
////////////////////////////

<div v-for="user in users" v-bind:key="user"> {{ user }} </div>

created() {
        var vm = this;
        axios.get('https://api.hnpwa.com/v0/news/1.json')
        .then(function(response) {
            vm.users = response.data;
        })
        .catch(function(error) {
            //
        })
    }
```
### axios의 api 함수 구조화 
- src/api/index.js 생성 
  - axios import 하기 
  - HTTP request & Response와 관련된 기본 설정 하기 `const config = {}`
  - API 함수들 정리하기 `function func() { return }`
  - __export__: export를 해줘야 다른 파일에서 import를 해올 수 있다!
```
import axios from 'axios'

const config = {
    baseUrl: 'https://api.hnpwa.com/v0/'
}

function fetchNewsList() {
    return axios.get(`${config.baseUrl}news/1.json`)
}

export {
    fetchNewsList
}
```
### 화살표함수
```
/// 변경 전

var vm = this;
fetchJobsList()
    .then(function(response) {
        vm.jobs = response.data;
    })
    .catch(function(error) {
        console.log(error);
    })
 
 
/// 변경 후

fetchJobsList()
   .then(response => this.jobs = response.data)
   .catch(error => console.log(error));
```

### 자바스크립트 비동기 처리 - CallBack
### 자바스크립트 비동기 처리 - Promise
