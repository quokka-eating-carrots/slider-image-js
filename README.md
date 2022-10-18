# slider-image-js

[참고 강의](https://youtu.be/7ZO2RTMNSAY)<br>
[완성 페이지](https://dainty-starlight-9eadc3.netlify.app)

---
## html 작성하기
```html
<div class="wrap">
    <div id="arrow-left" class="arrow"></div>
    <div id="silder">
      <div class="slide slide1">
        <div class="slide-content">
          <span>Image One</span>
        </div>
      </div>
      <div class="slide slide2">
        <div class="slide-content">
          <span>Image Two</span>
        </div>
      </div>
      <div class="slide slide3">
        <div class="slide-content">
          <span>Image Three</span>
        </div>
      </div>
    </div>
    <div id="arrow-right" class="arrow"></div>
  </div>
```

## css 작성하기
```css
#arrow-left {
  border-width: 30px 40px 30px 0;
  border-color: transparent rgba(255, 255, 255, .8) transparent transparent;
  left: 0;
  margin-left: 30px;
}

#arrow-right {
  border-width: 30px 0 30px 40px;
  border-color: transparent transparent transparent rgba(255, 255, 255, .8);
  right: 0;
  margin-right: 30px;
}
```

기존에 `border-width`와 `border-color`은 사용해 보지 않았던 부분인데 두 가지를 활용하여서 삼각형을 만들어 보았습니다.

## JS 작성하기
```javascript
let sliderImages = document.querySelectorAll('.slide'),
    arrowLeft = document.querySelector('#arrow-left'),
    arrowRight = document.querySelector('#arrow-right'),
    current = 0;
```

동시에 진행되어야 하는 것이기 때문에 `,`를 사용하여 변수를 작성합니다.

```javascript
function reset() {
  for(let i = 0; i < sliderImages.length; i += 1) {
    sliderImages[i].style.display = 'none';
  }
}
```
하나의 이미지만 나오게 해야 되기 때문에 페이지들을 숨길 수 있는 함수를 작성합니다. `reset` 함수를 실행하면 아무것도 보이지 않기 때문에 아래와 같은 함수를 작성합니다.

```javascript
function startSlide() {
  reset();
  sliderImages[0].style.display = 'block';
}
```

처음에 페이지가 로딩이 되었을 때 첫 번째 사진이 보이기 위해서 `[0]` 인덱스 값을 넣어 주었습니다.

```javascript
function slideLeft() {
  reset();
  sliderImages[current - 1].style.display = 'block';
  current -= 1;
}

arrowLeft.addEventListener('click', function () {
  if (current === 0) {
    current = sliderImages.length;
  }
  slideLeft();
});
```
왼쪽 화살표를 클릭하였을 때 `current - 1` 즉, 최근의 전 화면이 나타나야 합니다. `addEventListener`을 사용하여 왼쪽 화살표를  클릭하였을 때 `current` 값이 0이라면 왼쪽 화살표를 클릭하였을 때 제일 마지막 사진이 나와야 함으로 `length`를 사용해 주었고, 그게 아니라면 `current` 값에서 -1을 해 주는 함수를 사용해 줍니다.


```javascript
function slideRight() {
  reset();
  sliderImages[current + 1].style.display = 'block';
  current += 1;
}

arrowRight.addEventListener('click', function () {
  if (current === sliderImages.length -1) {
    current = -1;
  }
  slideRight();
})
```
오른쪽 화살표를 클릭하였을 때는 + 1 을 하는 것은 비슷한데, `addEventlistener` 부분이 살짝 다릅니다. `current`의 값이 슬라이드 수보다 하나 작을 땐 (index 값은 제로베이스이기 때문에) `current` 값을 -1로 주어서 다시 index 값이 0이 되게 해야 합니다.