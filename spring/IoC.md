## IoC 란
- 제어의 역전(Inversion of Control) 이란, 프로그램의 제어 흐름을 직접 제어하는 것이 아니라 외부에서 관리하는 것을 의미
### 기존 프로그램
- 클라이언트 구현 객체가 스스로 필요한 서버 구현 객체를 생성/연결/실행
- 구현 객체가 프로그램의 제어 흐름을 스스로 조정함

```
public class Order {

    private final String itemName;
    private final int itemPrice;
    private final int discountPrice;

    public Order(String itemName, int itemPrice, int discountPrice) {
        this.itemName = itemName;
        this.itemPrice = itemPrice;
        this.discountPrice = discountPrice;
    }

    public int getDiscountPrice() {
        return discountPrice;
    }
}

public interface OrderService {

    Order createOrder(int age, String itemName, int itemPrice);
}

public class OrderServiceImpl implements OrderService {

    private final DiscountPolicy discountPolicy = new FixDiscountPolicy();

    @Override
    public Order createOrder(int age, String itemName, int itemPrice) {
        int discountPrice = discountPolicy.discount(age, itemPrice);
        return new Order(itemName, itemPrice, discountPrice);
    }
}
```
- OrderService 의 구현 객체인  OrderServiceImpl 에서 주문이 발생. 인자로 나이, 제품이름, 가격을 입력하면, Order 객체를 반환함.
- 다만 OrderServiceImpl 는 DiscountPolicy 를 의존함.
- 이 할인 정책 종류에 따라 할인 금액이 정해짐.

```
public interface DiscountPolicy {

    int discount(int age, int price);
}

public class FixDiscountPolicy implements DiscountPolicy {

    private static final int ADULT = 20;
    private static final int DISCOUNT_FIX_AMOUNT = 1000;

    @Override
    public int discount(int age, int price) {
        if (age < ADULT) {
            return DISCOUNT_FIX_AMOUNT;
        }
        return 0;
    }
}

public class RateDiscountPolicy implements DiscountPolicy {

    private static final int ADULT = 20;
    private static final int DISCOUNT_PERCENT = 10;

    @Override
    public int discount(int age, int price) {
        if (age < ADULT) {
            return price * DISCOUNT_PERCENT / 100;
        }
        return 0;
    }
}
```
```
public class Main {

    public static void main(String[] args) {
        final OrderService orderService = new OrderServiceImpl();
        final Order order = orderService.createOrder(10, "샤프", 3000);
        System.out.println(order.getDiscountPrice());
    }
}
```
- 여기서는 일단 서비스에서는 고정 할인 정책을 수용한다고 가정.
- 그렇다면 사용자 입장에서는 OrderService 객체를 만들고 주문을 진행하여 할인된 금액을 알아낼 수 있음

