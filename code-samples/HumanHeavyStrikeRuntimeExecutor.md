# HumanHeavyStrikeRuntimeExecutor · 실제 코드 발췌

[목록](README.md)

원본 파일: `Assets/Game/V1/Abilities/Runtime/HumanHeavyStrikeRuntimeExecutor.cs`

원본 커밋: `309b096c21fbb854fe21997ec46463817340925b`

원본 전체 파일 Blob SHA: `798ac6b176cbbf9907929defa217c11acfb84465`

발췌 범위: 첫 Active 진입에서 Ticket을 확정하는 연속 블록. 기존 원본 314행 참조.

첫 Active의 비용·쿨다운 확정과 이후 공격 Beat·Recovery 진행을 구분합니다. Clock, 실행기, 효과 바인딩과 다른 진행 로직은 생략했습니다.

```csharp
if (advance.EnteredActive && !execution.Committed)
{
    execution.Binding.Effect.SetExecutionFacing(execution.FacingSign);
    if (!abilityRuntime.Loadout.TryCompleteExecution(
            execution.Ticket,
            true,
            out _))
    {
        StopExecution(
            cancelUncommitted: false,
            interrupted: true,
            AbilityExecutionBlockReason.InvalidTicket);
        return;
    }

    execution.Committed = true;
}
```

**검증 범위:** 원본 기준 커밋에서 코드의 존재와 내용을 확인했습니다. 이번 증빙 정리에서는 Unity 컴파일, EditMode/PlayMode Test Runner, 실제 플레이를 실행하지 않았습니다. 읽기용 발췌이며, 필요한 클래스·설정·Fixture 등을 생략하여 단독 실행하거나 컴파일할 수 없습니다. 원본의 들여쓰기만 읽기 좋게 조정했으며 새로 재구현한 예시 코드로 대체하지 않았습니다.
