# Code Samples · 구현 근거

[프로젝트 소개로 돌아가기](../README.md)

원본 전체 프로젝트와 외부·유료 Unity 에셋을 포함하지 않는 선별 발췌 모음입니다.

원본 기준 커밋: `309b096c21fbb854fe21997ec46463817340925b`. 공개 문서 업로드 커밋과 원본 구현 커밋은 다릅니다.

**검증 범위:** 원본 기준 커밋에서 코드의 존재와 내용을 확인했습니다. 이번 증빙 정리에서는 Unity 컴파일, EditMode/PlayMode Test Runner, 실제 플레이를 실행하지 않았습니다. 읽기용 발췌이며, 필요한 클래스·설정·Fixture 등을 생략하여 단독 실행하거나 컴파일할 수 없습니다. 원본의 들여쓰기만 읽기 좋게 조정했으며 새로 재구현한 예시 코드로 대체하지 않았습니다.

## 샘플 목록

- [AbilityLoadoutState](AbilityLoadoutState.md) — TryCompleteExecution 메서드 전체. 기존 원본 링크의 139행 부근에 대응.
- [HumanHeavyStrikeRuntimeExecutor](HumanHeavyStrikeRuntimeExecutor.md) — 첫 Active 진입에서 Ticket을 확정하는 연속 블록. 기존 원본 314행 참조.
- [HumanMainGrowthFlow](HumanMainGrowthFlow.md) — CanUseMainFormation의 초기 Stage 검사. 기존 원본 349행 부근 참조.
- [SourceBuildAbilityGrowthTests](SourceBuildAbilityGrowthTests.md) — RetryRestore_ReplaysQAndELoadoutAndDoesNotDuplicateOffer의 복원 직후 assertion 연속 발췌.
- [DeterministicRunHybridPathGateway](DeterministicRunHybridPathGateway.md) — RequestNextNodeCandidates의 기존 후보 재사용 조건. 기존 원본 124행 참조.
- [RunController](RunController.md) — EnterSelectedNode의 저장 요청 이후 진행 Gate 검사부터 정상 진입까지의 연속 블록.
- [RunCommitLedger](RunCommitLedger.md) — TryCommit 메서드 전체. 기존 원본 294행 참조의 중복 ID 검사를 포함.
- [RunControllerHybridPathIntegrationTests](RunControllerHybridPathIntegrationTests.md) — CommitThenEnter_IsExplicitAndDuplicateCallbacksCannotAdvanceTwice의 선택 반복 검사 연속 발췌.
- [HumanAbilityValidationHarness](HumanAbilityValidationHarness.md) — HumanAbilityValidationSelection.CreateSnapshot의 반환 부분 연속 발췌.
- [HumanAuthoredRuntimeIntegrationTests](HumanAuthoredRuntimeIntegrationTests.md) — EveryAuthoredAction_PreservesNonZeroStartupActiveRecovery 메서드 전체.
- [V1ProgressionDirector](V1ProgressionDirector.md) — HandleSourceProgressionChanged의 Stage 5 분기. 기존 원본 604행 부근 참조.
- [StageFiveFinalRunFlowTests](StageFiveFinalRunFlowTests.md) — StageFiveSourceResolution_ClearsExitGateAndSpawnsFinalPredecessor의 Final 진입 검사 연속 발췌.

[수정 전후 증빙](../docs/evidence/troubleshooting.md)

[원본 출처·발췌 해시 목록](../evidence-manifest.json)
