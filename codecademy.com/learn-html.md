- HTML?
    - 하이퍼텍스트 마크업 언어
        - 하이퍼텍스트 : 누르면 다른 문서로 이동하는 텍스트

    - 문서의 구조를 짜는 언어

- 요소 상속
    - 자식 요소는 부모 요소의 스타일과 동작을 상속받는다.

- 요소 속성
    - 열린 태그에 쓴다.
    - 태그를 꾸미거나 구별하는 데에 쓰인다.

- 텍스트 요소
    - p : 텍스트 블록
    - span : 작은 텍스트 조각

- 텍스트 스타일
    - em : italic
    - string : bold

- 줄바꿈 요소
    - br

- 목록 요소
    - ul, ol, li

- 이미지 요소
    - img
    - alt 속성의 역할
        - 이미지 로딩 실패 시 포인터를 올려두면 alt내용이 뜸.
        - 시각장애인들에게 도움이 되는 정보
        - SEO를 위한 정보

- 비디오 요소
    - &lt;video&gt;내용&lt;/video&gt; &lt;!-- 셀프 클로징 태그가 아님 --&gt;
    - 속성
        - width, height

    - 내용의 역할
        - 비디오 로딩 실패 시 대신 보여주는 텍스트

- HTML 파일구조
    - &lt;!DOCTYPE html&gt;
        - HTML5를 가리킨다.

    - &lt;html&gt;&lt;/html&gt; 
        - 페이지의 시작과 끝

    - &lt;head&gt;&lt;/haad&gt;
        - 페이지 정보
        - &lt;title&gt;
            - 탭에 보이는 페이지 타이틀

    - &lt;body&gt;&lt;body&gt;
        - 페이지 구조와 내용

- 링크 요소
    - a
    - target="_blank" 속성
        - 새 탭에서 열기

    - 상대적 경로
        - href="./aboutme.html" 
            - 현재 폴더 안에서 aboutme.html를 찾게 한다.

    - 페이지 내 링크
        - href="#id"

- 주석
    - &lt;!-- 내용 --&gt;

- 테이블 요소
    - table
        - thead
            - tr
                - th

        - tbody
            - tr
                - th, td

        - tfoot
            - tr
                - th, td

    - 속성
        - border는 deprecated 됨.
        - border를 쓰려면 CSS에서 사용하기
        - colspan, rowspan
