안드로이드 MVP 아키텍쳐

- https://en.wikipedia.org/wiki/Business_logic
    - business logic 또는 domain logic은 data가 어떻게 created, stored, changed 되는지를 결정하는 규칙을 프로그램으로 코딩한 부분이다. 이 logic은 low-level에서 db와 매핑 또는 UI 디스플레잉과 연관된다.

- https://en.wikipedia.org/wiki/Presentation_logic
    - presentation logic은 비지니스 객체들을 UI로 어떻게 보여줄지와 연관돼있다. presentation logic으로부터 business logic을 분리하는 것은 SW개발에서 중요한 관심사다.

- https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller
    - MVC는 UI 개발을 위해 흔히 사용되는 설계 패턴이다. 이 패턴은 어플리케이션을 서로 연결돼서 통신하는 세 부분으로 나눈다. 이 패턴은 사용자 이벤트를 받아 처리하는 과정에서 정보를 표현하는 부분을 분리시킨다. MVC 디자인 패턴은 이런 주요 컴포넌트들을 코드재사용과 평행개발(파트별 다른 개발자가 동시개발)에서 효과적으로 디커플링 시킨다. 
    - 설명
        - 컴포넌트
            - model은 패턴의 중심 컨포넌트다. 이것은 어플리케이션의 동적 데이터 구조이며, UI로부터 독립적이다. 이것은 직접 어플리케이션의 data와 logic을 다룬다.
            - view는 정보를 차트나 다이어그램과 같은 UI로 표현한다. 
            - controller는 사용자 이벤트를 받아 model 또는 view를 제어한다.

- https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93presenter
    - MVP는 MVC의 파생 패턴이다. MVP에서 presenter는 미들맨의 기능을 수행한다. 모든 프레젠테이션 로직은 presenter로 옮겨진다.
    - 개요
        - MVP는 자동화된 unit test를 쉽게 하기 위해, 프리젠테이션 로직에서 관심사의 분리를 향상시키기 위해 연구된 UI 아키텍쳐 패턴이다.   
첨언: 비지니스 로직에서 관심사의 분리를 향상시키기 위함은 아니구나.
        - model은 UI에 보여질 데이터를 정의한 인터페이스다.
        - view는 model의 데이터를 수동적으로 보여주는 인터페이스다. view는 유저 이벤트를 감지해 관련 데이터와 함께 presenter로 보낸다.
        - presenter는 model과 view 위에서 동작한다. repository(model)에서 데이터를 찾고, 데이터가 view에서 보여질 수 있도록 데이터를 가공한다.
        - 일반적으로 view 구현체는 presenter 객체를 생성해서 객체의 참조를 가지고 있는다. 아래 C#코드는 간단한 view 생성자를 설명한다.
        - ```
        - public class DomainView : IDomainView
        - {
            - private IDomainPresenter domainPresenter = null;
            - ///&lt;summary&gt;Constructor&lt;/summary&gt;
            - public DomainView()
            - {
                - domainPresenter = new ConcreteDomainPresenter(this);

            - }

        - }
        - ```
        - 내 정리
            - model엔 데이터가 들어있고, 데이터를 조회하고 갱신하는 로직이 들어있다.
            - view는 데이터를 받아서 그리거나 유저 이벤트를 presenter로 넘기는 수동적인 역할을 한다.
            - presenter는 model과 view을 다루는 미들맨 역할을 한다.
            - view는 presenter를 알고(known), presenter는 view와 model을 안다.

        - 뷰에서 허용되는 로직의 정도는 구현마다 다르다. 극단적인 예로, view가 모든 유저 이벤트를 presenter로 보내는 것과 같이 완전히 수동적일 수 있다. 이런 구현에선 유저가 view의 이벤트 메소드를 발생시켰을 때 view는 아무것도 하지 않고 파라메터도 없고 반환값도 없는 presenter의 메소드를 호출한다. presenter는 view에서 view 인터페이스에 정의된 메소드를 통해 데이터를 찾는다. 마지막으로 presenter는 model 위에서 명령을 수행하고, 수행의 결과를 view에 갱신한다. 다른 구현 버전에서는 view가 유저 이벤트를 약간은 다룰 수 있도록 허용하기도 한다. 이런 구현은 view가 있는 클라이언트 브라우저에서 실행되는 web-based 아키텍쳐에 적합하다. view는 유저 이벤트들 중 일부를 다루기 위한 최선의 장소가 될 수 있다.  
