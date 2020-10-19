---
layout: post
title: iOS) Bounds, Frame
category: iOS
---
*Publishing Date:2020-10-19*

# Bounds 와 Frame 의 차이점을 설명하시오

### 배경지식
#### UIView
> An object that manages the content for a rectangular area on the screen.
> 스크린의 사각형 지역 내용을 관리하는 객체

#### CGRect


### Bounds
> The bounds rectangle, which describes the view’s location and size in its own coordinate system.
> 바운드(사각형)는 자체 좌표계에서 뷰의 위치와 사이즈를 나타낸다.

```
var bounds: CGRect { get set }
```

바운드는 슈퍼뷰와 관계 없이자체의 좌표계를 가지기 때문에 원점이 항상 (0,0)이다.

<!-- The default bounds origin is (0,0) and the size is the same as the size of the rectangle in the frame property. Changing the size portion of this rectangle grows or shrinks the view relative to its center point. Changing the size also changes the size of the rectangle in the frame property to match. The coordinates of the bounds rectangle are always specified in points.
Changing the bounds rectangle automatically redisplays the view without calling its draw(_:) method. If you want UIKit to call the draw(_:) method, set the contentMode property to UIView.ContentMode.redraw.
Changes to this property can be animated. -->

### Frame
> The frame rectangle, which describes the view’s location and size in its superview’s coordinate system.
> 프레임(사각형)은 슈퍼뷰(부모뷰)의 좌표계를 기준으로 뷰의 위치와 사이즈를 나타낸다.

```
var frame: CGRect { get set }
```

프레임은 크기와 위치를 슈퍼뷰의 좌표계에서 정의하기 때문에 슈퍼뷰, 즉 부모 뷰의 원점에서부터의 위치를 나타낸다. 프레임은 주로 디바이스의 Layout이 뷰의 위치와 사이즈를 설정할 때 사용된다.

<!--
This rectangle defines the size and position of the view in its superview’s coordinate system. Use this rectangle during layout operations to set the size and position the view. Setting this property changes the point specified by the center property and changes the size in the bounds rectangle accordingly. The coordinates of the frame rectangle are always specified in points.

Changing the frame rectangle automatically redisplays the view without calling its draw(_:) method. If you want UIKit to call the draw(_:) method when the frame rectangle changes, set the contentMode property to UIView.ContentMode.redraw.
Changes to this property can be animated. However, if the transform property contains a non-identity transform, the value of the frame property is undefined and should not be modified. In that case, reposition the view using the center property and adjust the size using the bounds property instead. -->

### 차이점
요소|Bound|Frame
---|---|---
좌표계|자체 좌표계|슈퍼뷰 좌표계
원점|(0,0)|부모 뷰 원점이 (0,0)일 때 상대좌표
좌표 이동|내 뷰는 그대로, 자식 뷰가 바뀜|부모 뷰 그대로, 내 뷰가 바뀜
사용처|내부의 어떤 뷰의 위치에 대해 판단할 때|부모 뷰에 대한 내 위치, 대부분의 UIView 위치를 설정할 때


* 내가 이해 덜 가서 하는 추가 설명  
**Bound에서 좌표를 변경했을 때 내 뷰는 그대로, 자식 뷰가 바뀌는 이유**  
-> Bound는 내 자체 좌표계이기 때문에 부모 뷰와 정말 아무런 관계가 없다. 즉, (0,0)-> (a,b)로 위치좌표를 변경한다고 하더라도 부모 뷰와의 어떠한 관계도 없기 때문에 부모와의 상대적인 위치는 변하지 않는다. 그러나 내 좌표계에서의 원점이 바뀌었기 때문에 내 좌표계 밑에 있는 자식 뷰들은 (-a, -b)만큼 이동한다. 스크롤뷰 위에 있는 이미지가 이동하는 것을 상상해보자.    
**그렇다면 Frame에서 좌표를 변경했을 때는?**  
-> 당연히 부모 뷰는 그대로 있고, 부모 뷰의 원점에 대한 내 위치가 바뀌는 것이기 때문에 내 뷰의 위치가 바뀐다.    
**오토 레이아웃으로 인해 크기가 바뀐다면?**  
-> 오토 레이아웃으로 설정해주는 위치는 Frame을 의미한다. 따라서 어떻게 바뀌든 부모 뷰에 대하여 설정된 위치를 기준으로 위치하며 크기가 바뀔 수 있다.  
Bound는 자체 좌표계를 가지고 부모 뷰와 관계가 없기 때문에 오토 레이아웃과는 별개로 크기가 변하지 않는다. 대신 주로 해당 뷰 내부에 그림을 그리거나, 터치 등으로 발생하는 특정 위치 좌표를 구해야 할 때 사용한다.  
즉, 아예 용도가 다르다고 볼 수 있다.  
-> 맞는지 피어세션 때 확인

### Reference
[Apple Docs- UIView](https://developer.apple.com/documentation/uikit/uiview)  
[Apple Docs- Bounds](https://developer.apple.com/documentation/uikit/uiview/1622580-bounds)  
[Apple Docs- Frame](https://developer.apple.com/documentation/uikit/uiview/1622621-frame)  
[Zedd님 블로그](https://zeddios.tistory.com/203)
[UIView frame, bounds 그리고 좌표변환](https://soulpark.wordpress.com/2012/11/30/uiview-frame-bounds-coordinate-conversion/)
