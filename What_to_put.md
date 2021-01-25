# NETWORK 정리

## DAY 1_1

### LAN, WAN 
- LAN : Local Area Network - 공유기나 스위치를 사용해서 연결
- WAN : Wide Area Netwrok - LAN 과 LAN 사이를 연결해 줌

### 네트워킹 방법
- Ethernet
    - `CSMA/CD(한대의 컴퓨터가 독차지)` : `Carrier Sense Multiple Access / Collision Detection` = Carrier 에 없는 것을 보고 통신 신청 "대충 알아서 눈치로 통신하자"
    - [참고](http://itwiki.kr/w/CSMA/CD)
- 토큰링(TokenRing)
    - 순서를 기다리면서 차례로 통신
    - 장점 : Collision이 없다.
    - 단점 : 비효율적이다(보낼 것이 없어도 토큰을 받게 됨.)

```
케이블
    종류 : 광케이블, UTP케이블, 동축 케이블
    
    UTP케이블
        Unshielded Twisted Pair
        UTP, STP
```

### 맥 어드레스(Media Access Control Address)
- IP To MAC : ARP (Address Resolution Protocol)
- 라우터
- IP주소가 있어도 맥어드레스가 사용된다 ==> 보안 땜시?
- ARP에 대해서 알아보자    
- 통신방법(p.38) (BroadCast)
    
- 6 octet, octet = 8bit => 48bit
- 앞 6자리 = 벤더(생산자, OUI{Organizational Unique Identifier})
- 벤더를 보고 어느 회사에서 만든 것인지 알 수 있다.
- 뒤 6자리 = 일련번호 

### 유니캐스트
 - 프레임 : (출발지MAC주소, 목적지MAC주소) 목적지 주소를 본인의 MAC주소와 비교하고 같지않다면 그 프레임을 버림.
 - Ex: 편지

### 브로드캐스트
- Local LAN에 모든 네트워크 장비들에게 보내는 통신.
- Ex: 이장님 방송
- Local LAN이란 라우터로 구별되어진 공간(브로드캐스트 도메인).
- 일단 프레임을 받는다. 그리고 CPU가 처리한다 => CPU 성능 저하. 
- ARP : BroadCast => 30 sec to 1min 마다 한번씩 

### 멀티캐스트
- 동시 송출시 유니캐스트는 비효율적.
- 유니캐스트와 브로드캐스트의 장점을 가져옴.
- 스위치나 라우터에서 이 기능을 지원해줘야함.

### OSI 7 Layer (APSTNDP)
- Application 
- Presentation
- Session
- Transport
- Network
- Data Link
- Physical 

- 계층 구별 이유
1. 데이터 흐름이 한눈에 보임
2. 문제 해결하기 편리함.

    `Pysical` : 전기적, 기계적, 기능적임.
    0 과 1 에 해당되는 전기적 ON, OFF
    - 통신 케이블, 리피터, 허브

    `Data-Link Layer`
    정보의 오류와 흐름을 관리. 안전한 정보의 전달 수행을 도움.
    통신에서 오류를 찾고 재전송하는 기능도 있으며 맥 어드레스로 통신 가능 하게함.
    - 브리지, 스위치

    `Network Layer`
    목적 : Routing => 안전하고 빠르게 데이터를 목적기까지 안전하게 전달.
    
    등 등...
     
### Protocol
- 인터넷 통신을 하기 위한 규약

- TCP/IP => Trnsmission Control Protocol / Internet Protocol
- IPX => Internetwork Packet Exchange
- Appletalk => 매긴토시

### TCP/IP
- ARPANET에 의해 개발됨
- Internet Network Information Center(InterNIC)

### IP
- 컴퓨터마다 고유한 IP를 가지게 된다.
- 32 bit로 이루어짐
- NIC(Network Information Center)라는 곳에서 공인주소를 나눠주고 관리한다. IP 주소

- PAT, NAT

- IPX(Internetwork Packet eXchange)
    - 파일을 한곳에 두고(파일 서버) 공유하여 통신하는 프로토콜
    - Local 에서는 빠르지만 인터넷에서는 성능이 조금 떨어짐.

- IPv6
    - 다 떨어져가는 IP주소를 충당해주기 위해서 만들어짐. 128bit로 이루어짐. 

- DHCP(Dynamic Host Configuration Protocol) : 자동배정
    - IP를 가지고 있지 않고 서버가 관리. 필요할 때만 요청시 배급. 


### 이진수
- AND 연산
- 서브넷 마스크시 아주 긴요하게 쓰임

## DAY 1_2



### 허브(HUB)
- aka, Multiport Repeater : 한 포트로 들어온 데이터를 나머지 모든 포트로 뿌려준다.
- 거리가 먼 통신연결을 해주는 역활도 한다.
- 그냥 허브(10Mbps), 패스트 허브(100Mbps)
- Collision Domain : Collision이 일어날 수 있는 영역 (같은 허브 = 같은 Collision Domain)
- Shared Hub : 한번에 한 PC만이 데이터를 보낼수 있는 허브
- Hub의 한계 : 병렬적인 Data처리 불가
- Collision Domain이 커질시 Collision 또한 증가. 이를 해결하기 위해서 Bridge 또는 Switch 사용.
- Intelligent Hub : NMS(네트워크 관리시스템)이 원격으로 모든 데이터를 분석, 제어할수 있다. 이상한 데이터가 계속 들어올 때(계속 Collision 발생 시) 자동으로 Isolation 시켜버리고 따로 램프로 표시가 된다. 이를 Auto Partition이라고 부른다.  비싸다(개인용으로는 부적합). 
- Dummy Hub
- SemiIntelligent Hub
- Stackable vs. Standalone
- Stackable은 상호간의 연결이 효율적으로 설계되어 있다.Backplane (장비 간에 데이터 전송을 위해 연결된 일종의 고속도로)가 빨라지고, 하나가 고장이 나도 다른 장비에 영향을 미치지 않음. 한대의 장비처럼 사용가능
- 여러대의 허브나 스위치 사용시 Stackable. Else Standalone

### Switch
- 포트별로 Collision Domain이 나눠져있다.
- 허브에 비해 데이터를 처리하는 방법이 우수하며 전송 에러를 복구해주는 기능 등이 있다.
- 트래픽이 많은 경우 Switch 사용
- 하지만 하나로의 경로로 향하는 경우 (서버로) [ 그림] hub나 스위치나 비슷함.
- 요즘엔 그냥 스위치 쓴다고 함.

<네트워크 그림>

### Bridge
- Switch의 원조.
- Collision Domain 사이를 반으로 나누고 중간에 다리를 둔다. <Bridge 사진>

### Bridge / Switch
- 작동원리
    - Learning : 새로운 프레임이 수신될 시 MAC Adress Table (Bridge Table)에 추가
    - Flooding : 프레임이 MAC Adress Table에 존재하지 않을 시 송신한 포트제외한 모든 포트에게 뿌린다.
    - Forwarding : 프레임이 MAC Adress에 존재할 시 같은 Segment인지 확인하고 같지 않다면 목적지 주소가 있는 곳으로 Forwarding 시킨다. 
    - Filtering : 프레임이 MAC Adress에 존재할 시 같은 Segment인지 확인하고 만약 그렇다면 bridge를 건너는 것을 막는다.
    - Aging : MAC Adress Table이 갱신되면 Timer를 가동시키는데 일정 시간이 지나면 테이블에서 삭제시킨다. 만약 타이머가 가고있는 도중 해당 프레임이 들어올경우 타이머를 리셋하는데 이를 Refresh라고 한다. 
- 차이점
    - Switch가 ASIC이라서 처리속도가 Software적으로 처리하는 Bridge보다 빠름.
    - Switch는 서로 다른 속도를 연결해 줄 수 있는 기능 제공
    - 포트 수가 많음
    - cut-through, store-and-forward 방식 제공 vs. store-and-forward
        - Store-and-forwarding : 프레임을 모두 받아드린다. 에러 복구능력이 뛰어나서 회선상에 에러가 자주 발생하는 경우 자주 사용된다.
        - Cut-through : 처음 48 bit만 봄. 에러복구에는 약함
        - Fragment-Free : 처음 512 bit 만 봄. Cut-through 보다는 에러감지능력이 좋음
    - 인데 Store-and-forward 가 빨라져서 Cut-through 속도에 뒤지지 않는다.

[사진]

### Looping
- 프레임이 네트워크상에서 무한정으로 도는 현상
- 하나의 호스트에서 다른 호스트로 가는 경로가 두개 이상 있을시 발생가능
- Broadcast Packet이 두개 이상의 스위치를 통과하면 계속 반대편 스위치로 들어가는 현상 
- 방법론 : Spanning Tree Algorithm 
[Spanning Tree Algorithm]
- 두개 이상의 경로 존재시 하나 제외하고 모든 경로들을 막아두었다가 기존경로에 문제 발생시 사용한는 방법
- 새로운 링크 연결시 대략 1분 이상 소요. Uplink Fast 사용시 2~3초만에 가능
- Ether-Channel 기술 : 여러개의 링크가 마치 하나의 링크처럼 인식되게 하는 기술. Fastereher Channel(100 메가로 연결된 포트들 연결), Giga Ether Channel(1000 메가로 연결된 포트들 연결) 등이 있다.
- 그림
- Fault Tolerant vs. Load Balancing
상황발생 시 대비책. 일을 나눠서하는 것
Load Balancing > Fault Tolerant 

### Router
- 브로드캐스트 도메인을 나누기 위해 필요하다.
- 스위치가 보장 못 하는 보안기능, 패킷 필터링(불필요한 트래픽이 전송되는것을 막는)기능을 제공한다.
- 로드분배기능을 제공한다.
- QoS(프로토콜이나 데이터의 크기, 중요도에 따라 트레픽의 순서를 조정해주는) 기능도 제공.

### IP
[라우터 인터페이스 그림]
- Cerial Interace vs. Ethernet Interface
- CSU, DSU : 통신속도에 따른 디지털 모뎀의 종류 CSU : 56kps~64kbps의 전용회선에서 사용 , DSU : 128kbps, 3km 이상
- 네트워크 : 하나의 브로드캐스트 영역, 라우터를 거치지 않고도 통신이 가능한 영역
- 호스트 : 각각의 PC장비
- 네트워크부분은 같아야 하고 호스트 부분은 달라야 정상적인 통신가능.
- [그림 5-2 같은 그림]

### IP Address
5개의 클래스로 구분된다.
그 중 두개는 멀티캐스트용과 연구용이다. 
하나의 네트워크가 호스트의 수를 몇 개까지 가질 수 있는가에 따라서 클래스가 나뉜다.


- Class A
    - 이진수 IP 주소가 0으로 시작한다. 0xxx.xxxx.xxxx. ... .xxxx
    - 최소, 최대 : (0.0.0.0 ~ 127.255.255.255) 
    - 상위 8 bit = Network ID     

- Class B
    - 이진수 IP 주소가 10으로 시작한다. 10xx.xxxx.xxxx. ... .xxxx
    - 최소, 최대 : (128.0.0.0 ~ 191.255.255.255)
    - 상위 16 bit = Network ID

- Class C
    - 이진수 IP 주소가 110으로 시작한다. 110x.xxxx.xxxx. ... .xxxx
    - 최소, 최대 : (192.0.0.0 ~ 223.255.255.255)
    - 상위 24 bit = Network ID

브로드캐스트 주소 : 네트워크의 마지막 주소(호스트 부분이 모두 1일경우)
네트워크 주소 : 네트워크의 처음 부분(호스트 부분을 모두 0일 경우) 
###
###
###
###
###
###
###
