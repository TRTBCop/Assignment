# 개요
- 스터디에서 부여하는 과제는 `이론과제`와 `짬공부`로 2가지가 있습니다.
- 해당 템플릿은 `이론과제`를 제출할 때 사용하는 과제를 말합니다.
- 제목은 Theory-Typescript 처럼 강의 내용이 무엇인지 알 수 있도록 지정해줍니다.


----------
# 과제
## 설명
타입스크립트 입문 강의 Lect 2까지 듣기 (https://www.inflearn.com/course/%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%9E%85%EB%AC%B8)

## 인증
날짜와 시간, 수강 진도율, 강의명이 보이도록 캡쳐하여 사진을 올려주세요
![image](https://user-images.githubusercontent.com/48820696/177041730-a3e893b6-5fa2-4d13-ba52-c322083b1a57.png)


# 정리
## 요약
#### 타입스크립트 
: 타입이 부여된 자바스크립트
- 브라우저에서 실행되기 위해 컴파일 과정이 이뤄진다.
- 장점
   - 에러의 사전 방지
      - jsdoc만 사용해도 객체 내의 타입을 빠르게 확인할 수 있고 오탈자로 인한 에러 등을 방지할 수 있다.
     ```javascript
      /**
      * @typedef {object} User
      * @property {string} name 이것은 이름에대한 부가설명입니다.
      * @property {string} email 이것은 이메일에대한 부가설명입니다.
      * @property {string} address 이것은 주소에대한 부가설명입니다.
      */
      axios.get(url).then(function (response){
        response.address.city
      });
      ```
      - 하지만 이보다는 타입스크립트를 통해 정의하는게 가독성도 좋고, 사용에도 편리하고, 유지보수성도 높다.
      ```typescript
      type User = {
        name: string,
        email : string,
        address?: string
      }

      ```
   - 코드 가이드 및 자동완성
       - 숫자를 받아야 할 함수에 문자를 넣어도 자바스크립트 특성상 오류 발생이 아닌 이상한 결과를 리턴함.
         example)
         ```javascript
         function sum(a,b){return a+b};
         sum(10,'20'); // 1020
         ```
       - 이를 타입스크립트를 이용하면 인자가 숫자가 아닐때 오류를 발생시켜 올바른 값만 들어오도록 할 수 있다.
         example)
         ```typescript
         function sum(a:number,b:number):number {return a+b};
         sum(10,'20'); // 컴파일과정에서 error 발생
         sum(10, 20); // 30
         ```
       - 또한, 이를 result로 받았을 때 해당 타입에서 사용할 수 있는 자동완성기능을 사용할 수 있어 더 편리하다.
         example)
         ```typescript
         function sum(a:number,b:number):number {return a+b};
         let ret = sum(10,20);
         ret. //을 입력시 toString(), toFixed() 등 다양한 자동완성을 vsc에서 제안해준다.
         ```         
- 변환
  ```
  tsc tsfileName.ts
  ```
  위의 내용을 입력시 타입스크립트 파일을 자바스크립트 파일로 변환한 파일이 생성된다.
  
- tsconfig.json
  - 타입스크립트로 변환할때의 설정 내용을 정의할 수 있다.
  - ex. implicitAny는 any라도 타입을 정의하란 의미.
  - 참고 : https://www.typescriptlang.org/ko/docs/handbook/tsconfig-json.html 

- typescript playground
  - 타입스크립트로 작성한 파일이 자바스크립트론 어떻게 변환되어 실행되는지 테스트해볼 수 있다.
  - https://www.typescriptlang.org/ko/play

...

  
## 느낀점
```
// 최소 한 줄 이상으로 작성해주시고, 가볍게 이번 강의를 들으면서 느꼈던 내용을 적어주시면 됩니다.
```
jsdoc이란 걸 처음 알게되어 재밌었고, 타입스크립트 사이트에서 제공하는 생각보다 많아 흥미로웠다.
