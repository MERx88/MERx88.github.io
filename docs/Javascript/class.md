---
layout: default
title: 👨‍👦‍👦 Class
parent: Javascript
nav_order: 7
---

# 클래스

객체지향에 꼭 필요한 쉐끼!

## Intro

자바스크립트는 프로토타입 기반 객체지향 언어다.

즉, 다른언어와 달리 클래스가 필요없는 객체지향 프로그래밍 언어이다.

> 자바스크립트에서 클래스는 함수다!!!!!!

클래스는 es6에서 도입되었다. 새로운 객체 생성 매커니즘이며, 클래스 기반 객체 지향 처럼 사용하기 위해 만들어졌다. 속을 뜯어보면 프로토타입기반 객체지향이라는 것은 변함이 없다.

## 클래스에 대한 여러가지 사실들

클래스는 함수와 같이 일급객체다 (왜냐면 클래스가 함수니까 당연한거다)

- 무명의 리터럴로 생성가능하다. 즉, 런타임에 생성가능하다.
- 변수나 자료구조에 저장할 수있다.
- 함수의 매개변수에게 전달가능하다.
- 함수의 반환 값으로 사용가능하다.

> 클래스도 호이스팅은 일어난다. 단 변수처럼 일어난다.

> 클래스는 함수라고 했는데 정확히 말하면 인스턴스를 생성하기 위한 생성자 함수다.

**인스턴스 생성**

- new를 사용해야한다!
- 당연히 클래스 표현식에서 사용한 클래스 이름은 외부 코드에서 접근 불가 하다

```js
class Person {}

// 인스턴스 생성
const me = new Person();
console.log(me); //Person{}
```

### 메서드

**constructor**

인스턴스를 생성하고 초기화 하기 위한 특수한 메서드

```js
class Person {
  constructor(name) {
    this.name = name;
  }
}
```

this에 추가한 프로퍼티는 인스턴스의 프로퍼티가 된다.

인스턴스에는 constructor 메서드가 보이지 않는데 이는 단순한 메서드가 아님을 의미한다. 무슨 소리냐

클래스가 평가되어 생성자 함수 객체 코드의 일부가 된다는 것이다. 즉, 클래스 정의가 평가되면 constructor에 기술된 동작을 하는 함수 객체가 만들어진다는 것이다.

constructor 특징

- constructor는 클래스내에 최대한개만 존재가능하다
- constructor는 생략할수있지만 빈 constructor 자동으로 선언되고 빈 constructor에 의해 빈객체를 생성하게 된다.
- constructor에 초기 값을 넘겨 생성될때 프로퍼티를 설정하거나 고정값을 넣어 고정된 프로퍼티를 만들수도 있다.
- constructor는 별도의 반환문을 가지면 안된다. 암묵적으로 this 즉, 인스턴스를 반환한다. (만약 반환값을 설정하면 그 반환값이 할당된다 그러므로 클래스로 인스턴스를 만드는 행위가 변질될수있다)

> 인스턴스를 초기화 하기 위해선 constructor를 생략해선 안된다

{ .important }

> 프로토타입 constructor 와 class의 constructor는 다르며 직접적인 관련이 없다
>
> 프로토타입 constructor는 생성자 함수를 가르키며 vmfhvjxldlek.
>
> class constructor는 함수객체이다

**prototype method**

```js
class Person {
  constructor(name) {
    this.name = name;
  }

  sayHi() {
    console.log(`hi!`);
  }
}

const me = new Person("Lee");
me.sayHi(); // hi!
```

걍 선언하면 프로토타입 메서드가 된다

![프로토타입 메서드](image-7.png)

클래스가 생성한 인스턴스는 프로토타입 체인의 일원이 된다.

자바스크립트가 생성자함수를 통해 객체를 생성하는 방식 그대로 클래스도 따른다. 클래스가 생성자함수의 역할을 할 뿐이다

즉, 클래스는 프로토타입기반 객체 생성 매커니즘이다

> 위그림의 constructor는 당연하게도 자바스크립트가 객체를 만들어낼때 생겨나는 프로토타입의 프로퍼티이다!

**static method**

```js
class Person {
  constructor(name) {
    this.name = name;
  }

  static sayHi() {
    console.log(`hi!`);
  }
}
```

static을 붙여 선언할수있다.

![alt text](image-8.png)

위 그림과 같이 클래스 즉, 생성자함수에 바인딩된다.

그렇기 때문에 인스턴스 생성 없이 바로 호출이 가능하다

```js
Person.sayHi(); //hi!
```

**static vs prototype**

1. 서로 속해있는 프로토타입 체인이 다르다
2. 정적 메서드는 클래스로 프로토타입은 인스턴스로 호출한다
3. 정적메서드는 인스턴스 프로퍼티를 참조할수없지만 프로토타입 메서드는 참조가능하다

**클래스 메서드들 특징**

- 암묵적으로 strict mode에서 실행된다.
- 열거 불가능
- new 연산자와 함께 호출 불가능

### 프로퍼티

**인스턴스 프로퍼티**

```js
class Person {
  constructor(name) {
    this.name = name;
  }
}
```

인스턴스 프로퍼티는 constructor 내부에서 정의 해야한다.

그러면 this 에 바인딩되어있는 인스턴스에 프로퍼티가 초기화된다

**접근자 프로퍼티**

```js
class Person {
  constructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }

  get fullName(name){
    return `${this.firstName}${this.lastName}`
  }
  set fullName(name){
    [this.firstName, this.lastName]=name.split(' ');
  }
}

const me = new Person("ungmo", "Lee");
me.fullname = 'sh jang'
console.log(me.fullname)//sh jang
```

위와 같이 접근자 프로퍼티를 선언할수도 있다.

getter setter 함수로 구성된 프로퍼티다 위와 같이 getter setter 함수만 선언하면 일반 프로퍼티 처럼 사용할수있다

근데 여기서 중요한건 프로토타입 메서드로 선언되기 때문에 프로퍼티또한 프로토타입의 프로퍼티가 된다.

**클래스 필드**

클래스 필드 == 인스턴스의 프로퍼티

인스턴스 프로퍼티는 constructor를 사용해서 정의할수도 있고 클래스 필드에다가 정의할수도 있다. 하지만 중요한건 초기화를 어떤 값으로 해야하다면 꼭 constructor를 사용하자

**private 필드**

자바스크립트는 캡슐화를 완벽하게 지원하지는 않는다.

즉, 접근제한자를 지원하지 않는다. 인스턴스프로퍼티는 언제나 퍼블릭했었다

하지만...

업그레이드가 되어서 현재는 private한 필드를 정의할수 있게 되었다.

```js
class Person {
  #name = "";
  constructor(name) {
    this.#name = name;
  }
}
```

변수 명 앞에 #을 붙여 사용할수있다.

> private 필드는 클래스 내부에서만 참조가능하다!!!

> private 필드는 클래스 몸체에 선언해야한다 constructor에는 선언 불가능하다

**static 필드**

static 키워드를 사용해 정적 필드를 정의 할 수있다.

```js
class Person {
  static justName = "name";
}

console.log(Person.justName); //name
```
