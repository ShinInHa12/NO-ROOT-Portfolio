# SourceBuildAbilityGrowthTests · 실제 코드 발췌

[목록](README.md)

원본 파일: `Assets/Game/V1/Tests/EditMode/SourceBuildAbilityGrowthTests.cs`

원본 커밋: `309b096c21fbb854fe21997ec46463817340925b`

원본 전체 파일 Blob SHA: `d6b633b340fd10954925856aff9fa2bdfd1a1dbc`

발췌 범위: RetryRestore_ReplaysQAndELoadoutAndDoesNotDuplicateOffer의 복원 직후 assertion 연속 발췌.

Q/E 선택, ReadyAll Runtime 구성 및 실행 준비는 생략했습니다. 획득 상태 유지와 쿨다운 초기화를 검사하는 코드이며, Test Runner 통과 결과가 아닙니다.

```csharp
state.Ledger.RestoreCurrentStage();

Assert.That(runtime.LastProjection.Succeeded, Is.True);
Assert.That(runtime.Loadout.GetSlotState(AbilitySlotId.Q).AbilityId,
    Is.EqualTo(abilityId));
Assert.That(runtime.Loadout.GetSlotState(AbilitySlotId.Q).CooldownRemaining, Is.Zero);
Assert.That(runtime.Loadout.GetSlotState(AbilitySlotId.E).AbilityId,
    Is.EqualTo(eAbilityId));
Assert.That(runtime.Loadout.GetSlotState(AbilitySlotId.R).IsAcquired, Is.False);
```

**검증 범위:** 원본 기준 커밋에서 코드의 존재와 내용을 확인했습니다. 이번 증빙 정리에서는 Unity 컴파일, EditMode/PlayMode Test Runner, 실제 플레이를 실행하지 않았습니다. 읽기용 발췌이며, 필요한 클래스·설정·Fixture 등을 생략하여 단독 실행하거나 컴파일할 수 없습니다. 원본의 들여쓰기만 읽기 좋게 조정했으며 새로 재구현한 예시 코드로 대체하지 않았습니다.
