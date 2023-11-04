# Week 3

### [Terminal Commands](../commands.md)

---

### M VS U

- VS Code에서 파일 옆에 M과 U 아이콘들은 무엇인가?

    <img src="../imgs/w3/01.png" width="250">

  - **M = Modified**
    - 깃이 관찰하고 있는 파일이 수정 되었을 때
  - **U = Untracked**
    - 아직 깃에서 등록되지 않아 관찰되고 있지 않은 파일
    - 커밋을 해야 등록/관찰이 됨

---

### COMMIT HISTORY

- 개발자가 여태 커밋한 기록을 보는 것

  1. `git log`

     <img src="../imgs/commands/01.png" width="500px">

     - `commit # (HEAD -> main)` = 로컬 저장소
       - 마지막 커밋은 이전 커밋의 내용들이 다 합쳐져 있음
     - `commit # (origin/man)` = 원격 (깃헙) 저장소

      <img src="../imgs/commands/02.png" width="500px">

     - `commit # (HEAD -> main, origin/man)` = 로컬 저장소와 원격 저장소가 같은 커밋에 있음

  2. `q`
     - `git log` 에서 탈출하기

---

### HEAD

- "현재 브랜치 마지막 커밋의 스냅샷"
- HEAD의 위치를 변경하고...

  - 과거 커밋 조회
  - 과거 커밋 변경

---

### CHECKOUT

#### 과거 커밋 조회: `git checkout #`

- `checkout` 은 말 그대로 과거 커밋의 변경사항을 볼 뿐 수정하지는 않음
- `#` 에는 `git log`에서 보이는 커밋 번호를 넣어야함

  1. 현재 위치

     - 로컬 저장소도 원격 저장소도 제일 최근 커밋에 있음

       <img src="../imgs/w3/02.png" width="500px">

  2. 이전 커밋 조회

     - git checkout d7aa16ae5e4d46d529292e027934e727de9e4298

         <img src="../imgs/w3/03.png" width="500px">

  3. 제일 최근 커밋으로 돌아가기

     - `git checkout main`

---

### RESET

#### 과거 커밋 변경

<img src = "https://velog.velcdn.com/images%2Fsonypark%2Fpost%2F2dc11b3e-d04d-431d-9b53-6ccfd8af0e97%2Fgit-reset-movement.png" width="500px">

1. `git reset #`

   - `reset` = 삭제
   - `#`
     - `HEAD^`
       - `^`의 갯수에 따라 몇개의 커밋 뒤로 갈지 정해짐
         - `HEAD` → 삭제 없음
         - `HEAD^` → 바로 이전 커밋으로 돌아감
     - `HEAD~`
       - 취소할 커밋 수
       - `HEAD~3` → 최근 커밋에서 세번째 커밋으로 돌아감
     - `commit #`
       - `git log`에서 조회

2. `git pull origin main`

   - 원격 저장소(깃헙)는 로컬 저장소 파일보다 삭제된 커밋만큼 앞서 있기 때문에 충돌이 일어남
   - 원하는 수정 사항 선택 후 `merge`가 필요
     1. `Accept Current Change`로 로컬 저장소 파일의 수정 사항을 선택
     2. `git add .`
     3. `git commit -m "message"`
     4. `git push`
     5. 원격 저장소에서 과거 커밋은 삭제 되고 로컬 저장소와 동일한 커밋 히스토리를 갖게 됨
   - 하지만 이건 귀찮은 작업이기 때문에...

3. `git push origin main --force`
   - 위 순서를 밟지 않고 강제로 원격 저장소로 푸시
   - 푸시 후 해당 커밋은 로컬 저장소에서도 원격 저장소(깃헙)에서도 다 삭제 되고 동일한 커밋 히스토리를 갖게 됨

#### Mixed Reset (복합리셋)

- `git reset #`

  - 디폴트 리셋
  - 선택된 커밋에서의 변경사항들은 **working directory(unstaged, 작업영역)** 로 이동되고 파일은 **untracked** 상태로 변경 됨 (`git add` 하기 전 상태)
  - 커밋은 삭제되지만 파일은 유지

#### Hard Reset

- `git reset --hard #`
  - 최신 커밋들과 파일을 완전히 삭제하고 완전히 과거로 돌아가는 것

#### Soft Reset

- `git reset --soft #`
  - 선택한 커밋에서의 변경사항들은 **staging area**로 이동되고 파일은 **tracked** 상태 유지, 하지만 `git commit`하기 전 상태로 돌려놓음
  - 커밋은 삭제되지만 파일은 유지

---

### [GIT RESET VS GIT CHECKOUT](https://blog.naver.com/codeitofficial/222011693376)

<img src="https://codeit-images.s3.ap-northeast-2.amazonaws.com/images/5e345231f974fb2074b368c1/46-1.png?1587009625701" width="500px">

#### Reset

- `git reset 9033` 을 실행하면 `HEAD`가 `main`이라는 통해 간접적으로 커밋을 가리킴

    <img src="https://codeit-images.s3.ap-northeast-2.amazonaws.com/images/5e345231f974fb2074b368c1/37-2.png?1587009639934" width="500px">

#### Checkout

