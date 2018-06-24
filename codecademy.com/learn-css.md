- CSS?
    - HTML 내용을 꾸며주는 언어

- 인라인 스타일
    - style속성

- 스타일 요소
    - &lt;head&gt;
        - &lt;style&gt;
            - p { ... }

        - &lt;/style&gt;

    - &lt;/head&gt;
    - 재사용 할 수 있다.

- CSS 파일 링크
    - &lt;link href="./style.css" type="text/css" rel="stylesheet"&gt;
    - 재사용 할 수 있다.
    - 스타일 수정 시에 HTML 파일과 독립적으로 수정할 수 있다.
    - 여러 HTML파일에서 캐시된 CSS파일을 사용할 수 있다.

- CSS 코드 컨벤션
    - #large-title { background-color: red; }

- CSS 셀렉터
    - 태그 : h { ... }
    - 클래스 : .brand { ... }
        - 재활용을 위한 목적
        - 여러 클래스 : &lt;h1 class="brand card"&gt;

    - 아이디 : #container { ... }
        - 하나의 요소에만 적용할 목적

    - 우선순위
        - 아이디 &gt; 클래스 &gt; 태그
        - p {
            - color: blue !important; /* 우선순위 무시하고 덮어버림. 안 쓰길 권장 */ 

        - }

    - 체이닝
        - h.special /* special 클래스를 가지는 h태그만 선택 */
        - .main-list h5 /* main-list 클래스를 가지는 태그의 안에 있는 h5 태그만 선택 */

    - 여러 개 선택
        - h1, .menu {
            - font-family: Georgia;

        - }

- 스타일
    - font-family
    - font-weight
    - text-align
    - color
    - background-color
    - opacity
    - background-image: url("https://s3.amazonaws.com/codecademy-content/courses/freelance-1/unit-2/soccer.jpeg")
