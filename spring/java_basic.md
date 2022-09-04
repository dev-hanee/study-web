## Jar (file format)
- Java Archive
- 여러개의 자바 클래스 파일과, 클래스들이 이용하는 관련 리소스(텍스트, 그림 등..) 및 메타데이터를 하나의 파일로 모아서 Java platform 에 응용 소프트웨어나 라이브러리를 배포하기 위한 software package file format.
- Distribute 'application software' or 'library'
- 실제로 ZIP 파일 포맷으로 이루어진 압축 파일
- JDK 에 파홈된 jar 명령어를 포함하여 jar 파일을 만들거나, 압축을 풀 수 있음. 
- zip 도구를 사용할 수도 있으나, 압축 시에는 manifest 파일이 처음이어야 하는 경우가 있어서, zip 파일 헤더의 엔트리 순서가 중요함. 

### 설계
- Jar 파일은 Java Runtime 이 효율적으로 application 을 batch(deploy) 할 수 있는 수단으로 설계됨. 
- Java application 을 구성하는 클래스와 관련 리소스를 단일 파일로 묶어 합축된 형태인 JAR 파일은, 한 차례의 요청으로 어플리케이션 전체를 다운로드할 수 있게 함. 
- java.util.zip package 에 jar 파일을 읽고 쓰는 클래스들을 포함. 

### 관련 포맷
- WAR
- RAR
- EAR
- APK
