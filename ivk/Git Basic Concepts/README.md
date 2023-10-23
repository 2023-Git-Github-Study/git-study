# Git Basic Concepts
Git의 기본 용어 및 개념 정리

## Repository
프로젝트의 모든 파일과 폴더의 변경 이력을 저장하는 디렉토리
- Repository 생성
    <pre>$ git init</pre>
    - .git이라는 하위 디렉토리, .gitattributes라는 파일 생성

- 기존 저장소 복제 (Clone)
    <pre>$ git clone url


## Commit
프로젝트의 변경 사항을 Repository에 기록

## Areas
- Working Directory

    - 작업 내용을 Staging Area로 추가 (스테이징)
        <pre>$ git add file name</pre>

- Staging Area
    - 스테이징된 파일을 커밋하여 Git Directory에 저장
        <pre>$ git commit -m commit message</pre>

- Git Directory

## Status
![git status](../image/git%20status.png)
- Tracked
    - Unmodified
    - Modified
    - Staged
- Untracked

> ```git status```를 통해 파일의 상태 확인 가능

## Branch
프로젝트의 다양한 작업 흐름, 버전을 독립적으로 관리
- 브랜치를 생성한 시점의 커밋으로부터 분기

### Branch 작업 과정 예시

1. iss53 브랜치 생성
    <pre>$ git branch testing</pre>

2. 현재 작업 중인 브랜치를 iss53 브랜치로 이동
    <pre>$ git checkout iss53</pre>
    위 두 과정을 다음과 같이 축약 가능
    <pre>$ git checkout -b iss53</pre>   

    ![git branch checkout](../image/git%20branch%20checkout.png)

3. iss53 브랜치에서 새로운 변경 사항 커밋
    <pre>$ git commit</pre>
    ![git branch commit](../image/git%20branch%20commit.png)

4. iss53 브랜치 모두 구현
    ![git branch example](../image/git%20branch%20example.png)

5. iss53 브랜치를 모두 구현한 후 master 브랜치에 병합(Merge)
    > **Merge** : 두 개 이상의 브랜치를 결합하여 하나의 브랜치로 병합하는 과정 
    <pre>$ git checkout master
   $ git merge iss53</pre>
    ![git merge](../image/git%20merge.png)

6. iss53 브랜치 삭제
    <pre>$ git branch -d iss53</pre>


### 충돌 (Confilct)
Merge하는 두 브랜치에서 같은 파일의 한 부분을 동시에 수정하고 Merge하면 Git은 해당 부분을 Merge하지 못하고 충돌

예를 들어 5번 과정 이전에 iss53 브랜치와 master 브랜치에서 동일한 부분을 수정했다고 가정
-  Git은 Merge하지 못하고 아래와 같은 충돌(Conflict) 메시지 출력
    ![git conflict message](../image/git%20conflict%20message.png)

- ```git status```를 통해 어떤 부분에서 충돌이 발생했는지 확인 가능 (Unmerged)

    ![git conflict status](../image/git%20conflict%20status.png)


- 충돌한 부분은 표준 형식에 따라 다음과 같이 표시

    ![git conflict content](../image/git%20conflict%20content.png)
    - ```=======``` 를 기준으로 위쪽의 내용은 Merge 명령을 실행했을 때 작업하던 master 브랜치의 내용, 아래쪽은 iss53 브랜치의 내용
- 충돌을 해결하기 위해서는 둘 중 하나의 내용을 선택하거나 새로 작성한 후 Merge



    


    


