# Day 3 정리

## 1. Flexbox

부모에게 `display: flex`를 주면 자식 요소들을 가로/세로로 쉽게 배치·정렬할 수 있다.

```css
.container {
    display: flex;
    justify-content: space-between;  /* 주축 정렬 */
    align-items: center;             /* 교차축 정렬 */
    gap: 10px;                       /* 자식 사이 간격 */
}
```

| 속성 | 역할 | 자주 쓰는 값 |
|---|---|---|
| `flex-direction` | 배치 방향 | `row`(가로, 기본), `column`(세로) |
| `justify-content` | 주축 정렬 | `center`, `space-between`, `space-around` |
| `align-items` | 교차축 정렬 | `center`, `flex-start`, `stretch` |
| `flex-wrap` | 넘치면 줄바꿈 | `wrap` |
| `flex: 1` (자식) | 남은 공간 비율대로 차지 | |

> `row`면 justify = 가로 / align = 세로, `column`이면 반대

---

## 2. Navbar

사이트의 메뉴 모음. 시맨틱 태그 `<nav>` 안에 링크를 나열한다.

```html
<nav id="menu">
    <a href="#introduce">Introduce</a>
    <a href="#skills">Skills</a>
</nav>
```

- `href="#아이디"` → 같은 페이지의 해당 `id` 섹션으로 이동 (앵커 링크)
- 상단 가로 메뉴 / 사이드바(세로 메뉴) 형태가 있음

---

## 3. Position

| 값 | 특징 |
|---|---|
| `static` | 기본값 |
| `relative` | 원래 자리 기준으로 이동 |
| `absolute` | static이 아닌(relative, absolute, fixed 등) 조상 중 나와 가장 가까운 조상을 기준점으로 삼음.
실무 공식 (⭐): 부모(relative) + 자식(absolute) 조합을 99% 사용함. (부모를 틀로 만들고 자식을 그 안에서 자유롭게 배치할 때!) |
| `fixed` | 화면 기준 고정, 스크롤해도 그 자리 (공간 차지 X) |
| `sticky` | 원래 자리에 있다가 스크롤 시 붙음 (공간 차지 O) |

```css
#menu {
    position: fixed;
    top: 0;
    left: 0;
}
```

---

## 4. 반응형 디자인 (Media Query)

화면 크기에 따라 다른 CSS를 적용하는 **조건문**.

```css
@media (max-width: 768px) {   /* 768px 이하 (태블릿) */
    #menu { flex-direction: row; }
}

@media (max-width: 480px) {   /* 480px 이하 (모바일) */
    .item { flex-direction: column; }
}
```

- `max-width` = 이하, `min-width` = 이상
- 모바일(400px)은 768, 480 조건 **둘 다** 적용됨
- 큰 조건을 먼저, 작은 조건을 나중에 작성 (뒤에 쓴 게 우선)
- `<meta name="viewport" content="width=device-width, initial-scale=1.0">` 필수