- 과거 특정 커밋에서 새로운 브랜치를 만들 때 보통 `Checkout`을 사용

  1. `git checkout 9033` 을 실행하면 `HEAD`가 직접적으로 커밋을 가리키는데 이를 `Detached HEAD`라고 부름
     <img src = "https://codeit-images.s3.ap-northeast-2.amazonaws.com/images/5e345231f974fb2074b368c1/27-3.png?1587009652246" width="500px">

  2. `9033` 에서 브랜치 `premium`을 생성 후 `git checkout premium`을 하면 `Detached HEAD`에서 벗어나 정상적인 상태로 돌아옴 (`git checkout -b premium`하면 브랜치 생성 후 바로 체크아웃 가능)

     <img src="https://postfiles.pstatic.net/MjAyMDA2MjVfMTc4/MDAxNTkzMDUxMDg2NDM4.0AY3KlQJcP0zISUmOrmZ6GqGXi2HR9qMRoSsnX4v-Bgg.j4eRWfEVDuBEoUByooeVEH9zUwebRAg3W-TPC1Rc1mAg.PNG.codeitofficial/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2020-06-25_%EC%98%A4%EC%A0%84_11.11.07.png?type=w773" width="500px">

  3. 새 커밋을 하면 `premium` 브랜치에서 `main` 브랜치와 다른 작업을 할 수 있음
     <img src="https://codeit-images.s3.ap-northeast-2.amazonaws.com/images/5e345231f974fb2074b368c1/17-6.png?1587009690417" width="500px">

  4. `git checkout main`을 하면 `HEAD`가 다시 `main` 브랜치로 이동

     <img src ="https://codeit-images.s3.ap-northeast-2.amazonaws.com/images/5e345231f974fb2074b368c1/18-7.png?1587009703832" width="500px">

---

### [GIT RESET VS GIT REVERT](https://velog.io/@njs04210/Git-reset%EA%B3%BC-revert-%EC%95%8C%EA%B3%A0-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)

  <img src = "https://velog.velcdn.com/images%2Fnjs04210%2Fpost%2F52dd0ee6-2d56-406f-a4b7-3da19cc36e10%2Fimage.png" width="500px">

#### Reset

- 개발자 본인만 해당 브랜치를 사용할 경우
- 커밋이 완전히 삭제됨

  1. `git reset --hard a0fvf8`로 `a0fvf8`커밋으로 돌아감
  2. 커밋 히스토리 C와 D는 삭제됨

    <img src = "https://velog.velcdn.com/images%2Fnjs04210%2Fpost%2F9785918a-daeb-453f-a0f1-62a1c93ce02c%2Fimage.png" width="500px">

#### Revert

- `git revert commit#`
- 코드가 여러 개발자와 공유되어있을 때
- `revert`는 커밋을 삭제하지 않고 과거 커밋으로 돌아가 새로운 커밋을 생성하여 문제점, `revert`한 이유 등을 기록할 수 있음

  1. `git revert 5lk4er`로 커밋 C로 돌아가면서 `D'` 커밋 생성, `git revert 76sdeb`로 커밋 B로 돌아가면서 `C'` 커밋 생성
     - `git revert commit#`로 이전 커밋으로 돌아갈 수 있음
  2. `revert`한 이력을 남기면서 커밋 B로 돌아감

    <img src = "https://velog.velcdn.com/images%2Fnjs04210%2Fpost%2Fa9faa0ad-05a6-42d6-8f10-a0cda67ebf22%2Fimage.png" width="500px">

---

### [STASH](https://inpa.tistory.com/entry/GIT-%E2%9A%A1%EF%B8%8F-%EC%BB%A4%EB%B0%8B%ED%95%98%EC%A7%80%EC%95%8A%EA%B3%A0-%EB%B8%8C%EB%9E%9C%EC%B9%98-%EA%B0%84-%EC%9D%B4%EB%8F%99-git-stash)

- 아래에 해당되는 파일을 일시적으로 보관하는 곳

  - Tracked + Modified 파일들
  - Staging Area에 있는 파일들

- 왜 `Stash`를 하는가?
  - 파일 수정 중 다른 브랜치로 이동해야하는 경우
  - `main` 브랜치에서 작업을 해야하는데 다른 브랜치에서 작업하고 있을 경우 `stash`로 저장해서 `main` 브랜치로 넘어와 임시 저장한 내용을 적용

1. 파일 임시 저장: `git stash`
   - Working directory에서 수정한 파일만 저장
2. 임시 저장 설명 추가: `git stash save "message"`
3. 임시 저장한 리스트 조회: `git stash list`

   <img src = "https://velog.velcdn.com/images%2Fbyeol4001%2Fpost%2F26c6f00b-0845-400a-8537-d19abc325181%2Fimage.png" width="500px">

4. 가장 최근 stash를 적용: `git stash apply`
5. 다른 stash 적용: `git stash apply stash@{숫자}`
6. Staged 상태였던 파일을 다시 Staged 상태까지 복원 (자동으로 해주지 않음): `git stash apply --index`
7. stash 삭제 (적용 후 리스트에 여전히 남아 있음):
   - 가장 최근 stash: `git stash drop`
   - 다른 stash: `git stash drop stashName`
   - 전체: `git stash clear`
8. stash 적용 후 삭제:

   - 가장 최근: `git stash pop`
   - 다른 stash:`git stash pop stash@{숫자}`

9. 새 브랜치에 stash 적용 (생성 브랜치 checkout되며 stash는 삭제 됨): `git stash branch branchName stash@{숫자}`
   <img src="https://velog.velcdn.com/images%2Fbyeol4001%2Fpost%2F885f4d8d-520a-4ed9-81c4-15e7ccf6761b%2Fimage.png" width="500px">
10. stash 롤백 (stash 적용한 것을 되돌리고 싶을 때):

    - 가장 최근 stash: `git stash show -p`
    - 다른 stash: `git stash show -p stash@{숫자}`
