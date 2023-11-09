# Git Study Week 4

## 📌 4강 : CLI II

### ✔️ `git checkout`와 `git switch`,`git restore` 비교

Git 2.23버전 부터 `git checkout`이 하는 기능을 나누어 `git switch`와 `git restore`이 수행함으로써 기능을 보더 더 명확하고 정확하게 사용 가능졌다.

- `git checkout` = `git switch` + `git restore`

  | 명령어                     | 설명                          |
  | -------------------------- | ----------------------------- |
  | `git checkout [branch]`    | 다른 브랜치로 전환            |
  | `git checkout -b [branch]` | 새 브랜치 생성 및 전환        |
  | `git checkout -- [file]`   | (마지막 커밋 상태로)파일 복원 |

- `git switch`
  | 명령어 | 설명 |
  | --------------------- | ------------------ |
  | `git switch [branch]` | 다른 브랜치로 전환 |
  |`git switch -c [branch]`|새 브랜치 생성 및 전환|

  ✅ `git checkout`과 `git switch` 두 명령어 모두 지정된 브랜치로 작업디렉토리와 HEAD 포인터가 이동하는 동일한 결과를 갖는다.
  단, `git switch`는 브랜치 전환 기능만을 수행하는 반면, `git checkout`은 파일 상태를 되돌리는 기능까지 하는 다목적 명령어이다. 파일 상태를 되돌리는 기능만을 수행하는 명령어는 `git restore`이다.

  - 예제 : file.txt 파일을 마지막 커밋 상태로 되돌리기

    ```
    git checkout -- file.txt (또는)
    git restore -- file.txt
    ```

  <br/>

- `git restore`
  |명령어|설명|
  |--|--|
  |`git restore`|작업 디렉토리의 파일을 이전 상태로 복원<br/> <details><summary>예제</summary>`git add`를 통해 수정 사항을 이미 스테이징 영역에 넣었을 때, 스테이징 영역에서 빼는 동시에 작업 디렉토리의 파일을 이전 상태로 복원 </details>|
  |`git restore --staged [file]`|`--staged` 옵션을 통해 인덱스(스테이징 영역)에서의 변경사항을 취소<br/> 즉, `git add`를 사용하여 파일을 스테이징한 상태를 취소할때 사용|
  |`git restore --worktree [file]`|`--worktree` 옵션을 통해 워킹트리(작업 디렉토리)의 상태를 복원<br/>|

<br/>

> &nbsp; > **🧐 git checkout 기능을 분리하지 않았을 때 발생할 수 있는 주요 문제?**
>
> - **데이터 손실 발생**  
>   1.브랜치명 대신 파일명으로 잘못 입력하거나,<br/>2.'--'옵션이 누락된 상태로,<br/>파일 이름을 명령어에 포함시켰을 때, 해당 파일을 마지막 커밋 상태로 복원한다.
>   &nbsp;
> - **스테이징 영역의 변경사항 무시**
>   git checkout을 통해 브랜치를 전환할 때 스테이징에 있는 영역의 변경사항이 무시될 수 있고, 사용자가 실수로 중요한 변경사항을 커밋하지 않고 다른 브랜치로 전환하는 경우, 데이터(작업 디렉토리의 변경사항)을 잃을 수 있다.<br/><details><summary>예제</summary>1. file.txt 파일에 2개의 브랜치(main, new-branch)가 존재하며, main에서 작업을 진행한다고 가정<br/>2. 작업 디렉토리에서 변경사항을 스테이징 영역에 추가 (git add file.txt)<br/> 3. 커밋하지 않은 상태에서 new-branch로 브랜치 전환을 시도할 경우를 가정(git checkout new-branch)<br/>4-1.스테이징 영역에 추가한 main 브랜치의 변경사항이 new-branch와 충돌하지 않을 경우, 변경사항을 new-branch로 가져간다.<br/>💥4-2. 이때 new-branch에도 변경사항이 존재하여 충돌하는 경우, Git은 브랜치 전환을 거부하고 충돌을 해결할 것을 요구한다.<br/>5. 정상적으로 new-branch로 전환한 후, 파일을 변경한 후 커밋을 하면 해당 파일의 main브랜치와 new-branch는 서로 다른 내용을 갖게 됨<br/>💥6. 다시 main브랜치로 전환한 후, 스테이징 영역에 남아있는 변경사항(3번단계)을 커밋할 경우, 이미 수행(5번단계)한 new-branch의 커밋과 충돌할 수 있다.</details>
>
> ---
>
> **😄브랜치 전환으로 인한 충돌 예방 방법**
>
> - 브랜치를 전환하기 전에 스테이징 영역의 미커밋된 변경사항을 남기지 않고 모두 커밋한다.
> - git switch와 git restore 명령어를 사용하여 작업 디렉토리와 스테이징 영역에 대한 변경사항을 더 세밀하게 제어한다.
>   <br/>

