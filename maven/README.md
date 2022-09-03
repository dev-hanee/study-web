## 메이븐이란?
- 프로젝트 빌드 과정
  - 프로젝트 생성
  - 라이브러리 설정
  - 코드 작업
  - 컴파일
  - 테스트
  - 패키지만들기
  - 배포
  - 레포팅

- 빌드 작업을 통합해서 간단히 해주는 도구, 일종의 빌드툴
- Apache project 
- 비슷한 도구
  - gradle
  - Jenkins

- 프로젝트 생성이란?
  - ..


## Jenkins vs Maven
- https://www.browserstack.com/guide/maven-vs-jenkins

|               | Jenkins                                                                                                                                                                                                                                                                                                                                              | Maven                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| What is it?   | - Open-source automation tool created with Java <br> - extensively used as a CI& CD tool <br> - ideal for building and testing software projects continuously <br> <br> - Automation strategies <br> - development lifecycle <br> - numerous plugins (Git, Maven2, Amazon EC2, HTML publisher..) <br> - runs on Multiple platforms <br>              | - POM(project object model) based build automation and project management tool written in Java.<br> - It is compatible with projects written in C#, Python, Ruby.<br> - In Maven, software project is developed using its POM(Project Object Model) which includes information about the project and configuration such as construction directory, source directory, test source directory, dependency, plugins, goals, etc. <br> <br> - Comprehensive, reusable, easily maintainable model for projects.<br> - Plugins or tools to interact with and operate with this model. <br> <br> - Maven can be used to build any number of projects into predefined output types- jar, war, metadata.<br> - Can automatically download necessary files from the repository when building a project<br> |
| Advantages    | - since every code commit is built and tested automatically, it allows for the release of new features faster and with fewer errors. <br> - Whenever an error appears during a test, developers receive immediate feedback and can fix issues in the code at the moment.<br> - Thousands of plugins which makes CI/CD operations much simpler.  <br> | - Simple project setup aligned with best practice. <br> - Makes it easy to start projects in different environments. <br> - Users do not need to handle dependencies injection, builds, processing, and other incidentals. <br> - Dependency management including automatic updating. <br>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| Disadvantages | - interface is not as user friendly when compared to some of its competitors.<br> - Not too easy to maintain since it runs on a server and requires a skilled server administrator to monitor its activity.<br> - Running a Jenkins CI server requires some infrastructural setup. <br>                                                              | - If the maven code for an existing dependency is not available, then it is not possible to add that dependency at all. <br> - One must know the Maven command line or use an IDE with Maven integration, such as NetBeans or Eclipse. <br> - Its learning curve is longer <br>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |

## Maven vs Jenkins : Key difference
### Purpose
- A maven is a build tool designed to manage dependencies and the software lifecycle. It it also designed to work with plugins that allow users to add other taks to the standard compile, test, package, install, deploy tasks. 
- Jekins is designed for the purpose of implementing CI. It checks code out of a repository, builds and packages it, and sends it out to a server for testing - automatically. Jenkins can use Maven as its build tool. 
