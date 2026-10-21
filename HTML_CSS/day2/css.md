# CSS 정리하기

## 1. CSS란?

**CSS (Cascading Style Sheets)** 는 HTML 문서의 **모양(디자인)** 을 꾸미는 스타일 언어다.

- **HTML** = 구조와 내용 (뼈대) → "여기에 제목이 있다"
- **CSS** = 표현과 디자인 (옷) → "제목은 빨간색, 30px로 보여줘"

### 기본 문법

```css
선택자 {
  속성: 값;
  속성: 값;
}
```

```css
h1 {
  color: red;        /* 글자색 */
  font-size: 30px;   /* 글자 크기 */
}
```

- **선택자(Selector)**: 스타일을 적용할 대상 (`h1`)
- **선언(Declaration)**: `속성: 값;` 한 쌍 (`color: red;`)
- 선언이 여러 개면 세미콜론(`;`)으로 구분

### Cascading(폭포)의 의미

여러 스타일이 겹치면 정해진 우선순위에 따라 **위에서 아래로 흘러내리듯 적용**된다.

- 같은 우선순위면 **나중에 쓴 스타일**이 이긴다.
- 우선순위: `!important` > Inline 스타일 > `#id` > `.class` > `태그`
- 부모의 일부 속성(글꼴, 색상 등)은 자식에게 **상속**된다.

---

## 2. CSS 적용 방식 3가지

### ① Inline CSS (인라인)

HTML 태그의 `style` 속성에 직접 작성한다.

```html
<p style="color: blue; font-size: 20px;">안녕하세요</p>
```

| 장점 | 단점 |
|---|---|
| 특정 요소 하나만 빠르게 수정 가능 | 재사용 불가, 같은 스타일을 매번 반복 작성 |
| 우선순위가 가장 높음 | HTML과 CSS가 섞여 코드가 지저분해짐 |

### ② Internal CSS (내부)

`<head>` 안에 `<style>` 태그를 넣고 작성한다.

```html
<head>
  <style>
    div {
      background-color: orange;
      border: 1px solid black;
    }
    span {
      background-color: skyblue;
    }
  </style>
</head>
```

| 장점 | 단점 |
|---|---|
| 한 문서 안의 여러 요소에 한 번에 적용 | 그 HTML 파일 안에서만 사용 가능 |
| 별도 파일 없이 간단하게 테스트 가능 | 페이지가 많아지면 관리 어려움 |

### ③ External CSS (외부)

별도의 `.css` 파일을 만들고 `<link>` 태그로 연결한다. **실무에서 가장 많이 쓰는 방식.**

```html
<head>
  <link rel="stylesheet" href="./style.css">
</head>
```

```css
/* style.css */
header {
  font-size: x-large;
  font-weight: bold;
}
```

| 장점 | 단점 |
|---|---|
| 여러 HTML 파일이 하나의 CSS를 공유 (재사용 ↑) | 파일이 하나 더 생김 |
| HTML(구조)과 CSS(디자인)가 분리되어 관리 쉬움 | CSS 파일을 불러오는 요청이 추가됨 |
| 외부 라이브러리도 같은 방식 (Font Awesome, Google Fonts) | |

> 외부 CSS는 `<link>`를 여러 개 써서 **여러 개 동시에 연결 가능**하다.

### 한눈에 비교

| 구분 | 작성 위치 | 적용 범위 | 우선순위 |
|---|---|---|---|
| Inline | 태그의 `style` 속성 | 해당 요소 1개 | 가장 높음 |
| Internal | `<head>` 안 `<style>` | 해당 HTML 문서 | 중간 (나중에 쓴 것이 우선) |
| External | 별도 `.css` 파일 | 연결된 모든 문서 | 중간 (나중에 쓴 것이 우선) |

---

## 3. CSS Selector (선택자)

스타일을 적용할 HTML 요소를 **고르는 방법**.

### 기본 선택자

| 선택자 | 문법 | 예시 | 의미 |
|---|---|---|---|
| 전체 선택자 | `*` | `* { margin: 0; }` | 모든 요소 |
| 태그 선택자 | `태그명` | `p { color: gray; }` | 모든 `<p>` |
| 클래스 선택자 | `.클래스명` | `.tag { ... }` | `class="tag"`인 요소 (여러 개 가능) |
| 아이디 선택자 | `#아이디명` | `#github { ... }` | `id="github"`인 요소 (문서에 1개만) |

```html
<a id="github" class="link">GitHub</a>
```

```css
#github { color: gray; }      /* id로 선택 */
.link   { font-size: small; } /* class로 선택 */
```

### 그룹 / 조합 선택자

| 선택자 | 문법 | 의미 |
|---|---|---|
| 그룹 | `h1, h2` | h1과 h2 모두 |
| 자손 | `nav a` | nav **안에 있는 모든** a |
| 자식 | `ul > li` | ul의 **바로 아래** li만 |
| 인접 형제 | `h2 + p` | h2 **바로 다음** p |
| 일반 형제 | `h2 ~ p` | h2 **뒤에 오는 모든** p |

