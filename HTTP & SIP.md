# **HTTP & SIP** 



## HTTP 1.x 

- Web Client and Servers

  Web은 점과 줄로 연결되어 있다. 점은 정보이고 줄은 하나의 정보에서 추가적으로 알고싶은게 있으면 다른 정보로 이동할 수 있다. 이때 정보를 주고받을 때 HTTP 를 사용한다. Web Browser는 Web Client가 된다. 여기에 정보가 있어서

  - HTTP Protocol 
    1991 년 물리학자들이 Internet을 통해서 논문 같은 문서를 보여주고 싶어서 만들었다. 

  -  HTTP request

    Client 가 Server에게 정보를 요청할때 HTTP  request 메시지를 보낸다. 

  - HTTP response

    HTTP request 메시지가 Client 로부터 오면 Server가 HTTP response 를 보낸다.

- Resources

  HTTP 를 통해 주고받은 정보는 File 들이다. 이때 주고받는 형태에는 2가지로 Static과 Dynamic이 있다. 이는 Request 한 순간 이전부터 존재하던 File 이라면 Static content, 이후에 생성되면 Dynamic content 이다. 이때 File 들이 사용자에게 의미가 있지만 Computer 입장에선 그저 Resource 이다. 

  - Static content 

    넷플릭스 Video, Image file 등 Server 가 Disk 에서 끄집어 Response 해준 Data 다. 

  - Dynamic content 

    은행 계좌정보,  주식 상황 등 프로그램이  파일을 만들어 Response 해준다. Live Image 는 사용자가 Request 한 이후 생성된 Image를 말한다. 
    
  - Media Types 
  
    Resource로 Image, Text 등이 될 수 있다.  
  
    - MINE (Multipurpose Internet Mail Extensions)
  
      HTTP 는 Response 할 때 Content - type을 넣어준다. 이 방식이 MINE type 으로 Resource 의 형태와 jpeg 와 같은 방식도 표기해준다. 
  
    - Textual label
  
      이렇게 Client 와 Server 는 알파벳이 있는 Text 메시지를 주고 받게되었다. 이는 Byte로 통신해야만 하는 상황과 달리 통신에 여유가 생겼기 때문에 개발자 입장을 고려할 수 있게 되었기 때문이다. 
  
    - URI (Uniform Resource Identifier)
  
      HTTP 는 어떤 Resource를 표현하더라도 구분이 가능한 Identifier를 달았다. 이는 Internet 상의 주소이며, 어떻게든 하나여야만 하고, 위치에 관한 정보가 되어야 한다.  이런 기능을 수행하는 것으로 URL 와 URN 이 있다. 
  
      - URL (Uniform Resource Location)
  
        http: //www.example.com/index.html  에서 http:// (http 프로토콜을 사용해서) | example.com (example 이란 컴퓨터 domain 에) | index.html (이 directory 에 있다.)  
  
      - URN (Uniform Resource Name)
  
        고민은 했지만 쓰이지는 않는다. 
  
- Transactions 

  ``` http
  <%--Client--%>
  GET /specials/saw-blade.gif HTTP/1.0 
  HOST: Www.joes-hardware.com 
  <%--Server--%>
  HTTP/1.0 200 OK
  Content-Type : image/gif
  Content-length : 8572
  ```

  Client가  GET 이후의 dir 에 파일을 요청하고 이때 프로토콜은 HTTP/1.0을 사용해서 joes-hardware.com  에 요청한다.

  이후 Server가 HTTP/1.0 프로토콜에서 200 status 를 보내서 컴퓨터가 이해할 수 있게 하고 OK를 Duplicate 하게 같이 보내서 개발자가 쉽게 알 수 있도록 한다. 그렇게 길이 8572 의 image/gif 을 response 해준다.  

  

  - HTTP Methods

    Client 가 요청하는 동작이다.  

      1. GET  (Download)

         Client 가 Server로 부터 받기를 원하는 Resource를 요청한 것이 다. 

    2. PUT  (Upload)

       Client 가 Resource를 전달해서 Server가 이를 저장하ㄴ는 것이다. 

    3. Delete 

       PUT해서 올린 File을 Server에서 지운다. 
    
  - Status Codes 

    Response는 많이 있다. 

    1. 200 

       성공 

    2. 302

       보완이 중요하거나 음란물 사이트 같이 많은 곳을 갈아타야 하는 경우 존재는 하지만 여기는 없어니까 갈아탈게 라는 뜻이다. 

    3. 404 

       있었던 파일이 지워졌을 때. 

  - Web Pages Can Consist of Multiple Objects 

    NAVER의 메인 뷰에선 여러개의 서버에서 Data를 가져와서 띄운다. 

