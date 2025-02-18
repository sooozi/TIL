- **`prototype`** : **함수(특히 생성자 함수)**에만 존재하는 속성. 이 속성은 해당 함수를 통해 생성된 **인스턴스 객체의 프로토타입**이 된다. 예를 들어, `Rabbit.prototype`은 `new Rabbit()`으로 생성된 모든 객체가 참조하게 될 프로토타입
- **`__proto__`** : **모든 객체**에 존재하는 속성. 해당 객체가 상속하는 **프로토타입을 참조**한다. 즉, `__proto__`는 객체의 실제 프로토타입을 가리킨다.

```jsx
let animal = {
  eats: true
};

// Rabbit 생성자 함수
function Rabbit(name) {
  this.name = name;
}

**// Rabbit 생성자 함수의 prototype을 animal로 설정
Rabbit.prototype = animal;**

// 새로운 Rabbit 인스턴스 생성
let rabbit = new Rabbit("흰 토끼");

// rabbit 객체의 __proto__는 Rabbit.prototype, 즉 animal을 참조
console.log(rabbit.name);   // "흰 토끼" (rabbit 자체 속성)
console.log(rabbit.eats);   // true (animal에서 상속된 속성)

**// rabbit 객체의 __proto__는 Rabbit.prototype이므로
// rabbit.__proto__는 animal 객체를 가리킵니다.
console.log(rabbit.__proto__ === animal);   // true

// Rabbit 함수 자체의 prototype 속성
console.log(Rabbit.prototype === animal);   // true**
```

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/681aabec-185e-44d0-b64b-3d352bfbfae8/753d4cd1-b42b-4f8f-bf43-19c5c192fcfc/image.png)

### 함수의 디폴트 프로퍼티 prototype과 constructor 프로퍼티

모든 함수는 기본적으로 prototype 프로퍼티를 갖는다. 디폴트 프로퍼티 prototype은 constructor(객체를 생성하는 함수) 프로퍼티 하나만 있는 객체를 가리키는데, 여기서 constructor 프로퍼티는 함수 자신이다.

```jsx
function Rabbit() {}

/* 디폴트 prototype
Rabbit.prototype = { constructor: Rabbit };
*/
```

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/681aabec-185e-44d0-b64b-3d352bfbfae8/45c20999-4161-4a30-8fcf-076e70408237/image.png)

- 예시
    
    ```jsx
    function Rabbit() {}
    // 함수를 만들기만 해도 디폴트 프로퍼티인 prototype이 설정됩니다.
    // Rabbit.prototype = { constructor: Rabbit }
    
    alert( Rabbit.prototype.constructor == Rabbit ); // true
    
    let rabbit = new Rabbit(); // {constructor: Rabbit}을 상속받음
    alert(rabbit.constructor == Rabbit); // true ([[Prototype]]을 거쳐 접근함)
    ```
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/681aabec-185e-44d0-b64b-3d352bfbfae8/33ee939f-c19f-4dd4-bc66-3fae06c92a42/image.png)
    
- **constructor 프로퍼티**는 기존에 있던 객체의 constructor를 사용해 새로운 객체를 만들 수 있다.
    
    ```jsx
    function Rabbit(name) {
      this.name = name;
      alert(name);
    }
    
    let rabbit = new Rabbit("흰 토끼");
    **let rabbit2 = new rabbit.constructor("검정 토끼");**
    ```
    
- prototype을 덮어쓰면 기본으로 설정된 constructor가 사라진다.
    
    ```jsx
    function Rabbit() {}
    
    // Rabbit.prototype을 완전히 덮어쓰기
    Rabbit.prototype = {
      jumps: true
    };
    
    let rabbit = new Rabbit();
    
    // rabbit.constructor는 이제 Rabbit이 아님
    console.log(rabbit.constructor === Rabbit); // false
    
    //이때는 constructor를 수동으로 다시 설정
    Rabbit.prototype.constructor = Rabbit; // 수동으로 복구
    ```
    

---