### 가상 클래스 / 속성 선택자

| 선택자 | 의미 |
|---|---|
| `a:hover` | 마우스를 올렸을 때 |
| `input:focus` | 입력창을 클릭했을 때 |
| `li:first-child` / `li:last-child` | 첫 번째 / 마지막 자식 |
| `li:nth-child(2)` | 두 번째 자식 |
| `input[type="email"]` | type이 email인 input |

```css
#github:hover {
  text-decoration: underline;  /* 마우스 올리면 밑줄 */
}
```

### 선택자 우선순위 (명시도, Specificity)

```
!important  >  inline style  >  #id  >  .class / :hover  >  태그  >  *
```

- 더 **구체적인** 선택자가 이긴다.
- 우선순위가 같으면 **나중에 작성된** 스타일이 적용된다.

---

## 4. style 속성

### a. 텍스트 관련

| 속성 | 설명 | 값 예시 |
|---|---|---|
| `font-size` | 글자 크기 | `16px`, `1.5rem`, `small`, `x-large` |
| `font-weight` | 글자 굵기 | `normal`(400), `bold`(700), `100`~`900` |
| `text-align` | 가로 정렬 | `left`, `center`, `right`, `justify` |
| `font-family` | 글꼴 | `"Noto Sans KR", sans-serif` |
| `color` | 글자색 | `red`, `#333`, `rgb(0,0,0)` |
| `line-height` | 줄 간격 | `1.6`, `24px` |
| `text-decoration` | 밑줄 등 | `none`, `underline`, `line-through` |
| `letter-spacing` | 자간 | `1px` |

```css
header {
  font-family: "Bitcount Ink", system-ui;
  font-size: x-large;
  font-weight: bold;
  text-align: center;
}
```

### b. Box Model

모든 HTML 요소는 **사각형 상자**로 이루어져 있다. 안쪽부터 바깥쪽으로 4개 영역.

```
┌─────────────── margin (바깥 여백) ───────────────┐
│  ┌──────────── border (테두리) ──────────────┐   │
│  │  ┌───────── padding (안쪽 여백) ───────┐  │   │
│  │  │                                    │  │   │
│  │  │        content (내용)              │  │   │
│  │  │     width × height                 │  │   │
│  │  │                                    │  │   │
│  │  └────────────────────────────────────┘  │   │
│  └──────────────────────────────────────────┘   │
└─────────────────────────────────────────────────┘
```

| 속성 | 설명 | 예시 |
|---|---|---|
| `content` | 실제 내용(글자, 이미지)이 들어가는 영역 | — |
| `width` / `height` | content 영역의 가로 / 세로 크기 | `width: 300px;` |
| `padding` | content와 border 사이 **안쪽** 여백 (배경색 적용됨) | `padding: 20px;` |
| `border` | 테두리 (두께 스타일 색상) | `border: 1px solid black;` |
| `margin` | border 바깥의 **바깥쪽** 여백 (투명, 다른 요소와의 거리) | `margin: 20px;` |
| `box-sizing` | width/height를 어디까지 포함해서 계산할지 | `border-box` |

**margin / padding 값 쓰는 법 (시계 방향: 위 → 오른쪽 → 아래 → 왼쪽)**

```css
margin: 10px;                /* 4방향 모두 10px */
margin: 10px 20px;           /* 위아래 10px, 좌우 20px */
margin: 10px 20px 30px;      /* 위 10, 좌우 20, 아래 30 */
margin: 10px 20px 30px 40px; /* 위, 오른쪽, 아래, 왼쪽 */
margin-top: 100px;           /* 한 방향만 */
margin: 0 auto;              /* 블록 요소 가로 가운데 정렬 */
```

**box-sizing**

| 값 | 실제 차지하는 너비 |
|---|---|
| `content-box` (기본값) | width + padding + border → **지정한 것보다 커짐** |
| `border-box` | width 안에 padding, border 포함 → **지정한 크기 그대로** |

```css
.box {
  width: 200px;
  padding: 20px;
  border: 5px solid black;
}
/* content-box: 실제 너비 = 200 + 20×2 + 5×2 = 250px */
/* border-box : 실제 너비 = 200px (content가 150px로 줄어듦) */
```

> 그래서 보통 CSS 맨 위에 아래 코드를 넣고 시작한다.
> ```css
> * { margin: 0; padding: 0; box-sizing: border-box; }
> ```

**block vs inline 요소와 Box Model**

| 구분 | 예시 태그 | 특징 |
|---|---|---|
| block | `div`, `p`, `h1`, `ul`, `section` | 가로 한 줄 전체 차지, width/height/margin 모두 적용 |
| inline | `span`, `a`, `strong`, `img` | 내용만큼만 차지, **width/height·위아래 margin 적용 안 됨** |
| inline-block | `display: inline-block` | 한 줄에 나란히 + width/height 적용 가능 |
