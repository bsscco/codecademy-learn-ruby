flutter

- DartPad
  "https://dartpad.dartlang.org"
- 모음
  "https://codelabs.developers.google.com/?cat=Flutter"
- 목차
  - 첫앱 만들어보기: 파트1
    "https://codelabs.developers.google.com/codelabs/first-flutter-app-pt1"
  - 첫앱 만들어보기: 파트2
    "https://codelabs.developers.google.com/codelabs/first-flutter-app-pt2"
  - Java에서 Dart로 넘어가기
    "https://codelabs.developers.google.com/codelabs/from-java-to-dart/index.html"
    - 생성자
      - ```dart
        // 다음 두 생성자는 완전히 같은 동작을 한다.
        Bicycle(this.cadence); // 이거 추천
        Bicycle(int cadence) {
          this.cadence = cadence;
        }
        ```
    - 변수 선언
      - ```dart
        var bike = bicycle(1, 2, 0); // 변수 생성
        final bike = bicycle(1, 2, 0); // 상수 생성
        ```
    - toString()
      - ```dart
        @override
        String toString() => 'Bicycle: $speed mph';
        ```
    - String
      - single qoutes, double qoutes 둘 다 사용 가능하다.
      - string interpolation을 지원한다. `{
  - 이펙티브 Dart
    "https://www.dartlang.org/guides/language/effective-dart"
