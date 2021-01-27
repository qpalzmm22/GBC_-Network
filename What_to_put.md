# NETWORK 정리

## Day1_1

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

### LAN 카드PCI