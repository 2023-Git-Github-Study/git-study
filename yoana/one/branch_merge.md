## Branch Merge 실생활 개발 과정에서

1. 작업 진행하면서 이슈가 생겼을 때 이슈를 처리할 새 브랜치를 생성
   - 53번 이슈 발생하여 `git checkout -b iss53` ( = `git branch iss53` + `git checkout iss53`) 으로 이슈를 처리할 브랜치 생성 및 체크아웃
     <img src="https://git-scm.com/book/en/v2/images/basic-branching-2.png" width="500">
2. 해당 브랜츠에서 이슈를 해결
   - 53번 이슈를 `checkout` 했기 때문에 `head`가 `iss53`를 가리킴으로 커밋을 했을 때 `iss53` 브랜치 앞으로 나아감
     <img src="https://git-scm.com/book/en/v2/images/basic-branching-3.png" width="500">
3. 커밋 후 main 브랜치로 전환 (merge 아님 주의!)
   - `git checkout main`
     - 워킹 디렉토리는 53번 이슈 시작 전 모습으로 돌려지기에 새로운 문제 집중할 수 있는 환경이 만들어짐
     - ❕깃은 자동으로 워킹 디렉토리에 파일을 추가하고, 지우고, 수정해서 체크아웃한 브랜치의 마지막 스냅샷으로 돌려놓음
4. 해결해되는 핫픽스가 등장

   - 핫픽스 해결용 브랜치를 생성 `git checkout -b hotfix`

   <img src="https://git-scm.com/book/en/v2/images/basic-branching-4.png" width="500">

5. 핫픽스 해결 후 main과 merge

   - `git checkout main` 으로 먼저 메인을 체크아웃
   - `git merge hotfix` 로 메인에 핫픽스를 합치기

   <img src="https://git-scm.com/book/en/v2/images/basic-branching-5.png" width="500">
     
     - C4 커밋이 C2 커밋에 기반한 브랜치이기 때문에 브랜치 포인터는 머지 과정 없이 최신 커밋으로 이동 → **Fast Forward Merge**

6. 핫픽스 브랜치 삭제
   - `git branch -d hotfix`
7. 53번 이슈 브랜치와 메인 브랜치 merge

- `main`이 `checkout`인 상태에서 `git merge iss53`

  - 현재 merge하려는 `main`과 `iss53`의 조상이 같지 않음으로 `fast forward merge`를 사용하지 않음

    <img src="https://git-scm.com/book/en/v2/images/basic-merging-1.png" width="500">

  - `main`과 `iss53` 그리고 공통된 조상 하나를 사용해서 **3-Way Merge**를 사용

    <img src="https://git-scm.com/book/en/v2/images/basic-merging-2.png" width="500">

  - `main + hotfix merge` 와는 달리 별도의 커밋을 만들고 해당 브랜치가 그 커밋을 가리키도록 이동

    <img src="https://git-scm.com/book/en/v2/images/basic-merging-2.png" width="500">

8. 53번 이슈 브랜치 삭제
   - `git branch -d iss53`
