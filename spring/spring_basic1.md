## Spring container
- 자바 객체의 생명 주기를 관리하고 생성된 자바 객체들에게 추가적인 기능을 제공하는 역활
- 자바 객체를 스프링에서는 빈(bean) 이라고 부름
- IoC 를 이용해서 애플리케이션을 구성하는 컴포넌트를 관리함.
- ApplicationContext 를 스프링 컨테이너라고 함. 
- new 연산자의 사용, 인터페이스 호출 객체 생성/소멸을 Spring container 가 대신함.
- Single container 에서는 인스턴스를 싱글톤으로 관리하기 때문에 싱글톤 컨테이너라고도 함.
  - 싱글톤 빈을 미리 로딩해서(pre-loading) , 그 빈이 필요한 즉시 바로 사용될 수 있도록 함.
  - 

### Spring container 의 종류
- BeanFactory 와 ApplicationConext 가 있음

#### BeanFactory
- 빈을 등록하고 생성/조회하고 돌려주는 등 빈을 관리하는 역활
- getBean() 메소드를 통해 빈을 인스턴스 화 할 수 있음

```
@Configuration
public class AppConfig {

    @Bean
    public OrderService orderService() {
        return new OrderServiceImpl(discountPolicy());
    }

    @Bean
    public FixDiscountPolicy discountPolicy() {
        return new FixDiscountPolicy();
    }
}
```
```
public class Main {

    public static void main(String[] args) {
        final BeanFactory beanFactory = new AnnotationConfigApplicationContext(AppConfig.class);
        final OrderService orderService = beanFactory.getBean("orderService", OrderService.class);
        final Order order = orderService.createOrder(15, "샤프", 3000);
        System.out.println(order.getDiscountPrice());
    }
}
```
- BeanFactory 를 AnnotationConfigApplicationConext 로 정의하되, AppConfig 를 구성 정보로 지정함.
- 기존에는 개발자가 직접 AppConfig 를 이용해서 필요한 객체를 직접 조회했지만, 이제부터는 Spring Container 를 통해서 필요한 스프링 빈 객체를 찾을 수 있음

#### ApplicationConext
- ApplicationContext 도 BeanFactory 처럼 빈을 관리할 수 있음.  
```
public class Main {

    public static void main(String[] args) {
        final ApplicationContext beanFactory = new AnnotationConfigApplicationContext(AppConfig.class);
        final OrderService orderService = beanFactory.getBean("orderService", OrderService.class);
        final Order order = orderService.createOrder(15, "샤프", 3000);
        System.out.println(order.getDiscountPrice());
    }
}
```

### BeanFactory vs ApplicationConext
- 왜 두개가 있는지?
- ApplicationContext 가 BeanFactory 의 상속을 받음
```
public interface ApplicationContext extends EnvironmentCapable, ListableBeanFactory, HierarchicalBeanFactory,
		MessageSource, ApplicationEventPublisher, ResourcePatternResolver {

	...
}
```
- BeanFactory 를 정확하게 상속받은 것은 아니지만, 빈을 관리하는 기능을 받음
- ApplicationContext 는 그외에도 국제화가 지원되는 텍스트 메시지 관리, 이미지 파일 같은 파일 저원을 로드, 리스너로 등록된 빈에게 이벤트 알림 발생등 부가적인 기능을 가짐.
- 스프링 컨테이너 하면 주로 ApplicationContext 를 뜻함.



