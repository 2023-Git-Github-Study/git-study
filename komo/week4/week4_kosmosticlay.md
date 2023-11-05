# Git Study Week 4

## 📌 4강 : CLI II

### ✔️ `git checkout`와 `git switch`,`git restore` 비교

Git 2.23버전 부터 `git checkout`이 하는 기능을 나누어 `git switch`와 `git restore`이 수행함으로써 기능을 보더 더 명확하고 정확하게 사용 가능졌다.

- `git checkout` = `git swith` + `git restore`

  | 명령어                     | 설명                          |
  | -------------------------- | ----------------------------- |
  | `git checkout [branch]`    | 다른 브랜치로 전환            |
  | `git checkout -b [branch]` | 새 브랜치 생성 및 전환        |
  | `git checkout -- [file]`   | (마지막 커밋 상태로)파일 복원 |

- `git switch`
  | 명령어 | 설명 |
  | --------------------- | ------------------ |
  | `git switch [branch]` | 다른 브랜치로 전환 |
  |`git swtich -c [branch]`|새 브랜치 생성 및 전환|

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

### ✔️ `git reset --mixed`와 `git restore --staged` 비교

<br/>

### ✔️ `git reset --hard`와 `git restore --worktree` 비교

---

## ✏️추가 스터디

---

## 📖 References

- ['모두를 위 깃&깃허브', 노마드코더](https://nomadcoders.co/git-for-beginners/lobby)
- [새 버전에 맞게 git checkout 대신 switch/restore 사용하기](https://blog.outsider.ne.kr/1505)

```

```
