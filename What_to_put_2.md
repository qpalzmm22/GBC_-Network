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


## DAY 2_2
ISL Trunking
IEEE802.1Q Trunking
Native VLAN Untagged traffic
ISL

Server mode
Client mode
Transparent mode


VTP Pruning 