# Github
웹 기반의 Git 원격(Remote) 저장소 호스팅 플랫폼

</br>

## 기본 용어 및 명령어
### push
: 로컬 저장소의 변경 내용을 원격 저장소로 업로드

<pre>git push <원격 저장소> <로컬 브랜치>:<원격 브랜치></pre>
로컬 브랜치의 이름과 원격 브랜치의 이름이 같다면 생략 가능
<pre>git push origin master</pre>
로컬 `master` 브랜치의 변경 내용을 원격 저장소 `origin`의 `master` 브랜치로 업로드

> `origin` : Git에서 가장 흔하게 사용되는 원격 저장소의 별칭 중 하나

</br>

### clone
: 원격 저장소에 있는 코드를 로컬 컴퓨터로 복제

<pre>git clone <원격 저장소 URL></pre>

</br>

### fork
: 다른 사용자의 원격 저장소를 복제하여 자신의 계정에 독립적인 복사본 생성

</br>

### pull request
: 협업 및 오픈 소스 프로젝트에서 코드 변경 사항을 제안하고 검토하기 위한 메커니즘

1. Fork하거나 Branch 생성
2. 코드 변경 후 커밋
3. Pull Request 생성
4. 피드백
5. 피드백을 수용하여 코드 수정
6. 병합(Merge)
7. Pull Request 닫기

</br>

### Upstream Branch
: Fork 시 기준이 되는 원격 브랜치

- 원본 프로젝트에서 변경 사항 발생 시 Upstream Branch를 통해 Fork된 프로젝트에 해당 내용 반영

- 코드를 최신 상태로 유지 가능

#### Upstream Branch를 설정하는 방법
    
1. 원본 프로젝트(원본 저장소)의 URL을 원격 저장소로 추가

    <pre>git remote add upstream <원본 프로젝트 URL></pre>
    - 일반적으로 upstream이라는 이름으로 추가

</br>


2. Upstream으로 설정한 프로젝트의 원하는 브랜치로부터 변경 사항 가져와 병합 (선택 사항)

    <pre>git fetch upstream
   git merge upstream/<원하는 브랜치></pre>
    
</br>

### fetch
: 원격 저장소로부터 최신 변경 사항을 로컬 저장소로 가져오는 작업 수행

1. 원격 저장소 `origin`으로부터 변경 사항 가져오기
    <pre>git fetch origin</pre>

2. 원격 저장소 `origin`의 `master`브랜치의 변경 사항을 로컬 브랜치에 병합
    <pre>git merge origin/master</pre>
    - `git merge` 명령어는 병합 대상 브랜치를 현재 체크아웃된 브랜치로 가정

</br>

- `pull`과 다른 점은 `pull`의 경우 병합까지 한번에 수행

</br>

### Issue
: 프로젝트 내에서 해결해야 할 작업, 기능 요청, 버그 보고서 또는 기타 작업 항목들

- Issues 탭의 New issue 버튼을 통해 이슈 생성

- 이슈 페이지에서 댓글을 통해 토론

- 이슈가 해결되면 해당 이슈 폐쇄 (Closed 상태로 변경)

#### Milestone
: 프로젝트의 일련의 작업 단계, 목표를 나타내는 데 사용, 프로젝트의 일정을 계획하고 s추적

- Issues 또는 Pull requests 탭의 Milestone 버튼을 통해 마일스톤 생성

- 마일스톤에 Pull request, Issue를 연결하여 해당 마일스톤의 진행 상황 파악 가능