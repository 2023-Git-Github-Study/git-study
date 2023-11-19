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
  |`git restore`|작업 디렉토리의 파일을 이전 상태로 복원<br/> <details><summary>참고</summary>- `git add`를 통해 수정 사항을 이미 인덱스 영역에 스테이징한 상태일 때 `git restore` 명령어를 실행하면, 작업 디렉토리 내 변경사항은 마지막 커밋 상태로 복원되지만, 인덱스 영역의 스테이징 상태는 그대로 유지된다.<br/>- `git restore --worktree` 명령어를 사용하여 '협업하는 환경'에서 더 명확한 의사소통을 위해 옵션(`--worktree`)을 명시하기도 한다.</details>|
  |`git restore --staged [file]`|`--staged` 옵션을 통해 인덱스(스테이징 영역)에서의 변경사항을 취소<br/> 즉, `git add`를 사용하여 파일을 스테이징한 상태를 취소할때 사용|

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
  두 명령어 모두 스테이징된 변경사항(=스테이징 영역으로 `git add`된 변경사항)에 대해 스테이징을 해제하고, 변경사항은 작업 디렉토리에 남김  
  <br/>

- **차이점**

  - `git reset --mixed [커밋 해시]` 또는 `git reset --mixed HEAD~1`

    - 주로 커밋 해시와 함께 사용 -> 커밋 이력을 조정하거나 변경사항을 다시 작업하고자 할 때 사용
    - HEAD가 현재 브랜치의 마지막 커밋(최신 커밋)으로 이동

  - `git restore --staged <파일명>` 또는 `git restore <파일명>`

    - 주로 파일명과 함께 사용 -> 잘못 스테이징된 파일을 수정하고자 할 때 사용
    - HEAD의 위치는 변경되지 않고 스테이징 상태만 해제

    <br/>

<br/>

### ✔️ `git reset --hard`와 `git restore --worktree` 비교

- **공통점**
  두 명령어 모두 작업 디렉토리의 변경사항을 이전 상태로 되돌리는 데 사용
  <br/>

- **차이점**

  - `git reset --hard`

    - 주로 커밋 해시와 함께 사용 -> 스테이징 영역과 작업 디렉토리의 모든 변경사항을 취소
    - HEAD와 커밋 이력, 전체 브랜치, 스테이징 영역, 작업 디렉토리 모두 적용
    - 현재 브랜치의 HEAD를 마지막(또는 지정된) 커밋으로 이동
      ```
      git reset --hard  //현재 브랜치의 마지막 커밋 상태로 HEAD, 인덱스, 작업디렉토리 모두 이동
      git reset --hard <commit hash>  //<commit hash>의 지정된 커밋으로 셋 다 이동
      git reset --hard HEAD~1 // HEAD가 가리키는 커밋의 바로 이전 커밋으로 셋 다 이동
      ```

  - `git restore --worktree`

    - 주로 파일명과 함께 사용 -> 작업 디렉토리의 특정 파일 변경사항을 취소하고 싶을 때 사용
    - 그외 HEAD나 커밋 이력에 영향을 주지 않음
    - HEAD의 위치가 변경되지 않음

<br/>

### ✔️ `git commit --amend` 비교

- 가장 최근의 커밋을 수정하고자 할 때 사용
- `--amend` 옵션을 사용하여 기존 커밋의 이력을 변경하면 이전 커밋은 이력에서 사라짐
- 주의사항 : 사용 전 `git status`와 `git diff`를 사용하여 현재 스테이징 영역과 작업 디렉토리의 상태를 확인 권장

  <br/>

  <details><summary>사용 예제</summary>
  1. 커밋 메시지 수정

  ```
  git commit -m "First commit"  // 커밋 후, 커밋 메시지 수정이 필요한 상황
  git commit --amend -m "Corrected first commit"  // 이전 커밋이 새 커밋 메시지로 대체
  ```

  2. 커밋된 파일 변경사항 추가

  ```
  // 이미 파일 A를 커밋한 후, 추가적인 변경사항을 같은 커밋에 포함시켜야 하는 상황
  git add A
  git commit --amend  // 변경사항을 스테이징시킨 후 --amend옵션과 함께 재커밋
  ```

  </details>

