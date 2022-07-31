# 타입추론, 단언, 가드, 호환, 모듈화(Type Inference, Assertion, Guard, Compatibility, Module)
// 사진이 꺠지니 자세한 내용은 해당 노션 링크를 참고할 것. <br>
https://temporal-pest-1a5.notion.site/Type-Inference-Assertion-Guard-Compatibility-Module-0dfd3238641a4a738def85d38284da19

## 1. 타입추론

### 정의

: 에디터 상에서 타입이 무엇인지 추론해주는 것을 말한다.

- 기본적인 변수의 선언과 할당에 의해서 타입추론이 이뤄진다.

### 예시

- 인터페이스와 제너릭을 이용한 타입추론
    - Dropdown이란 인터페이스의 T란 타입이 들어오면 T의 타입에 따라 value를 자동으로 string이라고 추론해준다.
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f9117642-fb9b-4173-9465-b751ee7cc73e/Untitled.png)
        
- interface 확장인 경우에도 부모인터페이스까지 타입을 전달해 줄 수 있다.
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1b8aab28-bbc0-42aa-ab77-1aeb9cfdcd52/Untitled.png)
    
- **Best Common Type**
    - 표현식에 근거하여 가장 근접한 타입을 추론한다. (간단히 union으로 묶어나간다고 보면 됨)
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0a6ce665-94b5-4569-915d-a9dc37d0efce/Untitled.png)
        
    

## 2. 타입단언 (as)

**⇒ 이 아이의 타입은 에디터보다 개발자가 더 잘아니까 해당 타입으로 단언하는 것**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f6164b0a-7db9-4fbc-8d87-20172e50cd35/Untitled.png)

### 정의

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ab3959cc-bed1-4e35-a11c-29d137af1e17/Untitled.png)

ta를 할당없이 선언하고 그 후 할당을 하면, 후에 b에 ta를 할당할때 변경된 값이 아닌 초기 선언된 값(any)로 타입추론된다. 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/300ea8ec-9a15-4519-85ea-332bb976932a/Untitled.png)

개발자가 더 잘아니까 타입스크립트 넌 좀 뒤로가봐!! 라는 스타일로써 **as 라는 키워드를 통해 타입을 단언할 수 있다.**

### 예시 (DOM API)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1c8d78cc-0292-4959-bcfd-22232b8c1643/Untitled.png)

이렇게 Dom API결과로 대부분은 타입추론에 따라 알맞는 함수를 추천받을 수 있다.

그러나, 실무를 하다보면  div가 실제하는지도 체크하고 돌려야하기 떄문에 다음과 같은 경우가 많다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b84aef65-0d98-4934-975c-db4fd78d6752/Untitled.png)

이렇게 null일수도 있다고 말을 하기 때문에 if문으로 조건을 걸어 해결하곤 하는데, 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/689c3d68-4cad-4a35-9445-1c49d2bfc8ed/Untitled.png)

이를 타입단언을 사용하면 아래처럼 깔끔하게 작성할 수도 있다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a063dd92-410c-4ccf-8b15-8ac274693bc1/Untitled.png)

**해당 내용은 div라는 html요소에 접근하였을때 이게 HTMLDivElement로써 반드시 존재할거라고 단언하는 것이다.**

## 3. 타입 가드 (is)

### 정의

⇒ Union으로 연결된 인터페이스처럼 타입이 불분명해 속성을 간단히 불러올 수 없는 경우, 타입 가드를 정의하여 함수의 리턴 값을 한정지어 코드 가독성도 높이고 유지보수성도 높일 수 있다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1b01ddfd-76e7-4e4e-8b98-59db0e4e5cde/Untitled.png)

### 예시

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1c5cc67a-c76a-4880-aa6c-238c31b8b733/Untitled.png)

return값에 name, age, skill을 다 담아 넣어줬음에도 tony.skill하면 skill 속성이 없다고 뜬다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/aab814d0-16c6-4b65-8c4f-3227e7b4f71c/Untitled.png)

