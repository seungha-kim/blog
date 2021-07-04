# 2021-07 실시간 동시편집 웹 어플리케이션 PoC - Rust, WASM 이야기


Why Rust?

- 원래부터 좋아하는 언어라 그냥 쓰고 싶어서... + Figma 에서 썼다고 해서
- Client, server 에서 같은 언어를 썼을 때 장점이 있을 거라 생각했음
- serde 로 de/serialization 작업 대충 빠르게 작성
- 최근 async/await API 및 그 생태계가 성숙되어 안정된 API에 기반해서 웹/소켓 서버를 만들 수 있게 되었다.


- serde, serde-json, bincode, ...
- euclid
- actix-web
- 프로토콜 계층화 enum
- async trait 없어서 아쉽

### web -> wasm 인터페이스

- command

### wasm -> web 인터페이스

- material: invalidation 단위
