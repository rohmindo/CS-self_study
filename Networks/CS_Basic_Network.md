# Network
# Table Of Contents :

   + ### [1. TCP vs UDP](#1-tcp-vs-udp)
   + ### [2. OSI 7 layer](#2-osi-7-layer-vs-tcpip)
   + ### [3. HTTP](#3-http-프로토콜)
   + ### [4. RestFul API](#4-restful-api)
   + ### [5. Proxy server](#5-restful-api)
   + ### [6. Security](#6-보안)
## 1. TCP vs UDP
  + ### TCP와 UDP 모두 네트워크 계층 중 transport layer(전송 계층)에서 사용하는 프로토콜 입니다.
  + ### TCP 란 ? 
    + TCP는 3-way handshaking과정을 통해 연결을 설정해서 신뢰도를 확보해서 순서를 보장하는 대신 속도가 느리다.
    + TCP는 신뢰도가 필요한 HTTP 통신, 이메일 등에 사용.
  + ### UDP 란 ?
    + UDP는 순서를 보장하지 않고 신뢰도가 낮은 데이터 전송을 하는 대신, 단방향 데이터 전송으로 속도가 빠르다는 차이가 있습니다.
    + UDP는 빠른 속도가 중요한 스트리밍 서비스에 사용.
  ![image](https://user-images.githubusercontent.com/63469069/141098093-0f9d4b51-6afd-4c6c-96a9-063307c5c978.png)  
  + ### 4 Way-handshaking
    + step 1 : 클라이언트가 연결을 종료하겠다는 FIN플래그를 전송한다. 이때 A클라이언트는  FIN-WAIT 상태가 된다.
    + step 2 : B서버는 FIN플래그를 받고, 일단 확인메시지 ACK 보내고 자신의 통신이 끝날때까지 기다리는데 이 상태가 B서버의 CLOSE_WAIT상태다.
    + step 3 : 연결을 종료할 준비가 되면, 연결해지를 위한 준비가 되었음을 알리기 위해  클라이언트에게 FIN플래그를 전송한다. 이때 B서버의 상태는 LAST-ACK이다.
    + step 4 : 클라이언트는 해지준비가 되었다는 ACK를 확인했다는 메시지를 보낸다. A클라이언트의 상태가 FIN-WAIT ->TIME-WAIT 으로 변경된다.
    
    + 그런데 만약 "Server에서 FIN을 전송하기 전에 전송한 패킷이 Routing 지연이나 패킷 유실로 인한 재전송 등으로 인해 FIN패킷보다 늦게 도착하는 상황"이 발생한다면?  
    
    -> Client에서 세션을 종료시킨 후 뒤늦게 도착하는 패킷이 있다면 이 패킷은 Drop되고 **데이터는 유실**될 것입니다  
    
    ->  A클라이언트는 이러한 현상에 대비하여 Client는 Server로부터 FIN을 수신하더라도 일정시간(디폴트 240초) 동안 세션을 남겨놓고 잉여 패킷을 기다리는 과정을 거치게 되는데 이 과정을 **"TIME_WAIT"** 라고 합니다. 일정시간이 지나면, 세션을 만료하고 연결을 종료시키며, "CLOSE" 상태로 변화합니다. 
## 2. OSI 7 Layer vs TCP/IP
   ![image](https://user-images.githubusercontent.com/63469069/141115151-36c378b4-e675-4947-bb08-201b8d69f435.png)
   + ### OSI 7 Layer  
      
   + **Physical layer** : 단지 데이터 전기적인 신호로 변환해서 주고받는 기능만 할 뿐이다. 어떤 **에러가 있는지 등 그런 기능에는 전혀 관여하지 않습니다**.
   + **Datalink layer** : Physical layer에서 송수신되는 정보의 오류와 흐름을 관리하여 **안전한 정보**의 전달을 수행할 수 있도록 도와주는 역할을 합니다.
   + **Network layer** : 목적지까지 가장 안전하고 빠르게 데이터를 보내는 기능을 말합니다. 따라서 최적의 경로를 설정해야하지요. 이런 라우팅 기능을 맡고 있는 계층이 네트워크 계층입니다.
   + **Transport layer** : 전송 계층은 양 끝단의 사용자(end-to-end)들이 신뢰성있는 데이터를 주고 받게 해주는 역할을 합니다. 신뢰성있고 효율적인 데이터를 전송하기 위하여 오류검출 및 복구, 흐름제어와 중복검사 등을 수행. 데이터 전송을 위해서 port번호를 사용하며, 대표적인 프로토콜로 TCP,UDP가 있습니다. 
   + **Session layer** : 응용 프로세스가 **통신**을 관리하기 위한 방법을 정의합니다. 이 계층은 세션을 만들고 없애는 역할을 하고 있지요.
   + **Presentation layer** : 데이터를 어떻게 표현할 지 정하는 역할을 하는 계층으로 일종의 확장자같은 일을 하는 layer.
   + **Application layer** : 응용 프로세스와 직접 관계하여 일반적인 **응용 서비스를 수행**한다. ex) HTTP,SMTP,FTP..
   
   + ### TCP/IP layer
   
   + **Network interface layer** : Node-To-Node간의 신뢰성 있는 데이터 전송을 담당하는 계층입니다. OSI7 계층의 물리 계층과 데이터링크 계층의 역할을 바로 이 계층이 담당하는 것으로 볼 수 있습니다.
   + **Internet layer** : OSI7계층의 네트워크 계층을 담당하는 계층입니다. OSI7 계층처럼 호스트간의 라우팅을 담당하지요. 
   + **Transport layer** : OSI7 계층의 전송계층과 같습니다. 프로세스간의 신뢰성 있는 데이터 전송을 담당하는 계층입니다. 
   + **Application layer** : 사용자와 가장 가까운 계층입니다. OSI7계층의 5계층부터 7계층까지의 기능을 담당하고 있습니다. 서버나 클라이언트 응용 프로그램이 이 계층에서 동작합니다. 우리가 알고 있는 브라우저나 텔넷같은 서비스가 이 계층에 동작하며, 동작하기 위해서는 전송계층의 주소, 즉 포트번호를 사용합니다.

   
## 3. HTTP 프로토콜
   + ### HTTP(hypertext transfer protocol) 이란?
      + 인터넷상에서 데이터를 주고 받기 위한 서버/클라이언트 모델을 따르는 프로토콜이다. 애플리케이션 레벨의 프로토콜로 TCP/IP위에서 작동한다. HTTP는 어떤 종류의 데이터든지 전송할 수 있도록 설계돼 있다. 
   + ### Connectionless & Stateless
      + HTTP는 Connectionless 방식으로 작동한다. 서버에 연결하고, 요청해서 응답을 받으면 연결을 끊어버린다. 기본적으로는 자원 하나에 대해서 하나의 연결을 만든다.
      + 장점 : 불특정 다수를 대상으로 하는 서비스에 적합한 방식이다. 수십만명이 웹 서비스를 사용하더라도 접속유지는 최소한으로 할 수 있기 때문에, 더 많은 유저의 요청을 처리할 수 있다.
      + 단점 : 연결을 끊어버리기 때문에, 클라이언트의 이전 상태를 알 수가 없다. 이러한 HTTP의 특징을 stateless라고 하는데, Connectionless 로 부터 파생되는 특징이라고 할 수 있다.
      + 클라이언트가 과거에 로그인을 성공하더라도 로그 정보를 유지할 수가 없다. HTTP는 cookie를 이용해서 이 문제를 해결하고 있다. 
   + ### Cookie & Session
      + ### Cookie : 
         + 쿠키는 클라이언트(브라우저) 로컬에 저장되는 키와 값이 들어있는 작은 데이터 파일입니다.
         + 쿠키는 클라이언트의 상태 정보를 로컬에 저장했다가 참조합니다.  
         
      + ### Cookie 동작방식  
      
       ![image](https://user-images.githubusercontent.com/63469069/141121697-5d0f85fd-1618-48d1-b233-bfd03e20ae93.png)
      + ### Session :
         + 세션은 쿠키를 기반하고 있지만, 사용자 정보 파일을 브라우저에 저장하는 쿠키와 달리 세션은 서버 측에서 관리합니다.
         + 사용자에 대한 정보를 서버에 두기 때문에 쿠키보다 보안에 좋지만, 사용자가 많아질수록 서버 메모리를 많이 차지하게 됩니다.
      
      + ### Session 동작방식
      
       ![image](https://user-images.githubusercontent.com/63469069/141122413-284627b7-5b6a-4638-8c6e-4f4b348e5c98.png) 
  
   + ### HTTP Method :
      + GET : 정보를 요청하기 위해서 사용한다. (SELECT)
      + POST : 정보를 밀어넣기 위해서 사용한다. (INSERT)
      + PUT : 정보를 업데이트하기 위해서 사용한다. (UPDATE)
      + DELETE : 정보를 삭제하기 위해서 사용한다. (DELETE)
 
  
## 4. RestFul API

   + ### RestFul API란 ?
      + REST : HTTP Method(POST, GET, PUT, DELETE)를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것을 의미한다
      + API : 서로 정보를 교환가능 하도록 하는 것
      + RestFul API : rest기반으로 서비스 api를 구현한 것
   + ### GET vs POST
      + Get : Method = “get” : 데이터를 url 끝에 붙여 눈에 보이게 보냄(url 끝에(**Http header**) query string으로 붙여서 보냄 ex ggg.ggg.ggg/db.jsp?**id=mindo&pwd=1234**)
      + POST : Method = “post” : 데이터를 url에 적지 않고 내부에 숨겨서 보냄(**Http body**에 id=mindo,pwd=1234를 포함해서 보냄)
   + ### POST vs PUT
      + POST : 생성하는 것으로 여러번의 요청을 보내면 그 개수만큼 자원이 생성.
      + PUT : 동일한 자원이 존재하면(식별자를 포함해서 보냄) 하나의 자원에서 수정 및 업데이트가 됨.
   
   
## 5. 프록시 서버 / dns / ssl
   + ### Proxy server란? 
      + 
   + ㅇ
   + ㅇ
   + 

## 6. 보안(cors ssl oauth)