![image](https://user-images.githubusercontent.com/109256744/189495451-11ed8d2e-9599-4a89-bc6f-60d6af894224.png)

- 지금까지의 도메인 구조
- OrderServiceImpl 은 DiscountPolicy 와 FixDiscountPolicy 를 모두 의존함. 

- 만약 할인 정책에 변경이 생긴다면, OrderServiceIpml 의 코드를 수정해야 함
- 만약 해당 할인 정책을 의존하는 객체가 많고 로직이 많다면, 모두 다 수정해야 함
- OCP 법칙에 어긋남
```
new FixDiscountPolicy() -> new RateDiscountPolicy()
```

- 이를 해결하는 방법은 OrderServiceImpl 내에서 DiscountPolicy 의 구현 객체를 정해지주지 않으면 됨
- 그렇다고 코드를 아래와 같이 바꾸면, NullPointerException 이 발생함. 너무 나도 당연함.

```
public class OrderServiceImpl implements OrderService {

    private final DiscountPolicy discountPolicy;

    @Override
    public Order createOrder(int age, String itemName, int itemPrice) {
        int discountPrice = discountPolicy.discount(age, itemPrice);
        return new Order(itemName, itemPrice, discountPrice);
    }
}
```

- 이를 해소하기 위해서 외부에서 DiscountPolicy 를 주입해 주어야 함.
- 이때 의존성 주입(DI) 이 사용됨. 
### 개선안

#### 방법 1 :  Constructor 를 통해 DiscountPolicy 초기화

```
public class OrderServiceImpl implements OrderService {

    private final DiscountPolicy discountPolicy;

    public OrderServiceImpl(DiscountPolicy discountPolicy) {
        this.discountPolicy = discountPolicy;
    }
    @Override
    public Order createOrder(int age, String itemName, int itemPrice) {
        int discountPrice = discountPolicy.discount(age, itemPrice);
        return new Order(itemName, itemPrice, discountPrice);
    }
}
```
- 하지만, 이를 위해서 OrderService 를 사용할 때, 구현 객체를 정해줘야 함. 
- 조금 flexable 하지만, 매번 특정 객체를 만들어어 주어야 한다는 문제가 있음. 그래서 해당 객체를 주입해 주는 역활만 하는 설정 관련 객체를 새로 정의

#### 방법 2 : 해당 객체를 주입해 주는 역활만 하는 설정 관련 객체를 새로 정의
```
public class AppConfig {

    public OrderService orderService() {
        return new OrderServiceImpl(discountPolicy());
    }

    public FixDiscountPolicy discountPolicy() {
        return new FixDiscountPolicy();
    }
}

public class Main {

    public static void main(String[] args) {
        final AppConfig appConfig = new AppConfig();
        final OrderService orderService = appConfig.orderService();
        final Order order = orderService.createOrder(10, "샤프", 3000);
        System.out.println(order.getDiscountPrice());
    }
}
```
- AppConfig 는 프로그램 전반적으로 사용될 객체를 미리 정의해 둠. 
- 사용자 입장에서 무슨 할인 정책을 사용할지 선택할 필요 없음
- 단순히 AppConfig 로부터 제공받는 객체를 사용함. 
- 만약 할인 정책이 바뀐다면, AppConfig 에서 DixDiscountPolicy 를 RateDiscountPolicy 로 바꿈. 

```
public class OrderServiceImpl implements OrderService {

    private final DiscountPolicy discountPolicy;

    public OrderServiceImpl(DiscountPolicy discountPolicy) {
        this.discountPolicy = discountPolicy;
    }

    @Override
    public Order createOrder(int age, String itemName, int itemPrice) {
        int discountPrice = discountPolicy.discount(age, itemPrice);
        return new Order(itemName, itemPrice, discountPrice);
    }
}
```
- OrderServiceImpl 은 할인 정책이 바뀌어도 상관없음. 
#### 정리
- 구현 객체는 자신의 로직을 실행하는 역할만 담당.
- 프로그램의 제어 흐름은 AppConfig 가 가져감.
- 예를 들어 OrderServiceImpl 은 필요한 인터페이스들을 호출하지만 어떤 구현 객체들이 실행될 지 모르고 있음.
- 또한 OrderServiceImpl 자체도 AppConfig 가 생성하고 있으므로, AppConfig 는 OrderServiceImpl 이 아닌 OrderService 의 또란 하위 구현 객체를 정의하여 사용자에게 넘겨줄 수도 있음. 
- 이렇게 프로그램의 제어 흐름을 개발자가 직접 제어하는 것이 아니라 외부에서 관리하는 것을 제어의 역전이라고 함. 
- 이 예시에서 외부는 AppConfig 가 됨. 

> 지금 예제에서는 의존성 주입을 생성자 방식을 사용했지만, setter 문, 스프링의 경우 @Autuwired annotation 을 통해서도 가능함.

## IoC Container / DI Container
- 이렇게 AppConfig 처럼 객체를 생성하고, 관리하면서 의존 관계를 연결해주는 것을 IoC container / DI container 라고 함. 
- 최근에는 의존 관계 자체에 초점을 맞추어 DI 컨테이너라고 함.


