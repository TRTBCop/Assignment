## 1)  Interface

### 1. `변수` 로 활용

```tsx
interface User {
    age: number;
    name: string;
}

var seho: User = {
    age: 33,
    name: 'seho',
}
```

### 2. `함수`로 활용

```tsx
// 함수에 인터페이스 활용
function getUser(user: User): void {
    console.log(user);
}
getUser(seho);
const capt = { 
    name: '캡틴'
}
getUser(capt); // getUser함수의 파라미터인 user 인터페이스와 달라서 에러가 발생
```

### 3. `함수의 구조` 를 정의하는데 활용

```tsx
// 함수 스펙(구조)에 인터페이스를 활용
interface SumFunction {
    (a: number, b: number): number;
}
let sum : SumFunction;
sum = function (a: number, b: string): number;
```

![다음과 같이 함수의 모습이 다르면 에러가 `발생한다.`](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6f537d3a-ae84-4a64-b7b0-de2ba265deea/Untitled.png)

다음과 같이 함수의 모습이 다르면 에러가 `발생한다.`

### 4. 인덱싱으로 활용

```tsx
// 4) 인덱싱
interface StringArray {
    [index: number]: string;
}
var arr: StringArray = ['a', 'b', 'c'];
arr[0]; //'a'
```

### 5. 딕셔너리 패턴으로 활용

```tsx
// 5) 딕셔너리 패턴
interface StringRegexDictionary {
    [key: string]: RegExp;
}
// 객체의 인덱스에 접근
var obj = {
    sth: /abc/,
    cssFile: /\.css$/,
    jsFile: /\.js$/,
}

// using ... 
obj['sth']; // /abc/ // 이런식으로 접근 가능
obj['sth'] = "SDFS"; // sth에 대한 값이 RegExp가 아니면 에러가 발생
Object.keys(obj).forEach(function (value) { }); // 이런식으로 looping 가능
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7020296f-3b45-417b-8df0-5b1fb60bdcdf/Untitled.png)

### 6. 인터페이스를 확장하여 사용하기

```tsx
// 6) 인터페이스 확장
interface Person {
    name: string;
    age: number;
}

interface Developer extends Person {
    language: string;
}

var captain: Developer = {
    name: '캡틴',
    age: 33,
    language: 'TypeScript',
}
```

## 2) 타입 별칭 (Type Aliases)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/53bb1680-31b8-49f5-a128-e43af19810f9/Untitled.png)

### 별칭 활용시 장점

- 별칭활용시 쉽게 타입 정의가 가능하다.
- 코드 가독성을 높일 수 있다.

## 3) Type vs. Interface

- **타입별칭은** 새로운 값을 만드는게 아니라 나중에 사용하기 좋개 `이름을 부여하는 것과 같다`
- 가장 큰 차이는 `확장 가능 여부` 다.
    - interface : 확장 가능
    - type : 확장 불가능

*그래서 가능한 한 Interface를 사용하는걸 추천한다.*

## 4) Union Type ( typeA | typeB )

|의 앞뒤 type의 공통 API만 가능하도록 함.

```tsx
function logMessage(value: string | number) { 
    console.log(value);
}

logMessage('hello');
logMessage(100); // 이제 string과 number타입을 받을 수 있다 들어갈 수 있다.
```

### 장점

1. **`Type Guard` :** 정의된 타입의 관련 API를 IDE가 추천해준다.
2. Type Error : 타입을 허용하지만 그에 따른 에러를 따로 마련할 수도 있다.
    
    ```tsx
    function logMessage(value: string | number) { 
        if (typeof value === 'string') {
            value.toLocaleLowerCase();
        }
        throw new TypeError('value must be string');
    }
    
    logMessage('hello');
    logMessage(100); // 이제 number타입도 들어갈 수 있다.
    ```
    

### 특징

1. A | B 로 타입이 결합된 변수일 경우, 해당 변수의 API로는 **A와 B의 공통 API만 가능하다. (조건문으로 하나의 타입만 가능한 케이스로 바꿔야 그외의 API도 사용가능)**
    
    ```tsx
    // 1) Union Type
    function unionSomeone(someone: RealPerson | RealDeveloper) {
        // someone은 developer 와 person의 공통만 갖는 타입을 갖기에 에러발생
        someone.name
        someone.age // 공통이 아니라서 에러발생
        someone.skill // 공통이 아니라서 에러발생
    }
    ```
    

## 5) Intersection Type ( TypeA & TypeB )

typeA와 typeB의 API를 모두 갖는 경우 사용

```tsx
// 2) Intersection Type
function intersectionSomeone(someone: RealPerson & RealDeveloper) {
    // someone은 developer 와 person을 모두 갖는 타입을 갖기에 에러발생하지 않음
    someone.name
    someone.age 
    someone.skill 
}
```

## 6) Union vs. Intersection

```tsx
// 3) union vs. intersection
// developer 혹은 person을 가지면 가능
unionSomeone({ name: 'seho', age: 30 });
unionSomeone({ name: 'capt', skill: '웹 개발' });

// developer와 person 모두를 가져야 가능
intersectionSomeone({ name: 'seho', age: 30 });
intersectionSomeone({ name: 'capt', skill: '웹 개발' });
```