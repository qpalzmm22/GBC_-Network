## Day 3_1

### Wireless Network
- 무선 통신을 위해서 무선통신과 유선 토신을 연결시켜주는 AP(Access Point)가 필요하다. 
- 무선 통신은 **IEEE802.11**을 표준으로 사용한다.,
- CSMA / CA : Collision Sense Multiple Access / Collision Avoidance : 충돌을 최대한 피하는 형식.
- IEEE802.11
    - Listen Air Space : 통신이 일어나고 있는지 확인한다.
    - Wait Random time before sending : 데이터를 random 한 시간 기다렸다가 보낸다
    - Listen again : 진짜 통신 해도 되는지 다시 통신이 일어나고 있는지 확인한다.
    - Wait for ACK : 데이터를 잘 받았다는 신호(ACK)를 기다린다.
    - If no ACK, restart the process : 정해진 시간안에 (ACK)을 못 받으면 `Listen Air Space` 부터 다시 시도한다.

- Ad Hoc mode : 무선 통신 능력을 가진 두개 이상의 장치로만 통신하는 것. 별도의 기반시설을 필요로 하지 않는다.
    - IBSS(Independent BSS) : 외부의 관섭없이 소통.
- Infrastructure mode : 별도의 기반시설(AP를 사용하는 Router)를 사용하여 통신하는 것.
    - BSS(Basic Service Set) : AP 1대 사용
    - ESS(Extended Service Set) : AP 여러대 사용 (용량이 부족하거나 거리가 멀거나)
    - AP간에 주파수가 중첩되면 안된다. (IEEE802.11의 경우 3개까지 사용 가능)
- 주파수 대역과 속도에 따른 무선 랜 통신 표준이 있다.
- 멀리있는 AP와 통신을 가능케하기 위해 지원속도가 여러가지가 있다. 
 
|무선표준|IEEE802.11b|IEEE802.22g|IEEE802.11.a|
|--|--|--|--|
|최대속도|11Mbps|54Mbps|54Mbps|
|지원속도|1, 2, 5.5, 11Mbps|6, 9, 12, 18, 24, 36, 48, 54Mbps|6, 9, 12, 18, 24, 36, 48Mbps|
|사용주파수|2.4GHz|2.4GHz|5GHz|
|비 중첩채널|3채널|3채널|23채널(한국은 19)|

### Encoding
- 데이터를 무선신호로 바꾸는 과정
- FHSS(Frequency Hopping Spread Spectrum) : 무작위로 채널을 도약하며 도약전에 대상 채널에 잡음 또는 전파관섭이 있을경우 다른 채널로 Hopping 한다. IEEE802.11a, 11b, 11g는 이 방식을 사용하지 않는다.
- DSSS(Direct Sequence Spread Spectrum) : 한 채널로만 통신을 하는 방식. 낮은 전력으로 넓은 대역으로 전송하기 때문에 잡음에 영향을 덜 받고 다른 통신에도 영향을 덜주며 보안에도 우수하다. IEEE802.11b 에서 사용한다. 
- OFDM(Orthogonal Frequency Division Muliplexing) : 하나의 시그널을 직교성을 이용하여 여러개의 주파수로 나누어 보내는 방식. IEEE802.11a, 11g에서 이를 사용한다.


### IPv4의 문제점
- IPv4 사용 인구 증가
- IPv4 의 불필요한 헤더 제거
- 어려운 aggregation process => 복잡한 routing table
- 효율적이지 못 한 보안기능, Mobile IP

### IPv4 주소부족 해결방안
- NAT(Network Address Translation)
    - 외부 망과 통신 할때만 IP를 달고 나가는 것.
    - IP 변환하는 시간 필요
    - End to End 지원 호환문제
- Subnetting
- DHCP(Dynamic Host Configuration Protocol)
- CIDR(Classless Inter Domain Routing) : Subnet Mask로 클래스를 지정하는 방식. 주도 여러개의 작은 네트워크를 모아서 라우팅 테이블을 줄이는 Supernetting을 위해 사용된다

