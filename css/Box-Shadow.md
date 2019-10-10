# CSS Box-Shadow

[w3 css box-shadow property](https://www.w3schools.com/cssref/css3_pr_box-shadow.asp)

간단하게 요약해봅니다.

> `box-shadow:` [none || `h-offset`] [`v-offset`] [`blur`] [`spread`] [`color`] [ `inset | initial | inherit`];

`h-offset`: 수평 오른쪽으로 아님 왼쪽으로 얼마나 offset을 주고 싶은지 `px` 값 입력. 

`v-offset`: 수직 아래로 아님 위로 얼마나 offset을 주고 싶은지 `px` 값 입력.

- `px` 값에 따라 왼쪽 < 0 `px` < 오른쪽 offset 적용됨. 

`blur`: 얼마나 흐리게 하고 싶은지 `px` 값 입력

`spread`: shadow 범위를 `px` 값으로 정할 수 있다. 

`color`: 색깔 넣으시오

`inset`: 보통 `<div>` 태그가 넓이 높이가 있는데 inset으로 하면 안쪽 외곽선 쪽에서 그림자가 뜬다
`initial`: default 값이다. 안 넣어도 된다. 
`inherit`: 부모 element의 property를 이어 받는다. 

---

## Top shadow만 없애고 싶을 때
> `box-shadow`: `0 3px 4px grey`;
**Case:** 
header bar 컴포넌트에 메뉴 버튼이 있는데 누르면 메뉴 컴포넌트가 뜬다. 
하지만 메뉴 컴포넌트는 header bar 안에 들어가 있지 않고 밖에 있어서 메뉴 컴포넌트에다 box-shadow를 적용해보니깐 header-bar 위 box-shadow가 덮치고 있었다. `v-offset`으로 top border box-shadow를 없앨 수 있어다. 
참고로 메뉴 컴포넌트는 viewport를 채우고 있었는데 만약에 height viewport가 100% 아니라면 밑쪽 외곽선에 box-shadow가 더 보인다.  