<br/><br/>

### ✔️ `git reset --mixed`와 `git restore --staged` 비교

- **공통점**
  두 명령어 모두 스테이징된 변경사항(=스테이징 영역으로 `git add`된 변경사항)에 대해 스테이징을 해제하는 작업에 사용
  <br/>

- **차이점**

  - `git reset --mixed` : HEAD가 현재 브랜치의 마지막 커밋을 가리킴

  - `git restore --staged` : HEAD의 위치는 변경되지 않고 스테이징 상태만 해제
    <br/>

<br/>

### ✔️ `git reset --hard`와 `git restore --worktree` 비교

- **공통점**
  두 명령어 모두 작업 디렉토리의 변경사항을 이전 상태로 되돌리는 데 사용
  <br/>

- **차이점**

  - `git reset --hard`

    - 현재 브랜치의 HEAD를 마지막(또는 지정된) 커밋으로 이동
      ```
      git reset --hard  //현재 브랜치의 마지막 커밋 상태로 HEAD, 인덱스, 작업디렉토리 모두 이동
      git reset --hard <commit hash>  //<commit hash>의 지정된 커밋으로 셋 다 이동
      ```
    - 스테이징 영역과 작업 디렉토리의 모든 변경사항을 삭제

  - `git restore --worktree`

    - HEAD의 위치는 변경되지 않음
    - 작업 디렉토리의 변경사항을 이전 상태로 되돌리지만 스테이징 영역에는 영향을 주지 않음
      ✅ 작업 디렉토리의 변경사항만 되돌리고 싶을때 적절

---

## ✏️추가 스터디

### ✔️ `mirror push`

- 하나의 저장소(repository)의 모든 데이터(브랜치, 태그, 커밋, 리포지토리 설정 등)를 완벽하게 다른 저장소로 복사할 때 사용
- 원본 저장소를 정확하게 반영하는 미러(mirror)를 만들기 위해 사용되며, 주로 백업을 만들거나 저장소를 완전히 이전할 때 사용

⚠️ [Fork한 레포지토리의 커밋을 잔디에 반영하고 싶다면? Git Mirror Push (feat. 우테코)](https://velog.io/@pgmjun/Git-Fork%ED%95%9C-%EB%A0%88%ED%8F%AC%EC%A7%80%ED%86%A0%EB%A6%AC%EC%9D%98-%EC%BB%A4%EB%B0%8B%EC%9D%84-%EC%9E%94%EB%94%94%EC%97%90-%EB%B0%98%EC%98%81%ED%95%98%EA%B3%A0-%EC%8B%B6%EB%8B%A4%EB%A9%B4-Git-Mirror-Push-feat.-%EC%9A%B0%ED%85%8C%EC%BD%94)

<br/>

### ✔️ `cherry-pick`

- 다른 브랜치의 특정 커밋을 현재 브랜치에 가져오고 싶을 때 사용
- 전체 브랜치를 병합(merge)하지 않고도 특정 변경사항만 선택적으로 적용 가능

```
git cherry-pick <commit-hash>  // 현재 브랜치에 <commit-hash> 커밋에 있는 변경사항 추가
```

---

## 📖 References

- ['모두를 위 깃&깃허브', 노마드코더](https://nomadcoders.co/git-for-beginners/lobby)
- [새 버전에 맞게 git checkout 대신 switch/restore 사용하기](https://blog.outsider.ne.kr/1505)
