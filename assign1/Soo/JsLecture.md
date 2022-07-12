# 개요

- 자바스크립트 과제 
- 과제 내용 요약
- 결과물

------

# 과제

## 설명

노마드 코더 에 있는 강의를 듣고 JS로 어플리케이션 만들기 (날씨API + localstorage)활용

## 인증




# 정리

## 요약

#### 변수  

 const - 변하지않는 값 (상수)

 let - 변할수 있는 값 

Boolean

Null

Undefined

String 

BigInt 



** 변수들의 타입은 변수의 값에 따라 정수, 문자열, 블리언 등등으로 바뀔수 있는 동적 타입입니다. 



#### 배열 

< 예시 >

```javascript
let weeks1 = [mon, tue, wed, thu, fri, sat, sun];

let elements = new Array();
elements = [ undefined, null, false, NaN, 1000 ];
```



#### 오브젝트 

< 예시 >

```js
let player ={
	nickname : "soo"
    points : 10,
    speed : 10,
    fat : false;
};
```



#### LocalStorage 란?

- **HTML5에서 추가된 저장소**이다

- 브라우저 내에 key와 value로 이루어진 데이터를 String 타입으로 저장됩니다.

- LocalStorage 의 데이터 영속성은 동일한 컴퓨터에서 동일한 브라우저를 사용했을때 해당됩니다.

< 예시 >

```js
// 키에 데이터 쓰기
localStorage.setItem("key", value);

// 키로 부터 데이터 읽기
localStorage.getItem("key");

// 키의 데이터 삭제
localStorage.removeItem("key");

// 모든 키의 데이터 삭제
localStorage.clear();

// 저장된 키/값 쌍의 개수
localStorage.length;
```

#### 주의사항

웹스토리지를 사용할때 오직 문자형 데이터 타입만 지원합니다.

숫자형 데이터를 로컬 스토리지에 쓰고 다시 읽으면 숫자가 아닌 문자타입으로 읽습니다.



## 느낀점

이번 강의를 들으면서 쿠키/세션 외에도 Local Storage 이라는 공간 안에 데이터를 저장, 삭제 할 수 있다는 것에 배웠습니다. 또한 자바스크립트의 기본적인 문법들을 다시 한번 듣고 복습할 수 있어 좋았습니다. 



## 결과물




1. Todo 기능 - localstorage을 통해 데이터 값을 저장, 삭제를 할 수 있습니다.

2. 시간 기능 - 현재시간을 보여줍니다.

3. 명언 - 홈페이지 새로고침을 통해 명언이 랜덤으로 표시된다.

4. 날씨 기능 - 오른쪽 상단 위에 (도시/ 날씨 상태 / 온도 )형태로 표시된다.(openWeather API)활용

5. 날씨에 따른 배경  

   - 날씨로는 총 구름, 비, 천둥, 눈, 맑음, 기본 배경이며 날씨정보에 따라 배경이 달라집니다. 
     또한 날씨를 읽지못하는경우는 날씨를 읽어오는중 으로 표현되며 배경화면은 기본 배경화면으로 됩니다.

     
