- 객체 프로퍼티의 종류
1. 데이터 프로퍼티 : 우리가 지금까지 사용한 모든 프로퍼티
2. 접근자 프로퍼티 : 본질은 함수, 이 함수는 값을 획득(get)하고 설정(set)하는 역할을 담당

### getter와 setter

접근자 프로퍼티는 getter(획득자)와 setter(설정자) 메서드로 표현된다.

```jsx
let obj = {
  get propName() {
    // getter, obj.propName을 실행할 때 실행되는 코드
  },

  set propName(value) {
    // setter, obj.propName = value를 실행할 때 실행되는 코드
  }
};
```

```jsx
let user = {
  name: "John",
  surname: "Smith",

  **get fullName() {
    return `${this.name} ${this.surname}`;
  },**

  **set fullName(value) {
    [this.name, this.surname] = value.split(" ");
  }**
};

// 주어진 값을 사용해 set fullName이 실행됩니다.
user.fullName = "Alice Cooper";

alert(user.name); // Alice
alert(user.surname); // Cooper
```

이렇게 getter와 setter 메서드를 구현하면 객체엔 `fullName`이라는 '가상’의 프로퍼티가 생긴다. 가상의 프로퍼티는 읽고 쓸 순 있지만 실제로는 존재하지 않는다.



### 접근자 프로퍼티 설명자



- 접근자 프로퍼티는 다음과 같은 설명자를 갖는다.
    - **`get`** – 인수가 없는 함수, 프로퍼티를 읽을 때 동작함
    - **`set`** – 인수가 하나인 함수, 프로퍼티에 값을 쓸 때 호출됨
    - **`enumerable`** – 데이터 프로퍼티와 동일함
    - **`configurable`** – 데이터 프로퍼티와 동일함

```jsx
let user = {
  name: "John",
  surname: "Smith"
};

Object.defineProperty(user, 'fullName', {
  get() {
    return `${this.name} ${this.surname}`;
  },

  set(value) {
    [this.name, this.surname] = value.split(" ");
  }
});

alert(user.fullName); // John Smith

for(let key in user) alert(key); // name, surname
```

### getter와 setter 똑똑하게 활용하기

getter와 setter를 ‘실제’ 프로퍼티 값을 감싸는 래퍼(wrapper)처럼 사용하면, 프로퍼티 값을 원하는 대로 통제할 수 있다.

```jsx
let user = {
  get name() {
    return this._name;
  },

  set name(value) {
    if (value.length < 4) {
      alert("입력하신 값이 너무 짧습니다. 네 글자 이상으로 구성된 이름을 입력하세요.");
      return;
    }
    this._name = value;
  }
};

user.name = "Pete";
alert(user.name); // Pete

user.name = ""; // 너무 짧은 이름을 할당하려 함
```