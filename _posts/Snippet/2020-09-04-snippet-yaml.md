---
layout: post
title: YAML- multiple lines
category: Snippet
---
*Publishing Date:2020-09-04*

### 문제 발생
깃헙 블로그 소개글을 수정하고 싶어서 `_config.yml` 파일을 보던 중 `>-` 표시를 발견했다.
나는 현재 무료 테마인 'hydeout'을 클론해 사용하고 있고, config 파일의 해당 설정 부분은 다음과 같이 되어 있었다.
```
title: Devlog
tagline: 'A Jekyll theme'
email: ssej0221@gmail.com
description: >-  # this means to ignore newlines until "baseurl:"
  newbie developer
baseurl: "" # the subpath of your site, e.g. /blog
                  # the optional subpath of your site, e.g. "/blog"
                  # NB: This applies to all pages in your Jekyll site.
                  # If you want to move just the blog index pages but keep
                  # other pages at root, see the paginate_path and
                  # sidebar_blog_link below.
url: "https://devejs.github.io"
```
이 경우 내가 description을 길게 쓸 경우 줄바꿈이 되지 않았다. 하지만 나는 줄바꿈을 원했다. 그렇다면?

### 문제 해결
YAML은 `사람이 쉽게 읽을 수 있는` 데이터 직렬화 양식이다.
각설하고 필요한 내용만 정리하자면 위 코드 스니펫에서 `description`은 해시 구조이고, 이 때 해시는 키:값의 형태로 한 줄에 하나의 요소가 표현된다. 그러나 한 줄에 값이 끝나지 않을 때 인덴트로 리터럴 블록을 유지할 수 있다. 설명이 그지같으니 다음 스니펫을 보자.
```
description: |
  첫번째 줄
  두번째 줄
  리터럴 블록 마지막 줄
# 리터럴 블록 끝남
```
들여쓰기(indentation)을 통해 리터럴 블록을 구별할 수 있고, description 뒤의 지시어에 따라 리터럴 블록 안에서의 개행처리가 달라진다.
* Block Scalar Style : `|`, `>`
* Block Chomping : ` `, `-`, `+`
```
--- |   # new lines preserved; 개행 유지
--- >   # new lines folded; 개행 무시, 개행 문자 -> 스페이스
        # clip : Single newline at end
--- >-  # - : strip; No newline at end
--- |-  
--- >+  # + : keep; All newlines from end
--- |+
```
즉, `>`를 `|`로 바꿔주면 원하는 대로 multiline을 볼 수 있다.

<b>추가내용</b>
* Jekyll의 `_data` 디렉토리에 `파일명.yml` 파일을 넣어두면 `site.data.파일명`으로 파일 내 데이터에 접근할 수 있다!

### 이상한데
포스팅을 거의 끝내고 났더니 다시 이상한 문제가 발생했다. 사실 원하는 대로 multiline을 구현한 것은 `|` identifier가 아닌 <br> 줄바꿈 태그였다.
<br>을 넣으면 지시어에 관계없이 개행이 되고, 넣지 않으면 개행이 되지 않는 것...
이건... 무슨 일인지 모르겠다...ㅠ
나중에 시간 되면 YAML 문법을 더 공부해 봐야겠다

<b>혹시라도 이 부족한 블로그에 찾아와주시는 분이 있다면 틀린 부분에 대해 가르침을 주시면 감사하겠습니다.</b>

### References
[YAML 1.2 문서](https://yaml.org/spec/1.2/spec.html#id2794534)
[YAM Block identifier Demo](https://yaml-multiline.info)