---

## ✏️추가 스터디

### ✔️ `git rebase`

- 브랜치의 기반(base)를 변경하는 과정으로, 특정 브랜치의 커밋들을 임시로 저장한 후 다른 브랜치의 최신 커밋위에 적용하여 커밋 히스토리를 <u>선형적</u>으로 만든다.

⚠️ **`merge`와 `rebase` 비교**

- **merge option**

  ```
  git checkout feature
  git merge main
  ```

  또는

  ```
  git merge feature main
  ```

  명령어를 통해 `main`브랜치를 `feature`브랜치에 병합하면, `feature`브랜치에 두 브랜치의 기록을 연결하는 **새로운 병합 커밋**(`*`)이 생성됨
  ![merge commit](https://wac-cdn.atlassian.com/dam/jcr:4639eeb8-e417-434a-a3f8-a972277fc66a/02%20Merging%20main%20into%20the%20feature%20branh.svg?cdnVersion=1324)

<br/>

- **rebase option**

  ```
  git checkout feature
  git rebase main
  ```

  명령어를 통해 `feature`브랜치를 `main`브랜치로 rebase하면, 전체 `feature` 브랜치를 이동하여 `main`에서 모든 새 커밋을 통합(`*` `*` `*`)하여 **선형적**인 커밋 히스토리를 생성한다.
  ![rebase commit](https://wac-cdn.atlassian.com/dam/jcr:3bafddf5-fd55-4320-9310-3d28f4fca3af/03%20Rebasing%20the%20feature%20branch%20into%20main.svg?cdnVersion=1324)

### ✔️ `mirror push`

- 하나의 저장소(repository)의 모든 데이터(브랜치, 태그, 커밋, 리포지토리 설정 등)를 완벽하게 다른 저장소로 복사할 때 사용
- 원본 저장소를 정확하게 반영하는 미러(mirror)를 만들기 위해 사용되며, 주로 백업을 만들거나 저장소를 완전히 이전할 때 사용

⚠️ [Fork한 레포지토리의 커밋을 잔디에 반영하고 싶다면? Git Mirror Push (feat. 우테코)](https://velog.io/@pgmjun/Git-Fork%ED%95%9C-%EB%A0%88%ED%8F%AC%EC%A7%80%ED%86%A0%EB%A6%AC%EC%9D%98-%EC%BB%A4%EB%B0%8B%EC%9D%84-%EC%9E%94%EB%94%94%EC%97%90-%EB%B0%98%EC%98%81%ED%95%98%EA%B3%A0-%EC%8B%B6%EB%8B%A4%EB%A9%B4-Git-Mirror-Push-feat.-%EC%9A%B0%ED%85%8C%EC%BD%94)

<br/>

### ✔️ `cherry-pick`

- 다른 브랜치의 특정 커밋을 현재 브랜치에 가져오고 싶을 때 사용
- 전체 브랜치를 병합(merge)하지 않고도 특정 변경사항만 선택적으로 적용 가능

  ```
  git cherry-pick <commit-hash>  // 현재 브랜치에 <commit-hash> 커밋의 변경사항 추가
  ```

⚠️ **`cherry-pick`와 `merge` 비교**

- cherry-pick : 특정 커밋의 변경 내용만을 현재 브랜치에 적용하고 싶을 때 사용
- merge : 브랜치의 히스토리를 현재 브랜치와 합치는 것으로, 브랜치의 끝점을 현재 브랜치와 합치고 싶을 때 사용(특정 커밋만이 아니라 브랜치의 전체 컨텍스트를 함께 가져옴)

---

## 📖 References

- ['모두를 위 깃&깃허브', 노마드코더](https://nomadcoders.co/git-for-beginners/lobby)
- [새 버전에 맞게 git checkout 대신 switch/restore 사용하기, Outsider's Dev Story](https://blog.outsider.ne.kr/1505)
- [Merging vs. rebasing, ATLASSIAN](https://www.atlassian.com/ko/git/tutorials/merging-vs-rebasing)
