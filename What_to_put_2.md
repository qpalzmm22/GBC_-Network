## Day 2_1

### Router IP 배정
- 네트워크가 다른 두 장비간의 통신은 라우터만을 통해 가능하다.
- TCP/IP통신 시 라우터에도 IP주소를 부여해 주는 것이 좋다.
- IP주소 배정 시 호스트 도메인이 호스트 수 보다 커야 한다.
 
### Default Gateway
- 특정 목적지로 가는 패킷이 수신되었으나 내부 네트워크에서 찾지 못 할때 향하는 "문"
- Router의 Ethernet Interface
- Interface 갯수만큼 존재
- Switch나 허브는 하나씩만 존재(없어도 지장 X)   

### Subnet Mask
- 주어진 IP주소를 네트워크 환경에 맞게 나누어 주기 위해서 씌어주는 Mask.
- 브로드캐스트 도메인이 쓸데없이 크면 브로드캐스트 시 통신망이 어지럽혀지기 때문에 정사적인 통신이 불가능하다.
- 이러한 Subnet Mask로 나누어진 네트워크인 Subnet은 하나의 독립된 네트워크가 된다.
- Default subnet mask는 클래스에 따른 기본 Mask.
- Class A : 255.0.0.0
- Class B : 255.255.0.0
- Class C : 255.255.255.0
- Subnet Mask는 1 사이에 0이 없다.
- Subnet Mask = network 부분을 표시
- Class B를 Class C 처럼 사용 가능.
- 서브넷 마스크 사이에는 라우터가 필요하다.
- host갯수 연산시 맨 처음과 맨 마지막 주소는 각각 네트워크 주소로, Broadcast를 위해서 쓰인다.
- 2^(host bit 수) - 2 = (host 갯수), Upperbound(log(host 수 + 2)) = host bit 수

```
1111 1111  255 = 256 - 2^(0의 갯수) => 256 - (Mask) = host bit 수
1111 1110  254
1111 1100  252
1111 1000  248
1111 0000  240
1110 0000  224
1100 0000  192
1000 0000  128
0000 0000    0
```

### MAC Address
- Cisco Swtich 저장 방식
    - Dynamic 방식
    - Permanant 방식 (static)
        - 지워지지 않음
        - 자동 수정 불가
        - 메모리 낭비
        - 서버나 고정장비
MAC Table 

### 가상랜(Virtual LAN)
- 한 대의 스위치를 여러 개의 네트워크로 나누기 위해 사용(브로드캐스트 도메인 분활)
- 보안을 위해서(만약 지역이랑 LAN 주소랑 연간이 있다면 그만큼 information 이 leak 되기 때문?)
- VLAN 사용 시 한대의 스위치를 여러 대의 분리된 스위치 처럼 사용 가능하며 여러개의 네트워크 정보를 하나의 포트를 통해 전송이 가능하다.
 [그림이 좋을듯]
**다른 네트워크와의 통신은 반드시 라우터를 거쳐야 한다.**
- Trunk Port : 하나의 포트를 통해 서로 다른 여러개의 VLAN을 전송할 수 있게 하는 포트
- Dynamic VLAN : DHCP 처럼 VMPS(VLAN Memebership Policy Server)가 장비의 MAC 주소를 받아 그에 해당하는 VLAN을 지급하는 형식 


## DAY 2

### Router
- 가장 빠르고 효율적인 길을 찾는다.: 
- 네트워크 계층에서 동작하기 때문에 Layer 3 장비라고 부른다.
- Router가 하는 일
    - Path Determination
    - Switching
        - Routing Algorithm(Routing Protocol) : Routing Table 사용해서 가장 빠르고 안전한 길을 찾는다.    
- Router는 CPU, Memory, Interface를 가지고 있다.

- Routed Protocol vs. Routing Protocol
- Routed Protocol
    - TCP/IP, IPX, AppleTalk 등, 라우터가 라우팅을 해주는 프로토콜.
- Routing Protocol
    - RIP(Routing Information Protocol)
    - IGRP(Interior Gateway Routing Protocol), OSPF(Open Shortest Path First), EIGRP(Enhanced Interior Gateway Routing Protocol)
    - 라우팅 테이블을 가지고 있으며 자기가 찾아갈 경로에 대한 정보를 이곳에 기억해둔다.