- Connections 

  HTTP는 밑에 TCP 를 권장한다. UDP를 사용하면 Data 가 유실될 수 있다.  NAVER같은 곳에서 네트웍 하는 사람을 많이 뽑는 이유로 원하는 성능이 안나와서 HTTP를 보다가 그 아래인 TCP를 보게 되어서다. HTTP 는 TCP/IP를 밑에 두고 있기 때문에 Request, Response 라는 단순한 구조를 가진다. 

  - Connections Process
    1. Web browser의 URL 주소창에 주소 입력 
    2. HOST name 을 가져온다 .
    3. HOST name을 DNS를 통해 숫자로 변환
    4. Client 와 Server가 연결되고 request, response 한뒤 연결해지된다. 

- Architectural Components of the Web 

  - Proxy 

    Proxy 는 Client 와 Server 사이에 존재하고 HTTP 1.1에서 Proxy는 보이지 않는다. Client가 Server에 접속하려 할 때 Proxy 에서 막거나 통과시키고 Log를 남길 수도 있다.

    -  Performance Optimization 

      다른사람이 Server에서 정보를 뺐고, Client가 같은 정보를 Request 했다면 Proxy에서 줄 수 있다. 

      혹은 기업에서 해외 출장을 갔는데 그 나라 네트웍 상황이 좋지 못하다면 Proxy 가 Server의 정보를 압축해서 보내거나, Grayscale로 보낼 수 있다. 

- Methods

  - GET 

    URL을 주고 그 Resource를 주세요. 

  - PUT 

    File이나 Contents를 Server에 올린다. 

    PUT의 Response 메시지로 새로운 URL을 주는데 Request 에 보낸 File를 저장한 주소이다. 

  - Delete 

    Client 가 Data를 Request하면 Server에서 지우고 Response로 지웠다고 200 OK를 보낸다. 

  - HEAD 

    GET하고 동일하다. Request에서 GET 대신 HEAD 를 기입했다. Response에서도 GET과 동일한데 단 File 본채는 보내지 않는다. 즉 그 File의 크기와 Type 을 받는다. 

  - POST 

    다른 Method 들은 File을 다뤘다면 POST는 로그인같은 Data를 보낸다.  주로 Dynamic content를 주고받을 때 사용한다. 대부분의 Software는 Data를 주고 받기 때문에 POST 를 사용한다.

  - TRACE 

    Proxy가 있는지 없는지 확인하는 용도다. 

  - OPTIONS 

    주로 개발자가 사용한다. Server 가 지원하는 Methods 를 알려준다. 

- Status

  - Redirected 

    다른 곳에 가서 가져오세요. Server가 다른데를 알려주고 다른 Server에서 가져온다. Response는 300 번대가 Redirected 이다. 

  - Request redirected to use local copy

    Request 메시지로 만약 이 날짜 이후로 수정사항이 있으면 Server에서 File을 가져온다. 만약 수정이 없다면 Browser 는 Response를 받지 않고  Local 컴퓨터에 Cache 된걸 가져온다. 

## Web Browser as Development Tool

Chrome 이나 Firefox 같은 Web Browser에서는 개발자 도구를 통해 소스코드와 Methods 들이 오가는걸 볼 수 있다. 



## Web Server Development 

- Web Server

  Web Server를 제공하는 Software 를 설치한다. 

  Apache, Nginx, Wordpress 등이 있다. Static 하거나 간단한 Dynamic content를 제공하는 거라면 이 Software를 사용하는게 수월하다. 

- Web Server (programming language)

  직접 프로그래밍 언어를 통해서 Server를 만드는 것이다. Server에서 Logic을 구현해서 HTTP 메시지를 주고 받게 한다.

  ```javascript
  var http = require ('http');
  
  http.createServer(function (req, res)){
  	res.write(200, {'Content-type': 'text/plain'});
  	res.end('Hello World');
  }).listen(8088);
  ```

## Web based Mobile Application Development

HTML , Javascript, CSS가지고 Platform independent한 결과물을 만들 수 있다. 

## HTTP 2.0

기존 HTTP의 문제점을 해결하기 위해서다. 

- Overview 

  - Binary protocol 

    HTTP 1.x 가 텍스트로 전달해서 읽는덴 용이했지만 속도가 한계가 있어서 Binary 한 조합으로 만들었다. 

  - Multiplexing

    HTTP 1.x에선 NAVER 홈페이지에는 대략 200개의 Resource request 한다. 이때 하나의 요청이 지연되면 나머지 응답도 늦어진다. 이 문제점을 HTTP 2.0은 우선순위가 있어서 준비가 된 Response는 바로바로 보낸다. 

  - Header Compression 

    반복적으로 사용되는 헤더는 헤더 테이블로 인덱스로 표기한다. 이렇게 성능을 높힌다. 

  - Server Push 

    HTTP 1.x에선 사용자가 Request 하기 전까진 Server가 보낼 수 없었다. HTTP 2.0에선 Server가 예상을 하여 Client가 요청하지 않아도 Resource를 미리 보낸다. 광고같은 걸 띄울 수 있는 것이다.

