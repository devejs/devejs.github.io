---
layout: post
title: Git Error Logs
category: Snippet
---
*Publishing Date:2020-10-13*
*Keep Editing...*

# 깃 에러 로그 모음

### git push
#### 푸시 실패
**에러 로그**
> To `$repo_url`
> ! [rejected]        main -> main (non-fast-forward)
> error: 레퍼런스를 '`$repo_url`'에 푸시하는데 실패했습니다
> 힌트: 현재 브랜치의 끝이 리모트 브랜치보다 뒤에 있으므로 업데이트가
> 힌트: 거부되었습니다. 푸시하기 전에 ('git pull ...' 등 명령으로) 리모트
> 힌트: 변경 사항을 포함하십시오.
> 힌트: 자세한 정보는 'git push --help'의 "Note about fast-forwards' 부분을
> 힌트: 참고하십시오.

**에러 원인**
1. 원격과 로컬이 동기화된 상태
2. 로컬에서 특정 커밋 삭제(reset)
3. 삭제된 상태로 푸시
4. 원격에 존재하는 커밋이 로컬에 존재하지 않아 푸시 실패

**해결 방법**
1. `git pull`로 원격 저장소의 커밋(로컬에서 지운 내역)을 가져온 후 `push`
  - 로컬에서 작업한 내용이 있으면 다른 [에러](#자동-병합-실패)가 발생한다.
2. `git push origin main --force`으로 강제 푸시한다.  
`git push -f origin main`과 동일하다.
  - 이 방법을 사용하다가 깨달은 사실이, 최근 `master` 브랜치가 `main`으로 바뀌었다. 옛날 습관때문에 열심히 `git push -f origin master`로 시도하다가 안돼서 주변에 물어봤더니 `main`으로 바뀌었다고 한다.. 그러고 보니 깃헙 리포에도 `main`으로 바뀌어 있었다ㅎㅎ..😂 [해당 에러 로그](#푸시-실패2)   
  가장 최근에 생성한 리포(2020.10.02) 마스터 브랜치가 `main`으로 되어있는데 그 전에 생성한 리포(2020.09.26)에는 `master`로 되어 있는 거 보니 그 사이에 바뀌었나보다.
  - 이 방법은 일단 썩 좋은 방법은 아니다. 나 혼자 쓰는 리포면 크게 상관이 없다고 하지만, 협업하는 경우 내가 삭제/수정해 변경된 커밋이 다른 사람의 리포에는 그대로 들어있을 경우 문제가 발생할 수 있다.

#### 푸시 실패2
```
error: src refspec master does not match any
error: 레퍼런스를 '$repo_url'에 푸시하는데 실패했습니다
```
**에러 원인**
리포 경로나 브랜치가 잘못 설정되었을 때 발생한다.
1. 나의 경우 디폴트 브랜치 이름이 `master`에서 `main`으로 바뀐 것을 모르고  
`git push -f origin master` 커맨드 입력하다가 해당 에러를 마주쳤다.
2. 혹은 리포 주소가 변경되거나 하여 경로가 잘못 연결되더라도 해당 에러가 발생할 수 있다고 한다.   
결국 참조(내가 아는 경로, origin 혹은 upstream)를 따라갔더니 맞는 리포를 찾을 수가 없었다는 것이다.
3. 혹은 커밋할 내용이 아무것도 없었을 경우에도 해당 에러가 발생했다는 글을 볼 수 있었다.

**해결 방법**
1. `git remote -v`로 origin이나 remote 등 경로가 올바르게 설정되어 있는지 확인한다.
2. 1번에서 잘못된 경로를 확인했다면 다음 명령어로 경로를 고쳐준다.
```
// 1번 방법- 삭제하고 재등록
// 이름은 origin, upstream 등 이미 등록되어 있는 이름을 뜻함
git remote remove <이름>
git remote add <이름> <url>
// 2번 방법- 경로만 바꿔줌
git remote set-url <이름> <url>
```
3. 1번에서 경로도 올바르게 되어 있다면 로컬에 남아있는 캐시를 지우고 초기화를 해준 다음에 새로 경로를 설정해주라고 한다. 아직 해보지 못했으므로 다음에 깃 연습을 하거나 해 볼 기회가 생기면 추가할 것.
```
// 현재 폴더 하위의 모든 파일을 삭제
git rm --cached ./
// 리포 초기화 및 설정
git init
git remote add origin <url>
git add ./
git commit -m "commit message"
git push origin <브랜치>
```
4. 혹은 로컬에 아무것도 푸시할 것 없이 푸시해서 해당 메세지가 나왔을 수도 있다.
```
touch README.md
git commit -m "first commit"
git push
```
커밋을 생성해서 다시 푸시해보자.

### git pull
#### 자동 병합 실패
**에러 로그**
> warning: Pulling without specifying how to reconcile divergent branches is
discouraged. You can squelch this message by running one of the following
commands sometime before your next pull:
>
>  git config pull.rebase false  # merge (the default strategy)
>  git config pull.rebase true   # rebase
>  git config pull.ff only       # fast-forward only
>
> You can replace "git config" with "git config --global" to set a default
preference for all repositories. You can also pass --rebase, --no-rebase,
or --ff-only on the command line to override the configured default per
invocation.
>
> 자동 병합: `$파일명`
> 충돌 (내용): `$파일명`에 병합 충돌
> 자동 병합이 실패했습니다. 충돌을 바로잡고 결과물을 커밋하십시오.

**에러 원인**
1. 원격에 있는 커밋이 로컬에 없음
2. 로컬에 있는 커밋이 원격에 없음
3. 충돌된 파일에 대하여 에러 발생

`git status`로 확인한 결과
> 현재 브랜치 main
> 현재 브랜치와 'origin/main'이(가) 갈라졌습니다,
> 다른 커밋이 각각 1개와 1개 있습니다.
>   (리모트의 브랜치를 현재 브랜치로 병합하려면 "git pull"을 사용하십시오)
>
> 병합하지 않은 경로가 있습니다.
>  (충돌을 바로잡고 "git commit"을 실행하십시오)
>  (병합을 중단하려면 "git merge --abort"를 사용하십시오)
>
> 병합하지 않은 경로:
>  (해결했다고 표시하려면 "git add <파일>..."을 사용하십시오)
> 	양쪽에서 수정: `$파일명`
>
> 커밋할 변경 사항을 추가하지 않았습니다 ("git add" 및/또는 "git commit -a"를
사용하십시오)

**해결 방법**
1. `git diff`로 충돌한 내용을 확인한다.
2. 수정

### git merge upstream
