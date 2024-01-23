---

---

---

##### OSI 7Layer

**식별자**
MAC주소 = LAN카드의 식별자
IP = host 의 식별자
Port 번호 = L2 인터페이스 or 서비스 or 프로세스 의 식별자

**Host** = 네트워크에 연결된 컴퓨터

**End-point** = 네트워크 이용 주체 = 단말기
- Client/Server (단말기의 역할 분류)
- Peer : P2P

**Switch** = 네트워크 그 자체를 이루는 host. Infra
*Router / IPS / Tab, Aggregation switch

- 매트릭 = 비용
- 패킷 = 자동차
- 라우터  = 교차로
- 라우팅 테이블 = 이정표

---

#### L2

**NIC(Network Interface Card)** = LAN(Local Area Network) 카드
	LAN - MAN - WAN : 크기
**MAC 주소** = NIC의 식별자. 하드웨어 주소. 48bit
- 컴퓨터하나가 인터페이스 여러개 가질 수 있다.

**Frame** : LAN에서 보내는 데이터의 단위

**L2 Aceess switch 
- End-point와 직접 연결되는 스위치
	- MAC 주소를 근거로 스위칭
	- Link-up /down

**L2 Distribution switch
- L2 Access 스위치를 위한 스위치
	- Access -> Distribution -> Router(L3)
- VLAN(Virtual LAN) 기능을 제공

**Broadcast** : 주소가 모두 1 -> 전부 (브로드캐스트) 로 통용
Broadcast 는 최소화 해야한다.

**가상화** : HW를 SW로 구현. Virtual Machine
L2까지는 물리적 , L3(Internet) 부터는 논리적 네트워크

---
#### L3

**IP (Internet Protocol)

**IPv4** = 32bit = 8bit * 4
	Ex) 192.168.0.10 : 각 숫자가 8bit (0~255)
	앞에 3 숫자는 Network ID , 마지막은 Host ID

**Packet** = L3 IP Packet : 단위 데이터
	Header(Src -> Dst) + Payload
	MTU : 최대 크기 1500bytes

*Wireshark

**Encapsulation**
	L2 Frame -> L3 IP Packet -> TCP Segment(MSS :1460bytes) ... Stream

정보 -> Packet -> Gateway (택배기사) 
routing -> IPv4 Dst host로 , port번호(이름)

1. Process 가 정보를 TCP Socket에 Send (Stream -> 분할) 
2. TCP Segment화
3. IP Packet
4. Frame
5. L2 Acess 
6. Router 
7. Internet

User mode :5,6,7 -> Socket Stream
TCP -> Segmaent Mss
IP -> Packet MTU
L1 L2 -> Frame

**IPv4 Header 형식**
- version - IHL(5 * 4 =20) - ...

**Subnet Mask
- 마스크 연산 : bit And 연산으로 network/host ID 잘라냄
*Subnetting

**CIDR** : Classless Inter-Domain Routing
- 192.168.0.10/24 = 앞 24비트가 network ID

**Broadcast IP 주소**
- host ID가 모두1(255) =  Broadcast
*Multicast

**Host 자신을 가리키는 IP 주소** : 127.0.0.1
- Loopback Addresss
- ip주소 변경과 관련X,  L2로 안내려감

**TTL(Time To Live)과 단편화(fragmentation)**
- 인터넷은 라우터의 집합체
- 전송 실패한 Packet 을 폐기
- 단편화는 MTU크기 차이로 발생 -> 수신측 Host에서 조립
*VPN IPSec
*Hop : 라우터 -> 라우터

**인터넷 설정**
- IP주소
- Subnet mask
- Gateway Ip주소
- DNS 주소

**DHCP (Dynamic Host Configuration Protocol)
- 자동으로 인터넷 설정
- Client가 사용할 IP주소를 Server가 알려줌
- Broadcast 도메인안에 묶인 서버
 
**ARP (Address Resolution Protocol)**
- IPv4 주소로 MAC 주소를 알아내려 할 때 사용
	- L2 Frame에서 Gateway의 MAC주소를 알아야함(목적지)
- ARP Req(Broadcast) -> Reply (MAC주소) 캐싱.

**Ping / RTT (Round Trip Time)**
- Ping 유틸리티 : ICMP 프로토콜을 이용해 RTT를 측정
	- Echo Req

---
##### TCP/IP 송수신구조

**송신 - Encapsulation**
- File -> Process Buffer 
- Socket I/O Buffer 에 Copy = 'Send' 
	- Stream (파일을 다 읽을 때까지)
	- ->분해
- L4 (TCP) Segment (조각, 번호)
- L3 IP Packet (박스)
- L2 L1 Frame (트럭, 이동중에 바뀜)

**수신 - Decapsulation**
- Frame
- Packet
- Segment
- Socket I/O Buffer 
- Process Buffer 에서 Receive

- ACKnowledgement : 잘 받았어
	- 송신측 : Wait for ACK
	- Socket Buffer 여유공간(Window Size) 포함

*TCP 는 연결 지향 -> 상대방이 여유 공간이 있을 때 송신

**Network 장애**
1. Loss
2. Re-transmission + ACK Duplicate
3. Out of order : 순서가 잘못됨
4. Zero window ->App 문제 

*Transmission Control Protocol
Hypertext Transfer Protocol

---

#### L4

**TCP**
- TCP '연결' = Connection , Session
- 연결은 '순서번호' 로 구현 (byte 수)
- 연결은 '상태(전이)' 개념을 동반
- 논리적. virtual 한 연결

