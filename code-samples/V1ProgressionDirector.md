# V1ProgressionDirector · 실제 코드 발췌

[목록](README.md)

원본 파일: `Assets/Game/V1/Progression/Runtime/V1ProgressionDirector.cs`

원본 커밋: `309b096c21fbb854fe21997ec46463817340925b`

원본 전체 파일 Blob SHA: `0c6b1e421dee66a083e41525dd9ecdda9c20449e`

발췌 범위: HandleSourceProgressionChanged의 Stage 5 분기. 기존 원본 604행 부근 참조.

Source 결정 변경 후 공통 Gate를 다시 계산하고 지연 전이를 예약합니다. 메서드 앞부분의 Restoring 예외 처리와 다른 Stage의 처리는 생략했습니다. 관련 원본 수정 커밋은 762b89be47f5632c8d15f097b40c11675273051d입니다.

```csharp
if (run.CurrentStageId == RunStageId.Stage5)
{
    // Final Specialization can close the shared stage-exit gate while the Stage 5
    // Source decision is still pending. Re-evaluate it after that decision commits;
    // otherwise the completed Final boundary keeps deferring behind a stale gate.
    UpdateStageExitGate();
    ScheduleStageFiveDeferredTransition();
    return;
}
```

**검증 범위:** 원본 기준 커밋에서 코드의 존재와 내용을 확인했습니다. 이번 증빙 정리에서는 Unity 컴파일, EditMode/PlayMode Test Runner, 실제 플레이를 실행하지 않았습니다. 읽기용 발췌이며, 필요한 클래스·설정·Fixture 등을 생략하여 단독 실행하거나 컴파일할 수 없습니다. 원본의 들여쓰기만 읽기 좋게 조정했으며 새로 재구현한 예시 코드로 대체하지 않았습니다.
