- 공통점
    - 문장 끝에 세미콜론(;)을 붙이지 않는다.
    - 문자열 템플릿을 지원한다.

- 차이점
    - 함수에서 값을 반환할 때 return 키워드가
        - R : 필요없다.
        - K : 필요하다.

    - 문자열 템플릿 식의 구성이 조금 다르다.
        - R : "Hi #{var}."
        - K : "Hi ${var}."

    - 속성에 대한 기본 접근 권한이
        - R : 닫혀있다. 열려면 attr_accessor류를 써야 한다.
        - K : 열려있다.

    - 선택문
        - R : case
        - K : when

    - 괄호의 필요
        - R : 필요없음
        - K : 기본적으로 필요

    - 생성자 호출
        - R : AAA.new(a, b)
        - K : AAA(a, b)

    - 범위 생성
        - R : 1...10(exclusive), 1..10(inclusive)
        - K : 1..10(inclusive)

    - 스마트 캐스트
        - R : 없음
        - K : 있음

    - 포함 연산자(in)
        - R : 없음
        - K : 있음

    - 기본 출력함수
        - R : puts
        - K : println

    - 함수 선언 키워드
        - R : def
        - K : fun

    - 객체 비교
        - R : &lt;=&gt; 연산자 사용. 단, &lt;=&gt; 메소드를 오버라이딩 해야 정상 동작
        - K : == 연산자 사용. 단, equals를 오버라이딩 해야 정상 동작

    - 맵을 표현할 때
        - R : key =&gt; value 또는 key: value
        - K : key to value
