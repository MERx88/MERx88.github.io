---
layout: default
title: HTML & CSS
nav_order: 6
has_children: true
---

# HTML

## input

### checkbox

**id 속성**

고유 식별자이고 `<label>` 태그의 for 하고 같이 쓰면 해당 라벨을 클릭해도 체크 박스가 선택된다. 그 고유식별자이기 때문에 꼭 구분되게 쓰자 안그러면 다같이 전체주의 마냥 행동하는 체크박스 그룹을 볼수있다. 쓰지말거면 쓰지말자라고 하기엔 식별자니 넣어주자 그래도

**name 속성**

해당 체크박스 그룹의 이름을 지정해주는 느낌이다. 예를 들어 red, blue, yellow 의 체크박스 들을 묶는 'color' 를 name을 설정하면 좋다. 그리고 폼데이터를 제출할때 사용된다 즉, 서버로 보낼때 사용된다.

**value 속성**

value는 red, blue, yellow 이 각각의 체크박스 들을 나타내고 서버로 실제로 보내는 값이다. 식별자는 아니다. 그러니 유일하지않아도 된다.

**name value를 이용한 데이터 보내기**

```html
<label> <input type="checkbox" name="color" value="red" /> Red </label>
<label> <input type="checkbox" name="color" value="blue" /> Blue </label>
<label> <input type="checkbox" name="color" value="yellow" /> Yellow </label>
```

이러한 예제에서 red와 blue를 선택하고 폼 제출하면 `color=red&color=blue` 이렇게 날아간다.

# CSS
