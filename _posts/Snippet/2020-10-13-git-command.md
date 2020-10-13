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