첨언: 앱 아키텍쳐에서는 view가 극단적으로 수동적이어도 된다는 말이군.

- https://github.com/googlesamples/android-architecture/tree/todo-mvp
    - view를 부를 때 주의
        - "Android View"는 android.view.View 클래스를 뜻한다.
        - MVP의 presenter로부터 명령을 받는 View를 "view"라고 부른다.

    - 각 화면은 아래와 같은 클래스들과 인터페이스들로 구성된다.  
첨언: MVP 구현체 묶음이 화면 단위로 구분된다는 걸 알 수 있다.
        - Activity는 fragment들과 presenter들을 만든다.
        - Fragment는 contract.view 인터페이스를 구현한다.  
첨언: view 인터페이스의 구현이 유저 액션을 presenter로 넘기는 로직의 구현일까?
        - presenter는 contract.presenter 인테페이스를 구현한다.  
첨언: persenter 인터페이스 구현은 유저 액션을 실제로 처리하는 비지니스 로직의 구현이겠지?
        - contract 클래스는 view와 presenter 사이의 연결을 정의한다.
        - presenter는 일반적으로 비지니스 로직의 주인이 된다. (비지니스 로직이 있는 model을 제어하기 때문) presenter와 대응되는 view는 Android UI 작업을 다룬다. view는 비지니스 로직을 포함하지 않는다. view는 presenter의 명령을 UI 액션으로 전환시키고, 유저의 액션을 리스닝해서 presenter로 넘긴다.
        - 내 정리
            - Activity는 화면의 컨테이너 역할, Fragment는 view 역할, presenter는 미들맨 역할, Fragment와 presenter는 contract 인터페이스로 통신한다.
            - Activity는 Fragment(view)와 presenter를 알고, Fragment는 contract.presenter를 알고, presenter도 contract.view를 안다.

    - 공통의 구현 질문을 풀기 위해 따른 접근법들
        - asynchronousd task들을 다루기 위해 callbacks를 사용한다.
        - data는 Room을 통해 로컬의 SQLite DB에 저장된다.

    - 프래그먼트들을 사용하는 두 가지 이유
        - Activity와 Fragment를 둘 다 사용하는 것은 MVP에서 관심사의 분리를 돕는다. Activity는 Fragment(view)들과 presenter들을 만들고 연결하는 등 컨트롤러의 역할을 아우른다.
        - Fragment의 사용은 multiple views로 구성되는 태블릿 레이아웃 또는 UI 화면들을 지원할 수 있게 해준다.

    - 유닛테스트
        - presenter들, respository들, data source들에 이르기까지 unit test들을 포함한다. unit test는 fake data에 의존하며, fake module들을 제공하기 위해 DI를 사용한다. 

    - 패키지 구조
        - src/main/java/com.example.andoid.architecture.blueprints.todoapp
            - tasks
                - TasksActivity
                    - TasksFragment를 생성하고 추가한다.
                    - TasksPresenter를 생성하고 참조를 가지고 있는다. 이때 생성자의 파라메터로 TasksRepository 객체와 TasksFragment의 객체를 넣는다.

                - TasksFragment
                    - TasksContract.View 인터페이스를 구현한다.
                    - TasksPresenter 객체의 참조를 가지고 있는다.
                    - onResume에서 TasksPresenter 객체를 시작시킨다.
                    - 모든 유저 액션에 대응하는 TasksPresenter 객체의 메소드를 호출한다.

                - TasksPresenter
                    - 생성될 때 파라메터로 넘어온 TasksFragment에게 자신의 참조를 넘긴다.
                    - TasksContract.Presenter 인터페이스를 구현한다.
                    - TasksRepository 객체의 참조를 가지고 있는다.
                    - Contract.View 구현체의 참조를 가지고 있는다.

                - TasksContract
                - TasksFileType

            - taskdetail
            - addedittask
            - statistics
            - util

    - MVC vs Todo MVP vs 오집 MVC 
        - MVC
            - M : 비지니스 로직이 있다.
            - V : 프리젠테이션 로직이 있다.
            - P : M과 V를 제어하는 로직이 있다.

        - Todo MVP
            - M : Repository - 데이터 저장소이며 비지니스 로직이 있다.
            - V : Fragment - 프리젠테이션 로직이 있다.
            - P : Presenter - M과 V를 제어하는 로직이 있다.
            - Contract : V와 P의 통신 연결고리가 된다.

        - 오집 MVC
            - M : Data - 데이터 자제, 비지니스 로직은 없음.
            - V : Android custom Views - 프리젠테이션 로직이 있다.
            - C : RecyclerViewAdapter - M과 비지니스 로직, V를 제어하는 로직이 있다.
            - Util : 대부분의 비지니스 로직이 있다.

        - Todo MVP의 Repository 패턴이 오집 MVC의 Util이 비슷한 역할을 하고 있다. 오집 MVC는 view 영역을 컴포넌트화해서 코드재사용성을 높였다. Todo MVP가 화면당 하나의 Contract 인터페이스를 통해 Fragment(view)와 Presenter(미들맨)를 통신시키기 때문에 다른 사람이 읽기 쉽게 만들고, 관심사의 분리를 가져온다. 오집 MVC는 RecyclerViewAdapter(controller)가 Android custom Views(view)를 중간층 없이 다이렉트로 다루기 때문에 결합도가 높아지고, 다른 사람이 읽기도 어렵다.
        - 오집 MVC에 Repository 패턴을 적용해 M과 C 사이에 중간층을 만들어주고, Todo MVP처럼 Contract(V와 P 사이의 중간층)를 사용하는 MVP로 서서히 넘어간다면 다른 사람이 읽기 쉬워지고, 관심사의 분리도 성취할 수 있을 것이다.

