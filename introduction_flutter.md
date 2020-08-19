다트가 그동안 외면받아왔던 이유
-----------------------------
> 1) JS를 대체하기 위해서라면 TypeScript 등의 다른 언어를 사용할 수 있었음
> 2) Dart는 언어적 특성이 그렇게 세련되어 보이지 않았고 러닝 커브가 높았음
> 3) Dart 만으로 이루어진 구현체가 마땅히 없었음
> 4) 웹 브라우저에서 바로 Dart가 동작하는 것도 아니었기 때문에    굳이 Dart라는 언어를 배울 필요는 없었음

Flutter가 Dart를 선택하게 한 Dart의 주요 기능
-----------------------------
> 1) 두 가지 컴파일 방법 지원 (JIT + AOT)
> 2) 핫 리로드-> 빠른 개발 가능
> 3) 초당 60 프레임의 훌륭한 애니메이션
> 4) 선제적 스케줄링, 타임 슬라이싱 및 공유 리소스
> 5) Lock 없이 객체 할당 가비지 수집 가능
> 6) 선언적인 방식의 레이아웃
> 7) 두 가지 컴파일 방법 지원 (JIT + AOT)
>  > * JIT(Just-In-Time) 컴파일러는 프로그램 실행 중에 즉시 컴파일이 가능
      - 빠른 개발 주기로 개발이 가능
      - 실행 속도가 느려짐.(프로그램 실행이 시작될 때 코드를 실행하기 전에 분석 및 컴파일을 수행해야 하기 때문에)
>  > * AOT(Ahead-of-time) 컴파일러는 프로그램 작성 중(런타임 이전에) 컴파일을 실행
      - 개발 중에 AOT컴파일을 수행하면 개발 주기가 느려짐. (프로그램을 변경 후 실행하여 결과를 봐야 해서)
      - 런타임에 분석 및 컴파일을 위해 일시 ​​중지하지 않고, 보다 예측 가능하게 실행할 수 있는 프로그램을 만듬
      - 실행 속도가 더 빠름
>  >  > 개발 중에는 JIT 컴파일러를 사용하여 빠른 개발을 출시할 때는 AOT로 컴파일
>  >  > 개발중과 출시할때 다른 컴파일러 결과적으로 Dart는 매우 빠른 개발 주기와 빠른 실행 및 시작 시간이라는 두 가지 이점을 모두 제공

핫 리로드
Flutter의 가장 인기 있는 기능 중 하나 : Hot Reload
Flutter는 개발 중에는 JIT 컴파일러를 사용하여 일반적으로 1초 안에 코드를 다시 로드하고 계속 실행
앱 상태는 가능할 때마다 Reload를 통해 유지되므로 앱이 중단된 시점부터 계속할 수 있음

초당 60 프레임의 훌륭한 애니메이션
Fluter는 jank를 유발하는 일반적인 것들을 피함
* Jank
일반적인 모바일 앱은 GUI를 가지며 항상 사용자와 상호작용할 수 있어야 함
만약 어떠한 테스트를 처리에 16 밀리 세 컨트 이상 소요되어 GUI의 동작에 딜레이가 발생하거나 멈추는 현상이 발생한다면 
이러한 현상을 정크라고 하며 정크가 발생하면 사용자는 불편을 느낌

RN처럼 브릿지를 사용하지 않고 Flutter는 직접 프레임워크단에서 UI를 그리기 때문에 다른 크로스 플랫폼보다 빠름

선제적 스케줄링, 타임 슬라이싱 및 공유 리소스 Java, Kotlin, Objective-C, Swift 등 여러 개의 동시 실행 스레드를 지원하는 대부분의 프로그래밍 언어는
선점 기법을 사용하여 스레드 간에 전환

1) 각 스레드에는 실행시간이 "슬라이스"로 할당되고 할당된 시간을 초과하면 다른 스레드로 넘어감.
2) 그러나 메모리와 같은 스레드 간에 공유되는 리소스를 업데이트할 때 선점이 발생하면 경쟁조건이 발생
3) 경쟁 조건은 앱 충돌 및 데이터 손실을 포함한 심각한 버그를 유발 가능
   - 경쟁조건을 해결하는 일반적인 방법은 다른 스레드가 실행되지 않도록 Lock을 걸어 공유 리소스를 보호하는 것
