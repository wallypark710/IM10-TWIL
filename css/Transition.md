# CSS Transition

[CSS-TRICKS transition](https://css-tricks.com/almanac/properties/t/transition/)

"아주 쉽습니다."

The `transition` property is a shorthand property used to represent up to four transition-related longhand properties:

```
.example {
  transition: [transition-property][transition-duration][transition-timing-function][transition-delay]
}
```

- `transition-property`: element의 어떤 property를 효과 주고 싶은지 지정. 예) `background-color`, `height`, `width`, `all`
- `transition-duration`: time
- `transition-timing-function`: `linear`, `ease`, `ease-in`, `ease-out`, `ease-in-out`
- `transition-delay`: time

```
div {
  transition: background 0.2s ease,
              padding 0.8s linear;
}
```
> transition attribute 안에 원하는 transition property `,`로 사용하면 됨 
