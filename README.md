# mix-blend-mode

- 디자이너가 `mix-blend-mode`를 사용해서 디자인함.
- `background`에 이미지를 넣어야 하는데 이미지가 회색이라서 `blend-mode`가 없으면 어두워지지 않음.
- 디자인 시안대로 적용을 시켜야 예쁘게 나오는데 `mix-blend-mode` `multiply`는 레이어와 레이어를 겹치는 거라서 그냥 `div`에 사용하게 되면 그 안에 있는 요소들에게 `color, gradient`등~ 효과를 적용시킬 수 없음.
- 그래서 어떻게 해야 할지 여러가지 시도를 해봤음.

## 연구 일지

### filter, opacity로만 제어하기

```
.multi::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: url("human.png");
  background-size: contain;
  background-repeat: no-repeat;
  background-position: 94% bottom;
  opacity: 0.4;
}
.filter .multi::before {
  -webkit-filter: grayscale(1) hue-rotate(180deg);
  filter: grayscale(1) hue-rotate(180deg);
}
```

- 예시에서는 제대로 나오지만...
- 가상 클래스에 `filter`와 `opacity`로만 이미지를 제어했는데 오른쪽이 `body`의 뒷배경과 영역의 차이가 거의 나지 않았음.
- 또한, 배경에 `gradient`가 들어가야 하는데, 적용이 안 됨.

> 어차피 `::before` 가상 클래스를 쓸 거라면 그냥 `mix-blend-mode`를 써보자.

### mix-blend-mode

```
.multi {
  background: rgba(48, 51, 68, 0.2);
  position: relative;
  width: 100%;
  height: 100%;
}

.blend .multi {
  mix-blend-mode: multiply;
}
```

- 빈 `div`를 만들고 `multiply`를 넣었더니, 제대로 출력되는 걸 확인했음.
