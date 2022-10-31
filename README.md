# Spring-Core-Theory
Learn about Spring deeply 🎞🕶📽

### ⭐ 역할과 구현으로 구분하는 것이 무엇보다 중요하다.
### ⭐ 좋은 개발 습관은 제약을 두는 것이다.
### SOLID Principle🖐👴
- 클린코드로 유명한 로버트 마틴이 좋은 객체 지향 설계의 5가지 원칙을 정리
- SRP : 단일 책임 원칙(Single Responsibility Principle)
- OCP : 개방-폐쇄 원칙(Open/Closed Principle)
- LSP : 리스코프 치환 원칙(Liskov Substitution Principle)
- ISP : 인터페이스 분리 원칙(Interface Segregation Principle)
- DIP : 의존관계 역전 원칙(Dependency Inversion Principle)

1. SRP 단일 책임 원칙  
Single Responsibility Principle
   - 한 클래스는 하나의 책임만 가져야한다.
   - 하나의 책임이라는 것은 모호하다. 클 수 있고, 작을 수 있다. 문맥과 상황에 따라 다르다.
   - 중요한 기준은 변경이다. 변경이 있을 때 파급 효과가 적으면 단일 책임 원칙을 잘 따른 것이다.
   - 예) UI 변경, 객체의 생성과 사용을 분리

2. OCP 개방-폐쇄 원칙  
Open/Closed Principle
   - 소프트웨어 요소는 확장에는 열려 있으나 변경에는 닫혀 있어야 한다.
   - 다형성을 활용해보자
   - 인터페이스를 구현한 새로운 클래스를 하나 만들어서 새로운 기능을 구현
   - 지금까지 배운 역할과 구현의 분리를 생각해보자

3. LSP 리스코프 치환 원칙  
Liskov Substitution Principle
   - 프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야한다.
   - 다형성에서 하위 클래스는 인터페이스 규약을 다 지켜야 한다는 것, 다형성을 지원하기 위한 원칙, 인터페이스를 구현한 구현체를 믿고 사용하려면 이 원칙이 필요하다.
   - 단순히 컴파일에 성공하는 것을 넘어서는 이야기
   - 예) 자동차 인터페이스의 엑셀은 앞으로 가라는 기능, 뒤로 가게 구현하면 LSP 위반, 느리더라도 앞으로 가야함

4. ISP 인터페이스 분리 원칙  
Interface Segregation Principle
   - 특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다.
   - 자동차 인터페이스 -> 운전 인터페이스, 정비 인터페이스로 분리
   - 사용자 클라이언트 -> 운전자 클라이언트, 정비사 클라이언트로 분리
   - 분리하면 정비 인터페이스 자체가 변해도 운전자 클라이언트에 영향을 주지 않음
   - 인터페이스가 명확해지고, 대체 가능성이 높아진다.

5. DIP 의존관계 역전 원칙  
Dependency Inversion Principle
   - 프로그래머는 "추상화에 의존해야지, 구체화에 의존하면 안 된다." 의존성 주입은 이 원칙을 따르는 방법 중 하나다.
   - 쉽게 이야기해서 구현 클래스에 의존하지 말고, 인터페이스에 의존하라는 뜻
   - 앞에서 이야기한 역할(Role)에 의존하게 해야 한다는 것과 같다. 객체 세상도 클라이언트가 인터페이스에 의존해야 유연하게 구현체를 변경할 수 있다.
   - 구현체에 의존하게 되면 변경이 아주 어려워진다.
