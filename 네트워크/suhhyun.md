# 네트워크
## 네트워크 기초
네트워크: 노드-링크, 리소스를 공유하는 집합  
노드: 서버, 라우터, 스위치 등  
링크: 유/무선

### 처리량과 지연 시간
좋은 네트워크->처리량 많고 지연시간 짧은... 말 그대로 서비스를 잘 제공할 수 있어야 됨  
장애 빈도도 적고 보안 좋아야 됨 당연함
#### 처리량 (throughput)
단위: bps  
트래픽: 특정 시점에 링크 내에 흐르는 데이터의 양 
트래픽, NW 장치의 대역폭, NW 중간에 발생하는 에러, 장치의 HW 스펙에 영향받음  
++ throughput은 모든 e2e path의 min(R) 값을 가진다 -> 병목 현상이 일어날 수 있음
#### 지연 시간 (latency)
메시지의 왕복 시간 = 요청이 처리되는 시간  
매체 타입(유/무선), 패킷 크기, 라우터의 패킷 처리 시간에 영향받음

### 네트워크 토폴로지와 병목 현상
#### 네트워크 토폴로지
> 노드, 링크의 배치 방식과 연결 형태를 뜻함
- 트리 토폴로지 (계층형 토폴로지)
    > 노드 추가/삭제가 쉬움, but 상위 노드가 하위 노드에 영향을 끼칠 수 있음 -> 트래픽이 가장 많은 상위 계층 노드에 병목 현상이 생기기 쉬움

    <img src="https://velog.velcdn.com/images/dvshinny/post/377c6de0-5f5e-45ba-b6cf-cfca81f5e0ea/image.png">

- 버스 토폴로지
    > 중앙 통신 회선을 공유 -> 장애에 취약, 노드 수에 비례하여 성능 저하 -> 보통 LAN에서 사용, 스푸핑이 쉽다는 단점 존재  
       +스푸핑: 공격자가 공격 대상자로 가장하는 행위, 패킷을 가로채거나 훔쳐봄

    <img src="https://velog.velcdn.com/images/dvshinny/post/d920b8e2-bade-454d-877e-c8621428dc1d/image.png">

- 스타 토폴로지
    > 당연히 중앙 노드에 문제가 생기면 큰일남, 중앙 노드와 말단 노드는 두개의 point2point link로 연결됨  
       확장에 용이
    > 1. Hub : broadcast 방식, 물리적으로는 star 구조이나 논리적으로는 bus로 작동
    > 2. L2 Switch : frame switching device로 기능 -> 버퍼

    <img src="https://velog.velcdn.com/images/dvshinny/post/c3757c2a-6b0e-4aa4-9d7f-2907e3e8c549/image.png">  


- 링형 토폴로지
    > 고리 모양의 길을 통해 패킷 처리  
  >  노드 고장 쉽게 찾을 수 있음, 단방향으로 이동 -> 충돌 발생 가능성 적음, but 하나의 노드/회선 고장이 전체에 영향을 미침  
  > 네트워크 구성 변경이 어려움

    <img src="https://velog.velcdn.com/images/dvshinny/post/83006256-e4ba-4326-a0f5-fa7ddcc8d417/image.png">
- 메시 토폴로지
    > 모든 노드가 연결된 복잡한 구조
  > 장점 : e2e 여러 경로 존재 -> 하나가 문제 생겨도 괜찮음, 트래픽 분산 처리 가능  
  > 단점 : 복잡한 구조 -> 노드 추가가 어려움, 구축/운영 cost 높음
    
    <img src="https://velog.velcdn.com/images/dvshinny/post/5d0c0884-aa7a-44d9-8148-96b053ddcd2a/image.png">
#### 병목 현상
transmission rate가 가장 높은 link에 발생, 한 link에 너무 많은 traffic이 몰리지 않도록 노드 간 link 추가하는 방법으로 해결 가능

### 네트워크 분류
- LAN
- MAN
- WAN

### 네트워크 성능 분석 명령어
- ping: 네트워크 상태 확인을 위해 패킷을 전송
  > ICMP 프로토콜: 인터넷 제어 메시지 프로토콜
  > 1. NW 진단 : ping 또는 traceroute를 통해 NW 연결 여부 확인
  > 2. NW 흐름 통제 : ICMP 리다이렉트를 통해 메시지 전송 흐름을 제어 가능  
  >  ex. 스위치를 통하지 않고 노드로 바로 전송하도록 제어 -> 스푸핑 가능