이걸 해결하는 방법으론 

1. `타입단언` 을 쓸수도 있는데, 이 방식은 코드 가독성도 낮고, 반복되는 키워드도 너무 많음.
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/91e47a0b-1bb5-498e-b417-0fcd7cf322dc/Untitled.png)
    
2. `타입 가드` 를 쓸 수도 있다.
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/104a45c3-0fa4-4ead-b1c9-6887aa582b48/Untitled.png)
    
    이제 isDeveloper 함수를 통과하고 나면 developer인게 확실해짐.
    
    **이렇게 isDeveloper함수 같은걸 타입 가드라고 부른다.**
    

## 4. 타입 호환 (Type Compatibility)

### 정의

 **구조적 타이핑에 따라 타입호환이 이뤄진다.**

### 구조적 타이핑(Structural Typing)

: 코드 구조 관점에서 타입이 서로 호환되는지의 여부를 판단

[타입 호환 | 타입스크립트 핸드북](https://joshua1988.github.io/ts/guide/type-compatibility.html#%EA%B5%AC%EC%A1%B0%EC%A0%81-%ED%83%80%EC%9D%B4%ED%95%91-%EC%98%88%EC%8B%9C)

- **타입호환이란 것은 왼쪽(할당되는 변수)보다 오른쪽(할당하는 값)이 더 범위가 클 때 가능하다.**

### 예시1. Interface

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0b5e37c1-09e7-4a8a-9706-012c89231a24/Untitled.png)

 Person형식에 skill 속성이 없지만 developer에서는 skill이 필수적이라서 다음과 같은 컴파일 에러가 발생한다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3b2e4d1d-5a3b-4f59-9439-40a4262328a3/Untitled.png)

⇒ **타입호환이란 것은 왼쪽보다 오른쪽이 더 범위가 클 때 가능하다.**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/567bb67d-ea82-47a9-9747-f749052ab50a/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e98189d7-a792-4f2e-b9dd-49027896f9d6/Untitled.png)

**⇒ 타입호환은 구조적으로 동일하면 순서에 상관없이 오류가 발생하지 않는다.**

### 예시2. Class

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6a1e573b-6e46-4535-95ef-6313228fd6b5/Untitled.png)

**⇒ class나 interface같은 키워드로 분류되는것이 아닌 구조적 타이핑에 따라 타입호환이 이뤄진다.**

### 예시3. 함수

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4488cdb3-e8f3-498c-be45-7dd7236e12f8/Untitled.png)

좀 더 넓은 범위

### 예시4. 제네릭

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0b5100e5-9961-4f0b-8239-25d7e7e12293/Untitled.png)

- Empty인터페이스처럼 **비어있는경우** 제네릭이 달라도 **서로 타입 호환이 됨**. (에러는 할당 X에러임)
- NotEmpty 인터페이스처럼 **비어있지 않은 경우** 제네릭이 다르면 **타입호환이 되지 않음. (**에러는 할당 X에러임)

## 5. 타입 모듈화

### 정의

import와  export를 통해 모듈화를 진행하는 것.

### 모듈시스템 (Simple)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a3d197b3-7a50-4137-861d-53f9060301dc/Untitled.png)

모듈시스템처럼 Todo라는 인터페이스를 파일을 분리하여 가져다 쓸 수 있는 걸 말함.

require.js란 라이브러리가 점점 진화하여 ES6부터 import와 export로 가져올 수 있음.

[Modules | Cracking Vue.js](https://joshua1988.github.io/vue-camp/es6+/modules.html#%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%E1%84%92%E1%85%AA%E1%84%8B%E1%85%B4-%E1%84%91%E1%85%B5%E1%86%AF%E1%84%8B%E1%85%AD%E1%84%89%E1%85%A5%E1%86%BC)

### 예시
