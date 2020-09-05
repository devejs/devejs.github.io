---
layout: post
title: Install jekyll in MacOS
category: Snippet
---
*Publishing Date:2020-09-05*
# 맥에서 지킬 설치하기(깃헙 블로그 초기세팅)

나는 이미 윈도우에서 지킬을 사용한 깃헙 블로그 세팅을 전부 마쳐놓았다. 그러나 원래 사용하던 윈도우 노트북에서 맥북으로 갈아타며 맥북에 새로 로컬 리포를 만들고 지킬을 설치하는 과정을 (까먹을까봐) 간단하게 정리했다.

### 준비물
* 이미 생성된 블로그 리파지토리

### 이사 시작
1. 윈도우 로컬에 혹시나 빠진 파일이 있을까봐 `git status`를 확인하여 로컬과 원격 리파지토리를 동기화시켜주었다. 당연한 말이지만 전부 다 동기화되어 있다면 생략해도 된다.
```
$git status
$git add <files>
$git commit -m "Sync window local and remote"
$git push
```
2. 맥북에서 블로그 리파지토리를 클론받아 원하는 경로에 로컬 리포를 만들어주었다.
```
$git clone <본인 블로그 리포 경로>
```
3. 맥 OS에는 이미 루비가 설치되어 있다. 따라서 지킬 설정이 뭔가 복잡한 윈도우와 다르게 훨씬 간단하게 설치해줄 수 있다. 카탈리나 10.15는 루비 2.6.3이 기본적으로 포함되어 있으므로 문제가 없으나, 맥 OS 버전에 따라 설치되어 있는 루비 버전이 다르므로 한번 확인해주자. Jekyll이 필요로 하는 루비 버전은 현재 날짜[2020-09-04] 기준으로 2.4.0이다.
```
$which ruby
$ruby -v
```
4. 3번에서 문제가 있는 사람이라면 Homebrew를 사용해 최신 버전의 루비를 설치해주자. Homebrew가 설치되어있지 않다면 설치하는 것을 권장한다. 설치 후 3번을 되풀이해 버전을 확인해준다.
```
$brew update
$brew install ruby
```
5. 이 부분에서 내가 헤맸는데, 단순히 루비만 가지고 지킬을 설치하고 나자 경고메세지가 발생했다.
```
$gem install --user-install bundler jekyll
Fetching bundler-2.1.4.gem
WARNING:  You don't have /Users/devejs/.gem/ruby/2.6.0/bin in your PATH,
	  gem executables will not run.
Successfully installed bundler-2.1.4
  ...
```
지킬은 제대로 설치되었는데 환경변수가 제대로 설정되어있지 않아서 gem이 실행되지 않을 것이라고 한다.
--user-install로 GEM을 설치할 경우 RubyGems은 gem을 ~/.gem/ruby/~ 와 같이 홈 디렉터리 안의 디렉터리에 설치하는데, 설치된 gem의 명령어가 설치된 디렉터리 내부 bin 디렉터리에 있기 때문에 환경변수를 추가해줘야하는 것 같다. 따라서 쉘 환경변수에 위의 명령어 경로를 추가해주면 되는 듯!

6. 환경변수 설정을 하기 위해 쉘에 들어가 환경변수를 설정해주어야 하는데, 나는 환경변수 설정을 안하고 엉뚱한 방법으로 진행을 했다.
구글링하다가 발견한 글에도 그렇고, jekyll 문서에도 그렇고 시스템에 설치된 루비를 그대로 사용하는 것은 좋지 않다고 해서 jekyll 문서에 나온 rbenv로 루비를 새로 설치하기로 했다. 현재 날짜 기준으로 최신 루비의 버전이 2.7.1이라 해당 버전을 설치했다.
```
// rbenv 설치
$brew install rbenv ruby-build
// 설치 가능한 버전 확인
$rbenv install -l
$rbenv install 2.7.1
```

7. 설치한 루비를 확인해보았다.
```
$ruby -v
ruby 2.6.3p62 (2019-04-16 revision 67580) [universal.x86_64-darwin19]
$rbenv versions
* system (set by /Users/devejs/.rbenv/version)
  2.7.1
```
원래 기존 맥OS가 가지고 있던 루비 버전이 rbenv에서도 기본으로 설정되어 있다. 이 때 새로 설치한 2.7.1버전을 사용하려고 하면 다음 명령어를 입력한다. 다시 rbenv 버전을 확인하면 2.7.1을 사용하고 있는 것을 볼 수 있다.
```
$rbenv global 2.7.1
$rbenv versions
  system
* 2.7.1 (set by /Users/devejs/.rbenv/version)
```

8. 그리고 환경변수 설정 대신 다음 명령어를 사용했다. rehash는 환경변수에 포함된 ~/.rbenv/shims 경로에 링크를 만들어주는 명령어이다. rbenv 문서에 따르면 새 버전의 루비를 설치하거나 이 커맨드를 제공하는 젬을 설치한 후에 rehash를 사용하라고 한다. 이 커맨드를 제공하는 젬이라는 게 내가 이해한 바가 맞다면 rehash가 먹히는 게 있고 없는게 있는건가..? 나중에 알게 되면 추가할 것.
```
$rbenv rehash
// 환경변수 확인
$gem env
```



9. 마지막으로 내 블로그 리포 경로로 가서 실행시켜준다. 이미 만들어진 블로그를 실행시킨 적이 있으므로 윈도우에서 `jekyll new` 커맨드로 생성할 필요 없이 바로 `bundle exec jekyll serve`로 실행시켜주면 된다.


윈도우에 지킬 설치할 때는 뭐 설치할 것도 많고 설치해도 안되고 되게 애먹었던 것 같은데 맥에서 하니까 이렇게 쉽다니.. 어메이징한 루비의 세계
맥에서 환경변수 설정하는 것은 추가로 공부해서 포스팅할 것!

### References
[jekyll 문서](http://jekyllrb-ko.github.io/docs/installation/macos/)
[ruby-gem 가이드](https://ruby-korea.github.io/rubygems-guides/faqs/)
[rbenv 문서- rehash](https://github.com/rbenv/rbenv#rbenv-rehash)
[내 영혼의 고향 스택 오버플로우](https://stackoverflow.com/questions/19276621/jekyll-installed-but-command-not-found)
