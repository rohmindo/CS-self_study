# Android
# Table Of Contents :

   + ### [1. Android 4대 구성요소](#1-android-4대-구성요소)
   + ### [2. Intent](#2-intent란)
   + ### [3. Activity Lifecycle](#3-activity-life-cycle)
   + ### [4. Design Pattern](#4-디자인패턴)
   + ### [5. RecyclerView](#4-Recycler-View)
   + ### [6. Jetpack](#6-Jetpack-Library)
## 1. Android 4대 구성요소
  + ### Activity :
    + 액티비티는 사용자가 애플리케이션과 상호작용하는 단일화면을 의미하며 모든 안드로이드 애플리케이션은 액티비티로 구성되어 있습니다.
    + **사용자와 상호작용**을 담당하는 인터페이스라고 할 수 있습니다.
    + 안드로이드 애플리케이션은 반드시 하나 이상의 액티비티를 포함하고 있으며 액티비티는 생명주기(Life Cycle) 관련 메서드들을 재정의하여 원하는 기능들을 구현할 수 있습니다.
  + ### Service :
    + 서비스는 사용자와 직접적으로 상호작용하는 요소는 아닙니다 .백그라운드(Background)에서 어떠한 작업을 처리하기 위해 서비스를 사용.
    + 예를 들면 애플리케이션을 사용하면서 유튜브 또는 멜론, 지니 등등 음원 스트리밍 앱을 사용한다던지 다른 작업을 하면서 파일을 다운로드할 때 서비스를 주로 사용합니다.
    + 서비스는 엄연히 **메인 스레드**에서 동작하기 때문에 서비스 내에서 별도의 스레드를 생성하여 작업을 처리해야 합니다(UI에 방해받지 않고 백그라운드에서 동작한다고 해서 별도의 스레드에서 동작하는것이 아님).
  + ### Broadcast Receiver :
    + 방송 수신자(BroadCase Receiver)는 안드로이드 OS로부터 발생하는 각종 이벤트와 정보를 받아와 핸들링하는 컴포넌트입니다.
    + 사용자 안드로이드 디바이스의 시스템 부팅시 앱 초기화, 네트워크 끊김 등등 특수한 이벤트에 대한 처리나 배터리 부족 알림 ,문자 수신과 같은 정보를 받아 처리를 해야 할 필요가 있을 때 동작합니다.
    + 안드로이드 OS에서 메신저앱 또는 문자 메시지가 오면 모든 앱에 "메시지가 왔다"라는 하나의 정보를 방송(BroadCast)을 합니다. 이 메시지를 받기 위해 브로드캐스트 리시버를 구현하면 되며 해당 정보가 오면 특정 이벤트를 처리할 수가 있습니다 
  + ### Content provider :
    + 콘텐트 제공자(Content Provider)는 데이터를 관리하고 다른 애플리케이션의 데이터를 제공하는 데 사용되는 컴포넌트입니다.
    + 특정한 애플리케이션이 사용하고 있는 데이터베이스(DB)를 공유하기 위해 사용하며 애플리케이션 간의 데이터 공유를 위해 표준화된 인터페이스를 제공합니다.
