# DeterministicRunHybridPathGateway · 실제 코드 발췌

[목록](README.md)

원본 파일: `Assets/Game/V1/Run/Runtime/DeterministicRunHybridPathGateway.cs`

원본 커밋: `309b096c21fbb854fe21997ec46463817340925b`

원본 전체 파일 Blob SHA: `b857b4a624d67f255c790ca3ce3c7307b7f8f459`

발췌 범위: RequestNextNodeCandidates의 기존 후보 재사용 조건. 기존 원본 124행 참조.

이미 제시한 후보 Snapshot을 재사용하는 부분입니다. 요청 검증, 신규 결정론적 후보 생성 및 저장·복원 검증 구현은 이 발췌에 포함하지 않습니다.

```csharp
if (stagePath != null && stagePath.Stage == request.Graph.Stage &&
    stagePath.Phase == HybridPathPhase.AwaitingPath &&
    stagePath.Candidates.Count > 0)
{
    candidates = stagePath.Candidates;
    return true;
}
```

**검증 범위:** 원본 기준 커밋에서 코드의 존재와 내용을 확인했습니다. 이번 증빙 정리에서는 Unity 컴파일, EditMode/PlayMode Test Runner, 실제 플레이를 실행하지 않았습니다. 읽기용 발췌이며, 필요한 클래스·설정·Fixture 등을 생략하여 단독 실행하거나 컴파일할 수 없습니다. 원본의 들여쓰기만 읽기 좋게 조정했으며 새로 재구현한 예시 코드로 대체하지 않았습니다.
