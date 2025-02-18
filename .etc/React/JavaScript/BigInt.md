: **길이 제약 없이 아주 큰 정수를 다룰 수 있게 해주는 숫자형**
정수 리터럴 끝에 `n`을 붙이거나 함수 `BigInt`를 호출하면 문자열이나 숫자를 가지고 `BigInt` 타입의 값을 만들 수 있다.

```jsx
const bigint = 1234567890123456789012345678901234567890n;

**const sameBigint = BigInt("1234567890123456789012345678901234567890");**

const bigintFromNumber = BigInt(10); // 10n과 동일합니다.
```

- BigInt 만들기
    1. 숫자 뒤에 `n`을 붙이기
        
        ```jsx
        const bigIntValue = 1234567890123456789012345678901234567890n;
        ```
        
    2. `BigInt()` 함수를 사용
        
        ```jsx
        const bigIntFromString = BigInt("1234567890123456789012345678901234567890");
        const bigIntFromNumber = BigInt(10); // 결과: 10n => n은 이 숫자가 BigInt 타입임을 나타냄
        //일반 숫자와 구분을 위해 BigInt를 나타낼 때 숫자 뒤에 n을 붙인다.
        ```
        

### 수학 연산자

`BigInt`는 대개 일반 숫자와 큰 차이 없이 사용 가능

```jsx
alert(1n + 2n); // 3
alert(5n / 2n); // 2 (소수 부분은 버려짐)
```

- 다른 타입과 혼합 불가 : `BigInt`는 일반 숫자와 혼합 불가능
    
    ```jsx
    alert(1n + 2); // Error: Cannot mix BigInt and other types
    
    **//해결방법 : 명시적으로 형 변환하기!**
    let bigint = 1n;
    let number = 2;
    
    alert(bigint + BigInt(number)); // 3
    alert(Number(bigint) + number); // 3
    ```
    

### 비교 연산자

`BigInt`는 일반 숫자와 비교 가능! `>` 같은 비교 연산자는 두 타입에 모두 사용 가능

```jsx
alert(2n > 1n); // true
alert(2n > 1); // true

**//하지만 ==와 ===의 결과가 다를 수 있음!**
alert(1 == 1n); // true
alert(1 === 1n); // false
```

### 논리 연산자

`BigInt`는 `if` 문에서 일반 숫자처럼 행동! 0n은 false로 평가, 다른 값은 true로 평가

```jsx
if (0n) {
  // 실행되지 않음
}

**//또한 ||와 && 같은 논리 연산자에서도 일반 숫자와 비슷하게 동작**
alert(1n || 2); // 1
alert(0n || 2); // 2
```