---
### IoC, DI, Container 🕋 -> 🪑🚪🧳
1. 제어의 역전 IoC(Inversion of Control)
   - 기존 프로그램은 클라이언트 구현 객체가 스스로 필요한 서버 구현 객체를 생성하고, 연결하고, 실행했다.
   - 반면에 AppConfig가 등장한 이후에 구현 객체는 자신이 로직을 실행하는 역할만 담당한다. 프로그램의 제어 흐름은 이제 AppConfig가 가져간다. 예를들어서 'OrderServiceImpl'은 필요한 인터페이스들을 호출하지만 어떤 구현 객체들이 실행될지 모른다.
   - 프로그램에 대한 제어 흐름에 대한 권한은 모두 AppConfig가 가지고 있다. 심지어 'OrderServiceImpl'도 AppConfig가 생성한다. 그리고 AppConfig는 'OrderServiceImpl'이 아닌 OrderService 인터페이스의 다른 구현 객체를 생성하고 실행할 수도 있다. 그런 사실도 모른체 'OrderServiceImpl'은 묵묵히 자신의 로직을 실행할 뿐이다.
   - 이렇듯 프로그램의 제어 흐름을 직접 제어하는 것이 아니라 외부에서 관리하는 것을 제어의 역전(IoC)이라고 한다.

2. 의존관계 주입 DI(Dependency Injection)
   - 'OrderServiceImpl'은 'DiscountPolicy' 인터페이스에 의존한다. 실제 어떤 구현 객체가 사용될지는 모른다.
   - 의존관계는 `정적인 의존 관계와, 실행 시점에 결정되는 동적인 객체(인스턴스) 의존 관계`들을 분리해서 생각해야 한다.

   1. `정적인 클래스 의존 관계`
      - 클래스가 사용하는 import 코드만 보고 의존관계를 쉽게 판단할 수 있다. 정적인 의존관계는 애플리케이션을 실행하지 않아도 분석할 수 있다.

   2. `동적인 객체 인스턴스 의존 관계`
      - 애플리케이션 실행 시점에 실제 생성된 객체 인스턴스의 참조가 연결된 의존 관계다.
      - 애플리케이션 '실행 시점(런타임)'에 외부에서 실제 구현 객체를 생성하고 클라이언트에 전달해서 클라이언트와 서버의 실제 의존관계가 연결 되는 것을 '의존관계 주입'이라한다.
      - 객체 인스턴스를 생성하고, 그 참조값을 전달해서 연결된다.
      - 의존관계 주입을 사용하면 클라이언트 코드를 변경하지 않고, 클라이언트가 호출하는 대상의 타입 인스턴스를 변경할 수 있다.
      - 의존관계 주입을 사용하면 정적인 클래스 의존관계를 변경하지 않고, 동적인 객체 인스턴스 의존관계를 쉽게 변경할 수 있다.

3. IoC 컨테이너, DI 컨테이너
   - AppConfig처럼 객체를 생성하고 관리하면서 의존관계를 연결해 주는 것을 IoC컨테이너 또는 `DI 컨테이너`라 한다.
   - 의존관계 주입에 초점을 맞추어 최근에는 주로 DI 컨테이너라 한다.
   - 또는 어셈블러, 오브젝트 팩토리 등으로 불리기도 한다.
---
### Singleton Container and Pattern 🎲 🗃
1. Singleton Container
   - 웹 애플리케이션 싱글톤
   - 스프링은 태생이 기업용 온라인 서비스 기술을 지원하기 위해 탄생했다.
   - 대부분의 스프링 애플리케이션은 웹 애플리케이션이다. 물론 웹이 아닌 애플리케이션 개발도 얼마든지 개발할 수 있다.
   - 웹 애플리케이션은 보통 여러 고객이 동시에 요청을 한다.

2. Singleton Pattern
   - 클래스의 인스턴스가 딱 1개만 생성되는 것을 보장하는 디자인 패턴이다.
   - 그래서 객체 인스턴스를 2개 이상 생성하지 못 하도록 막아야 한다.
   - private 생성자를 사용해서 외부에서 임의로 new를 막아야한다.