- https://github.com/googlesamples/android-architecture/tree/todo-mvp-clean
    - Android 클린 아키텍쳐는 MVP에 데이터 layer를 더한 아키텍쳐다. MVP의 데이터 레이어에서는 repository 패턴도 함께 사용됐다.
    - domain layer는 재사용성을 높여주는데, presenter들 사이에서 반복되는 코드가 domain layer의 use case로 작성되기 때문이다.  
첨언: todo-mvp-clean 아키텍쳐 패턴에서는 비지니스 로직의 관심사 분리 향상에 초점이 맞춰져있구나.
    - 또 use case들은 클래스명 자체가 목적을 명시하기 때문에 가독성도 높여준다.
    - domain layer는 presentation layer와 data layer 사이의 층이기 때문에 안드로이드 sdk와 서드파티 사이를 디커플링하게 만들어준다.
    - use case는 ui 블로킹을 피하기 위해 스레드풀의 백그라운드 스레드에서 실행시킨다. 이를 위해 command 패턴을 사용한다. 스레드풀을 사용하기 위해 RxJava나 Promise를 사용할 수도 있다.
    - 레포지토리 또한 비동기로 사용하는데 use case가 백그라운드에서 실행되기 때문에 특별한 처리를 해줄 필요는 없다.
    - view layer, API layer, domain layer에서 각각 다른 model을 사용할 것을 추천한다. 하지만 이 예제에선 모든 model이 immutable이기 때문에 다르게 사용하지 않는다. 만약 view에서 쓰이는 model이 안드로이드와 연관된 필드를 가지고 있다면 view를 위한 model과 domain을 위한 model을 나눌 것이다. 두 모델 사이의 전환은 mapper class릉 사용해서 할 것이다.
    - 모든 domain 코드는 unit test로 테스트 된다. 이것은 use case부터 view와 repository 영역까지 통합 테스트로 확장될 수 있다.
    - 패키지 구조
        - src/main/java/com.example.andoid.architecture.blueprints.todoapp
            - tasks
                - TasksActivity
                    - TasksFragment를 생성하고 추가한다.
                    - TasksPresenter를 생성하고 참조를 가지고 있는다. 이때 생성자의 파라메터로 use case 객체들과 TasksFragment의 객체를 넣는다.

                - TasksFragment
                    - TasksContract.View 인터페이스를 구현한다.
                    - TasksPresenter 객체의 참조를 가지고 있는다.
                    - onResume에서 TasksPresenter 객체를 시작시킨다.
                    - 모든 유저 액션에 대응하는 TasksPresenter 객체의 메소드를 호출한다.

                - TasksPresenter
                    - 생성될 때 파라메터로 넘어온 TasksFragment에게 자신의 참조를 넘긴다.
                    - TasksContract.Presenter 인터페이스를 구현한다.
                    - TasksRepository 객체의 참조를 가지고 있는다.
                    - Contract.View 구현체의 참조를 가지고 있는다.

                - TasksContract
                - TasksFileType

            - taskdetail
            - addedittask
            - statistics
            - util

    - Todo MVP Clean vs 오집 MVC 
        - Todo MVP Clean
            - M : Repository - 데이터 저장소이며 비지니스 로직이 있다.
            - V : Fragment - 프리젠테이션 로직이 있다.
            - P : Presenter - M과 V를 제어하는 로직이 있다.
            - Contract : V와 P의 통신 연결고리가 된다.
            - Domain layer : presenter의 제어 로직을 use case로 관리한다.

        - 오집 MVC
            - M : Data - 데이터 자제, 비지니스 로직은 없음.
            - V : Android custom Views - 프리젠테이션 로직이 있다.
            - C : RecyclerViewAdapter - M과 비지니스 로직, V를 제어하는 로직이 있다.
            - Util : 대부분의 비지니스 로직이 있다.

        - 오집 MVC에 Repository 패턴을 적용해 M과 C 사이에 중간층을 만들어주고, Todo MVP처럼 Contract(V와 P 사이의 중간층)를 사용하는 MVP로 서서히 넘어간다면 다른 사람이 읽기 쉬워지고, 관심사의 분리도 성취할 수 있을 것이다. 여기에 Domain layer를 추가한다면 presenter 제어로직의 가독성과 코드재사용성을 높일 수 있을 것이다.  

