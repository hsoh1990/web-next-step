## 동영상 실습
https://github.com/slipp/web-application-server를 clone하여 동영상을 통해 진행된 것을 기록한다.
* https://www.youtube.com/watch?v=xHQ0X_Ails4 요구사항 1 
* https://www.youtube.com/watch?v=ioOGE8qTa94&t=10s 요구사항 2
* https://www.youtube.com/watch?v=q5bvPKbc_RM 요구사항 3
* https://www.youtube.com/watch?v=vfCpgIJU2XU 요구사항 4
* https://www.youtube.com/watch?v=wWEW7aYS66A 요구사항 5
* https://www.youtube.com/watch?v=pQhCqu_nQjc 요구사항 6

## 각 요구사항별 학습 내용 정리
* 동영상으로 학습한 각 요구사항별 진행상황을 기록하며, 3장에서 학습한 내용과 차이를 기록한다.
* 동영상으로 학습한 요구사항들에서 HTTP 프로토콜에 대해 정리한다.

### 학습내용
 영상은 3장에서 구현한 내용을 라이브코딩을 통해  요구사항을 따라 빠르게 구현하며, 로그로 보여지는 HTTP요청에 대한 내용을 바탕으로 학습한다.

#### HTTP 요청 

웹 클라이언트와 웹 서버와의 데이터를 주고박기 위해 HTTP라는 규약을 따른다. 웹 글라이언트가 웹 서버에 요청을 보내기 위한 규약은 다음과 같다

```basic
POST /user/create HTTP/1.1 ------------------------------> 요청라인
HOST: localhost:8080                               ]
onnection-Length: 59                               ] 
Content-Type: application/x-www-form-urlencoded    ] 
Accept: */*                                        ] ---> 요청 헤더
--------------------------------------------------------> 헤더와 본문 사이의 빈 공백 라인
userId=id&password=pw ----------------------------------> 요청 본문
```

반대로 서버가 클라이언트에게 보내는 응답 메시지는 다음과 같다

```basic
HTTP/1.1 200 OK ---------------------------------------> 상태라인
Content-Type: text/html;charset=utf-8             ]
Content-Length: 20                                ] ---> 응답 헤더
-------------------------------------------------------> 헤더와 본문 사이의 빈 공백 라인
<h1>Hello World</h1>-----------------------------------> 응답 본문
```

#### 참고 자료

더 학습하거나 먼저 학습해 보거나...

* http://www3.ntu.edu.sg/home/ehchua/programming/webprogramming/HTTP_Basics.html 
* HTTP 완벽 가이드 (데이빗 고울리, 브라이언 토티, 마조리 세이어, 세일루 레디, 안슈가왈 공저 / 이응준 , 정상일 공역, 인사이트 / 2014)
* 성공과 실패를 결정하는 1%의 네트워크 원리(Tsutomu Tone 저 / 이도희 역 / 이중호 감역, 성안당 / 2015)