# Socket Programming

Socket Programming = Network Programming
Socket = 두 컴퓨터간의 연결

소켓에서 함수를 생성하기 위해 필요한 library

<sys/socket.h>

- listening Socket

1. 소켓 생성
2. IP주소와 PORT 번호 할당
3. 연결요청 가능 상태로 변경
4. 연결요청 수락


socket(int domain, int type, int protocol); // 소켓 생성용 함수

소켓 생성후 IP번호와 포트번호를 할당 받아야 한다.

bind(int sockfd, struct sockaddr *myaddr, socklen_t addrlen); // 소켓 정보 할당

listen(int sockfd, int backlog); // socket을 연결요청 가능 상태로 변환

accept(int sockfd, struct sockaddr *addr, socklen_t *addrlen); // 연결요청 수락

- Client Socket 

connect(int sockfd, struct sockaddr *serv_addr, socklen_t addrlen); // 연결 요청을 하는 소켓(client)이 연결 요청을 하는 함수  

---
Linux 에서 Socket은 파일과 동일하게 간주된다. 

저수준 파일 입출력(Low-level File Access), 파일 디스크립터(File Descriptor) 

파일 디스크립터 : 시스템으로부터 할당 받은 파일 또는 소켓에 부여된 정수. 윈도우에서는 주로 파워핸들이라고 부른다.

파일과 소켓은 생성의 과정을 거쳐야 운영체제가 파일 디스크립터를 할당한다.

아래의 3가지는 생성과정을 거치지 않아도 프로그램이 실행되면 자동으로 할당된다.
파일 디스크립터 | 대 상(Target)
0 : 표준입력 : Standard Input 
1 : 표준출력 : Standard Output
2 : 표준에러 : Standard Error

open(const char *path, int flag); //파일을 열때 사용하는 함수

FLAG 값
O_CREAT : 필요하면 파일 생성
O_TRUNC : 기존 데이터 삭제
O_APPEND : 기존 데이터 보존, 뒤에 이어서 저장
O_RDONLY : 읽기 전용으로 파일 오픈
O_WRONLY : 쓰기 전용으로 파일 오픈
O_RDWR : 읽기, 쓰기용으로 파일 오픈

close(int fd); // 소켓을 닫을때도, 파일을 닫을때도 다음의 함수가 쓰인다.

ssize_t write(int fd, const void * buf, size_t nbytes); // (fd)파일에 *(buf)데이터를 nbytes만큼 write.

ssize_t = signed int 

Primitive 자료형 : typedef로 일반적인 자료형에 이름을 붙힌 것. 운영체제 처리단위(32bit, 64bit)에 따라 데이터의 크기 또한 변경되기 때문에 코드의 변경을 최소화 하기위해서 ssize_t, size_t 등을 쓴다. _t 가 붙으면 struct 된 자료형이다.

ssize_t read(int fd, void *buf, size_t nbytes); // fd의 내용을 buf에 nbytes 만큼 읽어드리는 것.

소켓도 파일이라 이러한 함수들이 소켓에도 적용이 된다. 
파일과 소켓은 순서대로 File Discrpitor가 numbering 된다.

## Ch 2
Protocol : 컴퓨터 상호간의 대화에 필요한 통신규약

socket(int domain, int type, int protocol); // 소켓 생성용 함수

domain : 소켓이 사용할 프로토콜 체계(Protocol Family) 정보 전달
type : 소켓의 데이터 전송방식에 대한 정보 전달
protocol : 두 컴퓨터간 통신에 사용되는 프로토콜 정보 전달 

## 프로토콜 체계(Protocol Family)

sys/socket.h에 선언되어 있는 프로토콜 체계

PF_INET : IPv4 인터넷 프로토콜 체계
PF_INET6 : IPv6 인터넷 프로토콜 체계
PF_LOCAL : 로콜 통신을 위한 UNIX 프로토콜 체계
PF_PACKET : Low Level 소켓을 위한 프로토콜 체계
PF_IPX : IPX 노벨 프로토콜 체계

## 소켓의 타입(Type)
소켓의 데이터 전송방식을 의미.
- SOCK_STREAM
- SOCK_DGRAM