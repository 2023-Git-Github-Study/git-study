# CLI

### Working Directory → Staging Area

<pre>git add file name</pre>

- 해당 파일 add
<pre>git add .</pre>
- 모든 파일 add

</br>

### Staging Area → Local Repository

<pre>git commit</pre>

- `i` 입력하면 INSERT 모드로 전환
- Commit Message 입력 후 ESC키 누르면 INSERT 모드 종료
- `:wq` 입력하면 Commit 완료

<pre>git commit -m commit message</pre>

- Commit Message 입력까지 동시에 수행

</br>

### Local Repository → Remote(Github) Repository

<pre>git push origin main</pre>

</br>

## Commit Log

<pre>git log</pre>

<img src="../image/HEAD to master.png" width="80%"></br>
: Local Repository의 최신 커밋

<img src="../image/origin:master.png" width="80%"></br>
: Github Repository의 최신 커밋, 아직 Local Repository의 최신 커밋이 반영되지 않은 상태

<img src="../image/both.png" width="100%"></br>
: Local Repository의 최신 커밋이 Github Repository에도 커밋된 상태

</br>

## Reset

### Hard Reset

: HEAD 포인터를 지정된 커밋으로 이동, 지정된 커밋 이후의 모든 커밋 삭제

- **_Hard Reset 이전_**

      <img src="../image/Before.png">

      <img src="../image/Before Log.png" width=80%>

  </br>

- **_Hard Reset_**

    <pre>git reset --hard HEAD~1</pre>

  > `HEAD~n` 대신에 지정할 커밋의 해쉬를 입력해도 됨

</br>

- **_Hard Reset 이후_**

    <img src="../image/After Log.png" width=80%>

  - Working Direcotry, Staging Area 어디에도 지정된 커밋 이후의 변경 사항 존재하지 않음

</br>

- **_Hard Reset한 내용 Github Repository에 강제로 Push_**
    <pre>git push origin main --force</pre>

    <img src="../image/After.png">

</br>

### Soft Reset

: HEAD 포인터를 지정한 커밋으로 이동, 지정된 커밋 이후의 변경 사항 Working Direcory와 Staging Area에 유지

<pre>git reset --soft HEAD~1</pre>

<img src="../image/Soft After Log.png" width=80%>

</br>

`git status`를 통해 상태 확인

<img src="../image/Soft Status.png" width=80%></br>

- Staging Area에 변경 사항 존재

- Working Directory에도 변경 사항 유지

</br>

→ 이후 커밋만 해주게 되면 reset 이전의 모든 변경 내용 복구

</br>

### Mixed Reset

: HEAD 포인터를 지정한 커밋으로 이동, 지정된 커밋 이후의 변경 사항을 Untracked 상태로 유지

<pre>git reset HEAD~1</pre>

`git status`를 통해 상태 확인

<img src="../image/Mixed Status.png" width=80%></br>

- Untracked 상태의 파일에 변경 사항 존재

→ add 이후 커밋 해주어야 reset 이전의 변경 내용 복구
