# Troubleshooting · 확인한 수정 근거

원본 저장소는 비공개로 유지합니다. 아래 SHA는 출처 식별자이며 공개 저장소에 원본 Git 이력이 존재한다는 의미는 아닙니다. 날짜는 KST입니다. 실행 결과를 새로 측정하지 않았습니다.

## HumanQMissing

원본 수정 커밋: `7f4bd351d35bc97fb233e651b96d775e4aac6249`  
메시지: `Fix Stage 1 Human Q validator contract`  
날짜: 2026-08-31

Stage 1의 정상 Main-only 상태를 누락으로 보고하던 조건을 제거한 수정입니다. Source·Main·필수 보상 등 나머지 검증은 유지했습니다. 다음은 `Assets/Game/V1/Progression/Runtime/StageOneVerticalSliceRuntimeValidator.cs`의 실제 diff 중 삭제 부분입니다.

```diff
-            if (roomNumber >= 4 && !humanQSelected)
-            {
-                issues |= StageOneVerticalSliceIssue.HumanQMissing;
-            }
```

같은 커밋의 `StageOneVerticalSliceContractTests.cs`에는 `HumanTrack_MainOnlyStateIsValidThroughStageOneAndStageTwoHandoff`, `HumanQState_DoesNotChangeMainOnlyStageOneContract`, `StageTwoEntry_RejectsIncompleteHumanHandoff`의 회귀 검사 변경이 있습니다. 검사 코드 존재를 확인했으며 실행 통과를 주장하지 않습니다.

## Final handoff gate

원본 수정 커밋: `762b89be47f5632c8d15f097b40c11675273051d`  
메시지: `Fix Final encounter handoff gate`  
날짜: 2026-08-31

Source 결정 완료 후 이전 stage-exit gate 상태가 남아 Final 전이를 보류하던 흐름을 수정했습니다. 다음은 원본 `V1ProgressionDirector.cs` 패치의 해당 구간입니다.

```diff
             if (run.CurrentStageId == RunStageId.Stage5)
             {
+                // Final Specialization can close the shared stage-exit gate while the Stage 5
+                // Source decision is still pending. Re-evaluate it after that decision commits;
+                // otherwise the completed Final boundary keeps deferring behind a stale gate.
+                UpdateStageExitGate();
                 ScheduleStageFiveDeferredTransition();
                 return;
             }
```

[콜백 발췌](../../code-samples/V1ProgressionDirector.md) · [PlayMode assertion 발췌](../../code-samples/StageFiveFinalRunFlowTests.md)

코드 기준 버전은 `309b096c21fbb854fe21997ec46463817340925b`입니다. 실행 검사에는 원본 Unity 프로젝트, Fixture 및 실제 Encounter 콘텐츠가 필요합니다. 이 문서와 부분 코드만으로 실행할 수 없습니다.
