- 메인
    - fun main(args: Array&lt;String&gt;) {
        - println("Hello")

    - }

- 함수
    - fun max(a: Int, b: Int): Int {
        - return if (a &gt; b) a else b # 루비랑 다르게 return이 필요

    - }

- 문자열 템플릿
    - println("Hello ${name}")
    - println("Hello ${if (args.size &gt; 0) args[0] else "someone"}")

- 주 생성자
    - class Person(val name: String, var isMarried: Boolean)
    - val p = Person("bsscco", true)
    - println(p.name + " " + p.isMarried)

- 커스텀 접근자
    - class Rectangle(val height: Int, val width: Int) {
        - val isSquare: Boolean # set, get, is 메소드는 인스턴스 변수를 활용한다.
            - get() = height == width

    - }
    - println(Rectangle(2, 2).isSquare)

- 임포트
    - import geometry.shapes.createRandomRectangle
    - val rect = careteRandomRectangle()

- 열거형
    - enum class Color {
        - RED, GREEN, BLUE

    - }
    - enum class Color2(val r: Int, val g: Int, val b: Int) {
        - RED(255, 0, 0),
        - GREEN(0, 255, 0),
        - BLUE(0, 0, 255);
        - fun rgb() = (r * 256 + g) * 256 + b

    - }
    - println(Color2.RED.rgb())
    - println(when(Color.GREEN) {
        - Color.RED, Color.GREEN, Color.BLUE -&gt; "origin color"
        - else -&gt; "else"

    - })
    - println(when(setOf(Color.YELLOW, Color.BLUE)) {
        - setOf(Color.YELLOW, Color.BLUE) -&gt; Color.GREEN
        - else -&gt; throw Exception("Dirty Color")

    - }) // 최적화 하려면 setOf 대신에 &&, || 를 사용하면 된다.

- 스마트 캐스트
    - interface Expr
    - class Num(val value: Int) : Expr
    - class Sum(val left: Expr, val right: Expr) : Expr
    - fun eval(e: Expr): Int = when (e) {
        - is Num -&gt; e.value
        - is Sum -&gt; eval(e.left) + eval(e.right)
        - else -&gt; throw IllegalArgumentException()

    - }
    - fun main(args: Array&lt;String&gt;) {
        - println(eval(Sum(Num(3), Sum(Num(1), Num(2)))))

    - }

- 반복
    - for (i in 100 downTo 1 step 10) {
        - println(i)

    - }

- 파괴적 선언
    - val binaryReps = HashMap&lt;Char, String&gt;()
    - for (c in 'A'..'F') {
        - binaryReps[c] = Integer.toBinaryString(c.toInt())

    - }
    - for ((letter, binary) in binaryReps) {
        - println("${letter} : ${binary}")

    - }

- 포함 확인
    - println(1 in 1..10)

- 예외 처리
    - val n = try {
        - Integer.parseInt("-")

    - } catch (e: NumberFormatException) {
        - return

    - } finally {
        - println("finally")

    - }
    - println(n)

- 콜렉션
    - 선언
        - val set = setOf(1, 2, 3)
        - val list = listOf(1, 2, 3)
        - val map = mapOf(1 to 1, 2 to 2)
        - println(set)
        - println(list)
        - println(map)

    - 메소드
        - val list = listOf(3, 2, 1)
        - println(list.max())
        - println(list.last())

- 확장 함수
    - fun &lt;T&gt; Collection&lt;T&gt;.joinToString(sep: String = ","): String {
        - val result = StringBuilder()
        - for ((idx, el) in this.withIndex()) {
            - if (idx &gt; 0) result.append(sep)
            - result.append(el)

        - }
        - return result.toString()

    - }
    - fun main(args: Array&lt;String&gt;) {
        - println(listOf(1, 2, 3).joinToString(sep = "-"))

    - }

- 클래스 상속
    - open class View {
        - open fun click() {
            - println("view")

        - }

    - }
    - class Button : View() {
        - final override fun click() { // final override는 자식부터 메소드 오버라이딩을 할 수 없게 막는다.
            - println("button")

        - }

    - }
    - 확장 함수는 상속 불가

