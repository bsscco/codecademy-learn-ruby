# codecademy-learn-ruby

- 데이터 타입
    - number, boolean, string

- 변수
    - my_num = 25

- 수학 연산자
    - +, -, *, **, /, %

- 출력
    - print
    - puts # add new line

- 객체
    - 모든 것이 객체

- 주석
    - ```# comment```
    - =begin
        - comment

    - =end

- 네이밍 컨벤션
    - 모듈, 클래스 CamelCace
    - 변수, 메소드 snake_case
    - 상수 ALL_CAPS

- 입력
    - gets
    - gets.chomp

- 문자열 interpolation
    - "I took #{monkey} to the zoo"
    - ''로 감싸는 건 인식 못함.

- 메소드!
    - name = 'bsscco'.capitalize # name = 'bsscco'
    - name = 'bsscco'.capitalize! # name = 'Bsscco'

- 메소드?
    - boolean 반환

- 문자열 메소드
    - capitalize
    - upcase
    - downcase
    - chomp
    - gsub

- 흐름 제어 : 분기
    - if문
        - if n &gt; 0
            - puts  'positive' # 들여쓰기 안 해도 잘 돌아감.

        - elsif n &lt; 0
            - puts  'negative'

        - else
            - puts 'zero'

        - end

    - unless문
        - unless n &gt; 0
            - puts 'zero or negative'

        - end

    - if, unless문은 식(expression)이라서 값이 될 수 있다.
    - case문
        - case lang
            - when 'ko'
                - puts 'ko'

            - when 'en'
                - puts 'en'

            - else
                - puts 'error'

        - end

- 흐름 제어 : 반복
    - while문
        - i = 0
        - while i &lt; 10
            - print i
            - i += 1

        - end

    - until문
        - i = 0
        - until i &gt;= 10
            - puts i
            - i += 1

        - end

    - for문
        - for i in 1...10
            - puts i

        - end

    - loop 메소드
        - loop do 
            - print 'hh' 

        - end
        - do 키워드는 curly braces {}를 대체한다.
        - break if
        - next if

- 범위
    - 1...5 # 1,2,3,4
    - 1..5 # 1,2,3,4,5

- 배열
    - arr = [1,2,3,4,5]
    - arr.each do |x| 
        - puts x

    - end
    - arr.each {|x| puts x }
    - arr.push 1
    - arr &lt;&lt; 1
    - arr.map do |n| # collect 메소드와 완전히 같다.
        - n ** 2

    - end
    - arr.select do |n| 
        - n % 3 == 0

    - end

- 반복 정리
    - while, until
    - for, loop, times
    - arr.each, hash.each
    - 10.times do 
        - puts 'hh' 

    - end
    - 'A'.upto 'Z' do |c| puts c end
    - 10.downto 1 do |n| puts n end

- 해시
    - hash = Hash.new
    - hash = {}
    - hash = {1 =&gt; 1, '2' =&gt; 2} # =&gt;을 해시로켓이라 부름.
    - hash['n1'] = 1
    - hash.each do |k, v| puts "#{k}, #{v}" end
    - hash = Hash.new 'no value'
    - puts hash['no key'] # 'no value'
    - hash.delete 'key'
    - 루비1.9부터 심볼을 해시키로 사용할 땐 :sym =&gt; 1 형태에서 sym: 1 형태로 써도 된다.
    - filtered = hash.select do |v, k| k &gt; 3 end
    - hash.each_key do
    - hash.each_value do

- 메소드
    - def func
        - puts 'f'

    - end
    - def func greeting, *friends
        - friends.each do |friend|
            - puts greeting + ' ' + friend

        - end

    - end
    - def add a, b
        - a + b

    - end
    - 블록은 이름없는 메소드다.
        - 1.times { puts 'As am I' }

    - def func d = false # optional 파라메터

- 결합 비교 연산자
    - title1 &lt;=&gt; title2

- nil
    - nil은 false와 다르다.

- 심볼
    - 심볼은 string과 다르다.
    - "s".object_id == "s".object_id # false
    - :s == :s # true
    - 심볼을 해시 키로 쓰는 이유
        - 메모리 절약
        - 접근 속도가 빠르다.

