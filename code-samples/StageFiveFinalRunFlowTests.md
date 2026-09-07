# StageFiveFinalRunFlowTests · 실제 코드 발췌

[목록](README.md)

원본 파일: `Assets/Game/V1/Tests/PlayMode/StageFiveFinalRunFlowTests.cs`

원본 커밋: `309b096c21fbb854fe21997ec46463817340925b`

원본 전체 파일 Blob SHA: `7f8441bd36c7c2ef6a8d3410c70ca60b0a0f4be0`

발췌 범위: StageFiveSourceResolution_ClearsExitGateAndSpawnsFinalPredecessor의 Final 진입 검사 연속 발췌.

원본 380행에서 시작하는 UnityTest의 일부입니다. Fixture, 저장 상태 복원, 선택 수행, yield와 생성 이벤트 집계 코드는 생략했습니다. 실제 PlayMode 실행 결과가 아닌 assertion 증빙입니다.

```csharp
Assert.That(rig.Run.CurrentStageId, Is.EqualTo(RunStageId.Final));
Assert.That(rig.Run.CurrentState, Is.EqualTo(RunPrototypeState.InRoom));
Assert.That(rig.Run.IsProgressionBlocked, Is.False,
    "The resolved Stage 5 Source decision must release the shared stage-exit gate.");
Assert.That(
    rig.ContentRuntime.RuntimeState,
    Is.EqualTo(EncounterRuntimeState.WaveRunning));
Assert.That(rig.Encounter.ActiveOpponents, Has.Count.EqualTo(1));
```

**검증 범위:** 원본 기준 커밋에서 코드의 존재와 내용을 확인했습니다. 이번 증빙 정리에서는 Unity 컴파일, EditMode/PlayMode Test Runner, 실제 플레이를 실행하지 않았습니다. 읽기용 발췌이며, 필요한 클래스·설정·Fixture 등을 생략하여 단독 실행하거나 컴파일할 수 없습니다. 원본의 들여쓰기만 읽기 좋게 조정했으며 새로 재구현한 예시 코드로 대체하지 않았습니다.
