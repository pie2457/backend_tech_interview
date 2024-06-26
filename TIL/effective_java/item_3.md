## "생성자나 열거 타입으로 싱글톤임을 보증하라."
### 싱글톤 개념
싱글톤(singleton)이란 인스턴스를 오직 하나만 생성할 수 있는 클래스를 말한다. 싱글톤의 전형적인 예로는 무상태 객체나
설계상 유일해야 하는 시스템 컴포넌트를 들 수 있다. 하지만 인터페이스로 정의하고 그것을 구현해서 만든 싱글톤 클래스가 아니라면 
테스트하기 어려워질 수 있다는 문제가 발생한다.
### 싱글톤을 만드는 방법 : public static 멤버가 final 필드인 방식
```java
public class Elvis {
  public static final Elvis INSTANCE = new Elvis();

  private Elvis() {}

  public void sing() {
    System.out.println("sing ~ ");
  }

  public static void main(String[] args) {
    Elvis elvis = Elvis.INSTANCE;
    elvis.sing();
  }
}
```
private 생성자는 public static final 필드인 Elvis.INSTANCE를 초기화할 때 딱 한번만 호출된다. public이나 protected 생성자가
없으므로 Elvis 클래스가 초기화될 때 만들어진 인스턴스가 전체 시스템에서 하나뿐임이 보장된다. 단, AccessibleObject.setAccessible()을 사용하여
private 생성자를 호출할 수 있는데, 이러한 리플렉션으로 변조하는 방법은 2번째 객체가 생성될 때 예외를 던져서 막을 수 있다. 
- 장점
  - 해당 클래스가 싱글톤임이 API에 명백히 드러난다.
  - 간결하다.
- 단점 : 싱글톤을 사용하는 클라이언트 코드를 테스트하기 어려워진다.
 