## HTTP 3.0

QUIC 을 사용하고 UDP가 사용된다. 

- Quic 

  - Coming HTTP/3 Protocol 

    2012년에 구글에 의해 탄생했다. 

  - Concept 

    Web service를 잘하기 위해서 만들어졌다. TCP 에서 HTTP에서 발생하는 문제를 해결하기 위해서 UDP를 올리는 것이 고안되었다. 

    TCP의 문제점으로 Connection 시 시간이 오래 걸리고, Transport latency가 발생하고, congestion control 하기 때문에 느린 문제가 있었다. 

    Transport layer를 건들기 위해선 Linux kernel 을 건드려야 하는 부담이 있기 때문에 Quic 은 UDP 를 사용하면서Transport layer로 고안은 되었지만 User space 이다. 

  - Fast Establishment

    암호화 프로토콜인 TLS를 사용한다. 

    TCP 에서 SYN / ACK 같은 오고 가는 시간을 HTTP 3.0에선 한번만에 끝낸다. 

    HTTP 3.0 은 Connection 이력이 있다면 0 ms, 이력이 없다면 100ms 안팍으로 연결된다. HTTP 2.0 대비 아주 빠르다. 

  - Enhanced Error Correction 

    HTTP 2.0 은 TCP 를 사용하기 때문에 Congestion control, slow start 같은 이유로 속도를 Control 할 수 없고 Resource를 한줄로 보낸다. 하지만 UDP 는 Resource를 따로따로 보낼 수 있고 빠르기 때문에 Error control 이 용이하다. 

  - Application Space Execution 

  - Google's Just Do It

    UDP를 사용한다는 것은 운영체제에서 IP만 사용한다는 것이다. 구글 입장에서 Quic은  Chrome 안에 들어가면 되고 Web Server 안에 들어가면 된다. 즉 구글이 만든 서비스가 IOS, Windows, Linux 의 도움을 받지 않고도 저런 운영체제 위에서 우리 회사의 서비스가 잘 돌아갈 수 있게 할 수 있다. Browser 를 가지고 있다는 것은 세상의 표준을 신경쓰지 않고 우리 회사의 Server에 붙어서알아서 성능개선을 할 수 있다.   UDP 의 장점이 극대화 되는  Video traffic 면에서 매우 크게 확산되고 있다. 

## SIP

Instant 메신저, 

- ​	Procedures

  (채팅방 생성) Invite -> 200 OK -> ACK

  (채팅 중)

  (채팅방 해체) BYE -> 200 OK  

- Concept 

  HTTP 를 모티브로 삼았기 때문에 Text를 사용한다. 

- SIP Entities 

  - User Agent 

  - Registrar 

    메신저를 이동통신으로 사용하면 IP address 가 변한다. 이러한 문제를 SIP의  ID 를 IP address로 변환 해서 사용하고 Registrar가 이를 수행한다. 따라서 카카오톡 ID 를 가지고 IP를 변환하는 작업을 계속 수행하고 있다. 

  - Proxy Server 

## Advanced Web Technologies 

- WebRTC

  Web 화상 시스템을 Browser 위에서 만들 수 있다. 

  - Concept

    Web Browser 위에서 사용하는 언어로 운영체제까지 내려가지 않고 Server를 돌린다.  Google meet 같은 프로그램들이 이에 해당한다. 

  - Feature 1

    WebRTC 는 

  - Feature 2

- asm.js

  어셈블리언어에 Web 이 붙었다. Web Browser는 하드웨어를 건들 수 없지만 WebAssembly 는 Java 가 Virtual 하게 Web Browser위에서 올라가는 것을 C/C++ 을 올린 것이다. 이게 나온 걸 좀 보면, Web Browser위에 고속의 게임을 올릴 수 있게된다. 

- Mixed Reality , Web VR 

   Web Browser위에 VR , 그래픽 도형들을 띄우는 것이다.

- Solid 

  Tim Berners-Lee (HTTP) 창시자가 만든 Social linked data 이다. 

  Secure user pod 에 내 사진을 올려 SNS 에 내 사진을 올리는게 아니고 링크를 가져가는 것이다. 내 사진은 내가 관리하는 것이다. 

