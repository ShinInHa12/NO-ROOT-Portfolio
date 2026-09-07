# HumanAbilityValidationHarness · 실제 코드 발췌

[목록](README.md)

원본 파일: `Assets/Game/V1/Abilities/Runtime/HumanAbilityValidationHarness.cs`

원본 커밋: `309b096c21fbb854fe21997ec46463817340925b`

원본 전체 파일 Blob SHA: `9f96f3be648414ea7b8af5bd8cdceafa30df2b41`

발췌 범위: HumanAbilityValidationSelection.CreateSnapshot의 반환 부분 연속 발췌.

파일은 UNITY_EDITOR 또는 DEVELOPMENT_BUILD 조건부 컴파일 대상입니다. 검증용 Q/E/R 획득 Snapshot을 구성하는 보조 함수이며 실제 저장 데이터 변경 코드가 아닙니다. Add, 입력 검사, 패널 및 일시 Loadout 투영 경로는 생략했습니다.

```csharp
List<AbilityAcquisitionRecord> records = new List<AbilityAcquisitionRecord>(3);
Add(records, mainStableId, AbilitySlotId.Q, qVariant);
Add(records, mainStableId, AbilitySlotId.E, eVariant);
Add(records, mainStableId, AbilitySlotId.R, 1);
return new AbilityAcquisitionSnapshot(records);
```

**검증 범위:** 원본 기준 커밋에서 코드의 존재와 내용을 확인했습니다. 이번 증빙 정리에서는 Unity 컴파일, EditMode/PlayMode Test Runner, 실제 플레이를 실행하지 않았습니다. 읽기용 발췌이며, 필요한 클래스·설정·Fixture 등을 생략하여 단독 실행하거나 컴파일할 수 없습니다. 원본의 들여쓰기만 읽기 좋게 조정했으며 새로 재구현한 예시 코드로 대체하지 않았습니다.
