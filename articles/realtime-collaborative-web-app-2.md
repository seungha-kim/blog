# 2021-07 실시간 동시편집 웹 어플리케이션 PoC - 구현

통신 프로토콜: 웹소켓 - 큰 고민없이 쓸 수 있다. '메시지' 단위로 추상화. 서버는 클라이언트와 binary 메시지를 주고 받게

Why Rust?

- 원래부터 좋아하는 언어라 그냥 쓰고 싶어서... + Figma 에서 썼다고 해서
- Client, server 에서 같은 언어를 썼을 때 장점이 있을 거라 생각했음
- server 자원을 아낄 수 있다! (관련글 많음)
- algebraic data type..
- serde 로 de/serialization 작업 대충 빠르게 작성
- 최근 async/await API 및 그 생태계가 성숙되어 안정된 API에 기반해서 웹/소켓 서버를 만들 수 있게 되었다.


- serde, serde-json, bincode, ...
- euclid
- tokio, actix-web, channel!
- 프로토콜 계층화 enum
- async trait 없어서 아쉽 - 하지만 async 파트와 sync 파트 나눌 수 있으면 나누는게 여러 면에서 좋은 것 같다.

serde 생산성 짱짱 - 같은 코드 가지고 

serde-json/bincode 미묘한 문제 - tagged union 으로 하려니 그걸 bincode 로 deserialize 못하게 됨 - 깃헙 이슈

bincode -> 프로토콜 계층화를 한다고 enum 중첩을 많이 해놨는데, enum 크기를 너무 크게 잡아서 (u32) 프로덕션에서 그대로 쓰기가 좀..

### web -> wasm 인터페이스

- JSON command (일일이 바인딩 만들기 귀찮다! serde 짱짱! enum 짱짱!)

### wasm -> web 인터페이스

- material: invalidation 단위

## base95

## 트랜잭션을 타는 통신과 안 타는 통신 나누기

- Presence(SessionSnapshot), LivePointer

## 문서 상태와 UI 상태 나누기

## rxjs

(P)react state 를 통한 invalidation -> 비효율적

예를 들어 svg viewBox

invalidation 범위를 좁히기

다만 까다로웠던 점은 behaviourSubject 가 첫 구독시 초기값을 내보낸다는 것... 이거 때문에 하나 따로 만들어서 썼다. 

자주 바뀌는 것과 자주 바뀌지 않는 것 나누기 -> 서버로부터 데이터를 한번에 확 받아와서 그리고 한동안 업데이트를 하지 않아도 되는 것 - (P)react state 쓰면 된다. 1초에 수십 번 씩 바뀌어야 하는 것은 (P)react state 쓰지 않는 것이 좋다.

## 그 밖에

esbuild 써봤는데 빨라서 좋았다. 빌드 속도 관련해서는 전혀 스트레스가 없었음. API도 쓰기 편했음