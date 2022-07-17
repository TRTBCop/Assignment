# Class & Prototype

## Class

- class는 ES2015 (ES6) 부터 등장한 것임.
- class는 instance를 만들어주는게 목적인 아이임.

```tsx
class Person {
    // 클래스 로직
    constructor(name, age) {
        console.log('생성되었습니다.')
        this.name = name;
        this.age = age;
    }
}

var snsd = new Person('소녀시대', 20);
```

## Prototype

### 특징

1) 자바스크립트는 프로토타입 기반의 언어다

```tsx
var user = {name: ‘capt', age: 100};
var admin = {name: 'capt', age 100, role:'admin');

// user의 정보를 admin에서 재탕할 수 있도록 하고자함.
admin.__proto__ = user;
```

2) admin.__proto__ 를 user로 정의해줬기에 admin의 빈객체지만 __proto__에 user의 내용이 나온다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9f0c0227-c3b9-4bba-a33d-7e8fce4761bd/Untitled.png)

3) proto로 정의한 값을 불러올 수도 있다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/80a1d572-3d12-4f23-bcc2-29dc2d9c73a0/Untitled.png)

### 활용사례

**1) Built in javascript (= Javascript Native API)**

- mdn 사이트의 object 설명 중 method를 보면, 수많은 여러 API가 나옴.
- 이게 다 최상위에 정의된 프로토타입으로부터 오는것임

**⇒ 코드의 재활용으로 많은 도움이 된다.**

## Class Vs. Prototype

```tsx
// class는 instance를 만들어주는게 목적인 아이임.
class Person {
    // 클래스 로직
    constructor(name, age) {
        console.log('생성되었습니다.')
        this.name = name;
        this.age = age;
    }
}

var snsd = new Person('소녀시대', 20);

// 생성자 함수
function Person(name, age) {
    this.name = name;
    this.age = age;
}
var capt = new Person('캡틴마블', 40);
```

- 클래스라는건 원래 생성자 함수를 통해 가능하던 걸 자바와 같은 객체지향형 사람들이 사용하기 좋게 하기위해 등장한 것이었다.

## Class 문법

1. 클래스 상단에 **`변수들을 미리 정의`**해야한다. 
2. `**접근제어자**`를 ****사용할 수 있다
    1. public, private, protected를 사용할 수 있다.
3. readonly같은 `**변수의 속성**`을 지정할 수도 있다.