- netstat: 네트워크 상태 표시
- nslookup: DNS과 관련된 내용 확인 -> 특정 도메인에 매핑된 IP 확인 가능
- traceroute: src - dest의 NW 경로 확인

### 네트워크 프로토콜 표준화
NW 프로토콜: IEEE, IETF과 같은 기관에서 정함  
- IEEE802.3 - 유선 LAN
- IEEE802.11 - wifi  
  > 프로토콜: 송신자, 수신자 간의 메시지의 syntax, semantic, timing을 명시한 규약

## TCP/IP 4계층 모델  
### 계층 구조  

<img src="https://velog.velcdn.com/images/ssulv3030/post/51bd3756-4e7d-4bc9-a984-fb59f14fc1bd/image.png">  

- 각 계층은 분리되어 있다 -> 한 계층의 변화가 다른 계층에 영향을 미치지 않음    
- 각 계층은 function call로 소통함  

#### Application Layer
FTP, HTTP, SMTP, SSH, DNS 등의 응용 프로그램이 실행되는 계층  
서비스를 사람들에게 실질적으로 제공함

#### Transport Layer
송신자와 수신자를 연결하는 통신 서비스 제공  
error control, flow control, congestion control(only TCP) 제공  
Internet Layer와는 달리 reliable service를 제공한다는 특징 존재  

| 특징                  | TCP                                     | UDP                                 |
|-----------------------|-----------------------------------------|-------------------------------------|
| 전송 방식             | 연결 지향 (Connection-oriented)         | 비연결 지향 (Connectionless)       |
| 데이터 순서          | 데이터의 순서를 보장                   | 데이터의 순서 보장을 보장하지 않음 |
| 흐름 제어            | 혼잡을 피하기 위한 흐름 제어 제공    | 흐름 제어 메커니즘이 없음          |
| 사용 사례             | 웹, 이메일, 파일 전송과 같은 신뢰성 있는 통신에 주로 사용 | 실시간 애플리케이션, 비디오 스트리밍, 온라인 게임 등에서 주로 사용 |
| 일반적인 프로토콜    | HTTP, HTTPS, FTP, SMTP, SSH 등          | DNS, DHCP, SNMP, VoIP (예: SIP), 비디오 회의 등 |
| 예시                 | 데이터 무결성이 중요한 신뢰성 있는 통신에 사용 | 신뢰성보다 속도와 효율성이 더 중요한 상황에서 사용 |

##### Circuit switching & Packet switching
**Circuit switching**   
사전에 communication path를 계산하고 할당하는 방식 -> in-order  
1. conn set-up delay
2. disconn delay  

각 path는 공유되지 않고 미리 계산이 이루어지므로 전송 중에 딜레이가 발생하지 않음  
ex. telephone network  
단점: path 할당 -> 적은 user에게 서비스 가능  

**(Datagram) Packet switching**  
하나의 메시지를 쪼개서 (called packet) 전송하는 방식으로 각 packet은 각각 독립적으로 전달됨  
미리 path를 계산하지 않고 각 node에서 다음 node를 결정 -> no order    
1. transmition delay
2. queueing delay

단점: 네트워크 혼잡 때문에 각 패킷에서 delay나 loss가 생길 수 있음  
-> congestion control 필요  
-> TCP가 담당  
    에러 처리

**Virtual Circuit Packet switching (V.C.P.S)**
1. Frame Relay: 하나의 메시지를 다양한 크기의 frame으로 쪼개서 전송 -> 에러 줄이고 오버헤드 감소
2. ATM (비동기 전송 방식): 하나의 메시지를 cell로 쪼개서 전송, but 미리 route 결정

##### 3-way handshaking - 연결(only TCP)
1. C: SYN
2. S: SYN+ACK
3. C: ACK

##### 4-way handshaking - 연결 해제 (only TCP)
1. C: FIN, FIN_WAIT_1
2. S: ACK, CLOSE_WAIT, C: FIN_WAIT_2
3. S: FIN, C: TIME_WAIT
4. C: ACK ... CLOSED, S: CLOSED  

<img src="https://images.velog.io/images/nnnyeong/post/fd5029e1-b84c-4fa3-9f7b-d5f702f1b1b9/image.png">
time-wait 이유: 늦게 도착하는 패킷이 있을 수 있기 때문

#### Internet Layer
best-effort service 제공: 서비스 품질 보장 안함
IP, ARP, ICMP 등  

