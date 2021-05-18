#   Lambda와 함수형 인터페이스
##  개념
- 익명 함수를 의미합니다.
- 람다식으로 구현하는 방식을 함수형 프로그래밍이라고 합니다.
- 함수형 프로그래밍에서 개발자는 핵심 내용만 구현하고, 나머지는 Java에서 자동으로 처리합니다.
- 함수형 스타일은 서술형 스타일에 객체의 개념과 명령문을 추가하여 처리하는 스타일입니다.

##  인터페이스를 람다식으로 구현
- 람다식으로 구현하려는 인터페이스는 반드시 1개의 메서드만 선언되어야 합니다.
- 1개의 메서드만 구현된 인터페이스를 `함수형 인터페이스`라고 합니다.
- 기본 문법
  - 명령문이 1개일 때 : `() -> 명령문;`
  - 명령문이 여러 개일 때 : `() -> {명령문1; 명령문2; ... 명령문n;}`
- @FunctionalInterface
  - 함수형 인터페이스를 구현할 때, 2개 이상의 추상 메서드 선언되는 오류를 방지하기 위해서 `@FunctionalInterface` 어노테이션을 사용할 수 있습니다.
- 매개 변수가 있는 람다식의 문법
  - `(변수명) -> 명령문;`
  - `(변수명1, 변수명2 ... 변수명n) -> 명령문;`
  - 변수명 앞에는 타입을 지정할 수도 있지만 굳이 지정하지 않습니다.
  - Java에서 추상 메서드의 매개변수 타입으로 알아서 처리해줍니다.
- 람다식 블록
  - 람다식의 명령문이 1개라면 `{}`를 지정하지 않습니다.
  - 명령문이 1개일 때, return을 명시하지 않아도 됩니다.
  - 명령문이 2개 이상일 때에는 람다식 명령문을 `{}`으로 감쌉니다.
  - 명성문이 2개 이상일 때에는 return을 명시해야 합니다.
- 제네릭 함수형 인터페이스에서 타입 인자는 람다식을 참조하는 참조변수에서 지정해야 합니다.
  - 람다식 내부에서는 제네릭을 사용할 수 없습니다.
  - `인터페이스명<타입 인자> 변수명 = () -> 명령문;`

##  람다식의 활용
- 람다식은 구현과 동시에 객체를 생성합니다. 따라서 람다식도 인자로 전달할 수 있습니다.
- 참조 변수를 통하지 않고도 인자 지정 부분에 람다식을 직접 선언할 수도 있습니다.
- 인자로 전달된 람다식을 받는 매개변수의 타입은 람다식이 구현한 인터페이스입니다.
- 람다식을 인자로 직접 지정하는 예는 기본 API에서 제공하는 함수형 인터페이스를 사용할 때입니다.
- 람다식에서 예외를 발생하게 하려면 반드시 함수형 인터페이스의 추상메서드 선언에서 `throws`를 지정해주어야 합니다.
- 람다식을 구현할 때 필드는 값을 사용하거나 수정할 수 있지만, 지역변수는 사용할 수만 있고 수정할 수 없습니다.

##  메서드 참조(Method Reference)
- 람다식 본문에 로직을 구현하다보면 가독성이 떨어질 수 있습니다.
  - 람다식을 메서드 형태로 구현하는 기능을 제공합니다.
- 메서드 참조는 지정한 메서드로 인터페이스의 추상 메서드를 구현한 객체를 생성합니다.
- 람다식을 구현하는 메서드의 리턴타입과 매개변수는 함수형 인터페이스의 추상 메서드와 동일해야 합니다.
  - `클래스명::메서드명`  static 메서드로 인터페이스 객체를 생성합니다.
  - `참조변수명::메서드명`  인스턴스 메서드로 인터페이스 객체를 생성합니다.

##  함수형 인터페이스 API
- `JDK 1.8` 이후로 Java에서는 기본 함수형 인터페이스를 제공하고 있습니다.
- 함수형 인터페이스는 `java.util.function` 패키지에서 제공합니다.
- 함수형 인터페이스
  - `Function<T, R>`
    - `R apply(T)` : T 타입 인자를 처리한 후 R 타입 값을 반환합니다.
  - `Predicate<T>`
    - `boolean test(T)` : T 타입 인자를 처리한 후 boolean 값을 반환합니다.
  - `Consumer<T>`
    - `void accept(T)` : T 타입 인자를 처리한 후 어떤 값도 반환하지 않습니다.
  - `Supplier<T>`
    - `T get()` : 어떠한 인자도 받지 않고 T 타입 값을 반환합니다.