3. Singleton Container의 장점과 주의점(실무에서 중요)
   1. `장점`
      - 스프링 컨테이너는 싱글톤 패턴의 문제점을 해결하면서, 객체 인스턴스를 싱글톤(1개만 생성)으로 관리한다. 지금까지 우리가 학습한 스프링 빈이 바로 싱글톤으로 관리되는 빈이다.
      - 스프링 컨테이너는 싱글톤 패턴을 적용하지 않아도, 객체 인스턴스를 싱글톤으로 관리한다. 이전에 설명한 컨테이너 생성 과정을 자세히 보자. 컨테이너는 객체를 하나만 생성해서 관리한다.
      - 스프링 컨테이너는 싱글톤 컨테이너 역할을 한다. 이렇게 싱글톤 객체를 생성하고 관리하는 기능을 싱글톤 레지스트리라 한다.
      - 스프링 컨테이너의 이런 기능 덕분에 싱글톤 패턴의 모든 단점을 해결하면서 객체를 싱글톤으로 유지할 수 있다.
   2. `주의점`
      - 싱글톤 패턴이든, 스프링 같은 싱글톤 컨테이너를 사용하든, 객체 인스턴스를 하나만 생성해서 공유하는 싱글톤 방식은 여러 클라이언트가 하나의 같은 객체 인스턴스를 공유하기 때문에 싱글톤 객체는 상태 유지(stateful)하게 설계하면 안 된다.
      - 무상태(stateless)로 설계해야한다.
      - 특정 클라이언트에 의존적인 필드가 있으면 안 된다.
      - 특정 클라이언트가 값을 변경할 수 있는 필드가 있으면 안 된다.
      - 가급적 읽기만 가능해야 한다.
      - 필드 대신에 자바에서 공유되지 않은, 지역변수, 파라미터, ThreadLocal등을 사용해야 한다.
      - 스프링 빈의 필드에 공유 값을 설정하면 정말 큰 장애가 발생할 수 있다.
---
### Various Dependency Injection Ways 💉🧬
스프링 라이프 사이클에서 스프링 빈을 등록하는 단계랑 스프링 의존관계를 주입하는 단계가 구분되어있다.
- 생성자 주입
- 수정자 주입(setter 주입)
- 필드 주입
- 일반 메서드 주입

1. 생성자 주입
   - 이름 그대로 생성자를 통해서 의존관계를 주입 받는 방법이다.
   - 지금까지 우리가 진행했던 방법이 바로 생성자 주입이다.
   - `특징`
     - 생성자 호출 시점에 딱 1번만 호출되는 것이 보장된다.
     - `* 불변, 필수 *` 의존관계에 사용
     - 클래스 내의 생성자가 딱 1개일 경우는 @Autowired를 생략해도 된다.

2. 수정자 주입(setter 주입)
   - setter라 불리는 필드의 값을 변경하는 수정자 메서드를 통해서 의존관계를 주입하는 방법이다.
   - `특징`
     - `* 선택, 변경 *` 가능성이 있는 의존관계에 사용
     - 자바빈 프로퍼티 규약의 수정자 메서드 방식을 사용하는 방법이다.

3. 필드 주입
   - 이름 그대로 필드에 바로 주입하는 방법이다.
     (* 안티 패턴)
   - `특징`
     - 코드가 간결해서 많은 개발자들을 유혹하지만 외부에서 변경이 불가능해서 테스트하기 힘들다는 치명적인 단점이 있다.
     - DI 프레임워크가 없으면 아무것도 할 수 없다.
     - 사용하지말자!
       - (예외) 애플리케이션의 실제 코드와 관계 없는 테스트 코드에선 사용 가능
       - (예외) 스프링 설정을 목적으로 하는 @Configuration 같은 곳에서만 특별한 용도로 사용

4. 일반 메서드 주입
   - 일반 메서드를 통해서 주입 받을 수 있다.
   - `특징`
     - 한번에 여러 필드를 주입 받을 수 있다.
     - 일반적으로 잘 사용하지 않는다.