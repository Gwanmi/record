# 웹의 개념
- 웹에서의 소통은 사용자(Client)와 서버(Server) 간에 이루어지며 다음과 같이 진행된다.
a. 사용자가 URL 혹은 IP로 웹 서버를 호출하여 리퀘스트(Request)에 담아 전송하면 웹 서버는 Request를 받아 처리하거나 WAS로 전달한다.
b. WAS는 리퀘스트를 받아서 처리하며 DB 작업이 필요할 경우 진행
c. 처리 후 웹 서버로 리스폰스(Respons) 회신
d. 웹 서버는 리스폰스를 다시 사용자에게 회신
e. 사용자의 브라우저는 웹 서버가 보내준 코드를 해석해 화면을 구성하여 출력

## 웹 서비스 구조
- 웹 서버 단일 구성
- 웹 서버-WAS 구성

## Web Server와 WAS의 차이

# 웹 게시판 만들기
## Java 설치 후 환경 변수 설정 하기
- terminal 실행 후 'cd /Library/Java/JavaVirtualMachines'로 들어가 설치된 jdk 확인
- 해당 경로에서 'cd (설치된 jdk).jdk/Contents/Home'를 들어가 pwd로 경로를 복사
- 복사한 경로를 'vi ~/.bash_profile'로 열어 'export JAVA_HOME=복사한 경로' 입력 후 저장
- 'java -version'을 입력하여 버전을 확인