- 형변환
    - 5.to_s
    - '1'.to_i
    - 's'.to_sym
    - 's'.intern
    - :sym.to_s
    - (1..10).to_a

- 단순한 if, unless
    - puts "it's true" if true
    - puts "it's false" unless false

- 삼항 연산자
    - true ? 'TRUE' : 'FALSE'

- 조건 할당 연산자
    - puts nil || 'str' # 'str'
        - v = nil 
        - v ||= 'str' # 'str
        - v = 'a'
        - v ||= 'str # a

    - puts nil && 'str' # ''
        - v = nil 
        - v &&= 'str' # nil
        - v = 'a'
        - v &&= 'str' # str

- 메소드 존재 확인
    - 4.respond_to? :next # true

- 연결 연산자
    - arr.push 1 # arr &lt;&lt; 1
    - 'a' &lt;&lt; 'b' # 'ab'

- 자료형 확인
    - 1.is_a? Integer

- yield
    - def func last
        - puts 'aaa'
        - yield 'bbb'
        - puts 'cccc'
        - puts last

    - end
    - func 'ddd' do |s| puts s end

- Proc
    - bl = Proc.new do |n| n % 3 == 0 end
    - print (1..10).to_a.select &bl
    - 블록을 Proc에 담는 이유
        - Proc은 블록과 달리 객체이기 때문에 객체의 기능을 100% 사용할 수 있다.
        - 블록과 달리 재사용 할 수 있다.

    - bl.call
    - 메소드 심볼을 Proc으로 만들기
        - strings.map &:to_i

- 람다
    - symbol_filter = lambda do |s| s.is_a? Symbol end
    - symbols = my_array.select &symbol_filter
    - Proc과 차의
        - Proc은 인자 수와 매개변수 수가 일치하는지 체크하지 않는다.
        - 람다는 인자 수와 매개변수 수가 일치하는지 체크한다.
        - Proc에서 return을 사용해 값을 반환하면 Proc을 호출한 메소드로 돌아가지 않고 바로 반환한다.
        - 람다는 호출이 끝나면 람다를 호출한 메소드로 돌아가서 다음 줄부터 실행된다.

- 클래스(OOP)
    - global = 'global' # 전역 변수
    - class Person
        - $global2 = 'global2' # 전역 변수를 클래스 안에서 선언할 때
        - @@people_count = 0 # 클래스 변수
        - def self.number_of_instances
            - @@people_count

        - end
        - def initialize name # 생성자
            - @name = name # 인스턴스 변수 초기화

        - end
        - def name
            - @name

        - end

    - end
    - puts Person.new('Bsscco').name
    - puts global
    - puts $global2

- 상속
    - class Creature
        - def initialize
        - end
        - def fight
            - puts 'Punch!'

        - end

    - end
    - class Dragon &lt; Creature # 상속
        - def fight # 메소드 오버라이드
            - super # 부모 클래스의 메소드를 사용

        - end

    - end
    - Dragon.new.fight

- 메소드 접근 제어
    - class Person
        - def initialize
        - end
        - def about_me
            - puts "it's me"

        - end
        - private
        - def bank_account
            - puts "123-456-78-9"

        - end

    - end

- 속성 접근자
    - class Person
        - attr_reader :name
        - attr_writer :age
        - attr_accessor :height
        - def initialize(name, age, height) 
            - @name = name
            - @age = age
            - @height = height

        - end

    - end
    - p =  Person.new('b', 12, 170)
    - puts p.name
    - p.age = 13
    - p.height = 180
    - puts p.height

- 모듈
    - module MyLibrary
        - FAVE_BOOK = 'hoho'

    - end
    - require ('my_library) # 다른 파일에서 모듈 불러오기
    - puts MyLibrary::FAVE_BOOK
    - module PrintableName
        - def print_name
            - puts @name 

        - end

    - end
    - class Person
        - include PrintableName # 인스턴스 레벨 믹스인
        - def initialize(name)
            - @name = name

        - end

    - end
    - Person.new('bsscco').print_name
    - module ThePresent
        - def now
            - Time.new

        - end

    - end
    - class TheHereAnd
        - extend ThePresent # 클래스 레벨 믹스인

    - end
    - TheHereAnd.now