**3-way handshacking** : 연결 과정
Sequence 번호 교환(SYN , ACK) -> 연결 판단
	- 정책 : 'MSS' 등 관리적 정보

**4-way handshacking** : 연결 종료과정
FIN , ACK 교환
time wait : socket은 자원, Client에서 Active Close 하도록
	= 서버는 Last ACK 받으면 close (passive)

*UDP는 연결 X

**TCP Header**

**UDP** : 멀티미디어 데이터 전송

##### TCP연결이라는 착각
LAN 케이블(L2)을 끊어도 L4연결은 유지 -> 연결재확인
충격(물리적 연결끊김)->Buffer가 완화
- 연결은 End-point의 주관적 판단에 불과하다

---

**DNS** : Domain Name Service
- DNS Cache
- RootDNS. 분산, 트리 구조

*'www' : host name  'naver.com' : Domain name

웹 기술은 HTML 문서 전달

**URL (Uniform Resource Locator)**
- URI (Uniform Resource Identifier)

- Protocol :// Address : Port number / Path(or filename)?Prarameter= value
	PortNumer 기본 : 80
	index.html

---

#### HTTP
HTML 문서를 전송 받기 위해 만들어진 L7 통신 프로토콜
client의 요청에 응답
- HTTP Header

**HTTP metod**
- GET POST ... 

**응답 코드**
- 200  OK
- 400 Bad request
- 403 Forbidden
- 404 Not found
- 500 Internal server error

---

#### 웹 서비스 구조

HTTP traffic = Socket -> stream 문자열
HTML 문저 요청  -> 전송

**정적 페이지 - GET**
- HTTP는 Stateless
- HTML(Data) -> +CSS -> +JS 
- 브라우저가 구문분석 , 렌더링 , JS엔진(client 에서 실행)

**동적 -> POST**
양방향 상호작용 + 상태 전이
Cookie : 상호작용을 위한 기억의 부산물
		Key + value
원격지 사용자 입력 - 검증 대상

**3 - Tier
Web App -WAS - Database
		MVC

APM - Scouter : 응답시간 모니터링

JVM : JAVA byte code
Middleware : WAS - tomcat
	Container
	Framework - Spring

**UI와 Data 분리**
json / xml 자료만 받아서 JS가 HTML 생성
	- React.js Vue.js

CRUD
- RESTful API : URI -> function

IPS / SSL / WAF
- HTTPS -> SSL뒤로 HTTP
*SQL injection

---

#### 네트워크 장치 구조

**Inline
- Packet(L3) + Drop/Bypass + 'Filtering'
- 공유기 라우터 방화벽 IPS

**Out of path
- Packet + Read only , 'Sensor'
- SPI DPI

**Proxy
- Socket stream + Filtering
- User mode , App L5~L7
- 우회 / 감시 차단 / 서버보호(Reverse Proxy) / https분석

*Fiddler

---

#### 공유기

**NAT(Network Address Translation)**
- IP주소 , Port번호 제어 -> IP 주소 부족문제 해결
- packet filtering 방화벽과 비슷한 보안성 제공
- Public(Global) / Private IP

**Symmetric NAT** : TCP 세션마다 외부포트 지정

'Outbound' traffic  = trigger -> NAT Table에 기록
	Local IP / Port - External Port - Remote IP / Port / Protocol

-> Inbound 시 찾아서 다시 변조 전달. 없으면 drop

Packet 수신한 서버입장에선 하나의 host로 판단


**Cone NAT** : Host단위로 외부포트 지정

**Full Cone NAT**
host IP/Port 와 External Port 매핑 
Remote IP/Port 기록 x , External Port만 보고 Inbound paket 전달
	-> 보안성 x 충돌가능성 , 게임이 잘된다
	External Port + Global IP -> 누구라도 유입

**Restricted Cone NAT**
Full Cone + Remote IP 기록.
상대방 IP 일치하면 통과. 포트는 달라도됨

**Port Restricted Cone NAT**
Restricted +Remote Port까지

- Cone 방식은 Port번호를 최대한 아낌
- NAT는 P2P통신을 방해

**포트 포워딩**
External Port -> Local Port
NAT Table -> 포트포워드 규칙


**UPnP** : 포트포워딩 설정 자동화
SSDP : Simple Service Discovery Protocol

##### L4 부하분산
L4 Switch 뒤로 서버 여러대

url -> DNS가 ip주소 -> 웹서버 n번에 포트포워딩
무정지 시스템.

라운드로빙 : 단순 돌아가며
Health check : 부하율 계산 -> Manager가 지정

*VM - Docker - Kubernetes

**GSLB** (Global Server Load Balancing)
DNS서버 여려개

- DNS 체계 활용
- CDN (Content Delivery Network service)
- Client 지리적위치 -> IP주소 DB

canonical name / alias

---

#### VPN (Virtual Private Network)

- 보안 서비스
- 데이터 인증 / 암호화 (무결성+ 기밀성)
- 터널링

**IPSec**
주로 G to G (gateway) Tunneling
Packet을 암호화 , 새 IP header 생성 -> 도착하면 복호화 (L3 터널링)
	라우터 - secure gateway

- ISAKMP (Internet Security Association Key Management Protocol)
- IP AH (Authentication Header) : 무결성
- IP ESP (Encapsulation security Payload) : 기밀성. 암호화

*SSL , PKI

주소가 2개. 변경됨

**PPTP**
공유기가 지원 vpn

---

#### 네트워크 보안 솔루션

- PC방화벽
- NAC + Probe
- 방화벽 , IPS, NIDS
- UTM
- VPN, SSL VPN
- 망분리, 망연계