#### Link Layer
물리 계층 + 데이터 링크 계층  
유/무선으로 실질적 데이터 전달 + 장치 간에 신호를 주고받는 **규칙** 정함  
식
### 유선 LAN (=Ethernet)
IEEE 802.3  
twisted pair, 광섬유 케이블 이용  
full duplex: 송/수신 동시에 가능   
(traditional 유선 LAN) half duplex:  
- (ALOHA: 일단 frame 보내고 ACK 기다리는 방식)  
- CSMA/CD: RX가 idle한지 확인 후 전송하는 방식, 전송하는 도중 충돌(half-duplex로 인한)이 탐지되면 idle한 상태를 기다리다가 다시 전송(1-persistance)  

### 무선 LAN (=wifi)  
IEEE 802.11  
송신과 수신이 같은 채널 이용 -> half duplex  
hidden node problem: 두개의 다른 node는 서로 겹치지 않는 반경에 존재해 서로를 감지하지 못할 수 있음  
-> CD 불가능
-> CSMA만? => ACK 기다리는 시간 비효율적(BW 낭비)
- CSMA/CA: 
  - RTS: Request to Send frame
  - CTS: Clear to Send frame
    1. Sender broadcasts RTS
    2. Receiver(AP) broadcasts CTS
    3. Sender transmits Data to AP
    4. AP broadcasts ACK

### 2.4GHz vs 5GHz
- 2.4GHz: 회절 good but 속도 느림
- 5GHz: 직진성 높아 회절 bad but 속도 빠름  
-> 파장 차이

#### 와이파이

#### BSS와 ESS
- BSS: 기본 서비스 집합, AP+장치로 구성
- ESS: BSS가 연결된 것, 자유롭게 이동하며 네트워크 접속 가능
<img src="https://thebook.io/img/080326/092.jpg">

#### 계층 간 데이터 송수신 과정
- 캡슐화: 상위 계층의 헤더와 페이로드를 페이로드로 묶고 새로운 헤더를 붙이는 과정
- 비캡슐화: 하위 계층의 헤더를 제거하는 과정

### PDU (Protocol Data Unit)
헤더 + 페이로드로 구성  

| 계층          | PDU 명칭                       |
|-------------|------------------------------|
| Application | 메시지                          |
| Transport   | TCP-Segment, UDP-Datagram    |
| Internet    | 패킷(Packet)                   |
| Link        | 데이터링크-프레임(Frame), 물리-비트(Bit) |

## 네트워크 기기
### L7 스위치 (=로드밸런서)
스위치: 여러 장비 연결, 목적지로만 데이터 전송 not broadcasting  
L7 스위치: 서버의 부하를 분산 -> 처리 가능한 트래픽 증가 목표  
URL, 서버, 캐시, 쿠키 기반 트래픽 분산  
ALB
주기적 헬스체크 <- 작동 X 서버 제외하기 위해!  

### L4 스위치
IP, 포트번호 기반 트래픽 분산
NLB

#### 헬스 체크
정상/비정상 서버 판별
전송 주기, 재전송 횟수 등을 설정해 서버에 반복적으로 요청을 보내는 방식
ex. TCP 요청 but 3-way handshake X => 비정상 서버로 판단

#### 로드밸런서
2대 이상의 서버를 기반으로 가상 IP 제공, 로드밸런서의 IP로 요청을 보내면 알아서 요청 분산해서 서버에 전달  

### 라우터
여러 개의 네트워크를 연결, 분할, 구분하는 역할  
네트워크에 존재하는 장치끼리 데이터를 주고받을 때, **최소 경로**로 패킷을 포워팅하는 라우팅 역할을 함

### L3 스위치
L2 스위치 + (hw 기반)라우팅 기능  

| 구분       | L2 스위치 | L3 스위치 |
|-----------|----------|--------|
| 참조 테이블  | MAC 주소 테이블 | 라우팅 테이블 |
| 참조 PDU   | 이더넷 프레임 | IP 패킷 |
| 참조 주소    | MAC 주소 | IP 주소 |

### 브리지
LAN과 LAN을 연결하는 역할  

하나의 큰 LAN을 구성하지 않는 이유
1. Reliability; fault is restricted to small area
2. Performance; clustering devices and separate intra-/inter-traffic
3. Security; keep diff. types of traffic that have diff. security needs on
physically separate media
4. Geography; two buildings separate by highway can be connected
by a microwave bridge link

#### NIC - 고유 MAC 주소 가짐
#### 리피터 - 신호 증폭
#### AP

## IP 주소

### ARP (Address Resolution Protocol)
- IP 주소를 통해 MAC 주소를 얻는 프로토콜
- ARP table: 같은 LAN에 존재하는 노드의 정보만 저장
- src: broadcast, dest: unicast

