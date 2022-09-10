## Spring Framework definition
> 자바 엔터프라이즈 개발을 편하게 해주는 오픈 소스 경량급 애플리케이션 프레임워크

### 애플리케이션 프레임워크란??
- 일반적으로 library 라 framework 는 특정 업무나 한 가지 기술에 특화된 목표를 가지고 만들어짐
  - 웹 계층을 MVC 구조
  - format 과 출력 장치를 유연하게 변경할 수 있는 application log
- application framework 는 특정 계층/ 기술/업무 분야에 국한되지 않고, application 전 영역을 포괄하는 범용적인 framework
- application framework 는 application 전 개발의 전 과정을 빠르고 편리하며 효율적으로 진행하는데 일차적인 목표를 두는 프레임워크


### 경량급이란?
- EJB 처럼 힘들고 난해한 설정파일 / 까다로운 패키징 / 불편한 서버 배치 등의 부담이 없음.


## Spring Framework 특징
- 경량 컨테이너
 - 경량 컨테이너로 자바 객체를 직접 관리함
 - 각각의 객체 생성/소멸 과 같은 lifecycle 을 관리, Spring 으로부터 필요한 객체를 얻을 수 있음

- POJO 기반의 구성
  - Plain Old Java Object
  - 평범한 자바 객체
 
- DI 를 통한 객체 간의 관계 구성
  - Spring 은 그 자체가 구조를 설계할 수 있어서 개발자가 부품을 만들어 조립하는 형태의 개발이 가능함. 
  - 이렇게 조립된 코드의 최종 호출은 개발자가 결정하는 것이 아니라 Spring Framework 내부에서 이루어짐. 이를 제어의 역행 이라고 함 (IoC)
  - 
