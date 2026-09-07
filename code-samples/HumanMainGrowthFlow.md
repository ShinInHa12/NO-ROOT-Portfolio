# HumanMainGrowthFlow · 실제 코드 발췌

[목록](README.md)

원본 파일: `Assets/Game/V1/Build/Runtime/HumanMainGrowthFlow.cs`

원본 커밋: `309b096c21fbb854fe21997ec46463817340925b`

원본 전체 파일 Blob SHA: `8fc43b495b059d688569e937d1638f54b43d1177`

발췌 범위: CanUseMainFormation의 초기 Stage 검사. 기존 원본 349행 부근 참조.

이 기준 버전에서는 Human Q/E가 Stage 2에 속합니다. SourceBuild·Form·Main에 대한 후속 조건은 생략했습니다. 전체 성장 규칙을 이 조건 하나가 대체하지 않습니다.

```csharp
// Stage 1 ends at Main selection. Q and E are authored Stage 2 decisions, so the
// commit authority rejects stale/debug offers that try to bypass the coordinator.
if (!ledger.IsActive || ledger.CurrentStageIndex != 1)
{
    return false;
}
```

**검증 범위:** 원본 기준 커밋에서 코드의 존재와 내용을 확인했습니다. 이번 증빙 정리에서는 Unity 컴파일, EditMode/PlayMode Test Runner, 실제 플레이를 실행하지 않았습니다. 읽기용 발췌이며, 필요한 클래스·설정·Fixture 등을 생략하여 단독 실행하거나 컴파일할 수 없습니다. 원본의 들여쓰기만 읽기 좋게 조정했으며 새로 재구현한 예시 코드로 대체하지 않았습니다.
