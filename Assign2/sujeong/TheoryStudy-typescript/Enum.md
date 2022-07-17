# Enums

# Enums

: 특정 값의 집합을 의미하는 자료형

- 정해져있는 목록 (ex. 드롭다운) 에서 사용하기 좋음

## 1. 숫자형 Enum

```tsx
// 1. 숫자형 enum
enum Shoes {
	Nike, 
	Adidas
}

var myShoes = Shoes.Nike;
console.log(myShoes);   // 0
```

## 2. 문자형 Enum

```tsx
// 2. 문자열형 enum
enum ShoesString {
	Nike = 'Nike', 
	Adidas  = 'Adidas'
}

var myShoes = Shoes.Nike;
console.log(myShoes); // 'Nike'
```

## 3. Enum의 활용