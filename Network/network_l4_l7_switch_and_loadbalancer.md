## L4, L7 스위치

### L7스위치

애플리케이션 계층을 처리하는 기기. 로드밸런서라고도 하며, 서버의 부하를 분산하는 기기이다. 클라이언트로부터 오는 요청들의 뒤쪽의 여러 서버로 나누는 역할을 하며 시스템이 처리할 수 있는 트래픽 증가를 목표로 한다.

- 스위치 : 여러 장비를 연결하고 데이터 통신을 중재하며 목적지가 연결된 포트로만 전기신호를 보내 데이터를 전송하는 통신 네트워크 장비이다.

### L4스위치

인터넷 계층을 처리하는 기기. IP와 포트를 기반으로(특히 포트를 기반으로) 트래픽을 분산한다.

| L4 스위치                                                                                                              | L7 스위치                                                                                                                                                 |
| ---------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| - IP, 포트를 기반으로 트래픽을 분산 - 클라우드 서비스(AWS)에서 NLB(Network Load Balancer) 컴포넌트로 로드밸런싱을 한다 | - IP, 포트 외에도 URL, HTTP 헤더, 쿠키 등을 기반으로 트래픽을 분산 - 클라우드 서비스(AWS)에서 ALB(Application Load Balancer) 컴포넌트로 로드밸런싱을 한다 |

- 핼스 체크
  - 전송 주기와 재전송 횟수 등을 설정한 이후 반복적으로 서버에 요청을 보내는 것
  - L4, L7 스위치 모두 헬스 체크를 통해 정상적인 서버, 비정상적인 서버 판별
- 서버 이중화
  - 로드밸런서의 대표적인 기능
  - 서비스를 안정적으로 운용하기 위해 2대 이상의 서버를 기반으로 가상 IP 제공

### 로드밸런서 방법

- 라운드 로빈 (Round Robin)
  - 요청이 들어오는 대로 서버마다 균등하게 요청을 분배한다.
  - 단순히 순서에 따라 세션을 할당하므로 경우에 따라 경로별로 같은 처리량이 보장되지 않는다.
- 가중치 및 비율 할당 방식 (Weighted Round Robin Scheduling)
  - 라운드 로빈 방식으로 분배하지만, 서버의 가중치에 따라 요청을 더 분배하기도, 덜 분배하기도 한다.
  - 특정 서버의 성능이 월등히 뛰어나다면 해당 서버에게 높은 가중치를 부여한다.
- 최소 연결 (Least Connection)
  - 가장 적은 세션을 가진 서버로 트래픽을 보내는 방식이다
  - 가장 많이 사용되는 방식
- 가장 빠른 응답 시간 (Fastest Response Time)
  - 가장 빠른 응답 시간을 보내는 서버로 트래픽을 보내 주는 방식이다
  - 각 서버들의 가용 가능한 리소스와 성능, 그리고 처리중인 데이터 등이 다를 경우 적합한 방식이다.
- 해시 기반 스케줄링 (Source hash Scheduling)
  - 사용자의 IP를 해싱한 후 그 결과에 따라 서버로 요청을 분배하기 때문에 특정 클라이언트는 특정 서버로만 할당하는 방식이다.
- 대역폭 기반 (Bandwidth)
  - 서버들과의 대역폭을 고려하여 트래픽을 분산하는 방식이다.

### 로드밸런서 작동 방식

1. 클라이언트가 브라우저에서 [www.google.com](http://www.google.com) 이라고 입력하면 PC에 설정된 DNS 서버로 DNS 쿼리를 보내고, 로컬 DNS 서버는 www.google.com 을 관리하는 DNS 서버로부터 L4의 VIP 주소를 획득한다.
2. 로컬 DNS 는 획득한 VIP 주소를 클라이언트에게 전송한다.
3. 클라이언트는 획득한 DNS 를 기반으로 L4 VIP 로 http(s) 요청을 한다.
4. LB는 최적의 서비스 서버를 내부 알고리즘을 통하여 선별한 후 요청을 전송하고, 서버 작업 결과를 LB에게 전송한다.
5. 전달 받은 결과를 LB를 통해 클라이언트에게 전송한다.

![image.png](./img/network_loadbalancer_mechanism.png)

VIP(Virtual IP) 가상 아이피 : 장비가 2대가 있고 각각 IP를 가지고 있으면 패킷을 어디에 전송해야할지 모르기 때문에 가상 IP를 사용한다.

→ 가상 IP를 가지고 있는 녀석이 대빵

## 예상 면접 질문

1. L4 스위치와 L7 스위치의 차이는 무엇인가?
2. 로드밸런서의 방법 중 서버의 가중치에 따라 요청을 덜 분배하기도, 더 분배하기도 하는 방법은 무엇인가?
3. 로드밸런서를 사용하는 이유는?

### 참고자료

- [https://velog.io/@corone_hi/로드-밸런서-Load-Balancer](https://velog.io/@corone_hi/%EB%A1%9C%EB%93%9C-%EB%B0%B8%EB%9F%B0%EC%84%9C-Load-Balancer)
- https://run-it.tistory.com/44