- https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html
    - 관심사의 분리에 초점이 맞춰져있다. layer를 통해 분리를 성취한다.
    - 클린 아키텍쳐는 프레임워크에 독립적이다. 이것은 프레임워크를 도구로써 제약조건 없이 사용할 수 있게 해준다.
    - 클린 아키텍쳐는 테스트 가능하다. 비지니스 로직은 UI, DB, Web 서버와 같은 어떠한 외부 요소에도 의존하지 않고 테스트 가능해야 한다.
    - 클린 아키텍쳐는 UI에 독립적이다. UI는 비지니스 로직의 수정 없이 쉽게 바뀔 수 있어야 한다.
    - 클린 아키텍쳐는 DB에 독립적이다. 비지니스 로직은 DBMS에 의존하지 않고 수정될 수 있어야 한다.
    - 클린 아키텍쳐는 외부 어떤 환경에도 의존하지 않는다. 비지니스 로직은 바깥 세계에 대해서 어떤 것도 알 수 없어야 한다.
    - 의존성 규칙
        - 소스코드의 의존성은 오직 안쪽으로만 향해야 한다. 어떤 안쪽 서클도 바깥쪽 서클을 알 수 없어야 한다. 바깥 서클에서 선언된 어떤 것도 안쪽 서클에서 언급되어서는 안 된다. 
        - 엔티티
            - 엔티티는 엔터프라이즈의 넓은 비지니스 로직을 캡슐화한다. 엔티티는 메소드를 포함한 객체가 될 수 있고 데이터 구조들이나 함수들의 묶음이 될 수도 있다. 이는 많은 다른 엔터프라이즈 어플리케이션의 엔티티들과 다르지 읺다.
            - 만약 앤터프라이즈가 아닌 단일 어플리케이션을 작성했다면 엔티티들은 어플리케이션의 비지니스 객체들일 것이다. 그들은 대부분의 로직을 캡슐화 한다. 그들은 외부의 어떤 것이 변경됐을 때 최소한의 변경점이다. 예를 들어, 당신은 내비게이션 페이지 또는 보안상의 변경에 의해 엔티티들이 영향을 받지 않기를 기대할 것이다.