## 2. Intent란
  + ### Intent 란?
    + Component를 실행하기 위해 시스템에 넘기는 정보이다.
    + 인텐트(Intent)란 이러한 어플리케이션 구성요소(컴포넌트) 간에 작업 수행을 위한 정보를 전달하는 역할을 한다.
  + ### Intent의 종류
    + **명시적 인텐트**(Explicit Intent)
      + 인텐트에 클래스 객체나 컴포넌트 이름을 지정하여 호출될 대상을 확실히 알 수 있는 경우
      + 실행하고자하는 Component 클래스명을 Intent에 담는 방법. 주로 동일 App에서 다른 Component를 실행시킬때 사용한다.
    + **암시적 인텐트**(Implicit Intent)
      + 호출될 대상의 속성들을 지정했지만 호출될 대상이 달라질 수 있는 경우
      + 설치된 애플리케이션들에 대한 정보를 알고 있는 안드로이드 시스템이 인텐트를 이용해 요청한 정보를 처리할 수 있는 적절한 콤포넌트를 찾아본 다음 사용자에게 그 대상과 처리 결과를 보여주는 과정을 거치게 됩니다
      + 예를들면 인터넷을 연결할 때 네이버앱, 다음앱, 크롬 등 여러개 선택 가능하게 하는 것.  

   + **Intent filter**
     + Intent filter를 이용하여 암시적 인텐트를 수신할 수 있다.
     + 각 인텐트 필터는 어느 유형의 인텐트를 수락할지 지정한다.
     + 활동, 서비스, broadcast receiver가 응답할 수 있는 인텐트의 유형 지정
     + Action(인텐트 필터에 action요소가 없으면 필터가 intent객체를 허용하지 않음), category,data 영역으로 구성됨.
