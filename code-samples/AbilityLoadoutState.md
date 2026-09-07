# AbilityLoadoutState · 실제 코드 발췌

[목록](README.md)

원본 파일: `Assets/Game/V1/Abilities/Runtime/AbilityLoadoutState.cs`

원본 커밋: `309b096c21fbb854fe21997ec46463817340925b`

원본 전체 파일 Blob SHA: `bf719c4c9cd846c49b3349f8285e5a71ecf55d72`

발췌 범위: TryCompleteExecution 메서드 전체. 기존 원본 링크의 139행 부근에 대응.

Ticket의 슬롯·sequence·Ability ID와 실행 상태를 대조한 뒤 실행을 확정합니다. 성공 시 쿨다운을 적용하고 실패 시 예약 자원을 반환합니다. SlotRuntime, Ticket, 자원 권한과 클래스의 다른 부분은 포함하지 않습니다.

```csharp
public bool TryCompleteExecution(
    in AbilityExecutionTicket ticket,
    bool succeeded,
    out AbilityExecutionBlockReason blockReason)
{
    blockReason = AbilityExecutionBlockReason.InvalidTicket;
    if (!ticket.IsValid || !AbilitySlotIds.IsValid(ticket.Slot))
    {
        return false;
    }

    SlotRuntime runtime = slots[(int)ticket.Slot];
    if (!runtime.Executing ||
        runtime.ExecutionSequence != ticket.Sequence ||
        runtime.Definition == null ||
        !string.Equals(
            runtime.Definition.StableId,
            ticket.AbilityId,
            StringComparison.Ordinal))
    {
        return false;
    }

    if (succeeded)
    {
        runtime.CooldownRemaining = runtime.Definition.CooldownSeconds;
    }
    else if (runtime.ReservedBy != null)
    {
        runtime.ReservedBy.Restore(runtime.Definition.ResourceCost);
    }

    runtime.ClearExecution();
    blockReason = AbilityExecutionBlockReason.None;
    Changed?.Invoke();
    return true;
}
```

**검증 범위:** 원본 기준 커밋에서 코드의 존재와 내용을 확인했습니다. 이번 증빙 정리에서는 Unity 컴파일, EditMode/PlayMode Test Runner, 실제 플레이를 실행하지 않았습니다. 읽기용 발췌이며, 필요한 클래스·설정·Fixture 등을 생략하여 단독 실행하거나 컴파일할 수 없습니다. 원본의 들여쓰기만 읽기 좋게 조정했으며 새로 재구현한 예시 코드로 대체하지 않았습니다.
