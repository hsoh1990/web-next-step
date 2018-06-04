# 실습을 위한 개발 환경 세팅
* https://github.com/slipp/web-application-server 프로젝트를 자신의 계정으로 Fork한다. 
Github 우측 상단의 Fork 버튼을 클릭하면 자신의 계정으로 Fork된다.
* Fork한 프로젝트를 eclipse 또는 터미널에서 clone 한다.
* Fork한 프로젝트를 eclipse로 import한 후에 Maven 빌드 도구를 활용해 eclipse 프로젝트로 변환한다.
(mvn eclipse:clean eclipse:eclipse)
* 빌드가 성공하면 반드시 refresh(fn + f5)를 실행해야 한다.

# 웹 서버 시작 및 테스트
* webserver.WebServer 는 사용자의 요청을 받아 RequestHandler에 작업을 위임하는 클래스이다.
* 사용자 요청에 대한 모든 처리는 RequestHandler 클래스의 run() 메서드가 담당한다.
* WebServer를 실행한 후 브라우저에서 http://localhost:8080으로 접속해 "Hello World" 메시지가 출력되는지 확인한다.

# 각 요구사항별 학습 내용 정리
* 구현 단계에서는 각 요구사항을 구현하는데 집중한다. 
* 구현을 완료한 후 구현 과정에서 새롭게 알게된 내용, 궁금한 내용을 기록한다.
* 각 요구사항을 구현하는 것이 중요한 것이 아니라 구현 과정을 통해 학습한 내용을 인식하는 것이 배움에 중요하다. 

### 요구사항 1 - http://localhost:8080/index.html로 접속시 응답
* http://localhost:8080/index.html로 접속했을 떄 webapp 디렉토리에 index.html파일을 읽어 클라이언트에 응답한다.
* RequestHandler에 InputStream을 한줄 단위로 읽어 HTTP 요청 정보 전체 출력(null값 예외처리)
    ```java
       BufferedReader br = new BufferedReader(new InputStreamReader(in, "UTF-8"));
       String line = br.readLine();
       
       log.debug("request line : {}", line);
      
       if (line == null) {
          return;
      }
    ```
* HTTP 요청 정보의 첫 번째 라인에서 요청 URL을 추출
    ```java
      String[] tokens = line.split(" ");
    ```
* 요청 URL을 webapp 디렉토리에서 읽어 전달
    ```java
      DataOutputStream dos = new DataOutputStream(out);
      byte[] body = Files.readAllBytes(new File("./webapp" + tokens[1]).toPath());
      response200Header(dos, body.length);
      responseBody(dos, body);
    ```
### 요구사항 2 - get 방식으로 회원가입
* GET /user/create?userId=admin&password=admin&namem=admin&email=admin HTTP/1.1 요청 처리
* HTTP 요청의 첫번쨰 라인에서 요청 URL을 추출
* 이름=값 파싱은 util.httpRequestUtils 클래스의 parseQueryString()를 이용
* indexOf("?")을 사용해서 path, queryString 분리
    ```java
      if ("/user/create".equals(url)) {
          int index = url.indexOf("?");
          String requestPath = url.substring(0, index);
          String queryString = url.substring(index + 1);
          Map<String, String> parmas = util.HttpRequestUtils.parseQueryString(queryString);
          User user = new User(parmas.get("userId"), parmas.get("password"), parmas.get("name"), parmas.get("email"));
      }
    ```

### 요구사항 3 - post 방식으로 회원가입
* /webapp/user/form.html에 form 태그의 method를 POST로 변경
* HTTP header에 Content-Length의 값이 있으면 body 존재
     ```java
      int contentLength = 0;

      while (!line.equals("")) {  
        line = br.readLine();
        log.debug("header : {} ", line);
        if(line.contains("Content-Length")){
            contentLength =  getContectLength(line);
            }  
      }
     ```
     ```java
      private int getContectLength(String line) {  
          String[] headerTokens = line.split(":");
          return Integer.parseInt(headerTokens[1].trim());  
      }
     ```
* Content-length가 있으면 util.IOUtils의 readDate()메소드로 BufferedReader에서 Body를 추출

     ```java
     if ("/user/create".equals(url)) {
           String body = IOUtils.readData(br, contentLength);
           Map<String, String> params = HttpRequestUtils.parseQueryString(body);
           User user = new User(params.get("userId"), params.get("password"), params.get("name"), params.get("email"));
           log.debug("User : {}" , user);
     }
     ```

     
### 요구사항 4 - redirect 방식으로 이동
* 

### 요구사항 5 - cookie
* 

### 요구사항 6 - stylesheet 적용
* 

### heroku 서버에 배포 후
* 