- 확장 속성
    - val String.lastChar: Char
        - get() = this.get(this.length - 1)

    - fun main(args: Array&lt;String&gt;) {
        - println("abcd".lastChar)

    - }

- 가변 인자
    - fun main(args Array&lt;String&gt;) {
        - println(listOf(*args)) // 스프레드 연산자

    - }

- 문자열 스플릿
    - println("ab.cd-ef".split("\\.|-".toRegex()))
    - println("ab.cd-ef".split(".", "-"))

- 문자열 확장함수
    - "abc/def".substringBeforeLast("/")
    - "abc/def".substringAfterLast("/")

- 트리플 쿼츠 문자열
    - 더 쉽게 쓰는 정규표현식
        - println("(.+)/(.+)\\.(.+)".toRegex().matches("a/b/c/d/e.f"))
        - println("""(.+)/(.+)\.(.+)""".toRegex().matches("a/b/c/d/e.f"))

    - 멀티라인
        - val kotlinLogo = """| //
            -                       .|//
            -                       .|/ \"""

        - fun main(args: Array&lt;String&gt;) {
            - println(kotlinLogo.trimMargin("."))

        - }

- 로컬 함수
- 인터페이스
    - interface Clickable {
        - fun click()
        - fun showOff() = println("Clicikable")

    - }
    - interface Focusable {
        - fun focus()
        - fun showOff() = println("Focusable")

    - }
    - class Button : Clickable, Focusable { // 클래스 상속과 다르게 ()을 안 붙임.
        - final override fun click() = println("I was clicked")
        - override fun focus() = println("I was focused")
        - override fun showOff() {
            - super&lt;Clickable&gt;.showOff()
            - super&lt;Focusable&gt;.showOff()

        - }

    - }

- 추상 클래스
    - abstract class Animated {
        - abstract fun animate()

    - }

- 중첩 클래스
    - class Button {
        - class ButtonState { ... }

    - }

- 내부 클래스
    - class Outer {
        - inner class Inner {
            - fun getOuter(): Outer = this@Outer

        - }

    - }

- sealed 클래스
    - 같은 파일 안에서만 상속 가능한 클래스

- 속성 상속
    - interface User {
        - val nickname: String // 인터페이스에선 상수형만 선언할 수 있다.

    - }
    - class PrivateUser(override val nickname: String) : User
    - class SubscribingUser(val email: String) : User {
        - override val nickname: String
            - get() = email.substringBefore('@')

    - }
    - fun main(args: Array&lt;String&gt;) {
        - println(PrivateUser("test@kotlinlang.org").nickname) // test@kotlinlang.org
        - println(SubscribingUser("test@kotlinlang.org").nickname) // test

    - }

- 속성 접근
    - class User(val name: String) {
        - var address: String = "unspecified"
            - set(value: String) {
                - field = value // 백킹 필드를 수정

            - }
            - // private set 이렇게 하면 세터에 접근할 수 없음.

    - }

- 객체 비교
    - class Client(val name: String, val postalCode: Int) {
        - override fun equals(other: Any?): Boolean {
            - if (other == null || other !is Client) return false
            - return name == other.name && postalCode == other.postalCode

        - }

    - }
    - fun main(args: Array&lt;String&gt;) {
        - println(Client("Alice", 342562) == Client("Alice", 342562))

    - }

- 데이터 클래스
    - data class Client(val name: String, val postalCode: Int) {
    - }
    - fun main(args: Array&lt;String&gt;) {
        - // toString, equals, copy 메소드를 자동으로 구현해줌.
        - println(Client("Alice", 342562) == Client("Alice", 342562))
        - println(Client("Alice", 12345))
        - println(Client("Alice", 12345).copy(postalCode = 382555))

    - }

- 객체 위임
    - class CustomList&lt;T&gt;(val innerList: MutableCollection&lt;T&gt; = ArrayList&lt;T&gt;()) : MutableCollection&lt;T&gt; by innerList
    - fun main(args: Array&lt;String&gt;) {
        - val cList = CustomList&lt;Int&gt;()
        - cList.addAll(listOf(1, 2, 3))
        - println("${cList.size}")

    - } // innerList의 메소드를 CustomList 객체의 것인 양 사용하고 있다.

- 싱글톤 클래스
    - object CaseInsensitiveFileComparator : Comparator&lt;File&gt; {
        - override fun compare(file1: File, file2: File): Int {
            - return file1.path.compareTo(file2.path, ignoreCase = true)

        - }

    - }
    - fun main(args: Array&lt;String&gt;) {
        - println(CaseInsensitiveFileComparator.compare(File("/User"), File("/user")))
        - val files = listOf(File("/Z"), File("/a"))
        - println(files.sortedWith(CaseInsensitiveFileComparator))

    - }

- 전역 메소드
    - class A {
        - companion object {
            - fun bar() = println("Companion object called")

        - }

    - }
    - fun main(args: Array&lt;String&gt;) {
        - A.bar()

    - }

- 람다
    - { println(42) }() // 블록은 람다다.
    - { println(42) }.invoke()
    - run { println(42) }

- 람다로 객체 접근
    - fun printProblemCounts(responses: Collection&lt;String&gt;) {
        - var clientErrors = 0
        - var serverErrors = 0 // 변수에 접근하고 변수를 수정할 수 있다.
        - responses.forEach {
            - if (it.startsWith("4")) {
                - clientErrors++

            - } else if (it.startsWith("5")) {
                - serverErrors++

            - }

        - }
        - println("$clientErrors client errors, $serverErrors server errors")

    - }
    - fun main(args: Array&lt;String&gt;) {
        - val responses = listOf("200 OK", "418 I'm a teapot", "500 Internal Server Error")
        - printProblemCounts(responses)

    - }
    - 외부 함수의 콜이 끝난 다음에 내부 람다가 외부 함수의 변수에 접근하는 것은 캡처가 되지 않았기 때문에 불가능하다.

- 함수를 변수로 쓰기
    - fun salute() = println("Salute!")
    - fun main(args: Array&lt;String&gt;) {
        - run(::salute)

    - }

- 생성자를 변수로 쓰기
    - data class Person(val name: String, val age: Int)
    - fun main(args: Array&lt;String&gt;) {
        - val createPerson = ::Person
        - val p = createPerson("Alice", 29)
        - println(p)

    - }

- 콜렉션 필터와 맵
    - listOf(1,2,3).filter { it % 2 == 0 }
    - listOf(1,2,3).map { it * it }
    - mapOf(1 to 1, 2 to 2).mapValues { it * it }
    - listOf(1,2,3).all { it &lt; 2 } // false
    - listOf(1,2,3).any { it &lt; 2 } // true
    - listOf(1,2,3).find { it &lt; 2 } // 1
    - listOf(1,2,3).groupBy { it &lt;= 2 } // (true=[1,2], false=[3])  
    - listOf("ab","cd").flatMap { it.toList() } // ["a", "b", "c", "d"]

- 콜렉션 지연 계산
    - listOf(1, 2, 3, 4).asSequence()
        - .map { print("map($it) "); it * it }
        - .filter { print("filter($it) "); it % 2 == 0 }
        - .toList() // 이 때 연산 시작

- 시퀀스 만들기
    - fun main(args: Array&lt;String&gt;) {
        - val naturalNumbers = generateSequence(0) { it + 1 }
        - val numbersTo100 = naturalNumbers.takeWhile { it &lt;= 100 }
        - println(numbersTo100.sum())

    - }
    - fun File.isInsideHiddenDirectory() = generateSequence(this) { it.parentFile }.any { it.isHidden }
    - fun main(args: Array&lt;String&gt;) {
        - val file = File("/Users/svtk/.HiddenDir/a.txt")
        - println(file.isInsideHiddenDirectory())

    - }

- with와 apply
    - fun alphabet() = with(StringBuilder()) {
        - for (letter in 'A'..'Z') {
            - append(letter)

        - }
        - append("\nNow I know the alphabet!")
        - toString()

    - }
    - fun alphabet() = StringBuilder().apply {
        - for (letter in 'A'..'Z') {
            - append(letter)

        - }
        - append("\nNow I know the alphabet!")

    - }.toString()
    - fun main(args: Array&lt;String&gt;) {
        - println(alphabet())

    - }
    - StringBuilder().apply {...}의 경우 간편한 buildString {...}를 제공해줌.
