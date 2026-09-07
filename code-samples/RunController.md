# RunController · 실제 코드 발췌

[목록](README.md)

원본 파일: `Assets/Game/V1/Run/Runtime/RunController.cs`

원본 커밋: `309b096c21fbb854fe21997ec46463817340925b`

원본 전체 파일 Blob SHA: `a1000d6f1a24a1167241fd2d77ee0a5e5c6de62a`

발췌 범위: EnterSelectedNode의 저장 요청 이후 진행 Gate 검사부터 정상 진입까지의 연속 블록.

CommitPathSelection과 EnterSelectedNode는 별도 메서드입니다. 이 블록은 저장 요청에 따라 Gate가 닫히면 전투 시작을 보류하는 흐름입니다. Gateway, 저장 이벤트 구독자, 앞부분의 Node·콘텐츠 검증과 중복 진입 검사는 생략했습니다. 이 블록 자체가 파일 저장 구현은 아닙니다.

```csharp
durableGateway.CompleteSelectedNodeEntry();
HybridPathStateChanged?.Invoke();
HybridPathPersistenceRequired?.Invoke();
if (IsProgressionBlocked)
{
    RoomFlowState = RunRoomFlowState.EnteringNextNode;
    encounter.QuiesceAtResolvedBoundary();
    return false;
}

nextNodeCandidates = Array.Empty<RunPathCandidate>();
BeginCurrentRoom(stageChanged: false);
NotifySemanticStageStateChanged();
return true;
```

**검증 범위:** 원본 기준 커밋에서 코드의 존재와 내용을 확인했습니다. 이번 증빙 정리에서는 Unity 컴파일, EditMode/PlayMode Test Runner, 실제 플레이를 실행하지 않았습니다. 읽기용 발췌이며, 필요한 클래스·설정·Fixture 등을 생략하여 단독 실행하거나 컴파일할 수 없습니다. 원본의 들여쓰기만 읽기 좋게 조정했으며 새로 재구현한 예시 코드로 대체하지 않았습니다.
