# RunCommitLedger · 실제 코드 발췌

[목록](README.md)

원본 파일: `Assets/Game/V1/Run/Runtime/RunCommitLedger.cs`

원본 커밋: `309b096c21fbb854fe21997ec46463817340925b`

원본 전체 파일 Blob SHA: `50563a34e9233189b1105b92d81ba6646f5b68e8`

발췌 범위: TryCommit 메서드 전체. 기존 원본 294행 참조의 중복 ID 검사를 포함.

Stable Commit ID를 이용해 동일 Ledger에서의 중복 적용을 거부합니다. Ledger 필드, RunCommitRecord, Apply와 저장 계층은 생략했습니다. 분산 트랜잭션이나 전역 exactly-once 보장을 주장하는 코드가 아닙니다.

```csharp
public bool TryCommit(
    string commitId,
    RunCommitKind kind,
    IReadOnlyList<RunFactAssignment> assignments,
    out RunCommitRecord record)
{
    RequireActive();

    if (string.IsNullOrWhiteSpace(commitId))
    {
        throw new ArgumentException("A commit requires a stable id.", nameof(commitId));
    }

    if (commitIds.Contains(commitId) || lastSequence == int.MaxValue)
    {
        record = null;
        return false;
    }

    int sequence = checked(lastSequence + 1);
    RunCommitRecord next = new RunCommitRecord(
        commitId,
        sequence,
        kind,
        CurrentStageIndex,
        CurrentRoomIndex,
        assignments);

    Apply(next);
    commits.Add(next);
    commitIds.Add(next.CommitId);
    lastSequence = sequence;
    record = next;
    CommitApplied?.Invoke(next);
    return true;
}
```

**검증 범위:** 원본 기준 커밋에서 코드의 존재와 내용을 확인했습니다. 이번 증빙 정리에서는 Unity 컴파일, EditMode/PlayMode Test Runner, 실제 플레이를 실행하지 않았습니다. 읽기용 발췌이며, 필요한 클래스·설정·Fixture 등을 생략하여 단독 실행하거나 컴파일할 수 없습니다. 원본의 들여쓰기만 읽기 좋게 조정했으며 새로 재구현한 예시 코드로 대체하지 않았습니다.
