# TCP
- full duplex data
	- 동일 연결에서 양방향 데이터 전송
	- MSS : maximum segmant size
- **connection-ortiented**
	- **연결 기반**
	- 3-way handshaking 통한 연결
		1. client -> server : TCP SYN
		2. server -> client : SYNACK
		3. client -> server : ACK segment
- flow control
	- 흐름 제어
	- overflow 하지 않도록 sender가 양 조절
- point-to-point
	- 1:1연결
- reliable, in-order
	- 신뢰성, 오류복구, 순서제어
- pipelining
	- 동시에 여러개 전송 가능

## TCP segment structure
총 32비트
- src port 16bits
- dst port 16bits
- seq number 32bits : bytes of data를 bytestream으로
- ack number 32bits
- 16 bit 째깐이들
	- head len
	- not used
	- C, E : 혼잡 제어
	- A : ack
	- R, S, F : 연결 관리
- receive window 16bits
- checksum 16bits
- options(옵션) 16bits
- apllication data (가변 길이)

## TCP length
14 byte ethernet header
20 byte ip header
20 byte tcp header
실제 길이 : 54 헤더값 뺀 값

## TCP Round Trip TIme and Timeout
- TCP 에러 제어 -> 재전송은 타이버 필수!
- timer 값은 어떻게?
	- RTT보다 길게
	- 적절한 값 설정 -> 평균값 -> 무빙 window avg 값
- `EstimatedRTT = (1-a)*EstimatedRTT + a*SampleRTT` 
	- a는 보통 0.125로 설정
	- EstimatedRTT : 현재 이용 TCP RTT 예측값
	- SampleRTT : 항상 변함
- `DevRTT = (1-b)*DevRTT + b*|SampleRTT-EstimatedRTT|`
	- b는 보통 0.25
	- DevRTT : 편차
- `TimeoutInterval = EstimatedRTT + 4*DevRTT`

## TCP 신뢰성있는 데이터전송
- TCP는 rdt service
	- **ip는 비신뢰성**
- 동시에 여러개 ACK
- 재전송
	1. timeout events
	2. duplicate acks (중복된 ack)
- cumulative acks 누적된 acks

## Fast Retransmit 빠른 재전송
- 타임아웃시간은 상당히 길다(RTT에 비해)
- 중복 ACK에 의해 세그먼트 손실 감지
- **송신자가 3개 ACK를 동일하게 수신하면, 해당 세그먼트가 손실되었다고 판단**

## TCP 흐름 제어
- flow control
	- 송신자는 너무 많이, 빨리 보내지 않게 하여 수신자의 버퍼 오버플로우가 발생하지 않도록 해야 함
- `RcvWindow = RcvBuffer - [LastBtyeRcvd - LastByteRead]` 
- 수신자는 여유공간을 세그먼트의 RcvWindow 필드값으로 송신자에게 알려줌

## TCP 연결관리 상태도
- TCP client lifecycle
	1. CLOSED
	2. SYN_SENT
	3. ESTABLISHED
	4. FIN_WAIT_1
	5. FIN_WAIT_2
	6. TIME_WAIT

- TCP server lifecycle
		1. CLOSED
		2. LISTEN
		3. SYN_RCVD
		4. ESTABLISHED
		5. CLOSE_WAIT
		6. LAST_ACK