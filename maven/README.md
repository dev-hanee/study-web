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
  - Both tools are the most frequently used build and integration tools 
  - DevOps practitioners have to pick the right tool because it operates and executes their entire CI/CD pipeline.

|               | Jenkins                                                                                                                                                                                                                                                                                                                                | Maven                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| What is it?   | - Open-source automation tool created with Java - extensively used as a CI& CD tool - ideal for building and testing software projects continuously  - Automation strategies - development lifecycle - numerous plugins (Git, Maven2, Amazon EC2, HTML publisher..) - runs on Multiple platforms                                       | - POM(project object model) based build automation and project management tool written in Java. - It is compatible with projects written in C#, Python, Ruby. - In Maven, software project is developed using its POM(Project Object Model) which includes information about the project and configuration such as construction directory, source directory, test source directory, dependency, plugins, goals, etc.   - Comprehensive, reusable, easily maintainable model for projects. - Plugins or tools to interact with and operate with this model.   - Maven can be used to build any number of projects into predefined output types- jar, war, metadata. - Can automatically download necessary files from the repository when building a project |
| Advantages    | - since every code commit is built and tested automatically, it allows for the release of new features faster and with fewer errors. - Whenever an error appears during a test, developers receive immediate feedback and can fix issues in the code at the moment. - Thousands of plugins which makes CI/CD operations much simpler.  | - Simple project setup aligned with best practice.  - Makes it easy to start projects in different environments.  - Users do not need to handle dependencies injection, builds, processing, and other incidentals.  - Dependency management including automatic updating.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Disadvantages | - interface is not as user friendly when compared to some of its competitors. - Not too easy to maintain since it runs on a server and requires a skilled server administrator to monitor its activity. - Running a Jenkins CI server requires some infrastructural setup.                                                             | - If the maven code for an existing dependency is not available, then it is not possible to add that dependency at all.  - One must know the Maven command line or use an IDE with Maven integration, such as NetBeans or Eclipse.  - Its learning curve is longer                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