But ARP는 같은 LAN에 존재하는 노드의 정보밖에 알지 못함  
-> 다른 LAN에 있는 노드와 통신하고 싶다면?  
A-R-B 통신
1. A - R: A's src MAC addr, R's dest MAC addr
2. R - B: dest MAC addr 확인 후 routing table과 IP 주소로 길 찾음  
  이때 R's src MAC addr, B's dest MAC addr로 바꿈

### 홉바이홉 통신
라우터의 라우팅 테이블 IP를 기반으로 목적지까지 패킷을 계속해서 전달하는 통신 방식

### 라우팅 테이블
해당 라우터에 들어가 있는 dest 정보와 그 방법이 들어있는 리스트
게이트웨이 + 다음 라우터 정보

#### 게이트웨이

### IP 주소 체계
#### IPv4
32bit(8+8+8+8) -> 주소 고갈로 인해 IPv6 등장

#### IPv6

##### 클래스 기반 할당 방식
<img src="https://thebook.io/img/080326/110_1.jpg">  
맨 앞의 구분 비트로 클래스 구별 (0,10,110...)  
ex) 클래스 A의 12.0.0.0 할당 -> 12.0.0.1 ~ 12.0.0.254만 호스트에 할당 가능

#### DHCP
적은 IP addr로 더 많은 사람들에게 서비스 -> 임시 IP 주소를 동적으로 할당, 실제 동시접속은 적기 때문

#### NAT (Network Address Translation)
공인 IP와 사설 IP로 나눠서 많은 주소 처리 가능  
각 라우터에 공인 IP 할당 -> 해당 local network에 속하는 노드는 사설 IP를 가짐  
라우터의 NAT 장치가 공인 IP <-> 사설 IP 변환  
장점: 보안 good
단점: 속도가 host에 반비례
**NAT is controversial**
NAT translation table에서는 IP addr와 port 번호를 함께 저장함
-> src 정보를 테이블에 저장하는 과정에서 헤더를 하나 더 까서 port 번호를 확인해야 됨
=> 하위 계층은 상위 계층의 정보를 볼 수 없다는 규칙에 위배

#### IP주소를 이용한 위치 정보

## HTTP
### HTTP/1.0 - TCP
한 연결당 하나의 요청 처리 -> RTT 증가  
- sol 1) 이미지 스플리팅: position 속성을 이용해 이미지 표기  
- sol 2) 코드 압축: 개행문자와 공백 제거  
- sol 3) 이미지 Base64 인코딩: 크기는 커지지만 http 요청 필요 X  

### HTTP/1.1 - TCP
parallel TCP conn: 한 연결로 여러 개의 요청 처리 가능 - keep-alive 옵션
- HOL Blocking: TCP 특성 상 차례대로 데이터 처리 -> 맨 앞에 있는 데이터가 너무 크면 뒤에 있는 데이터까지 지연됨  
- 무거운 헤더 구조

### HTTP/2 - TCP
멀티플렉싱: 여러 개의 스트림을 사용하여 쪼개진 데이터를 송수신(동시에 여러 개의 TCP conn 가능), 특정 패킷이 손실되어도 다른 스트림에 영향 X
- TCP가 아닌 HTTP가 데이터 분할

헤더 압축: 허프만 코딩 압축 알고리즘 사용 - 빈도가 높은 문자열에 짧은 비트 할당  
서버 푸시: 클라이언트 요청 없이 리소스 푸시 가능  
HTTPS: 통신을 암호화
SSL/TLS: 전송 계층에서 보안을 제공하는 프로토콜  
- 보안 세션
  - 인증 메커니즘: CA 발급 인증서 기반(Comodo, Godaddy, ClobalSign, 아마존 등)
  - 키 교환 암호화 알고리즘: 디피-헬만
  - 해싱 알고리즘: SHA-256   
  - 
SEO 관리
  - 캐노니컬 설정
  - 메타 설정
  - 페이지 속도 개선
  - 사이트맵 관리  

HTTPS 구축 방법
  1. CA 인증키 기반 HTTPS 서비스 구축
  2. 로드밸런서 이용
  3. CDN 이용

### HTTP/3 - UDP
QUIC 계층 위에서 작동 (Quick UDP Internet Connection)  
UDP 기반 -> 3-way handshaking 불필요 => 초기 연결 설정 지연시간 감소
멀티플렉싱  
FEC(Foword Error Connection): 패킷 손실 -> 수신 측에서 에러 감지하고 수정


