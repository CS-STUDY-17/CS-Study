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
  > 프로토콜: 송신자, 수신자 간의 메시지의 포맷, 순서, 행위 등을 명시한 규약
