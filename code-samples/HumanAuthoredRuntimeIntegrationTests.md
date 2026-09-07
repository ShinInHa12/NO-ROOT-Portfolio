# HumanAuthoredRuntimeIntegrationTests · 실제 코드 발췌

[목록](README.md)

원본 파일: `Assets/Game/V1/Tests/EditMode/HumanAuthoredRuntimeIntegrationTests.cs`

원본 커밋: `309b096c21fbb854fe21997ec46463817340925b`

원본 전체 파일 Blob SHA: `5ab1949494618777880b1e2e03ee4798c8362e39`

발췌 범위: EveryAuthoredAction_PreservesNonZeroStartupActiveRecovery 메서드 전체.

Startup·Active·Recovery가 0보다 큰지 검사합니다. using, 클래스, AllAuthoredEntries, AuthoredEntryView와 전체 콘텐츠 정의는 생략했습니다. 이 검사는 실제 전투의 플레이 품질이나 모든 타이밍 버그 부재를 증명하지 않습니다.

```csharp
[Test]
public void EveryAuthoredAction_PreservesNonZeroStartupActiveRecovery()
{
    foreach (AuthoredEntryView entry in AllAuthoredEntries())
    {
        Assert.Greater(
            entry.Action.Motion.Phases.StartupSeconds,
            0f,
            entry.AbilityId);
        Assert.Greater(
            entry.Action.Motion.Phases.ActiveSeconds,
            0f,
            entry.AbilityId);
        Assert.Greater(
            entry.Action.Motion.Phases.RecoverySeconds,
            0f,
            entry.AbilityId);
    }
}
```

**검증 범위:** 원본 기준 커밋에서 코드의 존재와 내용을 확인했습니다. 이번 증빙 정리에서는 Unity 컴파일, EditMode/PlayMode Test Runner, 실제 플레이를 실행하지 않았습니다. 읽기용 발췌이며, 필요한 클래스·설정·Fixture 등을 생략하여 단독 실행하거나 컴파일할 수 없습니다. 원본의 들여쓰기만 읽기 좋게 조정했으며 새로 재구현한 예시 코드로 대체하지 않았습니다.
