자바스크립트는 단일 상속만을 허용하는 언어, 하나의 클래스는 오직 하나의 다른 클래스만 상속 가능하다.

하지만 믹스인을 사용하면 기능 추가 가능하다!

### 믹스인(mixin)

**단일 상속 제한 극복을 위해 믹스인 사용**

: 특정 행동(메서드)을 실행하는 코드를 제공하는 클래스

: 다른 클래스와 함께 사용되며, 단독으로는 사용되지 않음

: 믹스인을 사용하면 여러 클래스의 기능 조합 가능

- 예시
  // 믹스인
let sayHiMixin = {
  sayHi() {
    alert(`Hello ${this.name}`);
  },
  sayBye() {
    alert(`Bye ${this.name}`);
  }
};

// 사용법:
class User {
  constructor(name) {
    this.name = name;
  }
}

// 메서드 복사
Object.assign(User.prototype, sayHiMixin);

// 이제 User가 인사를 할 수 있습니다.
new User("Dude").sayHi(); // Hello Dude!

let StreetSweeping = {
  sweep() {
    console.log("거리를 청소합니다!");
  }
};

// 자전거 클래스를 정의합니다.
class Bicycle {
  ride() {
    console.log("자전거를 타고 있습니다!");
  }
}

// 믹스인을 Bicycle에 추가합니다.
Object.assign(Bicycle.prototype, StreetSweeping);

let myBicycle = new Bicycle();
myBicycle.ride(); // 자전거를 타고 있습니다!
myBicycle.sweep(); // 거리를 청소합니다!