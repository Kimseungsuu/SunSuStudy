## 정의
```
두 프로그램 간의 메시지를 교환하기 위한 통신 방법 중에 하나

HTML5에서 많이 사용됨
```

## 특징
#### 1. 양방향 통신
	데이터 송수신을 동시에 처리
    클라와 서버가 서로에게 원할 떄 데이터를 주고 받을 수 있음
    기존의 http통신은 클라가 요청을 보내는 경우에만 서버가 응답할 수 있었음
    커넥션이 open, close 된 여부를 따짐
#### 2. 실시간 네트워킹 Real Time Networking
	웹환경에서 연속된 데이터를 빠르게 노출시켜야 할 때 곧잘 사용
	채팅, 주식, 비디오 데이터
    친구들과 채팅을 한다면 친구들과 연결된 것이 아니라 같은 websocket 서버에 들어가 있는 상태인거
    여기서 브라우저 끼리 연결을 시켜버리는 개념이 WebRTC. P2P 커뮤니케이션
	여러 단말기에 빠르게 데이터를 교환

#### 3. Polling, Long Polling, Streaming과의 차이
	서버로 일정 주기로 요청을 보냄
	real time 통신에 비해서 불필요한 요청을 보내게 됨 
    header가 불필요하게 큼