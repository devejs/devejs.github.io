---
layout: post
title: Git Commands
category: Snippet
---
*Publishing Date:2020-10-13*
*Keep Editing...*

# 맨날 까먹는 깃 커맨드 모음

### 가장 최근 커밋 메세지 수정하기
```
git commit --amend -m "New commit message"
```
`-m` 옵션을 빼고 커밋할 경우 에디터에서 새 커밋 메세지를 수정해줄 수 있다.

### add된 파일 스테이징 해제하기
```
git restore --staged <file>
```
파일명을 적어주지 않으면
```
fatal: you must specify path(s) to restore
```
에러가 발생한다. 모든 파일을 unstaging하고 싶으면 `*`을 사용하면 된다.

### 커밋 취소하기
```
// 가장 최근 커밋 취소
git reset HEAD^
```

### 로컬에서 깃 연결하기
```
git init
git remote add origin <github_URL>
git add *
git commit -m "Commit message"
git push --set-upstream origin master
```
push하기 전에 --set-upstream 을 해주지 않으면
```
fatal: 현재 브랜치 master에 업스트림 브랜치가 없습니다.
현재 브랜치를 푸시하고 해당 리모트를 업스트림으로 지정하려면
다음과 같이 하십시오.
```
위와 같은 오류 메세지가 뜬다.  
이는 로컬에서 브랜치를 지정해주지 않았기 때문!  
리포를 클론해오지 않고 바로 로컬에서 작업한 것을 깃헙 리포에 연결할 때 사용한다.
