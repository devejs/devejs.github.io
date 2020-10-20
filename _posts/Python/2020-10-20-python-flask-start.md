---
layout: post
title: Starting the Flask-- install virtualenv
category: Python
---
*Publishing Date:2020-10-20*

### Virtualenv
`Virtualenv`는 `anaconda`와 같은 dependency 관리 툴이다. dependency, 의존성을 관리한다는 것은 여러 가지 버전의 파이썬과 파이썬 라이브러리들의 버전을 관리한다는 말과 흡사하다. 그렇다면 이 버전 관리가 왜 필요할까?  
일반적으로 내 컴퓨터에서 하나의 파이썬 프로젝트만 진행하는 경우에는 상관이 없지만, 시간이 흐르며 여러 프로젝트를 진행하게 되는 경우를 생각해보자.  
<!-- ~~ 아직 작성 안함 ~~ -->

`Virtualenv`는 하나의 프로젝트를 진행하기 위해 일종의 가상 환경을 만들어줌으로써 여러 프로젝트가 하나의 컴퓨터에서 진행되더라도 서로에게 영향을 미치지 않게 해 준다.  
그렇다고 이 툴이 VirtualVM처럼 아예 가상 컴퓨터를 만들어주거나 하는 것은 아니고, 파이썬 패키지 관리 프로그램인 `pip`을 비롯해 파이썬 스탠다드 라이브러리 등을 전부 복사한 폴더를 만들어준다. 이 폴더에서 작업하는 한 파이썬 프로그램을 실행시키는 데 문제가 없는 것을 보장해준다는 의미에서 가상 환경이라고 말하는 것이다.  
따라서 우리는 `virtualenv` 툴을 설치하고, 진행할 프로젝트 루트 폴더에서 가상환경을 생성할 폴더를 만들어주면 된다.


### Installation
MacOS, Catalina를 기준으로 설치를 진행했다.  
homebrew로 설치해야 하는지 pip으로 설치해야하는지 찾아보았는데, pip이 OS 독립적이고 파이썬 패키지만 설치할 수 있는 툴이라는 것 외에는 별다른 차이점이 없어 조금 더 나에게 익숙한 pip을 사용하기로 했다.  
이 내용은 따로 [포스트]()를 작성하면서 공부하기로 했다.
```
pip3 install virtualenv
virtualenv --version
// 출력
virtualenv 20.0.35 from /Library/Python/3.8/site-packages/virtualenv/__init__.py
```
`virtualenv`를 설치하고 버전을 확인했을 때 제대로 출력되면 된다. 이제 내 프로젝트를 진행할 폴더로 이동해서 환경설정을 해보자.
```
cd ~/ProjectDir
virtualenv env  //가상 환경 생성
ls -a ./env   //생성된 폴더 확인
// 출력
.Python  .gitignore  bin  lib  pyvenv.cfg
```
생성된 env 디렉터리를 확인해보면 위와 같이 생성된 것을 볼 수 있다. `.Python`은 사용할 파이썬을 가리키는 심볼릭 링크이고, bin과 lib 디렉터리에서 파이썬을 실행하는데 필요한 파일들을 확인할 수 있다.  
이제 가상환경을 실행해보자.
```
. env/bin/activate
```
터미널 앞에 (env), 즉 내가 생성한 가상 환경 폴더명이 나타나면 가상 환경이 실행된 것이다. 드디어 Flask를 설치해보자.
```
pip list
pip install Flask
pip list
```
pip list로 이 가상환경 안에 설치된 라이브러리들을 확인할 수 있다. 처음에는 설치된 라이브러리가 없을 것이다. Flask를 설치한 후에 다시 확인해보면 설치된 라이브러리들을 확인할 수 있다.  

마지막으로 어디에나 있는 다음 예제를 통해 플라스크 애플리케이션을 실행해보자.
```
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello World!'

if __name__ == '__main__':
    app.run()
```
위 코드를 `hello.py` 이름으로 저장하고 `python hello.py`로 실행한다.  
```
* Serving Flask app "hello" (lazy loading)
* Environment: production
  WARNING: This is a development server. Do not use it in a production deployment.
  Use a production WSGI server instead.
* Debug mode: off
* Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
127.0.0.1 - - [20/Oct/2020 23:11:16] "GET / HTTP/1.1" 200 -
127.0.0.1 - - [20/Oct/2020 23:11:16] "GET /favicon.ico HTTP/1.1" 404 -
```
그리고 브라우저에서 `http://127.0.0.1:5000/`을 실행하면
> Hello World!

를 출력하는 웹 화면을 볼 수 있다.


### Reference
[Pip and Virtualenv](https://www.dabapps.com/blog/introduction-to-pip-and-virtualenv-python/)  
[Flask Docs- installation](https://flask-docs-kr.readthedocs.io/ko/latest/installation.html)  
