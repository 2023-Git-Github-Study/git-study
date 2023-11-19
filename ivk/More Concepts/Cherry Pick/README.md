# Cherry Pick

특정 커밋 하나를 선택하여 다른 브랜치로 가져오는 Git 명령어

### ✓ 특정 커밋 선택

`git cherry-pick commit-hash` 명령을 사용하여 가져올 커밋의 해시값 명시

### ✓ 변경사항 적용

해당 커밋의 변경사항이 현재 브랜치에 적용</br>
선택한 커밋의 내용을 현재 브랜치로 복사하여 새로운 커밋으로 생성

### ✓ 새로운 커밋 생성

체리 픽 작업은 원본 커밋의 내용을 변경하지 않고, 복사하여 새로운 커밋으로 생성</br>
→ 동일한 변경사항이 다른 브랜치에 적용

### 예시

`main`, `feature` 두 개의 브랜치가 있다고 가정</br>
`feature` 브랜치의 새로운 내용을 `main` 브랜치에 적용하기 위해 체리 픽 작업 수행

<pre>
# feature 브랜치로 이동
$ git checkout feature

# 특정 커밋을 가져오기 위해 cherry-pick 실행
$ git cherry-pick commit-hash

# main 브랜치로 이동
$ git checkout main

# feature 브랜치에서 가져온 변경사항을 main 브랜치에 적용
$ git merge feature
</pre>

</br>

### 충돌 발생 시

충돌을 해결하고 난 후 `git cherry-pick --continue` 명령어를 통해 계속 진행

</br>

### 체리 픽 작업 취소

`git cherry-pick --abort` 명령어를 통해 체리 픽 작업을 취소