## 3. activity life cycle
  + ### Activity 상태
    + **Active 상태**(활성화) : 
      + 액티비티가 스크린 전면에서 실행되고 있는 상태
      + 사용자의 입력을 받을수 있는 상태
    + **Pause상태**(일시멈춤) :
      + 사용자의 입력은 못 받으나 스크린에는 보여지는 상태
      + Pause 상태일때도 상태정보와 리소스는 운영되고 있지만, 이 또한 여의치 않으면 강제 종료
    + **Stop**상태*(정지)
      + 아예 스크린에 보여지지 않는 상태 (다른 액티비티에 가려짐)
      + 여전이 상태정보와 리소느는 유지되지만, 여의치 않으면 강제 종료됨
  + ### life cycle 고려해야 하는 이유
    + 사용자가 앱을 사용하는 중에 전화를 받았을 경우 앱에서 충돌이 일어나지 않게 방지한다
    + 사용자가 앱을 사용하다가 다른 앱에 들어갔을 때 충돌이 일어나지 않게 방지한다.
    + 사용자가 앱을 사용하고 있지 않을 때 다양한 리소스들을 낭비하지 않게 방지한다.
    + 사용자가 앱을 사용하다가 떠났다가 다시 들어왔을 때 이전에 하고 있던 프로세스를 이어서 할 수 있도록 지원한다.
    + 화면이 가로나 세로로 돌릴 때 사용자의 프로세스를 이어서 해주도록 해주고 충돌이 일어나지 않게 해준다.
  + ### life cycle
    ![image](https://user-images.githubusercontent.com/63469069/141296427-e48d53d0-71b4-4f79-8ac0-012c09822210.png)
    + **Oncreate** : 
      + 액티비티가 생성되면 가장 먼저 실행되는 메서드이다. **화면 레이아웃 정의, 뷰**를 생성하거나 **데이터 바인딩** 등을 이곳에서 하면 된다.
      + 생명 주기 동안 딱 한 번만 실행되는 메서드이기도 하다. 그래서 액티비티 **최초 실행 시**에만 해야 할 작업을 여기서 하면 된다.
    + **Onstart** :
      + 액티비티가 화면에 표시되기 직전에 호출된다.
      + **화면에 진입할 때마다 실행**되어야 하는 코드를 이곳에 작성하면 된다.
    + **Onresume** :
      + 다른 액티비티가 액티비티를 덮어버리거나 앱 사용 중 전화가 와서 잠시 앱을 떠나거나 카톡에서 사진 첨부할 때 '갤러리'가 아닌 '카메라'를 클릭해 카메라를 켠다거나 등의 상황
      + 잠시 액티비티가 **일시정지 되었다가 돌아오는 경우** onResume 메서드가 호출된다.
      + 만약 액티비티가 **재개되었을 때 실행해야 할 코드**가 있다면 이곳에 작성하면 된다.
      + onStart에서 초기화 작업을 했다면 -> onStop에서 리소스 해제/종료 작업.
      + onResume에서 초기화 작업을 했다면 -> onPause에서 리소스 해제/종료 작업을.
      + onResume 이후 activity는 활성상태가 되고 사용자에게 보여지게 된다.
    + **onPause** :
      + 방금 앞서 말했듯 방해되는 이벤트가 발생하면 이 메서드가 호출된다.
      + 즉, 사용자가 액티비티를 잠시 떠나기 때문에 리소스를 계속 소모하거나 GPS가 계속 작동하거나 이럴 필요가 없는 것이다.
      + 포그라운드에 있지 않을 때 실행할 필요가 없는 기능들을 onPause에서 일시 정지하면 된다.
      + onPause는 **아주 잠깐 실행**되는 메서드이므로 데이터를 저장하거나, 네트워크를 호출하는 등 **무거운 작업**을 하면 안 된다.
      + 무거운 작업은 어떻게 해야 하는가? 바로 다음에 설명할 onStop에서 하면 된다.
    + **onStop** :
      + 액티비티가 사용자에게 더 이상 보이지 않으면 이 메서드가 호출된다.
      + 앞서 말했듯이 **무거운 작업**을 이곳에서 해주면 된다.
    + **onRestart** :
      + 홈으로 나갔다가 다시 돌아오거나 다른 액티비티로 갔다가 뒤로 가기 버튼을 통해서 돌아오는 경우 이 메서드가 호출된다.
    + **onDestroy** :
      + 앱을 종료하는 경우 호출된다. onStop에서 혹시 아직 해제하지 못한 리소스 작업을 하면 된다.
    + 예시 :
      + 앱을 실행할 때 : onCreate - onStart - onResume
      + 홈 화면으로 나왔을 때 : onPause - onStop 
      + 앱으로 다시 돌아왔을 때 : onRestart - onStart - onResume
      + 앱을 종료 했을 때 : onPause - onStop
      + 액티비티 이동 했을 때 : onPause - onCreate - onStart - onResume - onStop
      + 다시 원래 액티비티로 돌아왔을 때(뒤로가기) : onPause - onRestart - onStart - onResume - onStop - onDestroy
      + 핸드폰 화면 전환 했을 때 : onPause - onStop - onDestroy - onCreate - onStart - onResume
   + ### 핸드폰 화면전환 처리
      +  디바이스를 회전할 때는 다른 상태변화 와는 다르게 액티비티가  destroy 되었다가 다시 create 된다. 그래서 사용중이던 상태를 잃어버리게 된다. 
      +  onSaveInstanceState 메서드를 이용해서 Bundle 객체에 저장할 데이터를 저장한 후, Oncreate에서 Bundle 객체를 이용해서 데이터를 다시 복원한다.    
## 4. 디자인패턴
   + ### MVC 구조
      + View : UI(XML,웹layout등)
      + model : DB(data)
      + Controller : Activity(logic)
      + 모든 입력은 controller에서 처리 & 입력에 대한 logic 및 화면에 무었을 보여줄지 controller에서 처리 --> controller에서 하는일이 너무 많아짐.
      + 단점 :
         + **View가 model을 이용하므로 의존성**이 커진다.
         + Controller가 안드로이드에 깊게 종속적이므로 **테스트하는데 문제가 발생**한다.
         + 새로운 기능을 추가하거나 수정을 할때 많은 코드가 Controller에 모이면서 유지보수가 어려워진다.
    
   + ### MVP 구조
      + View : Activity(사용자의 Input + UI)
      + Presenter : Model과 View를 연결시켜주는 **매개체** & 뷰에 연결되는 것이 아닌 단순한 인터페이스
      + 사용자의 입력은 View를 통해 들어오고 Model과 View 는 항상 Presenter를 거쳐서 동작
      + --> MVC의 단점인 **View와 Model의 의존성이 없어짐 !**
      + View에 Input이 들어오면 presenter에서 처리 & 화면에 보여줄 것도 model과 상호작용 후 View에 전달
      + Presenter는 Input/Output 과는 연관이 있지만 **화면과는 관련이 없어짐**.
      + MVC와의 가장 큰 차이점 화면에 종속받는 Controller와 다르게 Presenter는 화면에 종속받지 않아 **테스트가 가능**해짐
      + 단점 :
         + View와 Presenter가 1:1 대응 이므로 종속성이 커짐
         + --> 비슷한 화면 비슷한 기능이여도 Presenter가 **여러개 필요**하게 되어 불필요한 코드증가

   + ### MVVM 구조
      + ViewModel : **화면에 무엇을 표시할지 신경쓰지 X** & 단지 Model과 상호작용하며 **data만 관리**
      + View와의 의존성을 **완전히 분리**
      + Data가 변경되면 ViewModel에서는 단지 수정만 해줌 & View에서 ViewModel을 구독하면서 데이터가 바뀌었는지 확인하며 화면갱신
      + 여러 View가 있다고 하더라도 비슷한 data를 가지고 있다면 하나의 ViewModel을 보고있음
      + ViewModel 과 View의 종속성이 1:n 이므로 그만큼 코드가 줄어듬
      + 단점 :
         + ViewModel을 설계하기가 어려운 단점이 존재
         + 표준화된 틀이 존재하지 않아 사람마다 이해도가 다름
         + 데이터 바인딩이 필수적으로 요구됨
## 5. Recycler View
   + ### RecyclerView vs ListView :
      + ![image](https://user-images.githubusercontent.com/63469069/141772705-6a1433a8-677a-4457-a2ad-92012e3228d0.png)
      + 총 데이터 100개 화면에 보여지는 개수 10개라고 생각해보자.
      + ListView를 사용할 경우 위아래 스크롤 할때마다 View객체들이 계속해서 생성되고 삭제되므로 많은 작업이 필요하게 된다.
      + RecyclerView의 경우 화면에서 사라질 View객체를 **새로 나타날 View로 재사용하는 것**.
      + RecyclerView의 경우 View객체만을 재사용하는 것이지 담고 있는 **data를 재사용하는 것은 아니다**. 
      + 하지만 View 객체를 새로 생성하지 않는 것만으로도 ListView에 비해 훨씬 효율적이다.
   + ### RecyclerView 요소
      + ViewHolder : 처음 보여줄 개수를 기억(홀딩)하고 있는 객체이다.
      + Adapter : 전체 data를 RecyclerView에 바인딩 시켜주기 위해 사전 작업이 이루어 지는 객체이다.
      + LayoutManager : 간단하게 어디로 이동할지, 즉 좌우 스크롤 or 상하 스크롤할 지 결정해주는 것 정도로만 생각.
## 6. Jetpack Library
   + ### Jetpack 이란 ?
      + 안드로이드 Jetpack은 개발에 자주 쓰이는 여러 라이브러리들과 툴들을 묶어놓은 모음집이다. 
      + 개발자들이 더욱더 편리하기, 빠르게, 쉽게 높은 퀄리티의 앱을 개발하도록 돕는 모음 도구이다.
   + ViewModel을 쓰는 이유 : 수명 주기를 고려하여 UI 관련 데이터를 저장하고 관리하도록 설계되었기에 -> 생명주기에 관계없이 데이터를 보존하기 위해서!
   + ### DataBinding 
      + Ui 요소와 데이터를 프로그램적 방식으로 연결하지 않고, 선언적 형식으로 결합할 수 있게 해주는 것.
      + 레이아웃 파일에서 직접 View에 텍스트를 할당해주는 것을 선언적이라고 표현한다.
      + 왜 사용할까 ?
         + 데이터 바인딩을 사용하면, 데이터를 UI 요소에 연결하기 위해 필요한 코드를 최소화할 수 있다.
         + 데이터 바인딩은 MVP 또는 MVVM 패턴을 구현하기 위해 유용하게 사용된다
   + ### 코루틴
      + Thread 보다 매우매우 가볍고 비용이 저렴하다.
      + (1)협력형 멀티 태스킹
      + (2)동시성 프로그래밍 지원
      + (3)비동기 처리를 쉽게 도와줌
      + 추후 사용& 공부 후 보완 !!
