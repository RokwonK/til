# DI - Dependency Injection
DI는 의존성 주입이라고 부른다. 의존성 주입이란 뭐고 대체 왜 사용하는 것일까?  

```swift
class B {}
class A {
    let b: B
    init() {
        self.b = B();
    }
}
```

어떤 객체가 다른객체를 참조하고 있다면 어떤객체는 다른객체에 의존성을 지닌다.  
위의 경우에 객체A는 객체B에 의존한다.  
위와 같이 직접적(내부)으로 객체를 생성해서 넣어주는게 아닌
외부에서 객체를 생성해서 넣어주는 것(주입한다는 뜻)을 보고 `의존성 주입`이라고 한다  
이렇게 외부에서 객체 생성 후 주입하는 것을 `DI`라고 부를까?  

아니다. DI의 목표는 의존성의 분리이다.  
위의 코드를 보면 상위 계층인 A가 하위계층인 B에 의존하게 된다.  
의존성 분리는 '의존관계 역전 원칙' 으로 의존관계를 분리 시킨다.

> 의존관계 역전 원칙이란?  
소프트웨어 모듈들을 분리하는 특정 형식을 지칭. 위의 상황을 반전 시킴으로써 상위계층이 하위계층의 구현으로부터 독립한다

어떻게 의존관계를 역전시킬 수 있을까?... **protocol을 사용한다!**  
```swift
protocol NameProtocol : AnyObject {
    var name : String { get set }
}

class B : NameProtocol {
    var name = "rok"
}

class A {
    var b : NameProtocol
    init(value v : NameProtocol) {
        self.b = v
    }
}
```

구현 부분을 프로토콜로 선언하고 받아오는 객체의 타입또한 프로토콜로 설정하여 제어의 주체를 프로토콜로 바꾸는 것이다.  
이렇게 의존의 방향이 역전된 상황을 보고 IOC(Inversion Of Control)이라고 부른다.  
그렇다면 DI는 왜 필요할까?  
첫번째로 의존성 파라미터를 생성자에 작성하지 않아도 된다. protocol을 이미 구현한 객체(주입한 객체)의 메서드, 값들을 사용하면 된다.  
두번째로 protocol을 구현한 객체를 유연하게 바꾸어 사용할 수 있다.(타입은 프로토콜을 가지니 그 프로토콜을 구현한 어느객체든지 주입할 수 있다) 즉, 재활용성이 뛰어나다.  

