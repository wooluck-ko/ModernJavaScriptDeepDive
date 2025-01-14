# 📒19 - 프로토타입
C++ , Java : 클래스 기반의 객체지향 프로그래밍 언어
자바스크립트는 명령형, 함수형, 프로토타입기반의 객제치향형 프로그래밍 언어
원시타입(primitve) 제외한 모든것이 객체

### 객체지향 프로그래밍
객체
- 다른 것과 구별되는 속성들을 모아 하나의 단위로 만든 자료구조
- 상태 ( **프로퍼티**) 와 동작(**메서드**)을 묶은 자료구조

객체지향 프로그래밍 : 독립적인 객체의 집합으로 프로그램을 표현하려는 프로그래밍

### 상속
어떤 객체의 프로퍼티나 메서드를 받아서 사용할 수 있는 것

인스턴스(동일한 생성자 함수에서 만들어진)들이 공통적으로 사용할 `프로퍼티`나 `메서드` 를 프로토타입에 미리 구현해 둠으로써 인스턴스들이 별다른 구현 없이 상위 객체의 프로토타입 자산을 공유할 수 있다.
  
  
## 프로토타입
어떤 객체의 상위 객체 역할을 하는 객체로 하위 객체에게 자신의 프로퍼티와 메서드를 상속한다.
### 프로토타입 체인
객체의 프로퍼티나 메서드에 접근할 때 없으면 프로토타입 체인을 따라 **프로토타입의 프로퍼티와 메서드**를 차례고 검색하게 된다.


**프로토타입 객체**

- 모든 객체가 가진 것
- 하위 객체에게 상위 객체의 공유 프로퍼티(+메서드) 공유
- 상속의 개념을 구현

![](https://i.imgur.com/djz5LzI.png)

## __proto__ 프로퍼티
Object.prototype의 **접근자 프로퍼티**
- 모든객체가 가지고 있음
- 객체가 자신의 프로토타입에 간접적으로 접근하기 위해 사용하는 것
모든 객체는 상속을 통해 `__proto__` 사용 가능
`const obj = {}
obj.__proto__`

![](https://i.imgur.com/IKTK4ds.png)



**❓프로토타입에 직접 접근하지 않고 proto로 접근하는 이유**

프로토 타입은 단방향 링크드 리스트로 참조되어저야 하는데 서로 참조하는 순환참조와 같은 상황이 벌어지면 프로퍼티 검색 시 무한루프에 빠지기 때문에 접근자 프로퍼티(__proto__)를 통해 체크하고 프로토타입을 교체하게 한다.

## prototype 프로퍼티
생성자 함수의 인스턴스 프로토타입을 가리키는 값
- 함수 객체가 가지고 있음 (생성자함수로 만들어 지지 않은 `화살표함수`,`축약메서드`는 없다)
- 생성자 함수가 인스턴스의 프로토타입을 할당하기 위해 사용

#### prototype프로퍼티와 __proto__
```javascript=
//prototype프로퍼티 === __proto__접근자 프로퍼티
foo.prototype === foo1.__proto__```


리터럴로 생성된 객체는 생성자 함수에 의해 생성되는 것은 아니지만 결론적으로 객체의 역할을 동일하기 때문에 constructor 프로퍼티를 통해 연결된 생성자 함수들로 생성한다