4) 그러나 Lock은 더 심각한 교착상태, 기아상태를 유발할 수도 있음

Dart는 이 문제에서 다른 접근방식으로 접근
- isolates라고 하는 다트의 스레드는 메모리를 공유하지 않으므로 Lock이 필요하지 않음
- isolate는 채널을 통해 메시지를 전달하여 통신. (Erlang의 행위자, JavaScript의 웹 작업자와 유사)

Dart는 기본적으로 단일 스레드에서 작동하므로 선점을 허용하지 않음 (대신 스레드는 명시적으로 산출 (async /await , Futures or Stream 사용)

Lock 없이 객체 할당 가비지 수집 가능
가비지 컬렉션은 공유 리소스(메모리)에 액세스 하는 특별한 경우이며 , 많은 언어에서 수행기간 동안 잠금을 사용해야 함
잠금 되어 사용 가능한 메모리가 수집되는 동안 전체 앱 실행이 중지될 수도 있음

Dart는 항상 가비지 컬렉션을 잠금 없이 수행할 수 있음

Dart는 generational garbage collection and allocation scheme을 사용
이 기법은 특히 수명이 짧은 많은 객체들을 할당하는데 빠릅니다.
(모든 프레임에 대해 불변의 뷰 트리를 재구성하는 Flutter와 같은 반응적인 사용자 UI에 적합)

선언적인 방식의 레이아웃
Flutter는 명령적인 방식이 아닌 선언적인 방식으로 UI를 작성
Flutter는 JSX나 XML 같은 추가 템플릿 또는 레이아웃과 언어 간에 레이아웃을 분할하지 않으며 별도의 시각적인 레이아웃 도구가 필요하지 않다는 것

♦ 명령형 프로그래밍(imperative programming)은 언어 해석이 순차적이며 어떠한 방법으로 문제를 해결할지 가 주요 관심
♦ 선언형 프로그래밍(declarative)은 순서나 문제 해결 과정을 다루기보다 무엇을 나타내야 할지에 초점

Flutter는 선언형 프로그래밍 방식을 사용하여 위젯을 변경해야 하는 상황이 생길 때 기존의 것을 변경하는 것이 아니라 지우고 새로 다시 만듬

선언형 프로그래밍 방식의 장점
 - 가독성
-  재사용성
- 오류 복구: 특정 부분만 오류 체크할 수 있음
- 참조 투명성: 다른 시스템에 영향을 주지 않음
- 대체 가능성

"The first “mobile apps” to be built cross platform are simply WebViews that run on WebKit (a browser rendering engine). These are literally just embedded web pages. The problem with this is basically that manipulating the DOM is very expensive and doesn’t perform well enough to make a great mobile experience.

Some platforms have solved this problem by building the “JavaScript bridge.” This bridge lets JavaScript talk directly to native widgets.

This is much more performant than WebViews, because you eliminate the DOM from the equation, but it’s still not ideal. Every time your app needs to talk directly to the rendering engine, it has to be compiled to native code to “cross the bridge.” On a single interaction, the bridge must be crossed twice: once from platform to app, and then back from app to platform"

* https://skia.org/
 - lutter는 Chrome에서 사용되는 것과 동일한 렌더링 엔진 인 자체 렌더링 엔진 인 Skia를 사용
 - Skia는 Flutter 앱과 통신
 - Flutter는 먼저 JavaScript로 컴파일하지 않고 로컬 이벤트를 직접 받음 (Flutter가 네이티브 ARM 코드로 컴파일 되기 때문)



-Reference
1) https://medium.com/airbnb-engineering/sunsetting-react-native-1868ba28e30a
2) https://skia.org/
3) https://css-tricks.com/flutter-googles-take-on-cross-platform/#flutter-vs-react-native-and-other-options
4) http://murmurblog.com/layouts-in-flutter/
5) https://beomseok95.tistory.com/315
