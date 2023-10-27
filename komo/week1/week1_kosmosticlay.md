# Git Study Week 1

## 📌 1강 : BASIC GIT CONCEPT

### ✔️ 버전 관리

- 버전 : 유의미한 변화가 결과물로 저장된 것
- 버전 관리 : 특정 순간의 변경사항을 기억하는 것

### ✔️ 기본 개념

- Repository : 프로젝트의 파일과 변경 이력 등을 저장하는 공간 (예: 로컬저장소/원격저장소)
- Git : 버전 관리 제어 도구 -> 백업 / 협업에 유용
- Branch : 특정 커밋으로부터 분기한 독립된 개발 타임라인

### ✔️ Git Workflow

![git workflow diagram](https://miro.medium.com/v2/resize:fit:640/format:webp/1*OqKfKe3mqCRbaWT2Y8YDOQ.png)

- Working Directory : 현재 작업하고 있는 폴더/디렉토리
- Staging Area(=Index) : 다음 버전이 될 후보들을 지정하는 곳
- Local Repository : 스테이지(staged)된 파일들로 새로운 버전을 커밋하는 곳; 로컬 저장소
- Remote Repository : 원격 저장소(Cloud)

---

## ✏️추가 스터디

### ✔️ 먼지TIP

- VSCode Extension - Markdown Preview Enhanced
- [마크다운(Markdown) 6분 순삭 정리@드림코딩](https://www.youtube.com/watch?v=kMEb_BzyUqk)

### ✔️ 버전 / 패치 / 업데이트

- '모든 패치는 업데이트지만, 모든 업데이트가 패치는 아니다'
- **버전** : 소프트웨어의 특정 지점의 '스냅샷'
  <details>
  <summary>버전 표기 방식</summary>
  vX.Y.Z 를 기준으로, <br/>
  - X : 주(Major)버전 / 기존 버전과 호환이 되지 않을 정도의 큰 변화 <br/>
  - Y : 부(Minor)버전 / 기존 버전과 호환이 되지만 새로운 기능을 추가 <br/>
  - Z : 수(Patch)버전 / 기존 버전과 호환이 되며 버그 수정 정도의 작은 변화 <br/>
  </details>
- **패치** : 구체적인 문제/취약점 해결 / 규모가 작고 가벼움 / 빈번하게 발생
  (예: 버그수정, 안정성 향상)
- **업데이트** : 소프트웨어의 일부를 수정, 개선, 또는 기능 추가등 포괄적 과정

### ✔️ 릴리즈와 태그

- **릴리즈** : 최종 사용자에게 공개될 준비가 된 버전
- **태그**
  - 각 커밋은 고유한 해시 값이 있지만, 무작위한 문자열이기에 가독성이 좋지 않음
  - 특정 커밋에 붙일 수 있는 '꼬리표' 또는 '네임택'

---

## 📖 References

- ['모두를 위 깃&깃허브', 노마드코더](https://nomadcoders.co/git-for-beginners/lobby)
