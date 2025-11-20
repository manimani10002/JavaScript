## 🚀 HTML, css, javascript together

### 1\. 🎨 CSS 복습 및 프로젝트 적용

| 핵심 속성                | 역할                                         | 예시                                  |
| :----------------------- | :------------------------------------------- | :------------------------------------ |
| **`background-color`**   | 요소의 배경색을 지정                         | `background-color: black;`            |
| **`padding` / `margin`** | 내부 여백 / 외부 여백을 설정하여 간격을 조절 | `padding: 10px; margin-bottom: 30px;` |
| **`border-radius`**      | 요소의 모서리를 둥글게 변환                  | `border-radius: 50px;`                |
| **`cursor`**             | 마우스를 요소 위에 올렸을 때 커서 모양 변환  | `cursor: pointer;`                    |

이러한 CSS 스타일을 HTML 문서 내의 `<style>` 태그에 정의하거나, 별도의 `.css` 파일에 작성하여 프로젝트에 적용.

---

### 2\. 💡 동적 스타일 제어: `.classList`

**`.classList`** 는 JavaScript가 DOM 요소를 조작하여 CSS 스타일을 동적으로 적용하고 해제할 수 있게 해주는 핵심 기능이다. CSS 규칙은 그대로 두고, JavaScript는 해당 규칙이 적용될지 말지만 결정한다.

#### 주요 `.classList` 메서드

| 메서드            | 코드 예시                                      | 설명                                                                          |
| :---------------- | :--------------------------------------------- | :---------------------------------------------------------------------------- |
| **`.add()`**      | `element.classList.add('is-subscribed');`      | 요소에 해당 CSS **클래스를 추가**합니다.                                      |
| **`.remove()`**   | `element.classList.remove('is-subscribed');`   | 요소에서 해당 클래스를 **제거**합니다.                                        |
| **`.toggle()`**   | `element.classList.toggle('is-subscribed');`   | 클래스가 있으면 **제거**, 없으면 **추가**합니다. 상태 전환에 가장 효율적이다. |
| **`.contains()`** | `element.classList.contains('is-subscribed');` | 해당 클래스가 있는지 **boolean (true/false)** 으로 확인한다.                  |

**예시 (구독 버튼 토글):**

```javascript
// 버튼 클릭 이벤트 핸들러 내부
function handleSubscribe() {
  const buttonElement = document.querySelector('.js-subscribe-button');
  // CSS에 정의된 'is-subscribed' 클래스를 토글하여 스타일을 변경한다.
  buttonElement.classList.toggle('is-subscribed');
}
```

---

### 3\. 📂 JavaScript 및 CSS 코드 분리 (Organize Code)

잘 조직된 코드는 유지보수와 가독성을 높입니다. 오늘은 모든 코드를 하나의 HTML 파일에 두는 대신, 역할을 분리하여 별도의 파일로 관리하는 방법을 학습.

#### 1\. JavaScript 파일 분리 (`.js`)

HTML 파일 내의 `<script>` 태그 내용을 별도의 `.js` 파일로 이동하고, HTML에서 이 파일을 불러온다.

```html
<body>
  ...
  <script src="script.js"></script>
</body>
```

#### 2\. CSS 파일 분리 (`.css`)

HTML 파일 내의 `<style>` 태그 내용을 별도의 `.css` 파일로 이동하고, `<link>` 태그로 HTML에 연결한다.

```html
<head>
  <link rel="stylesheet" href="styles.css" />
</head>
```

이렇게 코드를 분리하면 **HTML은 구조**, **CSS는 디자인**, **JavaScript는 동작**이라는 각자의 역할에만 집중할 수 있어 프로젝트 관리가 훨씬 효율적이다.
