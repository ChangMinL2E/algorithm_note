# Django 

`웹 서비스 개발`을 할때, 새롭게 틀을 만들기보다는 만들어져있는 library사용하는게 편하다.  
&rarr; Framework를 이용.  

- Framework  
: 서비스 개발에 필요한 기능들을 미리 구현해서 모아 놓은 것  
  &rarr; 일정한 뼈대, 틀이 있지만, 정해져있는 규약을 맞춰서 사용해야 한다.  
  
&Rightarrow; 소프트웨어의 생산성과 품질을 높인다.  


### Django  
: Python으로 작성된 프레임워크  

---
### WWW (World Wide Web)  
: 전 세계에 퍼져 있는 거미줄 같은 연결망  
이는 해저케이블로 연결되어 있다.  

무선으로 연결? &rightarrow; 위성끼리 데이터 교환  
문제점 : Starlink Train, 우주 쓰레기  

인터넷을 이용한다. &rightarrow; 전 세계의 컴퓨터가 연결되어 있는 하나의 인프라를 이용하는 것  

---  
### 클라이언트 - 서버  
- 클라이언트  
: 웹 사용자의 인터넷에 연결된 장치 (ex. wi-fi에 연결된 컴퓨터 혹은 모바일)  
  Chrome 혹은 Firefox와 같은 웹 브라우저  
  서비스를 요청하는 주체 (requests)
  
- 서버  
: 웹 페이지, 사이트 또는 앱을 저장하는 컴퓨터  
  클라이언트가 웹 페이지에 접근하려고 할 때 서버에서 클라이언트 컴퓨터로  
  페이지 데이터를 응답해 사용자의 웹 브라우저에 표시됨  
  요청에 대해 서비스를 응답하는 주체 (responses)  

DMS (Domain Main Server)  
: 각 로컬에서 서버에 resources를 요청할 때, 고유의 IP를 사용하는데 이를 알아서 처리해주는 역할해주는 서버(컴퓨터)  

정리  
- resource를 request 하는 쪽 &rightarrow; 클라이언트  
- resource를 responses 해주는 쪽 &rightarrow; 서버  

---
### 웹 브라우저  
: 웹에서 페이지를 찾아 보여주고, 사용자가 하이퍼링크를 통해 다른 페이지로 이동할 수 있도록 하는 프로그램  
  웹 페이지 파일을 우리가 보는 화면으로 바꿔주는(렌더링, rendering) 프로그램  

#### 정적 웹 페이지(Static Web page)  
: 있는 그대로를 제공하는 것(served as-is)  
우리가 지금까지 작성한 웹피이지, 한 번 작성된 HTML 파일의 내용이 변하지 않고 모든 사용자에게 동일한 모습으로 전달되는 것  

#### 동적 웹 페이지(Dynamic Web page)  
: 사용자의 요청에 따라 웹 피이지에 추가적인 수정이 되어 클라이언트에게 전달되는 웹 페이지  

- 서버 : 웹 페이지의 내용을 바꿔주는 주체  
    - 서버에서 동작하고 있는 프로그램이 웹 페이지를 변경  
    사용자의 요청을 받아 적절한 응답을 만들어주는 프로그램을 쉽게 만들 수 있게 도와주는 프레임워크 &rightarrow; `Django`  
      
--- 
### Design Pattern  
: 자주 사용되는 구조를 일반화해서 하나의 공법(패턴화)으로 만들어 둔 것  

- 목적  
  - 특정 문맥에서 공통적으로 발생하는 문제에 대해 재사용 가능한 해결책 제시  
  - 프로그래머가 어플리케이션이나 시스템을 디자인할 때 발생하는 공통된 문제들을 해결하는데 형식화 된 가장 좋은 관행  
    
- 장점  
: 디자인 패털을 알고 있다면 서로 복잡한 커뮤니케이션이 간단해진다.  
  
다수의 엔지니어들이 일반화된 패턴으로 소프트웨어 개발을 할 수 있도록 한 규칙, 커뮤니케이션의 효율성을 높이는 기법  

### Django's Design Pattern  

Django에 적용된 디자인 패턴: MTV 패턴  
MTV 패턴은 MVC 디자인 패턴을 기반으로 조금 변형된 패턴이다.  

MVC(Model View Controller)
MTV(Model Template View)  

<center> MVC MTV  </center>
<center>Model &rightarrow;  Model  </center>
<center>View  &rightarrow;  Template  </center>
<center>Controller &rightarrow;  View </center>
















