# Generic

## Generic

- 타입을 쓰는 언어에서 많이 쓰는 문법
- <T> 이런 방식으로 사용함.
- 타입을 함수의 파라미터정도로 받는걸라 보면 됨.

## Generic의 기본문법

```tsx
// generic사용법과 특징
function logText<T>(text: T) {
    console.log(text);
    return text;
}

// 이런식으로 <>안에 타입을 지정하여 사용(클래스, 함수 등에서 사용가능)
logText<number>(10); // 숫자 10
logText<string>('10'); // 문자 10

// 인터페이스에서 제네릭을 사용하는 방법
interface Dropdown<T> {
    value: T; // value의 타입만 다를 때 발생가능한 중복 문제를 해결
    selected: boolean;
}
const dbobj: Dropdown<string> = { value: 'abc', selected: false };
```

## 기존 정의 방식과 Generic의 비교

### 1. 함수 중복을 줄일 수 있다.

Generic을 사용하면 유지보수성이 더 높아진다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/13e5f6b0-8c07-44d0-bc99-279cb7d17672/Untitled.png)

![Generic으로 유지보수성상승](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/74a59cc2-ba4b-4e4b-b182-a8a6f09d534e/Untitled.png)

Generic으로 유지보수성상승

### 2. 기존 방식의 타입 유니온은 특정 API만 사용할 수 있다.

```tsx
function logText(text: string | number) {
    console.log(text);
    return text;
}
const a = logText('a');
a.split(''); 
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d2ffad62-ad4e-49d3-b58d-3dc42177220e/Untitled.png)

## Generic의 장점

### 1. 타입 호출 시에 타입을 정의할 수 있다

```tsx
function logText<T>(text: T) {
    console.log(text);
    return text;
}
logText<string>('10');
```

### 2. 타입 추론을 통해 반환값의 타입까지도 제어할 수 있다.

```tsx
function logText<T>(text: T) {
    console.log(text);
    return text;
}
let retVal: string = logText<string>('10');
```

### 3. 코드의 중복을 줄일 수 있다

```tsx
interface Dropdown<T> { // 코드의 중복을 줄일 수 있다.
    value: T;
    selected: boolean;
}

const emails: Dropdown<string>[] = [
    { value: 'naver.com', selected: true },
    { value: 'gmail.com', selected: false },
    { value: 'hanmail.net', selected: false },
];

const numberOfProducts: Dropdown<number>[] = [
    { value: 1, selected: true },
    { value: 2, selected: false },
    { value: 3, selected: false },
];

function createDropdownItem(item : Dropdown<number | string>) {
    const option = document.createElement('option');
    option.value = item.value.toString();
    option.innerText = item.value.toString();
    option.selected = item.selected;
    return option;
}
```

## Generic의 타입제한

### 1. 함수 내부의 API 제한

```tsx
// 제네릭의 타입 제한 - 1. 함수 내부의 API 제한
function logTextLength<T>(text: T[]): T[] {
    //함수 내에선 text가 배열이라는 가정이 이뤄져 관련 API만 가능하도록 변경된다.
    console.log(text.length);
    text.forEach(function (text) {
        console.log(text)
    });
    return text;
}
logTextLength<string>(['a', 'b', 'c']);
```

### 2. 정의된 타입 이용하기

```tsx
// 제네릭의 타입 제한 - 2 정의된 타입 이용하기
interface LengthType {
    length : number;
}
function logTextLength<T extends LengthType>(text: T): T{
    text.length;
    return text;
}

// LengthType은 length를 포함하는 값이라면 상관없음.
logTextLength({ length: 10, value: 'a' });
// 문자열은 length라는 함수가 자동으로 있어서 문제가 되지않음.
logTextLength<string>('a');
// 반면, 숫자는 length가 없어서 error가 발생함
logTextLength<number>(10);
```

![length가 없는 숫자는 에러가남.](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3f21e15d-0765-48e1-94b6-34f4cb09a2c3/Untitled.png)

length가 없는 숫자는 에러가남.

![위의 코드와 달리 length를 지운 객체({value: string})를  넣으면 에러가 남.](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/af6db26e-11df-4fc2-863e-6781eca453bd/Untitled.png)

위의 코드와 달리 length를 지운 객체({value: string})를  넣으면 에러가 남.

### 3.  keyof로 타입제한하기