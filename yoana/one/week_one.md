# Week 1

### Git vs. GitHub

#### Git

- DVSC (Distributed Version Control Systems, 분산 버전 관리 시스템)
- 데이터를 스냅샷(커밋)의 스트림으로 취급
  - 파일을 커밋했을 때, 해당 파일 스냅샷의 레퍼런스를 저장

#### GitHub

- 개발자들 사이에서 소스 코드의 버전을 관리, 공유, 협업하는 데 사용되는 툴

---

### Repositories (Repo, 저장소)

- 깃이 항상 주시하고 있는 폴더
- **Local** Repository (**로컬** 저장소)
  - 작업자의 PC에 설정된 깃 저장소
- **Remote** Repository (**원격** 저장소)

  - 외부서버(ex. 깃허브)에 저장된 깃 저장소

#### Repository 만들기

- 기존 디렉토리를 깃 저장소로 만들기

  1.  .git이라는 하위 디렉토리를 만들기
      - `git init`
        - 저장소에 필요한 뼈대 파일 (skeleton)이 들어있음
        - 아직 어떤 파일도 관리하고 있지 않음
  2.  파일을 저장소에 추가
      - `git add .` or `git add file`
  3.  커밋으로 파일을 관리하기
      - `git commit -m "message"`

- 기존 저장소를 Clone (복제)하기
  - 프로젝트 히스토리를 포함한 모든 데이터를 복제
    - `git clone url` or `git clone url name`
      - `url` 뒤에 `name`이 있을 경우, 디렉토리 이름이 지정한 `name`으로 복제

---

### Commit (커밋)

- 저장소에 수정된 작업을 스냅샷으로 남기는 것

---

### Git Areas (Git Workflow, 작업 환경)

#### Working Directory (Working Area, Unstaged Area)

- 현재 개발자가 작업하고 있는 폴더가 있는 디렉토리 (ex. VSCode)
- 파일 상태:

  - Tracked (관리 대상): 깃이 이미 주시하고 있는 파일
    - Unmodified: 커밋한 파일
    - Modified: 커밋한 파일을 수정했을 때
    - Staged: 커밋으로 저장소에 기록 준비
  - Untracked (비관리 대상): 새로 만들어진 파일로 깃이 아직 주시하고 있지 않음

    ✔︎ `git status`로 파일의 상태를 확인 할 수 있음

  **[라이프사이클](https://ordo.tistory.com/133)**

  <img src="https://git-scm.com/book/en/v2/images/lifecycle.png" width="500">

  1. Untracked 파일을 git add 명령어로 Staged 상태로 만듬
  2. Tracked 파일을 수정하면 Modified
  3. Modified 된 파일을 git add 명령어로 Staged 상태로 만듬
  4. Commit을 하게되면 Staged 상태에서 Unmodified 상태로 돌아감
  5. (a) ~ (d) 반복

#### Staging Area

- 커밋할 준비가 되어있는 파일을 옮겨두는 곳

#### Git Directory (Repository Area)

- 파일들이 커밋된 곳으로 스냅샷을 가지고 있는 곳

---

### Branch (브랜치)

**[Branch Merge 예시](/branch_merge.md)**

- 동일한 코드를 고유의 공간에 복제하여 독립적으로 작업하는 것
- 추후 main 또는 다른 브랜치와 합치고 충돌을 해결 할 수 있음

#### 1. Branch 생성

- main에서 새로운 브랜치를 생성했을 때, main에서의 마지막 커밋이 브랜치의 첫번째 커밋이 됨
- main에서 복제한 파일을 새로 생성한 브랜치에서 수정
- 이때 main의 파일은 영향을 받지 않음
  - 단! 꼭 해당 브랜치를 선택한 후 VSCode에서 수정을 해야함

#### 2. Branch Merge (합치기)

- 수정했던 부분이 main 브랜치 파일에 적용 됨

#### 3. Branch Conflict (충돌)

- 충돌은 왜 일어나는가?
  - 두 브랜치의 동일한 파일에서 같은 라인이 수정 되었을 때
- 해결하기

  - VSCode에서 친절하게 충돌된 부분을 알려줌
  - 세가지 옵션:

    1.  Accept Current Change: main에서 수정한 부분을 킵
    2.  Accept Incoming Change: 합치려는 브랜치에서 수정한 부분을 킵
    3.  Accept Both Changes: 모든 수정을 킵
