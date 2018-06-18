- 자바에서 루비로(https://www.ruby-lang.org/ko/documentation/ruby-from-other-languages/to-ruby-from-java/)
- 대화형 셸
    - $ irb

- 모듈 사용
    - Math::PI # 3.141592653589793
    - Math::sqrt 4 # 2.0

- 메소드 정의, 사용
    - def hello(name = "anonymous")
        - puts 'Hello' + name + '!'

    - end
    - hello 'bsscco'

- 문자열 템플릿
    - puts "Hello #{name.capitalize}"

- 클래스 정의, 사용
    - class Person
        - def initialize(name)
            - @name = name

        - end
        - def hello
            - puts "Hello #{@name}!"

        - end

    - end
    - Person.new('bsscco').hello

- 객체 정보 보기
    - Person.instance_methods
    - Person.instance_methods false # 상속된 메소드는 제외
    - Person.new('bsscco').respond_to? :hello # 어떤 메소드에 응답하는지 확인

- 런타임에서 클래스 수정하기
    - class Person
        - def initialize(name)
            - @name = name

        - end
        - def hello
            - puts "Hello #{@name}!"

        - end

    - end
    - class Person
        - attr_accessor :name

    - end
    - Person.new('bsscco').hello
    - puts Person.new('bsscco').name

- 프로그램 실행
    - file.rb
        - if __FILE__ == $0 # 현재 파일이 메인파일로 실행된 것이라면
            - ```# 실행 코드```

        - end

    - $ ruby file.rb