### IPv6
- IPNG(IP Next Generation)이 1995년도에 `RFC 1883`을 내놓았는데 이가 IPv6의 근간이 된다.
- IPv5는 QoS 제공을 위한 실험적인 Recource reservation protocol 로써 Internet Stream Protocol이다
    - 디지털 사운드나 멀티미디어 데이터와 같은 리얼 타임 데이터를 효과적으로 전송하기위해 만들어진 프로토콜

## 변화된 IP 주소 
- IPv6의 특징
    - 넓어진 주소
    - Header 간편화
    - IPv4와 호환

- 주소가 넓어짐(Global Address)
    - Flexibility : 융통성 있는 주소 배정 가능
    - Easy Aggregation : 주소를 묶어주기 쉬움
    - Multihoming : 두개 이상의 네트워크에 연결해 문제가 있을 시 돌아가는 길을 마련하는 것.

- 주소의 크기 : 32 bit x 4 = 128 bit
- 주소공간의 크기 : 3.4e38

### 넓어진 주소의 이점
- Global Reachability : 전 세계의 네트워크 어디에서나 주소를 변경하지 않고(고유의 주소로) 접속이 가능하다는 것.
- End to End Reachability : 주소 변환이 없이 송신지에서 수신지까지 통신하는것
- Hierarchical Addressing(Addressing Hierarachy) : 긴 주소를 목차 나누듯이 나눈다.
    - Aggregation이 효과적으로 가능[그림(Aggregation이 뭔지)]
    - Prefix Aggregation : 라우팅 테이블을 줄이고 라우팅을 효과적으로 빠르게 진행가능해진다.
    - 트래픽 감소(카풀 느낌)
- Stateful Auto Configuration : 어떠한 상태를 유지시키며 자동 구성을 시켜준다. Ex : DHCP : 특정 서버에서 테이블을 관리하며 IP분배 
- Stateless Auto Configuration : 특정 서버 없이 자동으로 호스트의 IP 구성 가능.
 
Auto Configuration step
1. 48 bit MAC 주소 => 64 bit MAC 주소
1. Router에게 64 bit prefix를 받는다
1. 둘이 합쳐 IPv6주소가 된다.
- DHCPv6 : DNS 서버, NTP 서버 정보, SIP 서버나 Novell Directory 서비스 정보 구성을 도운다.
- Stateless auto => Stateful Auto if flags exists
- IPv6에서는 브로드캐스트 대신 멀티캐스트 사용
    - 4 bit 짜리 scope ID
- 불필요한 헤더는 반으로 줄였지만 주소 길이가 늘어나 주소 처리 속도는 늘었다.
- Mobility = 움직면서 인터넷을 사용할 수 있는 능력이 built-in 되었다.
- 보안 좋아짐 IPSec이 default로 들어간다.

### IPv6 표기방식
1. 16진수로 4자리마다 `:`으로 구분한다.
1. 앞쪽에0 오는 0은 안써도 된다.
1. 0이 연속으로 나올 때는 `::`으로 대체 가능하지만 딱 한번만 가능하다.

- Multicast 가 broadcast 역활을 함. 
- Anycast : 가장 가까운 라우터에게 패킷을 보내는 형식. 탐색 메카니즘에 쓰인다.

### IPv4, IPv6 혼동 사용법
- Dual-Stack : IPv4, IPv6 둘다 인식 가능하게 해서 IPv6를 인식 못하는 경우 IPv4를 사용하는 방식. [그림]
- Tunnel 방식 : IPv4 패킷에 IPv6패킷을 캡슐화(encapsuplation) 한다. [그림]
    - Tunnel이 어떤 식으로 만들어지냐에 따라 메뉴얼 방식, 반자동 방식, 자동방식 으로 나누어진다.