### Static vs. Dynamic Routing Protocol
    - Static Routing Protocol
    - 사람이 일일이 경로를 입력해주는 것.
        - 성능 좋고, 메모리도 적게듬.
        - 네트워크 대역폭 절약 가능
        - 보안에도 좋음(외부에 자신의 정보를 알리지 않기 떄문에)
        - 귀찮다.
        - 경로에 문제가 있을 때 직접 수정을 해줘야 함 문제 생김 (Humman Error)
    -  Dynamic Routing Protocol
        - 라우터에 부담을 준다.
        - RIP, IGRP, OSPF, EIGPR 이 예시

### Routing table
- 목적지와 목적지로 가려면 어느 인터페이스로 가야 하는지를 라우팅 테이블에 가지고 있다. 
[그림]
- 라우터의 protocol에 따라 달라진다.
- 최적의 경로를 찾아 라우팅 테이블에 유지한다.
- Routing table은 RAM에 올라가기 떄문에 휘발성이다.

### Autonomous System
- 하나의 관리 규정에 따라 운용되는 라우터의 집단
- 라우터가 가지는 정보를 효율적으로 관리하고 인터넷 서비스를 좀 더 간편하게 하기 위해서
- 외부의 정보를 필요로 할때 ASBR(Autonomous System Boundary Router)를 통해 통신한다.
- Router들을 자신이 속한 AS에 대한 정보만 있으면 된다. 
- AS 내부에서 사용하는 Routing Protocol을 Interior Router Protocol, Interior Gateway Protocol(IGP)라고 부른다. 그 예로는 RIP, IGRP, EIGRP, OSPF 등이 있고
- AS 외부에서 서로 라우팅 정보를 주고 받을 때 사용하는 프로토콜을 Exterior Routing Protocol, Exterior Gateway Protocol(EGP)라고 부른다. 그 예로는 EGP, BGP 등이 있다.
[그림]
### Distance Vector vs. Link State
- 라우팅 프로토콜의 종류
- 라우팅 테이블을 어떻게 관리하느냐
- Distance Vector
    - 목적지까지의 거리와 어떤 인접라우터를 거쳐서 가야하는지를 저장
    - 30초에 한번씩 정보를 교환해서 변화를 감지한다.
    - 메모리를 절약하고 간단하다.
    - 정해진 시간마다 업데이트가 필요해 쓸대없는 트래픽이 발생한다.
    - 라우팅 테이블에 변화가 생길경우 모든 라우터가 알 때까지 걸리는 시간(Convergence Time)이 너무 느리다. 
    - 홉 카운트가 15를 넘지 못 하게 되어있다.
    - 작은 규모의 네트워크에 적합
    - RIP, IGRP 가 그 예
- Link State
    - 한 라우터가 목적지까지의 모든 경로 정보를 다 알고 있다.
    - Topology Table을 만들고 이를 이용새 SPF(Shortest Path First)알고리즘을 계산한다.
    [SPF 그림]
    - 링크의 변화가 생겨도 이를 알아내는데 걸리는 시간이 짧다.
    - 정보 교환시 변화가 있는 것만 교환하여 트래픽 발생을 줄인다.
    - 메모리가 많이 소모된다. SPF 계산을 해야하기 때문에 CPU 또한 많이 사용된다.
    - OSPF가 그 예

### Ping 과 Trace
- 네트워크에 이상이 없는지 테스트하는 프로그램
- Ping
    - 네트워크 상태를 확인하려는 대상(target) 컴퓨터를 향해 일정 크기의 패킷을 보낸후(ICMP echo request) 대상 컴퓨터가 이에 대해 응답하는 메시지(ICMP echo reply)를 보내면 이를 수신, 분석하여 대상 컴퓨터가 작동하는지, 또는 대상 컴퓨터까지 도달하는 네트워크 상태가 어떠한지 파악한다.
- 확장형 Ping
    - Protocol, Target IP, Repeat Count(Echo message를 몇번 보낼지), source adress 등을 설정하여 보네어 송신하는 IP주소를 달리 하여 그곳의 네트워크의 이상여부를 확인할 수 있다.
- Trace
    - 출발지에서 목적지뿐만 아니라 중간 경로에 대한 정보와 소요시간을 확인해준다.
    - TTL(Time To Live)을 사용한다.
        - Router를 하나씩 거칠 때마다 1씩 감소.
        - 1 ~ 목적지까지 하나씩 올리면서 Error message를 받음으로 경로를 추적한다.
        - 무한 루핑을 도는 것을 방지하기 위해. 