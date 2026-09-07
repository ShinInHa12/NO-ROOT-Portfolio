# RunControllerHybridPathIntegrationTests · 실제 코드 발췌

[목록](README.md)

원본 파일: `Assets/Game/V1/Tests/EditMode/RunControllerHybridPathIntegrationTests.cs`

원본 커밋: `309b096c21fbb854fe21997ec46463817340925b`

원본 전체 파일 Blob SHA: `bf0724cfe22aca680bf4272f7a328121e131ad7f`

발췌 범위: CommitThenEnter_IsExplicitAndDuplicateCallbacksCannotAdvanceTwice의 선택 반복 검사 연속 발췌.

같은 후보를 두 번 선택해도 Commit이 한 번만 증가하고, 선택 확정만으로 방 진입 횟수가 증가하지 않는지를 검사합니다. Fixture, Setup 및 이어지는 Node 진입 검사 등은 생략했습니다. NUnit/Unity 프로젝트 의존성이 필요하며 이번 작업에서 실행하지 않았습니다.

```csharp
Assert.That(
    fixture.Run.CommitPathSelection(selected.CandidateStableId),
    Is.True);
Assert.That(
    fixture.Run.CommitPathSelection(selected.CandidateStableId),
    Is.True,
    "A repeated UI callback for the committed candidate must be idempotent.");
Assert.That(fixture.Run.CommitLedger.Commits,
    Has.Count.EqualTo(commitsBeforeSelection + 1));
Assert.That(fixture.Run.RoomFlowState, Is.EqualTo(RunRoomFlowState.PathSelected));
Assert.That(fixture.Run.CurrentHybridPathPhase,
    Is.EqualTo(HybridPathPhase.PathSelected));
Assert.That(fixture.Run.CurrentSemanticStageState.SelectedRoomCount, Is.Zero,
    "Selection commit and semantic node entry are separate transactions.");
```

**검증 범위:** 원본 기준 커밋에서 코드의 존재와 내용을 확인했습니다. 이번 증빙 정리에서는 Unity 컴파일, EditMode/PlayMode Test Runner, 실제 플레이를 실행하지 않았습니다. 읽기용 발췌이며, 필요한 클래스·설정·Fixture 등을 생략하여 단독 실행하거나 컴파일할 수 없습니다. 원본의 들여쓰기만 읽기 좋게 조정했으며 새로 재구현한 예시 코드로 대체하지 않았습니다.
