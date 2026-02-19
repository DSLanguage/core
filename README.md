# DS Core

DS(Dualsoft) 시스템의 핵심 도메인 모델 라이브러리입니다.

## Domain Model

산업 자동화 시퀀스 제어를 위한 계층적 도메인 모델을 정의합니다.

```
Project
  └── DsSystem
        ├── Flow (UI: Button, Lamp, Condition, Action)
        ├── Work
        │     ├── Call
        │     └── ArrowBetweenCalls
        ├── ArrowBetweenWorks
        ├── ApiDef (Parameter)
        └── ApiCall
```

### Parent-Only 구조

모든 엔티티는 `Id`와 `ParentId`만 보유하며, 자식 리스트를 포함하지 않습니다.
중앙 `DsStore`에서 플랫하게 관리하고 쿼리 함수로 탐색합니다.

```fsharp
// 엔티티는 부모 ID만 참조
type Work = {
    Id:       EntityId
    Name:     string
    ParentId: EntityId  // -> DsSystem
}



### 설계 원칙

- **불변성**: F# record 기반, 순환 참조 없음
- **플랫 저장**: `Map<EntityId, T>` 기반 중앙 Store
- **엔티티 이동**: `ParentId` 변경 한 줄로 완료
- **관심사 분리**: 도메인 모델은 DB/직렬화와 독립

## Tech Stack

- F# / .NET 9.0

## License

[MIT](LICENSE)

