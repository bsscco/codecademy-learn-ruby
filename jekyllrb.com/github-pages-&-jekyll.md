- https://jekyllrb.com
- 튜토리얼  
https://jekyllrb.com/docs/step-by-step/01-setup/
    - 1. 설치 및 개발서버 실행
        - git clone https://github.com/bsscco/bsscco.github.io.git
        - cd bsscco.github.io
        - gem install jekyll bundler
        - jekyll new .
        - jekyll serve
        - 주의
            - index.html과 index.md가 함께 있으면 index.html 무시됨.

    - 2. Liquid
        - Objects
            - {{ }} 
            - 동적 출력

        - Tags
            - {% %}
            - 로직 또는 컨트롤 플로우

        - Filters
            - Object 출력을 가공한다.

    - 3. Front Matter
        - ```---```
        - ```---```
        - 파일 첫부분에 적는 내용
        - Object로 사용된다.

    - 4. Layouts
        - 페이지 레이아웃
        - 각 페이지에서 레이아웃을 재사용할 수 있다.
        - _layouts/default.html
            - {{ content }} 로 내용을 채운다.

        - about.html
            - ---
            - layout: default
            - title: About
            - ---

    - 5. Includes
        - 레이아웃에 다른 레이아웃을 삽입해서 재사용성을 높일 수 있다.
        - _includes/navigation.html
            - &lt;nav&gt;
                - &lt;a href="/"&gt;Home&lt;/a&gt;
                - &lt;a href="/about.html"&gt;About&lt;/a&gt;

            - &lt;/nav&gt;

    - 6. Data Files
        - YAML, JSON, and CSV 파일 지원
        - 소스코드와 컨텐츠를 분리하는 용도. 유지보수가 쉽다.
        - _data/navigation.yml
            - - name: Home
            -    link: /
            - - name: About
            -    link: /about.html

        - _includes/navigation.html
            - &lt;nav&gt;
                - {% for item in site.data.navigation %}
                    - &lt;a href="{{ item.link }}"&gt;
                        - {{ item.name }}

                    - &lt;/a&gt;

                - {% endfor %}

            - &lt;/nav&gt;

    - 7. Assets
        - assets
            - css
            - images
            - js

        - &lt;link rel="stylesheet" href="/assets/css/styles.css"&gt;

    - 8. Blogging
        - 파일명은 발행날짜, 타이틀, 확장자 순으로 짓는다.
        - _posts/2018-08-20-bananas.md
        - 포스트 리스팅
            - blog.html
                - ```---```
                - layout: default
                - title: Blog
                - ```---```
                - &lt;h1&gt;Latest Posts&lt;/h1&gt;
                - &lt;ul&gt;
                    - {% for post in site.posts %}
                        - &lt;li&gt;
                            - &lt;h2&gt;&lt;a href="{{ post.url }}"&gt;{{ post.title }}&lt;/a&gt;&lt;/h2&gt;
                            - &lt;p&gt;{{ post.excerpt }}&lt;/p&gt;

                        - &lt;/li&gt;

                    - {% endfor %}

                - &lt;/ul&gt;

            - post.excerpt : 첫 p 태그의 내용

    - 9. Collections
        - 포스트와 비슷하지만 날짜로 그루핑 되지 않는다.
        - _config.yml
            - collections:
            -   authors:
            -     output: true

        - staff.html
            - ```---```
            - layout: default
            - ```---```
            - &lt;h1&gt;Staff&lt;/h1&gt;
            - &lt;ul&gt;
                - {% for author in site.authors %}
                    - &lt;li&gt;
                        - &lt;h2&gt;&lt;a href="{{ author.url }}"&gt;{{ author.name }}&lt;/a&gt;&lt;/h2&gt;
                        - &lt;h3&gt;{{ author.position }}&lt;/h3&gt;
                        - &lt;p&gt;{{ author.content | markdownify }}&lt;/p&gt;

                    - &lt;/li&gt;

                - {% endfor %}

            - &lt;/ul&gt;

        - _authors/jill.md
            - ```---```
            - short_name: jill
            - name: Jill Smith
            - position: Chief Editor
            - ```---```
            - Jill is an avid fruit grower based in the south of France.

        - _authors/ted.html
            - ```---```
            - short_name: ted
            - name: Ted Doe
            - position: Writer
            - ```---```
            - Ted has been eating fruit since he was baby.

        - output: true
            - 컬렉션 아이템이 각자의 URL을 가지도록 한다.
