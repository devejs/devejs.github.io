---
layout: post
title: Swift) Defer
category: iOS
---
*Publishing Date:2020-10-15*
# defer란 무엇인지 설명하시오.
# defer가 호출되는 순서는 어떻게 되고, defer가 호출되지 않는 경우를 설명하시오.

### defer
`defer` 키워드는 현재 실행중인 코드 블럭을 나가기 전에 실행되어야 하는 명령들을 실행시켜준다.
> 그냥 코드 블럭에 해당 내용을 넣으면 되는거 아닌가요?

라는 생각이 들 수 있는데, 해당 코드 블럭이 어떻게 종료되든 관계없이 **반드시 수행되어야만 하는** 정리 작업을 하게 해 준다. 즉, 반드시 메모리에서 해제되어야 하는 파일을 닫고 메모리를 해제해주는 작업을 할 수 있도록 코드 자체에서 *보장* 해주는 역할을 한다.  

`defer` 키워드는 다음과 같이 클로저 형태로 사용할 수 있다. `defer` 키워드는 내부 코드들을 해당되는 코드 블럭이 종료될 때까지 실행을 연기시키므로 해당 코드가 실행되었다는 것은 곧 해당 코드 블럭이 종료된다는 것을 의미한다. 따라서 `defer` 키워드 안에는 코드를 종료시킬 수 있는 `return`, `break`, `throw ~` 등의 코드가 들어가서는 안 된다.

```
func deferTest{
  ...
  defer {
    print("defer test")
    // error occurred! -- 'return' cannot transfer control out of a defer statement
    // return
  }
}
```

Swift 문서에서는 오류 처리 항목에 해당 키워드가 설명되어 있지만, 반드시 오류 처리 상황에서만 사용되어야 되는 것은 아니고 코드 블럭 어디든 사용할 수 있다고 한다.  

#### 호출 순서
실행이 연기된 `defer` 키워드 내부 코드들은 소스 코드 내부에 작성된 순서의 반대로 실행된다. 즉, 여러 개의 `defer` 키워드가 있을 때 마지막으로 작성된 키워드의 코드들이 먼저 실행되고, 아래에서 위로 올라가며 각각 실행된다.

#### 왜 사용하는가?
가장 큰 이유는 반드시 정리해야 하는 자원들에 대해 정리를 보장해줄 수 있다는 것이다. 또 반드시 메모리 해제를 해 줘야 하는 상황에서 프로그램 진행에 여러 가지 경우의 수가 있을 때 코드의 중복 없이 깔끔하게 처리를 해 줄 수 있고, 유지보수가 용이해진다.

### 사용 예제
<script src="https://gist.github.com/devejs/e1ddf4b4d664fd594449a93e22433c2a.js"></script>  

해당 예제의 결과는 다음과 같다.
```
defer test: function start
function executing
0
defer in for
1
defer in for
executed first
executed second
exit soon
```

1. 호출 순서  
아래에 있는 `defer` 블록부터 실행되는 것을 확인할 수 있다.  

2. defer 내부에 return 불가  
첫 번째 `defer` 블록에서 바로 리턴했을 때, `'return' cannot transfer control out of defer statement` 오류를 알려준다. 리턴 문이 `defer` 구문 안에서는 바깥으로 함수의 종료를 명령할 수 없는 것이다.

3. 코드 블럭의 정의  
함수 내부에 for문이 있고, for문 안에 `defer` 구문이 존재한다. 이 `defer`문은 언제 실행될까?   
자칫 잘못해서 이 `defer`문도 함수가 종료될 때 실행된다고 생각하면 안 된다. `defer`문은 **코드 블럭** 이 끝날 때 실행되므로, 하나의 코드 블럭을 형성하는 for문이 끝날 때 실행이 된다. 즉, for문이 돈 횟수를 출력한 후 `defer` 내부 프린트문이 출력되는 것을 볼 수 있다.

4. 실행되지 않는 코드  
앞서 코드가 실행되는 것을 **보장** 해 준다고 했지만, 코드가 실행되지 않는 경우도 있다. 바로 `defer` 키워드에 실행 포인트가 도달하기도 전에 종료된 경우다.  
마지막 `defer` 구문을 보면 실행되지 않는다. 해당 구문에 도달하기 전에 코드 블럭이 끝나버리기 때문이다. 그래서 xcode에서는 다음 warning을 뿜뿜하며 코드를 고치라고 권유해준다.
```
- 'defer' statement at end of scope always executes immediately; replace with 'do' statement to silence this warning
Replace 'defer' with 'do'
- Code after 'return' will never be executed
```

첫번째 경고에서는 블록 마지막에 있는 `defer` 구문이 곧바로 실행되므로 `do` 구문으로 바꾸라고 권유해준다. 실제로 23행의 `return`을 지우고 실행할 경우 `function executing...` 문장이 출력된 후 바로 `defer after return` 문장이 출력될 것이다.   
두번째 경고에서 `return` 뒤의 코드가 실행되지 않는다는 것을 알려준다.  
xcode가 경고를 주는 건 다 이유가 있는 법, 가능하면 경고가 뜨지 않게 코딩하는 것이 좋다.

### Reference
[Swift Docs- Error Handling](https://docs.swift.org/swift-book/LanguageGuide/ErrorHandling.html)  
[야곰- Swift 프로그래밍 3판]()  
[참고한 블로그](https://swieeft.github.io/2020/02/26/defer.html)
