## 서문

![](img/logo.jpg) 

자바 스크립트 어플리케이션을 구조화하기 위한 [Backbone.js](http://documentcloud.github.com/backbone/) 에 대한 책(현재 집필중)을 읽는 것을 환영합니다. 이 책은 Creative Commons Attribution-NonCommercial-ShareAlike 3.0 Unported [license](http://creativecommons.org/licenses/by-nc-sa/3.0/) 아래에서 배포되었고 그것은 여러분이 자유로이 복제할 수도 있고 [개선](https://github.com/addyosmani/backbone-fundamentals/)할 수도 있음을 의미합니다.

저는 이 책이 [O'Reilly Media](http://oreilly.com)를 통해 실제 책으로 출판되게 됨을 알려드리게 되어서 기쁘게 생각합니다. 독자분들은 그때 출간물이나 다양한 디지털 형태로 초기 버젼을 구매하시거나 이 git 저장소에서 최신의 버젼을 얻을 수 있습니다.

잘못된 부분의 교정은 언제나 환영하며 저는 우리 모두가 커뮤니티에 유용한 최신의 자료를 제공할 수 있으면 좋겠습니다.
Backbone.js를 만든 [Jeremy Ashkenas](https://github.com/jashkenas)와 이 프로젝트를 개선하는데 도와준 커뮤니티의 [멤버들](https://github.com/addyosmani/backbone-fundamentals/contributors)에게 공로를 돌립니다.

저는 이책이 당신에게 유용하길 바랍니다.

# 소개

프레임워크없이 웹 어플리케이션을 개발할 때, 우리는 단순히 (jQuery와 갈은) DOM 조작 라이브러리와 편리한 유틸리티 플러그인들에 의지하는 것이 쉽게 느껴진다. 문제는 어플리케이션을 위한 어떤 적합한 구조도 없는 jQuery 콜백의 중첩과 DOM 엘레먼트안에서 길을 잃어버리는데 오래 걸리지 않는다는 점이다.

간단히 말하면, 우리는 스파게티 코드를 만나게 된다. 다행이도 우리의 프로젝트가 오랜기간 손쉽게 유지보수 할 수 있으면서 구조화할 수 있도록 도와주는 현대적인 자바스크립트 프레임워크와 라이브러리들이 있다.

### MVC란?

최근 툴들은 개발자가 MVC(Model-View-Controller)라고 알려진 패턴의 변형들을 이용한 코드를 결합하는 쉬운 방법을 제공한다. MVC는 어플리케이션의 관심을 다음의 세 부분으로 쪼갠다.

* 모델은 어플리케이션이 다루는 영역의 정보를 표현한다. 이것을 (사용자, 사진 혹은 할일 목록과 같이 )모델링할 수 있는 데이타의 '종류'로 생각해라. 모델은 그 상태를 관찰하고 있는 누군가(예를 들면 뷰)에게 현재 상태를 알려주어야 한다.
* 뷰는 보통은 어플리케이션에서 (마크업이나 템플릿과 같은)사용자 인터페이스로 생각되지만 반드시 그렇지만은 않다. 뷰는 모델을 감시하기 위해서 모델의 존재를 알아야만 하지만 직접적으로 연계하지는 않는다.
* 컨트롤러는 어플리케이션에서 (클릭, 사용자 동작과 같은) 입력을 처리하고 뷰는 출력을 처리하는 것으로 생각할 수 있다. 컨트롤러가 (예를 들어 노트의 내용을 편집하는 것과 같은) 모델의 상태를 변경할 때, 바로 뷰에 전달되지 않는다. 뷰와 모델간의 감시 특성이 있는 이유이다.

우리 코드를 구조화하는 것을 도와주는 자바스크립트 'MVC' 프레임워크가 항상 위의 패턴을 엄격히 지키는 것은 아니다. 어떤 솔루션은 뷰에서 컨트롤러의 책임을 포함하며(Backbon.js가 그러하다) 또 다른 것들은 자기들이 좀 더 효율적이라고 느끼는 방식으로 자신만의 독자적인 컴포넌트를 섞어 사용한다.

이러한 이유로 우리는 그런 프레임워크는 MV*패턴을 따른다고 한다. 즉 당신은 뷰와 모델을 가질 수 있을 뿐만 아니라 다른 어떤 것을 추가로 가질 수 있을 것이다.

### Backbone.js란?

![](img/backbonejsorg.png)

Backbone.js는 당신의 클라이언트 코드에 구조를 추가하기 위한 자바스크립트 경량 라이브러리이다. Backbone.js는 오랜기간 좀 더 유지보수성이 좋은 코드를 갖도록 하기 때문에 어플리케이션의 관심사를 관리하고 의존성이 없도록 하기 쉽다.

개발자들은 보통은 Backbone.js과 같은 라이브러리를 소위 SPAs라고 하는 단일 페이지 어플리케이션( 페이지 전환이 일어나지 않는 어플리케이션 )을 만드는데 사용한다. 쉽게 말해서 이런 앱들은 브라우져가 서버에서 모든 마크업을 완전히 로드할 필요없이( 완전한 페이지 리프레쉬가 필요없음을 의미한다 ) 클라이언트의 데이타 변화에 따라 동작하도록 해준다.

이글을 쓰는 시점에 Backbone.js는 성숭되고 인기있는 라이브러리이며 온라인상에 대규모의 개발 커뮤니티와 그 위에서 개발된 방대한 량의 유용한 플러그인과 익스텐션을 가지고 있다. Backbone.js는 Disqus, Walmart, SoundCloud, Foursquare와 같은 회사들에 의해 독특한 어플리케이션을 개발하는데 사용되어 왔다.


### 자바스크립트 MVC 프레임워크는 언제 필요한가?

자바스크립트로 SPA를 개발할 때면(복잡한 UI를 필요로 하든 단순히 새로운 뷰를 위해 필요한 HTTP 요청의 수를 줄이려고 하든간에), 당신은 Backbone.js와 같은 MV* 프레임워크를 구성하는 많은 조각들을 스스로 개발하고 있는 것을 깨닫게 될 것이다.

작업 초기에는 스파게티 코드를 피하기 위해 독자적인 방법을 제공하는 어플리케이션을 작성하는 것은 그렇게 어렵지 않지만, 보통 Backbone의 어떤 표준을 작성하는 것과 보통은 같아질 거라고 말하는 건 심하게 잘못된 가정이다.

DOM 조작, 템플릿, 라우팅 라이브러리를 묶는 것보다 어플리케이션을 구조화하는데 노력하는데 훨씬 더 많은 가치가 있다. 성숙한 MV* 프레임워크는 일반적으로 당신이 직접 작성해야 하는 많은 코드 조각들을 포함하고 있을 뿐만 아니라 나중에야 겨우 도달하게 될 문제의 해결책도 포함하고 있다. 이것은 과소평가해서는 안되는 시간절약인 것이다.

그래서 결국, MV* 프레임워크는 어디에 필요하고 어디에 필요하지 않는가?

당식이 데이터를 보여주고 조작하는데 매운 무거운 동작들이 브라우져에서 발생하고 API나 백엔드 데이터 서비스로만 통신하는 어플리케이션을 작성한다면 자바스크립트 MV* 프레임워크가 유용하다는 것을 알게될 것이다.
이런 류에 포함되는 어플리케이션의 좋은 예는 지메일과 구글 독스이다.

이들 어플리케이션들은 일반적으로 사용자들의 공통 작업에 필요로 하는 모든 스크립트와 스타일시트, 마크업을 포함하는 하나의 요청으로 다운로드하고 나서 많은 추가적인 동작을 백그라운드에서 수행한다. 이메일을 읽는 것과 문서를 작성하는 사이을 오가는 것은 당연한 것이고 당신은 어플리케이션이 전체 페이지를 다시 그릴지 전혀 궁금해 할 필요가 없다.

하지만, 당신이 대부분의 무거운 뷰 및 페이지에 대해서 여전히 서버에 의지하는 어플리케이션을 작성하고 약간의 자바스크립트나 조금더 인터렉티브하게 하기 위해 JQuery를 사용하고 있다면, MV* 프레임워크는 오바일 수도 있다. 확실히 부분적으로 화면을 그리는 것( partial rendering )이 SPA에 효율적으로 적용될 수 있는 복잡한 웹 어플리케이션이 있지만, 다른 것들에 대해서는 더 쉬운 셋팅을 고수하는 것이 낫다는 것을 알게 될 수도 있다.

소프트웨어(프래임워크) 개발에서 성숙도란 단순히 프레임워크가 얼마나 오랬동안 진행되었냐에 대한 것이 아니다. 그것은 프레임워크가 얼마나 견고한고 그역할을 충족하기 위해 얼만나 잘 발전해 왔는가에 대한 것이다. 공통된 문제를 풀 때, 더 효율적으로 되었는가? 개발자들이 그 프레임워크로 더 크고 복잡한 어플리케이션을 개발할 때, 끊임없이 개선되고 있는가?


### 왜 Backbone.js을 고려하는가?

다음의 문장이 당실을 표현하는가?:

MVC (Model-View-Controller)는 관심의 분리( SoC )를 통해 개선된 어플리케이션 구조를 장려하는 구조적인 디자인 패턴이다. 그것은 전통적으로 논리 흐름, 사용자 입력, 모델과 뷰의 결합을 관리하는 제 3의 컴포넌트( 컨트롤러 )를 사용하여 비즈니스 정보( 모델 )를 사용자 조작( 뷰 )를 분리하도록 한다. 이 패턴은 원래 Smalltalk-80(1979)에서 일할 때 [Trygve Reenskaug](http://en.wikipedia.org/wiki/Trygve_Reenskaug)가 설계하였는데, 그곳에서 처음에는 Model-View-Controller-Editor라고 불렸다. MVC는 1994년에 출간된 [“Design Patterns: Elements of Reusable Object-Oriented Software”](http://www.amazon.co.uk/Design-patterns-elements-reusable-object-oriented/dp/0201633612) (The "GoF" or “Gang of Four” book)에 상세히 설명되어 있다. 이 책은 MVC사용을 대중화하는데 큰 역할을 했다.


### Smalltalk-80 MVC

MVC 패턴은 탄생이후 크게 바뀌었기 때문에, 원래의 MVC 패턴이 풀려고 했었던 것에 대해 이해하는 것이 중요하다. 70년대에 돌아가서, 그래픽 유져-인터페이스는 매우 드물었다. (사진이나 사람과 같은) 현실의 개념을 모델링한 도메인 오브젝트와 사용자의 눈에 보여지는 프리젠테이션 오브젝트간에 명확한 구분을 하기 위한 수단으로 [Separated Presentation](http://martinfowler.com/eaaDev/uiArchs.html) 라고 알려진 접근이 시작되었다.

Smalltalk-80의 MVC 구현은 이러한 개념을 더욱 발전시켜서 사용자 인터페이스로 부터 어플리케이션 로직을 분리하려는 목적을 가졌었다. 기본 생각은 어플리케이션의 이런 부분들을 분리해내는 것이 어플리케이션의 다른 인터페이스에서 모델의 재사용이 가능하게도 한다는 것이었다. Smalltalk-80의 MVC 구조에 대해서 주목해야 할 몇가지 재미있는 부분들이 있다.

* 도메인 요소는 모델이라고 알려져있는데 사용자 인터페이스(뷰와 컨트롤러)에 대해서 알지 못한다.
* 표현 요소는 뷰와 컨트롤러에 의해서 관리되지만 하나의 뷰와 컨트롤러만 있는 것은 아니다. 화면상에 보이는 각각의 요소를 위해서는 뷰와 컨트롤러 쌍이 필요하지만, 그들 간에 실제로 분리되어 있지는 않았다.
* 뷰-컨트롤러 쌍에서 컨트롤러는 ( 키 입력과 클릭과 같은 ) 사용자 입력을 감시하면서 그것들을 처리하는 것이다.
* 모델이 변경될 때 뷰를 갱신하기 위해 옵져버 패턴이 적용된다.

개발자들은 때론 옵져버 패턴( 오늘날에는 보통 발행/구독 시스템으로 구현된다 )이 수십년 전의 MVC 구조의 일부분으로 포함되어 있다는 것을 배울때 놀라기도 한다. Smalltalk-80의 MVC에서 뷰와 컨트롤러 모두 모델을 감시한다: 모델이 바뀌면 뷰는 반응한다. 이것의 일례는 주식 시장 정보에 의해 움직이는 어플리케이션이다- 어플리케이션이 실시간 정보를 보여주기 위해서 그 모델의 정보에 어떤 변화라도 뷰가 즉각적으로 갱신되도록 해야한다.

Martin Fowler는 수년에 걸쳐 MVC의 [기원](http://martinfowler.com/eaaDev/uiArchs.html)에 대한 글을 쓰는 엄청난 일을 했다. 만일 Smalltalk-80의 MVC의 역사에 더 관심이 있다면 그것을 읽어보기를 권한다.



## 우리가 알고 있는 MVC

70년대를 살펴보았지만 이제 현재로 돌아가 보자. MVC 패턴은 각양각색의 프로그랭밍 언어에 적용되었다. 예를들면, 인기가 많은 루비 온 레일즈는 루비 언어를 위한 MVC에 기반한 웹 어플리케이션 프레임워크의 구현체이다. 자바스크립트는 AngularJS( 동적인 변경을 위해 HTML과 자바스크립트를 확장한 프레임워크)와 Backbone을 포함해 현재 많은 MVC 프레임워크를 가지고 있다. "스파게티" 코드( 구조가 부족함으로써 인해 읽거나 유지보수하기 매우 어려운 코드를 말하는 용어 )를 피한는 것이 중요하다고 가정하고 MVC 패턴으로 자바스크립트 개발자가 할 수 있는 것을 살펴보자.

MVC는 세개의 주요 컴포넌트로 구성된다:

### 모델

모델은 어플리케이션을 위한 정보를 관리한다. 모델은 사용자-인터페이스나 표현 계층에 관심이 없지만, 대신 어플리케이션이 필요로 하는 구조화된 정보를 대표한다. 모델이 변경될 때( 예를 들어 값이 갱신될 때 ), 보통은 감시자들( 예를 들어 간단히 알고 있는 뷰 )에게 변경이 발생했으니 그에 따라 반응하라고 알려줄 것이다.

모델을 좀 더 이해하기 위해 자바스크립트로 만들어진 할일 목록(todo) 어플리케이션이 있다고 생각해보자. 그 어플리케이션에서 할일 항목은 독특한 종류의 도메인 특화된( domain-specific ) 정보를 표현하기 따문에 자신만의 모델을 가질만하다. Todo 모델은 아마도 제목과 완료와 같은 속성을 갖을 것이다. 특정 할 일은 모델의 객체로 저장된다. 다음에 Backbone.js로 구현된 단순한 Todo 모델의 예가 있다.

```javascript
  var Todo = Backbone.Model.extend({
    // Todo에 대한 기본 속성
    defaults: {
      title: '',
      completed: false
    }
  });

  // 기본 속성으로 todo 객체를 생성한다.
  var firstTodo = new Todo();

  console.log("Todo's default title: " + firstTodo.get('title')); // ""
  console.log("Todo's default status: " + firstTodo.get('completed')); // false

  firstTodo.set('title', 'Enjoy reading the book');
  console.log('Title changed: ' + firstTodo.get('title'));

  // 특정 정보로 todo 객체를 생성한다.
  var secondTodo = new Todo({ title: 'Try this code in chrome console'});

  console.log("Second todo title: " + secondTodo.get('title'));
  console.log("Second todo status: " + secondTodo.get('completed'));
```

모델이 원래 가지고 있는 기능은 프레임워크마다 다르지만 모델의 아이디와 같은 모델의 특성을 표현하는 속성에 대해서 그 값이 유효한지 검증하는 기능은 공통적이다. 실제 어플리케이션에서 모델을 사용할 때, 보통은 모델을 유지하는(presist) 방법도 필요로 한다. 유지성(persistence)은 모델의 가장 최신의 상태가 어디엔가(예를들면 웹브라우져의 지역저장소나 데이터베이스와의 동기화) 저장되었다는 것을 알고 모델을 수정하고 갱신할 수 있게 해준다.

모델을 감시하는 여러개의 뷰들이 있을 수도 있다. 우리의 (일반적으로 무언가를 한다고 하면) Todo 모델이 예약 일자, 알람, 반복 주기와 같은 메타 정보를 갖는다고 상상해보자. 개발자는 이들 속성 모두를 보여주는 하나의 뷰를 생성할 수도 있고, 각 속성을 보여주는 세 개의 분리된 뷰들을 생성해도 된다. 중요한 것은 Todo 모델이 뷰들이 어떻게 구성되는지 관심갖지 않는다는 점이다. 그것은 단순히 필요에 따라 그 데이타가 갱신되었음을 알려줄 뿐이다. 나중에 우리는 뷰에 대해서 자세히 살펴볼 것이다.

현대적인 MVC 혹은 MV* 프레임워크가 모델들을 함께 묶어주는 방법을 제공하는 것은 특이한 것이 아니다. Backbone에서는 이러한 묶음을 "Collections"라고 부른다. 묶음으로 모델들을 다루는 것은 포함된 모델에 변경이 발생했을 때, 묶음으로부터의 통지에 기반해서 어플리케이션 로직을 작성하도록 해준다. 이런 특성은 일일이 각각의 모델 객체를 감시할 필요가 없게 한다.

다음에 우리가 어떻게 Todo 모델들을 Backbone Collection으로 묶는지 보여준다:

```javascript
  var Todo = Backbone.Model.extend({
    // Todo에 대한 기본 속성
    defaults: {
      title: '',
      completed: false
    }
  });

  var Todos = Backbone.Collection.extend({
    model: Todo,
    
    // 책의 첫번째 부분동안 localStorage를 간단히 사용할 것이다.
    // `"todos-backbone"` 네임스페이스에 모든 todo 항목을 저장한다.
    localStorage: new Store('todos-backbone')
    
    // 서버와 REST API로 동작할 때, 여기에 적당히
    // 작성할 것이다:
    // url: "/todos"
    
  });

  var firstTodo = new Todo({title:'Read whole book'});

  // 컬렉션 객체에 모델 배열을 전달한다.
  var todos = new Todos([firstTodo]);
  console.log(todos.length);

  // 컬렉션 스스로 그 안에서 모델 객체를 생성하는데
  // 사용하는 컬렉션의 편의 메쏘드
  todos.create({title:'Try out code examples'});
  console.log(todos.length);

  var thirdTodo = new Todo({title:'Make something cool'});

  // 모델을 컬렉션에 추가한다.
  todos.add(thirdTodo);
  console.log(todos.length);

  // 컬렉션은 모델들을 배열의 형태로
  // models 속성에 저장한다.
  console.log(todos.models);
```

당신이 만일 MVC에 대한 오래된 책을 읽는다면, 어플리케이션의 "상태"(state)를 관리한다는 모델의 묘사를 본적이 있을지도 모른다. 자바스크립트 어플리케이션에서 일반적으로 상태라고 하는 것은 특정 시점에 사용자의 눈에 보이는 뷰나 하위 뷰의 현태상태를 가리키는 특별한 의미를 갖는다. SPA를 볼 때, 어디에서 상태라는 개념을 모방했는지가 일반적인 논쟁거리이다.


### 뷰

뷰는 모델의 현재 상태를 정제하여 모습을 보여주는 가시적인 표현이다. 뷰는 일반적르ㅗ 모델을 감시하고 변경에 따라 갱신되기 위해 모델 변경을 통지받는다. 어플리케이션에서 모델과 컨트롤러에 대한 정보가 한정되어있다고 가정하면, 디자인 패턴 분야에서 뷰는 일반적으로 '바보'로 취급된다.

사용자들은 뷰와 상호동작하는데, 이 말은 일반적으로 모델의 데이타를 읽고 수정하는 것을 의미한다. 예를들어, 우리의 todo 어플리케이션 예제에서 todo 모델의 모습는 모든 todo 항목들과의 사용자 인터페이스로 나타난다. 그 속에서 각각의 todo는 제목과 완료 체크박스를 가진 형태로 보여진다. 모델 수정은 특정 todo를 선탠한 사용자가 폼으로 그 제목을 수정할 수 있도록 하는 "수정" 뷰를 통해 수행할 수 있다.

MVC에서 모델을 갱신하는 실제 작업은 컨트롤러에게 주어진다. 컨트롤러에 대해서도 곧 알아볼 것이다.

간단한 자바스크립트 예제를 이용해서 뷰를 좀 더 살펴보자. 아래에서 우리는 모델 객체와 컨트롤러 객체를 모두 사용하는 하나의 Todo 뷰를 생산하는 기능을 볼 수 있다.

```javascript
var buildTodoView = function ( todoModel, todoController ) {
  var base       = document.createElement('div'),
      todoEl     = document.createElement('div');

  base.appendChild(todoEl);

  var render= function(){
    // 우리는 todo 항목을 위한 HTML을
	// 생성하는 Underscore 템플릿팅과 같은
	// 템플릿팅 라이브러리를 사용한다.
    todoEl.innerHTML = _.template( $('#todoTemplate').html(), { src: todoModel.getSrc() });
   }

  todoModel.addSubscriber( render );     

  todoEl.addEventListener('click', function(){
    todoController.handleEvent('click', todoModel );
  });

  var show = function(){
    todoEl.style.display  = '';
  }

  var hide = function(){
    todoEl.style.display  = 'none';
  }

  return {
    showView: show,
    hideView: hide
  }
}
```

우리는 자바스크립트 템플릿 엔진인 ([Underscore](http://underscorejs.org "Underscore.js") templating)를 이용해서 ```todoModel```의 내용을 보여주고, 뷰의 내용을 갱신하는 역할을 하는 뷰(```todoEl```에 의해서 참조된다) 안에 ```render()``` 유틸리티 함수를 정의하였다.

그리고 나서 옵져버 패턴을 통해 모델이 변경될 때 뷰가 갱신되도록 하기 위해 ```todoModel```은 우리가 만든 ```render()``` 콜백 함수를 구독자(subscribers)로 추가한다.

당신은 이 코드에서 유저 조작이 어디에 작용하는지 궁금해 할지도 모르겠다. 사용자가 뷰안에 어떤 엘레멘트라도 클릭할 때, 다음에 무슨 일을 할지는 뷰가 담당하는 것이 아니다. 이 결정은 컨트롤러가 한다. 우리 예제 구현에서는 클릭 동작을 처리하는 것을 컨트롤러에 위임하는 이벤트 리스너를 ```todoEl```에 추가한다. 컨트롤러는 필요에 따라 모델 정보를 전달받는다.

이런 구조의 장점은 어플리케이션의 기능을 만드는데 있어서 각 컴포넌트들은 필요에 따라 각자의 독립된 역할을 수항한다는 것이다.


**템플릿팅**

MVC/MV*를 지원하는 자바스크립트 프레임워크의 문맥에서 자바스크립트 템플릿팅과 그것의 뷰와의 관계에 좀 더 자세히 살펴볼 가치가 있다.

오래전부터 스트링 결합을 통해서 큰 HTML 블럭을 메모리에 일일이 생성하는 것은 비실용적으로 생각되어 왔다.( 계산해봐도 비용이 높다. ) 이 기술을 사용하는 개발자들은 종종 자신들이 데이터를 순회하면서 중첩된 div테그로 감싸고, '템플릿'을 DOM에 삽입하기 위해 ```document.write```같은 구닥다리를 쓰고 있다는 것을 알아차리게 된다. 이런 접근은 가끔 스크립트 마크업 언어를 표준 마크업 안에 유지하게 만든다. 그리고 그것은 코드를 읽고 유지보수하는데 어렵게 만든다. 특히 대형 어플리케이션을 개발할때 그러하다.

( Handlebars.js나 Mustache같은 ) 자바스크립트 템플릿팅 라이브러리들은 템플릿 변수를 포함하고 있는 HTML언어로서의 뷰에 대해서 템플릿들을 정의하는데 종종 쓰인다. 이런 템플릿 블럭들은 외부에 저장되거나 사용자 정의 타입( 예를 들면, 'text/template' )으로 script 태그안에 저장될 수 있다. 변수들은 변수 문법을 사용해서 구분된다.( 예를 들면 {{title}} ) 자바스크립트 템플릿 라이브러리들은 일반적으로 JSON의 형태로 데이타를 받고 템플릿에 데이타를 채우는 반복적인 작업은 프레임워크에 의해서 관리된다. 이것에는 몇가지 장점이 있다. 템플릿을 외부에 저장하도록 했을 때, 어플리케이션이 필요에 따라 동적으로 템플릿을 로드할 수 있기 때문에 특히 장점이 될 수 있다.

HTML 템플릿들의 두 예를 비교해보자. 하나는 인기있는 Handlebars.js 라이브러리를 사용해 구현되었고, 다른 하나는 Underscore의 'microtemplates'을 사용하였다.

**Handlebars.js:**

```html
<div class="view">
  <input class="toggle" type="checkbox" {{#if completed}} "checked" {{/if}}>
  <label>{{title}}</label>
  <button class="destroy"></button>
</div>
<input class="edit" value="{{title}}">
```

**Underscore.js Microtemplates:**

```html
<div class="view">
  <input class="toggle" type="checkbox" <%= completed ? 'checked' : '' %>>
  <label><%= title %></label>
  <button class="destroy"></button>
</div>
<input class="edit" value="<%= title %>">
```

당신은 Microtemplates에서 두개의 중괄호( 즉 ```{{}}``` )를 쓸 수도 있다.( 아니면 당신 편하다고 생각되는 다른 어떤 태그라도 쓸 수 있다. ) 중괄호의 경우, 다음과 같이 Underscore의 ```templateSettings``` 속성을 설정해서 사용할 수 있다.

```javascript
_.templateSettings = { interpolate : /\{\{(.+?)\}\}/g };
```

**이동과 상태에 대한 메모**

고전적인 웹 개발에서 독립적인 뷰 사이를 이동하는 것은 페이지 갱신을 필요로 한다는 것에 주목할 필요도 있다. 하지만, SPA 자바스크립트 어플리케이션에서는 Ajax를 통해 한버 서버에서 데이타가 넘어오면, 같은 페이지 안에서 새로운 뷰의 형태로 동적으로 그려질 수 있다. 이것이 URL 갱신을 자동적으로 하지 않기 때문에, 페이지 이동의 역할은 "router"에게 부여된다. 라우터는 어플리케이션의 상태을 관리하는 것을 보조해준다.( 예를들면 사용자가 방문한 특정 뷰를 북마크하게 해준다 ) 하지만 라우터는 MVC의 일부분도 아니고 모든 MVC 프레임워크에 존재하지도 않기 때문에 여기에서는 더 자세히 들어가지는 않을 것이다.

### 컨트롤러

컨트롤러는 전통적으로 두가지 일을 수행하는 모델과 뷰간의 중개자이다: 컨트롤러는 모델이 변경되었을 때 뷰를 갱신하고 사용자가 뷰를 조작했을 때 모델을 갱신한다.

우리 Todo 어플리케이션에서 컨트롤러는 사용자가 수정을 마쳤을 때 어떤 todo 모델을 갱신함으로써 사용자가 todo에 대한 수정 뷰에서 만든 변경을 처리하는 일을 한다.

대부분의 자바스크립트 MVC 프레임워크는 MVC 패턴의 이러한 해석에서 벗어나는 것은 컨트롤러로 한다. 그 이유는 다양한데, 내의견에는 자바스크립트 프레임워크 개발자은 초기에 ( 루비 온 레일즌같은 ) MVC의 서버쪽 해석을 보았지만 이런 접근법이 클라이언트 쪽에는 1:1로 변환되지 않는 다는 것을 깨닫게 되었다. 그래서 MVC에서 C가 상태관리에 관한 문제를 풀도록 재해석하였다. 이것은 영리한 접근 방법이었지만 MVC를 처음 접하는 개발자가 고전적인 MVC 패턴과 그렇지않은 자바스크립트 프레임워크에서 컨트롤러의 "적절한" 역할을 모두 이해하는 것을 어렵게 만들수도 있다.

그래서 Backbone.js가 컨트롤러를 가지고 있는가? 사실 그렇지 않다. Backbone의 뷰가 일반적으로 "컨트롤러"의 로직을 가지고 있고 ( 아래에서 논의할 ) 라우터가 어플리케이션의 상태를 관리하는데 사용되지만 둘다 전통적인 MVC에 따르면 진짜 컨트롤러는 아니다.

	이런 관점에서 정규 문서나 블로그 글에서 언급된 것과는 반대로 Backbone은 진정한 MVC 프레임워크가 아니다. 사실 그것을 독자적인 방식으로 아키텍쳐를 접근하는 많은 MV* 프레임워크들로 보는 것이 더 낫다. 물론 이것이 나쁠 것이 없지만, 전통적인 MVC와 MVC의 논의가 당신의 Backbone 프로젝트를 도와줄 것이라 믿는 MV*를 구별하는 것이 중요하다.


### Spine.js의 컨트롤러 vs Backbone.js의 컨틀롤러


**Spine.js**

우리는 이제 전통적으로 모델이 변경될 때 컨틀롤러가 뷰를 갱신하는 것을 알고 있다.( 사용자가 뷰를 갱신하면 모델에 갱신하는 것도 유사하다. ) Backbone은 **자신**만의 뚜렷한 컨트롤러를 갖지 않기 때문에 구현상 차이를 이해하기 위해 다른 MVC 프레임워크의 컨트롤러를 살펴보는 것이 유용하다. [Spine.js](http://spinejs.com/)를 살펴보자:

이 예제에서, 어플리케이션에서 각 할일들을 담당하는 ```TodoController```라 불리는 컨트롤러가 있다. 그것은 뷰가 갱신되면( 예를들어 사용자가 할일을 수정한 경우 ) 대응되는 모델도 같이 갱신되도록 해 줄 것이다.

(주: 우리는 이 예제 이상으로 Spine.js를 깊게 탐구하지 않겠지만 일반적으로 자바스크립트 프레임워크에 대해 좀 더 배우기 위해 살펴볼 가치는 있다. )


```javascript
// Spine에서 컨틀롤러는 Spine.Controller를 상속해서 생성된다.

var TodoController = Spine.Controller.sub({
  init: function(){
    this.item.bind('update', this.proxy(this.render));
    this.item.bind('destroy', this.proxy(this.remove));
  },

  render: function(){
    // Handle templating
    this.replace($('#todo-template').tmpl(this.item));
    return this;
  },

  remove: function(){
    this.$el.remove();
    this.release();
  }
});
```

Spine에서, 컨트롤러들은 DOM 이벤트를 추가하고 대응하고, 템플릿을 적용하고 뷰와 모델이 동기화( 우리가 컨트롤러라고 알고 있는 것들의 문맥에서 적합한 역할이다 )되도록 어플리케이션의 아교같은 것으로 생각된다.

우리가 위의 예제에서 하는 것이라고는 ```render()```와 ```remove()```를 이용해서 ```update```와 ```destroy``` 이벤트에 리스너들을 설정하는 것이다. 할일 항목이 갱신될 때, 우리는 할일 제목에 그 변경을 반영하도록 뷰를 다시 그린다. 비슷한 방식으로 할일이 할일 목록에서 삭제되면 우리는 뷰에서 없애버린다. 당신이 ```render()``` 코드 상의 ```tmpl()``` 함수에 대해서 궁금해하는 경우를 위해 설명하자면, 컨트롤러의 현재 엘레멘트를 바꾸는데 사용되는 HTML 문자열을 반환하는 #todoTemplate이라고 불리는 자바스크립트 템플릿을 그리는데 사용한 함수이다.

이것은 우리에게 모델과 뷰간의 변화를 관리하는 가볍고 단순한 방법을 제공한다.

**Backbone.js**

이 섹션의 후반부에 우리는 Backbone과 전통적인 MVC간의 차이를 다시 살펴볼 것이지만, 지금은 컨트롤러에 집중하자.

Backbone에서 컨트롤러 로직은 Backbone.View와 Backbone.Router 사이에 공유된다. Backbone의 초기버젼은 Backbone.Controller라고 불리는 것이 있었지만 그 역할을 명확히 하기 위해 Router로 이름을 바꿨다.

라우터의 주요 목적은 URL 요청을 어플리케이션의 상태로 변환한는 것이다. 그것은 URL들을 함수들로 맵핑함으로써 변환을 수행한다. 사용자가 URL www.example.com/filter/completed로 접근할 때, 라우터는 완료된 할일들만 보여주는데 사용될 수 있고 그 요청에 대한 응답으로 어플리케이션의 동작이 무엇을 수행하는지를 정의할 수 있다. 라우터는 모델와 뷰간의 이벤트 바인딩이나 페이지의 일부를 그리는 정통적인 컨틀로러의 역할을 포함할 수 있다. 그러나 Backbone 기여자인 Tim Branyen은 Backbone.Router가 전혀 필요없이도 가능하다는 점을 지적해왔다. 그래서 라우터 패러다임을 사용해서 그것에 대해서 생각하는 한가지가 가능하다:

```javascript
var TodoRouter = Backbone.Router.extend({
  routes: { "/filter/:name": "setFilter" },
  setFilter: function (name) { console.log("set filter: " + name); }
});

var router = new TodoRouter();
Backbone.history.start();
```

## MVC는 우리에게 무엇을 주는가?

요약해 보면, MVC에서 관심의 분리( SoC )는 어플리케이션의 기능을 모듈화하도록 도와주고 다음과 같은 일을 할 수 있게 해준다.

* 전체 유지보수를 더 쉽게한다. 어플리케이션을 수정해야만 할때, 변경이 데이터 중심인지( 모델 또는 컨트롤러에 대한 변경을 의미한다 ) 혹은 화면인지가( 뷰에 대한 변경을 의미한다 )
* 모델과 뷰의 분리는 비즈니스 로직에 대한 유닛 테스트를 작성하는 것이 직관적이라는 것을 의미한다.
* 하위 모델과 컨트롤러 코드의 중복이 어플리케이션 전반에 제거된다.
* 어플리케이션의 크기와 역할의 분리 정도에 따라 이 모듈화 정도가 개발자가 핵심 로직과 동작하는 사용자 인터페이스에 동시에 집중할 수 있게 해준다.


### 좀더 알아보기

이제 당신은 MVC 패턴이 제공하는 것에 대한 기본적인 이해를 갖게되었지만 호기심을 충족하기 위해 조금더 알아볼 것이다.

GoF (Gang of Four)는 MVC를 디자인 패턴으로 언급히자 않았지만 사용자 인터페이스를 구성하는 일련의 클래스로 생각했다. 그들의 관점에서 그것은 실제로 세개의 고전점인 디자인 패턴의 변형이다: 옵져버( 발행/구독 ) 패턴, 전략 패턴, 컴포지트 패턴. 프레임워크내에서 MVC가 어떻게 구현되었는지에 따라 팩토리 패턴이나 데코레이터 패턴이 사용될 수도 있다. 나는 나의 다른 책, 초심자를 위한 자바스크립트 디자인 패턴에서 이들 패턴을 다루었다. 나중에 읽어보길 바란다.

우리가 논의해왔던 대로, 뷰가 사용자에게 화면으로 사용자에게 보여지는 반면 모델은 어플리케이션의 데이타를 표현한다. 그래서, MVC는 핵심 동작의 일부를 위해 발행/구독 패턴에 의지한다( 놀랍게도 MVC 패턴에 관한 많은 글들이 이것을 다루지 않는다 ). 모델이 변경되었을 때, 모델은 어플리케이션의 다른 부분에 변경되었다고 "발행"을 한다. 그러면 "구독자"( 일반적으로 컨트롤러 )는 그에 따라 뷰를 갱신한다. 이러한 관계의 감시자-관찰자 특성은 여러개의 뷰가 같은 모델에 붙어있도록 해주는 것이다.

개발자들이 MVC의 독립성에 대해 더 알고 싶다면( 다시 말하지만 구현에 따라 다르지만 ), 그 패턴의 목적중에 하나는 대상과 그것의 관찰자간의 일대다 관계를 정의하는 것이다. 대상이 변경되었을 때, 그 관찰자들은 갱신된다. 뷰와 컨트롤러들은 조금 다른 관계를 가진다. 컨트롤러는 뷰가 다른 사용자 입력에 대응하도록 해주고 전랙 패턴의 한 형태이다.


### 결론

고전적인 MVC 패턴을 살펴보면서, 당신은 이제 개발자들이 어떻게 어플리케이션에서 관심을 명확하게 분리하게 해주는지 이해해야만 한다. 당신은 또 자바스크립트 MVC 프레임워크가 스스로의 해석에 따라 어떻게 달라질 수도 있고 어떻게 원래 패턴의 기본적인 컨셉중 일부를 공유하는지도 이해해야만한다.

새로운 MVC/MV* 프래임워크를 살펴볼 때, 다음을 기억하라 - 초심으로 돌아가서 프레임워크가 모델, 뷰, 컨트롤러 혹은 그것들의 대체객체를 어떻게 접근하는지 생각해 보는 것은 유용할 것이다. 이것은 당신이 프레임워크를 어떻게 사용해야 할지 완전히 이해하는데 좀 더 도움을 줄 것이다.


## MVP

Model-view-presenter (MVP)는 표현( presentation ) 로직을 개선하는데 중점을 둔 MVC 설계 패턴의 파생물이다. 그것은 원래 1990년대 초반에 [Taligent](http://en.wikipedia.org/wiki/Taligent)라는 회사에서 C++ CommonPoint 환경을 위한 모델에 적용하면서 만들어졌다. MVC와 MVP 모두가 여러개의 컴포넌트의 간에 관심의 분리를 목적으로 하는 반면 약간의 기초적인 차이가 있다.

이 결론의 목적을 위해 우리는 웹 기반의 구조에 가장 적합한 MVP 버젹에 중점을 둘 것이다.

### 모델, 뷰, 그리고 표현자

MVP에서 P는 표현자( presenter )를 의미한다. 그것은 뷰를 위한 사용자 인터페이스 비즈니스 로직을 담고 있는 컴포넌트이다. MVC와 달리 뷰에서의 호출은 표현자로 위임되는데, 표현자는 뷰와 독립적으로 인터페이스를 통해 뷰와 연동한다. 이러한 점이 유닛 테스트에서 뷰를 목킹(mocking)할 수 있도록 해주는 그런 유용한 것들이 가능하도록 한다.

MVP에서 대부분의 공통 구현은 로직을 거의 담지 않으면서 패시브 뷰( Passive View - 전적으로 "껍데기" 역할을 하는 뷰 )를 사용하는 것이다. MVP 모델은 MVC 모델과 대부분 구분이 되고, 어플리케이션 데이터를 다룬다. 표현자는 뷰와 모델 모두와 연계하는 중계자로 동작한다. 하지만 뷰와 모델은 서로 분리되어 있다. 표현자는 MVC에서 컨트롤러에 의해 수행되었듯이 모델을 뷰에 효과적으로 연결한다. 표현자는 MVP 패턴의 핵심이고 이미 알아차렸 듯이 뷰의 뒷단에서 표현 로직을 포함하고 있다.


뷰에 의해 요청받아서 표현자는 사용자 요청에 의해서 어떤 작업을 하고 사용자에게 데이타를 다시 돌려준다. 이러한 관점에서, 표현자는 데이타를 가져와서 조작하고 뷰에 어떻게 보여줄 지를 결정한다. 어떤 구현체들은 표현자가 데이타( 모델 )을 유지하는 서비스 계층과 연동하기도 한다. 모델은 이벤트를 일으키지만 표현자의 역할은 이벤트를 구독해서 뷰를 갱신할 수 있도록 하는 것이다. 이러한 수동적인 구조에서 우리는 직접적인 데이타 결합의 개념은 찾을 수 없다. 뷰는 표현자가 데이타를 설정하는데 쓰는 setter만을 외부에 노출한다.

MVC로부터 이런 변형의 잇점은 어플리케이션의 테스트 용이성을 증가시키고 뷰와 모델간의 더 명확한 분리를 제공한다는 것이다. 하지만 이것은 패턴에서 지원되는 데이타 결합의 부재가 종종 이 작업을 독립적으로 관리하는데 비용이 들게 한다.

[Passive View](http://martinfowler.com/eaaDev/PassiveScreen.html)의 공통적이 구현이 인터페이스를 구현한 뷰에 대한 것일지라도, 뷰를 표현자로부터 조금더 독립적으로 해주는 이벤트를 하는 것 같은 구현상의 차이가 있다. 자바스크립트에서 인터페이스 생성자가 없기 때문에, 우리는 여기에서 명시적인 인터페이스보다는 프로토콜은 훨씬 더 많이 사용할 것이다. 이런 방식도 여전히 API이고 그런 관점에서 우리가 그것을 인터페이스로 다루는 것은 아마 정당한 것일 것이다.


MVP의 변형으로 [Supervising Controller](http://martinfowler.com/eaaDev/SupervisingPresenter.html)도 있다. 그것은 MVC와 뷰에 모델을 직접즉으로 데이타 결합시키는 [MVVM](http://en.wikipedia.org/wiki/Model_View_ViewModel)패턴에 더 가깝다. (Derick Bailey가 만든 Backbone.ModelBinding 플러그인과 같은) 키-밸류 관찰(Key-value observing - KVO ) 플러그인은 Backbone에 Supervising Controller의 사상을 추가해준다.


## MVP냐 MVC냐?

보통 MVP는 가능한 많은 표현 로직을 재사용해야만 하는 엔터프라이즈 수준의 어플리케이션에서 자주 쓰인다. 복잡한 뷰와 많은 사용자 동작을 다루는 어플리케이션에서는 MVC는 여러개의 컨트롤러들에 무겁게 묶이는 문제를 풀기 위해 모든 조건을 만족시키지는 않는다. MVP에서 이러한 복잡한 로직 모두는 표현자로 감싸질 수 있다. 이러한 방식은 유지보수를 매우 단순화 시킬 수 있다.

MVP 뷰들이 인터페이스를 통해 정의되고 인터페이스는 기술적으로 시스템과 (표현자보다는)뷰의 유일한 연결점이기 때문에, 이 패턴도 개발자가 디자이너가 어플리케이션을 위한 레이아웃이나 그래픽을 만들기를 기다릴 필요없이 표현 로직을 작성하게 해준다.

MVP는 그 구현에 따라 MVC보다 단위 테스트가 더 손쉬워지기도 한다. 이점이 종종 언급되는 이유는 표현자가 사용자 인터페이스를 완전히 목킹(mocking)하고 그러한 점이 다른 컴포넌트와 독립적으로 단위 테스트를 할 수 있게 한다. 내 경험상 이점은 MVP를 구현한 언어에 따라 달라진다( 자바스크립트 프로젝트와 ASP.NET 프로젝트간에 꽤 큰차이가 있다 ).

결국, MVC와 MVP간에 차이는 주로 의미적인 것이라는 가정하에서 당신이 MVC에 대해 가지고 있던 기초 개념은 MVP에도 동일하게 적용될 것이다. 당신이 관심을 모델, 뷰, 컨트롤로( 혹은 표현자 )로 명확히 분리하는 한 선택한 패턴에 관계없이 동일한 이득을 얻을 수 있다.

## MVC, MVP 그리고 Backbone.js

많은 자바스크립트 개발자들은 MVC와 MVP를 상호배타적인 것으로 보지 않기 때문에 고전적인 형태로 MVC나 MVP를 구현했다고 하는 구조적인 자바스크립트 프레임워크가 있다 하더라도 거의 없을 것이다( 우리는 실제로 ASP.NET이나 GWT같은 웹 프레임워크를 볼 때 MVP가 엄격하게 구현되었다고 볼 것이다 ). 그 이유는 어플리케이션에 추가적인 표현자/뷰 로직을 추가하는 것이 가능하고 그것은 여전히 MVC의 특성으로 생각되기 때문이다.

Backbone 기여자인 [Irene Ros](http://ireneros.com/)는 Backbone의 뷰를 자신만의 독특한 컴포넌트로 분리할 때, 그것들을 실제로 구성하기 위한 뭔가를 해야한다고 생각한다고 말한다. 이것이 ( 이책 후반부에 다룰 ```Backbone.Router```같은) 우회하는 컨트롤러가 될 수도 있고 조회된 데이타에 대한 응답을 하는 콜백이 될 수도 있다.

즉, 어떤 개발자들은  Backbone.js는 MVC가 아니라 MVP의 설명이 더 잘 맞는다고 느낀다.
. 그들의 관점은 다음과 같다:

* MVP에서 표현자가 컨트롤러보다 ( 뷰의 템플릿과 그에 결합되는 데이타 사이 계층으로써 )
```Backbone.View```를 더 잘 표현한다
* 모델은 ```Backbone.Model```과 잘 맞는다 ( 고전적인 MVC "모델"과 차이가 없다 )
* 뷰가 가장 잘 표현하는 것은 템플릿이다( 예를 들어 Handlebars/Mustache과 같은 마크업 템플릿 ) 

이에 대한 답변은 Backbone은 다양한 목적을 위해 사용될 수 있을만큼 충분히 유연하기 때문에 뷰는 단순히 (MVC에서의) 뷰가 될수도 있다는 것이다. ```Backbone.View```는 두가지 목적을 수행할 수 있기 때문에MVC에서 V와 MVP에서 P 모두가 될 수 있다: 단일 컴포넌트를 그리는 것과 다른 뷰들에 의해 그련진 컴포넌트를 조립하는 것

우리는 또한 Backbone에서 컨트롤러의 연할이 Backbone.View와 Backbone.Router에서 시작하는 것도 알고 있고 다음 예제에서 그런 관점에서 확실히 사실이라는 것을 실제로 보게 될 것이다.

여기에서 우리의 Backbone ```TodoView```는 ```this.model.on('change',...)```가 있는 줄에서 뷰의 모델에 대한 변경을 "구독"하는 관찰자 패턴을 사용한다. 그것은 ```render()``` 메쏘드에서 템플릿팅을 제어하기도 하지만, 다른 구현에서와 달리 사용자 조작은 뷰에서도 처리된다( ```events```부분을 보자 ).


```javascript
// 할일 항목에 대한 DOM 객체...
app.TodoView = Backbone.View.extend({

  // list 태그
  tagName:  'li',

  // 할일에 대한 템플릿 내용을 템플릿 함수에 전달하고
  // 그것을 단일 할일 항목으로 캐시한다.
  template: _.template( $('#item-template').html() ),

  // 함목에 지정된 DOM 이벤트
  events: {
    'click .toggle':  'togglecompleted'
  },

  // TodoView는 다시 그리기 위해 그 모델에 대한 변경을 관찰한다. 
  // 이 어플리케이션에서 **Todo**와 **TOdoView**간에 일대일 일치가 있기 때문에
  // 우리는 편의를 위해 메델에 작접 설정한다.
  initialize: function() {
    this.model.on( 'change', this.render, this );
    this.model.on( 'destroy', this.remove, this );
  },

  // 할일 항목의 제목을 다시 그린다.
  render: function() {
    this.$el.html( this.template( this.model.toJSON() ) );
    return this;
  },

  // 모델의 "완료" 상태를 전환한다.
  togglecompleted: function() {
    this.model.toggle();
  },
});
```

(완전히 다른) 또 하나의 선택은 Backbone이 [Smalltalk-80 MVC](http://martinfowler.com/eaaDev/uiArchs.html#ModelViewController)(앞에서 살펴보았다)를 좀 더 비슷하게 흉내내도론 하는 것이다.

일반적인 사용자인 Derick Bailey이 [작성했던](http://lostechies.com/derickbailey/2011/12/23/backbone-js-is-not-an-mvc-framework/) 대로, Backbone이 어떤 특정 설계 패턴에 적합하도록 하지 않는 것이 궁극적으로는 최선이다. 설계 패턴은 어플리케이션이 어떻게 구조화되어야 하는가에 대한 유연한 안내여만하고 이런 관점에서 Backbone은 MVC나 MVP와 완벽하게 맞아 떨어지지 않는다. 대신 Backbone은 여러개의 구조적 패턴에서 좋은 개념 몇몇을 차용해서 그저 잘 돌아가는 유연한 프레임워크를 만든 것이다. 그것을 **Backbone 방식**, MV* 그도 아니면 어플리케이션 구조의 특성을 잘 지칭하는 어떤 것으로 불러도 상관없다.

하지만, 이들 개념이 어디서 왜 나왔는지 이해할 가치가 *있기* 때문에, MVC와 MVP에 관한 설명이 도움이 되길 바란다. 대부분의 구조화된 자바스크립트 프레임워크는 의도적이든 우연이든 고전적인 패턴에서 가져온 자신만의 것을 채택하지만, 중유한 것은 그것들이 우리가 복잡하고 깨끗하고 쉽게 유지보수할 수 있는 어플리케이션을 개발하는데 도움이 될 것이라는 것이다.


## 최근의 사실들

### Backbone.js

* 주요 컴포넌트: 모델, 뷰, 컬렉션, 라우터. MV*의 자신만의 특성을 갖도록 한다.
* SoundCloud와 Foursquare갈은 큰 회사에서 일반적이지 않는 어플리케이션을 만드는데 사용된다.
* 뷰와 모델간의 이벤트-드리븐 통신. 알다시피 개발자에게 뷰에서의 발생한 것에 대한 상세한 제어를 준다면 모델의 어떤 특성에 이벤트 리스너를 다는 것은 상대적으로 직관적이다.
* 수동 이벤트를 통해 데이타 결합을 지원한다. 혹은 따로 키-밸류 감시(KVO) 라이브러리를 지원한다.
* REST API를 인터페이스적으로 지원해서 모델이 서버쪽과 쉽게 연동되도록 한다.
* 확장가능한 시스템이다. Backbone에서 발행/구독을 지원하도록 추가하는 것은 [당연](http://lostechies.com/derickbailey/2011/07/19/references-routing-and-the-event-aggregator-coordinating-views-in-backbone-js/)한 일이다.
* 클래스 원형은 ```new``` 키워드를 사용해서 객체로 생성할 수 있고, 그런 방식을 선호하는 개발자들이 있다.
* 템플릿팅 프레임워크를 알지못해도, Underscore의 마이크로-템플릿팅을 기본적으로 사용할 수 있다. Backbone은 Handlebars와 같은 라이브러리와 잘 동작한다.
* [Backbone-relational](https://github.com/PaulUithol/Backbone-relational)과 같은 플러그인이 잘 도와준다고는 하지만 중첩된 모델을 잘 지원하지는 않는다.
* 어플리케이션을 구조화하는데 명확하고 편리하다. Backbone은 컴포넌트 전체를 사용할 필요는 없고 필요에 따라서만 사용할 수 있다.



# 내부


이 센셕에서 당신은 Backbone의 모델, 뷰, 컬렉션 그리고 라우터의 핵심뿐만 아니라 당신의 코드를 결합하는 namespace를 이용하는 것에 대해서 배울 것이다. 이문서가 정규문서를 대체한다는 뜻은 아니지만, 당신이 Backbone으로 어플리케이션을 만들기 전에 핵심 개념의 다수를 이해하는데 도움이 될 것이다.

* 모델
* 컬렉션
* 라우터
* 뷰
* 의존성
* 네임스페이싱


## 모델

Backbone 모델은 어플리케이션을 위한 상호작용하는 데이타들 뿐만 아니라 이 데이타와 관련된 로직들도 담고 있다. 예를들어, 우리는 제목( 할일 내용 )과 완료( 할일의 현재 상태 ) 속성을 가지고 있는 할일 항목의 개념을 표현하기 위해 모델을 사용할 수 있다.

모델은 다음과 같이 `Backbone.Model`을 확장해서 만들 수 있다.

```javascript
var Todo = Backbone.Model.extend({});

// 이제 우리는 전혀 속성값을 가지고 있지않은
// Todo 모델의 실제 객체를 생성할 수 있다.
var todo1 = new Todo();
console.log(todo1);

// 아니면 임의의 데이타를 가진 객체를 생성할 수 있다.
var todo2 = new Todo({ 
  title: 'Check attributes property of the both model instances in the console.', 
  completed: true
});
console.log(todo2);
```

#### 초기화

`initialize()`메쏘드는 모델의 새로운 객체가 생성될 때 호출된다. 메쏘드 구현은 선택이지만 아래에서 사용하는 것이 좋은 이유를 알게될 것이다.

```javascript
var Todo = Backbone.Model.extend({
  initialize: function(){
      console.log('This model has been initialized.');
  }
});

var myTodo = new Todo();
```

**기본 값**

당신은 모델이 기본값을 갖게 하고 싶을 때가 있다( 예를 들어 사용자가 완전한 데이타 셋을 주지않을 경우 ). 이것은 모델에 `defaults`라고 하는 특성을 사용해서 설정할 수 있다.

```javascript
var Todo = Backbone.Model.extend({
  // 할일 속성의 기본값들
  defaults: {
    title: '',
    completed: false
  }
});

// 이제 아래와 같이 기본값을 가진
// 객체를 생성할 수 있다.
var todo1 = new Todo();
console.log(todo1);

// 혹은 ( 예를 들어 ) 속성 일부를 가지고 객체를 생성할 수도 있다.
var todo2 = new Todo({ 
  title: 'Check attributes property of the logged models in the console.'
});
console.log(todo2);

// 그도 아니면 (기본) 속성 전체를 가지고 생성할 수 있다.
var todo3 = new Todo({
  title: 'This todo is done, so take no action on this one.',
  completed: true
});
console.log(todo3);
```

#### Getters & Setters

**Model.get()**

`Model.get()`은 모델 속성에 쉬운 접근법을 제공한다. 객체화된 모델을 통해 기본값이 전달되면 모든 속성을 조회할 수 있다.

```javascript
var Todo = Backbone.Model.extend({
  // 할일 속성의 기본값들
  defaults: {
    title: '',
    completed: false
  }
});

var todo1 = new Todo();
console.log(todo1.get('title')); // 빈 문자열
console.log(todo1.get('completed')); // false

var todo2 = new Todo({
  title: "Retrieved with models get() method.",
  completed: true
});
console.log(todo2.get('title')); // 모델의 get() 메쏘드로 조회한다.
console.log(todo2.get('completed')); // true
```

모델의 데이타 속성 전체를 읽거나 복제할 필요가 있다면 `toJSON` 메쏘드를 사용해라. 그 이름에도 불구하고 JSON문자열이 아니라 속성의 복제본을 객체로 반환한다( "toJSON"는 JSON.stringify 스펙의 일부분이다. toJSON 메쏘드를 가진 객체를 전달하는 것이 객체 자체 대신에 그 메쏘드의 반환값을 문자열화해준다.).

```javascript
var Todo = Backbone.Model.extend({
  // 할일 항목의 기본값들
  defaults: {
    title: '',
    completed: false
  }
});

var todo1 = new Todo();
var todo1Attributes = todo1.toJSON();
// 다음 출력: {"title":"","completed":false} 
console.log(todo1Attributes);

var todo2 = new Todo({
  title: "Try these examples and check results in console.",
  completed: true
});
// 출력: {"title":"Try examples and check results in console.","completed":true}
console.log(todo2.toJSON());
```

**Model.set()**

`Model.set()`은 속성을 모델 객체에 전달하게 해준다. 속성은 초기화할 때나 그이후 언제라도 설정할 수 있다. Backbone은 모델의 데이타가 변경되었음을 언제 알려야 할지 알기 위해 Model.set()를 사용한다.

```javascript
var Todo = Backbone.Model.extend({
  // 할일 항목의 기본값들
  defaults: {
    title: '',
    completed: false
  }
});

// 객체 생성을 통한 속성값 지정
var myTodo = new Todo({ 
  title: "Set through instantiation." 
});
console.log('Todo title: ' + myTodo.get('title'));
console.log('Completed: ' + myTodo.get('completed'));

// Model.set()를 통해 한번에 하나의 속성을 지정한다:
myTodo.set("title", "Title attribute set through Model.set().");
console.log('Todo title: ' + myTodo.get('title'));
console.log('Completed: ' + myTodo.get('completed'));

// Model.set()을 통해 속성 맵을 설정한다:
myTodo.set({ 
  title: "Both attributes set through Model.set().",
  completed: true
});
console.log('Todo title: ' + myTodo.get('title'));
console.log('Completed: ' + myTodo.get('completed'));
```

**직접 접근**

만약 모델 객체의 속성들을 직접 접근할 필요가 있다면, `Model.attributes`가 있다. 하지만 위에서 설명한대로 Model.get(), Model.set()이나 직접 초기화가 가장 좋은 사용법임을 기억하라.

#### 모델의 변경을 관찰

Backbone 모델에서 어떤 혹은 전체 속성은 그 값이 변경될 때 감지하는 리스너들을 가질 수 있다. 리스너들은 `initialize()` 함수에서 추가될 수 있다.

```javascript
var Todo = Backbone.Model.extend({
  // 할일 함목의 기본값
  defaults: {
    title: '',
    completed: false
  },
  initialize: function(){
    console.log('This model has been initialized.');
    this.on('change', function(){
        console.log('- Values for this model have changed.');
    });
  }
});

var myTodo = new Todo();

myTodo.set('title', 'On each change of attribute values listener is triggered.');
console.log('Title has changed: ' + myTodo.get('title'));

myTodo.set('completed', true);
console.log('Completed has changed: ' + myTodo.get('completed'));

myTodo.set({
  title: 'Listener is triggered for each change, not for change of the each attribute.',
  'complete': true
});
```

다음 예제에서, 우리는 특정 속성( Todo모델의 제목 )이 바뀔 때, 메시지를 출력한다.

```javascript
var Todo = Backbone.Model.extend({
  // 할일 항목의 기본값
  defaults: {
    title: '',
    completed: false
  },
  initialize: function(){
    console.log('This model has been initialized.');
    this.on('change:title', function(){
        console.log('Title value for this model have changed.');
    });
  },
  setTitle: function(newTitle){
    this.set({ title: newTitle });
  }
});

var myTodo = new Todo();

// 다음의 변경은 리스너를 동작시킨다.
myTodo.set('title', 'Check what\'s logged.');
myTodo.setTitle('Go fishing on Sunday.');

// 하지만, 이 변경은 감시되지 않아서 어떤 리스너도 동작하지 않는다.
myTodo.set('completed', true);
console.log('Todo set as completed: ' + myTodo.get('completed'));
```

#### 값의 검증

Backbone은 `Model.validate()`을 통해 모델의 검을을 지원하는데, 속성이 모델에 설정되기 전에 값을 확인하도록 한다.

검증 함수는 필요에 따라 단순할 수도 있고 복잡할 수도 있다. 주어진 속성이 올바르면, `.validate()`에서 아무것도 반환되지 않을 것이다. 대신에 올바르지 않으면, 사용자 정의 에러가 반환된다.

검증에 관한 기본적인 예제는 아래에서 볼 수 있다.

```javascript
var Todo = Backbone.Model.extend({
  validate: function(attribs){
    if(attribs.title === undefined){
        return "Remember to set a title for your todo.";
    }
  },

  initialize: function(){
    console.log('This model has been initialized.');
    this.on("error", function(model, error){
        console.log(error);
    });
  }
});

var myTodo = new Todo();
myTodo.set('completed', false); // 출력: Remember to set a title for your todo.
```

**메모**: Backbone은 Underscore의 `_.extend` 메쏘드를 사용해서 얕은 복제된 `속성들`( 위의 예제에서 attribs 인자 )을 `validate`에게 인자로 넘긴다. 이것은 어떤 숫자, 문자, 참/거짓 속성을 바꿀 수 없지만, 레퍼런스로 넘어온 객체 속성은 바꿀수 *있다*는 것을 의미한다. 얕은 복제는 내부까지 복사하는 방신이 아니기 때문에, 그 객체의 손성들을 바꿀 수 있다.

이 예제(by @fivetanley)는 [여기](http://jsfiddle.net/2NdDY/7/)에서 볼 수 있다.


## 뷰

Backbone에서 뷰는 어플리케이션을 위한 마크업을 포함하지 않지만, 대신 사용자에게 어떻게 보여져야 하는지에 대한 로직을 정의함으로써 모델을 지원한다. 이 작업은 자바스크립트 템플릿팅( 예를들어 Mustache, jQuery-tmpl 등 )을 사용해서 보통 수행된다. 뷰의 `render()` 함수는 전체 페이지를 갱신할 필요없이 항상 최신의 상태로 유지하기 위해 모델의 `change()` 이벤드에 바인딩될 수 있다.


#### 새로운 뷰 생성하기

이전 섹션과 유사하게, 새로운 뷰를 생성하는 것은 상대적으로 간단하다. 새로운 뷰를 만들기 위해서, 단순히 `Backbone.View`를 확장(extend)해라. 아래에서 코드로 상세히 설명할 것이다.

```javascript
var TodoView = Backbone.View.extend({

  tagName:  'li',

  // 단인 항목에 대한 템플릿 함수를 캐쉬한다.
  todoTpl: _.template( $('#item-template').html() ),

  events: {
    'dblclick label': 'edit',
    'keypress .edit': 'updateOnEnter',
    'blur .edit':   'close'
  },

  // 할일 항목의 제목을 다시 그린다.
  render: function() {
    this.$el.html( this.todoTpl( this.model.toJSON() ) );
    this.input = this.$('.edit');
    return this;
  },

  edit: function() {
    // 할일의 제목을 더블 클릭했을 때 수행된다
  },

  close: function() {
    // 할일이 포커스를 잃었을 때 수행된다.
  },

  updateOnEnter: function( e ) {
    // 할일이 편집 모드에서 키가 눌릴 때 마다 수행된다
    // 하지만 우리는 동작을 위해 엔터를 기다릴 것이다
  }
});

var todoView = new TodoView();

// 뷰 인스턴스에 대응되는 DOM 요소의 레퍼런스를 출력한다.
console.log(todoView.el);
```

#### `el`은 무엇인가?

`el`은 기본적으로 DOM 요소의 레퍼런스이고 모든 뷰들이 하나씩 가져야만 한는 것이다. 그것은 뷰의 모든 내용이 DOM에 한번에 들어가도록 해준다. 그런 방식은 브라우져가 새로 배치하고 새로 그리는 것을 최소화하기 때문에 좀더 빠른 렌더링을 하게 해준다.

DOM 요소를 뷰에 붙이는 두가지 방법이 있다: 뷰를 위한 새로운 요소를 생성해서 개발자가 직접 추가하는 방법이나 패이지에 이미 존제하는 것을 추가하는 방법

만일 뷰에 새로운 요소를 추가하고 싶으면, 다음의 뷰 속성을 조합해서 지정해라: `tagName`, `id` 그리고 `className`. 프레임워크가 새로운 요소를 생성해서 요소의 레퍼런스를 `el` 특성에 가용하도록 해줄 것이다. 지정된 것이 없으면 `el`은 기본적으로 `div`이다.

```javascript
var TodosView = Backbone.View.extend({
  tagName: 'ul', // 필수값, 지정하지 않으면 'div'이 된다.
  className: 'container', // 부가값, 'container homepage'와 같이 이 특성에는 여러 개의 클래스들을 할당할 수 있다
  id: 'todos', // 부가값
});

var todosView = new TodosView();
console.log(todosView.el);
```

위의 코드는 아래의 ```DOMElement```를 생성하지만 DOM에 추가하지는 않는다.

```html
<ul id="todos" class="container"></ul>
```

요소가 페이지에 이미 존재한다면, 당신은 `el`을 그 요소에 맞는 CSS 선택자로 지정할 수 있다.

```javascript
el: '#footer'
```

**`render()` 이해하기**

`render()`는 템플릿을 렌더링하기 위한 로직을 정의하는 부가적인 함수이다. 우리는 예제에서 Underscore의 마이크로-템플릿팅을 사용할 것이지만, 선호하는 다른 템플릿 프레임워크가 있다면 그것을 쓸 수도 있다는 점을 기억하라.

Underscore에서 `_.template` 메쏘드는 자바스크립트 템플릿을 렌더링을 수행할 수 있는 함수로 컴파일한다. 위의 뷰에서, 나는 아이디가 `item-template`인 템플릿의 마크업을 컴파일하기 위해 `_.template()`에 전달했다. 그다음에 나는 `el` DOM 요소의 html을 컴파일된 템플릿을 통해 뷰와 연결된 모델의 JSON버젼을 처리한 결과에게 넘겼다.

이런 방식은 당신에게 마크업의 데이타들이 주어졌을 때, 단 몇줄의 코드로 빠르게 템플릿을 적용하게 한다.

**`이벤트` 속성**

Backbone의 `events` 속성은 사용자 정의 선택자나 주어진 선택자가 없으면 `el`에 직접적으로 이벤트 리스너를 붙이게 해준다. 이벤트는 `{'eventName selector': 'callbackFunction'}`같은 형태를 가지고 `click`, `submit`, `mouseover`, `dblclick`를 포함해서 많은 DOM 이벤트 종류를 지원한다.

내부에서 Backbone은 이벤트 위임을 즉각적으로 지원하기 위해 jQuery의 `.delegate()`를 사용하지만, 좀더 확장해서 `this`는 항상 현재의 뷰 객체를 가리키는 것이 명확하지 않다. 꼭 기억해야 할 것은 이벤트 속성에 지정된 어떤 문자열 콜백이라도 뷰내에 같은 이름으로 대응되는 함수가 있어야 한다는 것이다.


## 컬렉션

컬렉션은 모델의 집합이고 `Backbone.Collection`을 확장해서 만든다.

보통은, 컬렉션을 생성할 때 컬렉션에 담고 싶은 모델을 지정한 특성뽄만 아니라 필요한 객체 특성도 전달하고 싶을 것이다.

다음 예제에서, 우리는 Todo 모델을 담을 TodoCollection을 생성한다.

```javascript
var Todo = Backbone.Model.extend({
  defaults: {
    title: '',
    completed: false
  }
});

var TodosCollection = Backbone.Collection.extend({
  model: Todo,
  localStorage: new Store('todos-backbone')  
});

var myTodo = new Todo({title:'Read the whole book', id: 2});

// 컬렉션 객체에 모델의 배열을 전달한다.
var todos = new TodosCollection([myTodo]);
console.log("Collection size: " + todos.length);

// 컬렉션안에서 새로운 모델 객체를 생성하는데
// 쓰이는 컬렉션의 편의 메쏘드
todos.create({title:'Try out code examples', id: 48});
console.log("Collection size: " + todos.length);
```

**Getters 와 Setters**

컬렉션에서 모델들에 접근하는 몇가지 방법들이 있다. 가장 직접적인 것은 아래와 같이 단일 아이디를 받는 `Collection.get()`을 사용하는 것이다.

```javascript
// 앞의 예제에 이어서

var todo2 = todos.get(2);

// 모델은 객체로서 레퍼런스가 넘어간다.
console.log(todo2 === myTodo);
```

내부적으로 `Backbone.Collection`은 모델이 가지고 있다면 모델의 `아이디`에 의해 열거되는 모델의 배열을 설정한다. `collection.get(id)`이 불리기만 하면, 일치하는 `id`를 가진 모델 객체가 있는지 이 배열을 확인한다.

당신은 때때, 클라이언트의 아이디에 기반해서 모델을 얻고 싶을 때도 있다. 클라이언트 아이디는 Backbone이 아직 저장되지 않은 모델에 자동으로 할당하는 특성이다. 당신은 모델에서 `.cid` 특성에서 클라이언트 아이디를 얻을 수 있다.

```javascript
// 앞의 예제에 이어서

var todoCid = todos.get(todo2.cid);

// 앞의 예제에서 언급한 대로
// 모델은 레퍼런스로 전달된다.
console.log(todoCid === myTodo); 
```

Backbone의 컬렉션은 setter를 가지지 않지만 `.add()`를 통해 새로운 모델을 추가하고 `.remove()`를 통해 모델을 제거하도록 지원해준다.

```javascript
var Todo = Backbone.Model.extend({
  defaults: {
    title: '',
    completed: false
  }
});

var TodosCollection = Backbone.Collection.extend({
  model: Todo,
  localStorage: new Store('todos-backbone')  
});

var a = new Todo({ title: 'Go to Jamaica.'}),
    b = new Todo({ title: 'Go to China.'}),
    c = new Todo({ title: 'Go to Disneyland.'});

var todos = new TodosCollection([a,b]);
console.log("Collection size: " + todos.length);

todos.add(c);
console.log("Collection size: " + todos.length);

todos.remove([a,b]);
console.log("Collection size: " + todos.length);

todos.remove(c);
console.log("Collection size: " + todos.length);
```

**이벤트에 대한 감시**

컬렉션이 항몪의 묶음을 표현하기 때문에, 우리는 새로운 모델이 추가되거나 컬력션에서 제거될 때, `add`와 `remove`에 대해 감시할 수도 있다. 여기 예제가 있다:

```javascript
var TodosCollection = new Backbone.Collection();

TodosCollection.on("add", function(todo) {
  console.log("I should " + todo.get("title") + ". Have I done it before? "  + (todo.get("completed") ? 'Yeah!': 'Not.' ));
});

TodosCollection.add([
  { title: 'go to Jamaica.', completed: false },
  { title: 'go to China.', completed: false },
  { title: 'go to Disneyland.', completed: true }
]);
```

또한, 우리는 컬렌션내의 모델에 대한 변경을 강시하는 `change` 이벤트를 바인딩할 수 있다.

```javascript
var TodosCollection = new Backbone.Collection();

TodosCollection.on("change:title", function(model) {
    console.log("Changed my mind where I should go, " + model.get('title'));
});

TodosCollection.add([
  { title: 'go to Jamaica.', completed: false, id: 3 },
]);

var myTodo = TodosCollection.get(3);

myTodo.set('title', 'go fishing');
```

**서버에서 모델 가져오기**

`Collections.fetch()`는 서버에서 기본 모델들을 JSON 배열의 형태로 조회한다. 데이타가 반환될 때, 현재 컬렉션의 내용은 그 배열의 내용으로 대체될 것이다.


```javascript
var TodosCollection = new Backbone.Collection;
TodosCollection.url = '/todos';
TodosCollection.fetch();
```

설정에서, Backbone은 서버가 확장된 HTTP 메쏘드를 지원하는지를 표시하는 변수를 지정한다. 다른 설정은 서버가 JSON을 위한 올바른 MIME을 이해하는지를 제어한다:

```javascript
Backbone.emulateHTTP = false;
Backbone.emulateJSON = false;
```

이런 값을 사용하는 Backbone.sync 메쏘드는 실제로 Backbone.js의 중요한 부분이다. jQuery같은 ajax 메쏘드를 가정됬었기 때문에, HTTP 파라미터는 jQuery의 API에 기초해서 구성되었다. 코드에서 sync 메쏘드가 호출되는 것을 찾아보면 모델이 저장되고 조회되고 삭제(제거)될 때 사용됨을 알 수 있다.

`Backbone.sync`는 Backbone이 모델을 서버에서 읽거나 쓸려고 할 때마다 내부적으로 호출되는 함수이다. RESTful 요청을 만들기 위해 jQuery나 Zepto의 ajax 구현을 사용하지만 필요에 따라 덮어써질 수 있다.

동기화 함수는 전체에 대해서는 Backbone.sync으로 덮어 쓸 수 있고, 그렇지않고 세부적으로는 Backbone 컬렉션이나 각 모델에 syn함수를 추가해서 덮어 쓸 수 있다.

데이터 유지(persistence) 계층을 추가하는 좋은 플러그인은 없다 - 그냥 Backbone.sync를 같은 함수 시그너쳐로 덮어써라:

```javascript
Backbone.sync = function(method, model, options) {
};
```

method 인자가 무엇을 하는지 연습하기에는 기본 methodMap가 유용하다.

```javascript
var methodMap = {
  'create': 'POST',
  'update': 'PUT',
  'delete': 'DELETE',
  'read':   'GET'
};
```

위의 예제에서 `.sync()`가 호출될 때, 이벤트를 출력하고 싶으면 다음과 같이 할 수 있다:

```javascript
var id_counter = 1;
Backbone.sync = function(method, model) {
  console.log("I\'ve been passed " + method + " with " + JSON.stringify(model));
  if(method === 'create'){ model.set('id', id_counter++); }
};
```


**컬렉션을 초기화하기/갱신하기**

때로는 모델을 각각 추가하거나 삭제하는 것보다 전체 컬렉션을 한번에 갱신하고 싶을 때가 있을 것이다. ```Collection.reset()```은 다음과 같이 우리가 새로운 모델들로 전체 컬렉션을 대체하도록 해준다:

```javascript
var TodosCollection = new Backbone.Collection();

TodosCollection.on("reset", function() {
  console.log("Collection reseted.");
});

TodosCollection.add([
  { title: 'go to Jamaica.', completed: false },
  { title: 'go to China.', completed: false },
  { title: 'go to Disneyland.', completed: true }
]);

console.log('Collection size: ' + TodosCollection.length);

TodosCollection.reset([
  { title: 'go to Cuba.', completed: false }
]);
console.log('Collection size: ' + TodosCollection.length);
```

`Collection.reset()`을 사용하는 것은 어떤 `add`나 `remove` 이벤트를 발생시키지 않는 것을 알아야 한다. 대신 예제에서처럼 `reset` 이벤트가 발생된다.

### Underscore 유틸리티 함수

Backbone은 Underscore를 직접적으로 필요로 하기 때문에, 우리는 어플리케이션 개발을 위해 제공되는 많은 유틸리티를 사용할 수 있다. 여기에 컬렉션을 순회하는데 사용될 수 있는 Underscore의 `forEach`와 특정 속성에 따라 할일 컬렉션을 정렬하는데 사용할 수 있는 `sortBy()`의 사용법이 있다.

```javascript
var TodosCollection = new Backbone.Collection();

TodosCollection.on("reset", function() {
  console.log("Collection reseted.");
});

TodosCollection.add([
  { title: 'go to Belgium.', completed: false },
  { title: 'go to China.', completed: false },
  { title: 'go to Austria.', completed: true }
]);

TodosCollection.forEach(function(model){
  console.log(model.get('title'));
});

var sortedByAlphabet = TodosCollection.sortBy(function (todo) {
    return todo.get("title").toLowerCase();
});

console.log("- Now sorted: ");

sortedByAlphabet.forEach(function(model){
  console.log(model.get('title'));
});
```

Underscore가 할 수 있는 전체 목록은 이 문서의 범위를 벗어나서 다루지 않지만, Underscore의 정규 [문서](http://documentcloud.github.com/underscore/)에서 찾을 수 있다.


### 연속해서 호출 가능한 API

유틸리트 메쏘드에 대해 말할 때, Backbone에서 또 다른 작은 장점은 Underscore의 체인 메쏘드를 지원하는 것이다. 이것은 현재 모델 배열로 원래의 메쏘드를 불러서 그 결과를 반환하는 방식으로 동작한다. 이러한 것을 전에 본적이 없다면, 다음에서 볼 수 있다.

```javascript
var collection = new Backbone.Collection([
  { name: 'Tim', age: 5 },
  { name: 'Ida', age: 26 },
  { name: 'Rob', age: 55 }
]);

var filteredNames = collection.chain()
  .filter(function(item) { return item.get('age') > 10; })
  .map(function(item) { return item.get('name'); })
  .value();

console.log(filteredNames); // 출력: ['Ida', 'Rob']
```

Backbone 특화된 어떤 메쏘드들은 this를 반환하는데, 이것은 그것들끼리 잘 연결될 수 있음을 의미한다:

```javascript
var collection = new Backbone.Collection();

collection
    .add({ name: 'John', age: 23 })
    .add({ name: 'Harry', age: 33 })
    .add({ name: 'Steve', age: 41 });

var names = collection.pluck('name');

console.log(names); // 출력: ['John', 'Harry', 'Steve']
```

## 이벤트


우리가 알아본 것처럼, `Backbone.Events`는 다음의 다른 Backbone "클래스"에 합쳐진다.

* Backbone.Model
* Backbone.Collection
* Backbone.Router
* Backbone.History
* Backbone.View

이벤트는 뷰뿐만 이나라 모델과 컬렉션의 변경에 선언적인 이벤트를 바인딩함으로써 사용자 인터페이스의 동작을 다루는 표준적인 방법이다. 이벤트를 정복하는 것이 Backbone을 사용해서 더 생산적이게 되는 가장 빠른 길 중에 하나이다.

`Backbone.Events`도 어떤 객체에 사용자 정의 이벤트를 바인딩하는 능력을 가지고 있다. 우리는 이 모듈을 어떤 객체에 쉽게 넣을 수도 있고, 이벤트가 바인딩되기 전에 선언될 필요도 없다.

예제:

```javascript
var ourObject = {};

// Mixin
_.extend(ourObject, Backbone.Events);

// 사용자 이벤트를 추가한다.
ourObject.on('dance', function(msg){
  console.log('We triggered ' + msg);
});

// 사용자 이벤트를 발동한다.
ourObject.trigger('dance', 'our event');
```

만일 jQuery의 사용자 이벤트나 발행/구독의 개념에 익숙하다면, `Backbone.Events`는 `구독`과 매우 유사한 `on`과 `발행`과 유사한 `trigger`과 비슷한 시스템을 제공한다.

위의 예제에서 우리가 `dance`로 했던 것처럼 기본적으로 `on`은 우리가 어떤 객체에 콜백 함수를 바인딩하게 해준다. 이벤트가 구동되면, 콜백이 호출된다.

페이지에서 꽤 이벤트를 사용하게 된다면, Backbone.js의 정구 문서는 콜론을 사용해서 이벤트 이름을 구분하도록 추천한다. 예제:

```javascript
var ourObject = {};

// Mixin
_.extend(ourObject, Backbone.Events);

function dancing (msg) { console.log("We started " + msg); }

// 이름 구분이 된 사용자 이벤트들을 추가한다.
ourObject.on("dance:tap", dancing);
ourObject.on("dance:break", dancing);

// 사용자 이벤트들을 구동한다.
ourObject.trigger("dance:tap", "tap dancing. Yeah!");
ourObject.trigger("dance:break", "break dancing. Yeah!");

// 이것은 감시하는 리스너가 없기 때문에 아무것도 발동시키지 않는다.
ourObject.trigger("dance", "break dancing. Yeah!");
```

`all`이라는 이벤트는 특별히 어떤 이벤트가 발생했을 때, 이벤트가 구동되도록 하고 싶은 경우에 사용하도록 만들어졌다( 예를 들어, 단일 지점에서 이벤트를 출력하고 싶은 경우 ). `all` 이벤트는 다음과 같이 사용할 수 있다.


```javascript
var ourObject = {};

// Mixin
_.extend(ourObject, Backbone.Events);

function dancing (msg) { console.log("We started " + msg); }

ourObject.on("all", function(eventName){
  console.log("The name of the event passed was " + eventName);
});

// 각 이벤트가 잡힐 때마다 'all' 이벤트 리스너를 호출할 것이다.
ourObject.trigger("dance:tap", "tap dancing. Yeah!");
ourObject.trigger("dance:break", "break dancing. Yeah!");
ourObject.trigger("dance", "break dancing. Yeah!");
```

`off`는 우리가 객체에 이전에 붙였던 콜백 함수를 제거하게 해준다. 발행/구독과 다시 비교해서 사용자 이벤트의 `unsubscribe`로 생각해라.

`ourObject`에 이전에 붙였던 `dance` 이벤트를 제거하기 위해, 단순히 이렇게 한다:

```javascript
var ourObject = {};

// Mixin
_.extend(ourObject, Backbone.Events);

function dancing (msg) { console.log("We  " + msg); }

// 이름으로 구분된 사용자 이벤트를 추가한다
ourObject.on("dance:tap", dancing);
ourObject.on("dance:break", dancing);

// 사용자 이벤트를 발동한다. 각각은 리스너가 잡아서 동작한다.
ourObject.trigger("dance:tap", "started tap dancing. Yeah!");
ourObject.trigger("dance:break", "started break dancing. Yeah!");

// 객체에 붙은 이벤트를 제거한다.
ourObject.off("dance:tap");

// 사용자 이벤트를 다시 발동하지만 하나는 출력이 되지 않는다.
ourObject.trigger("dance:tap", "stopped tap dancing."); // 감시되고 있지 않기 때문에 출력되지 않는다.
ourObject.trigger("dance:break", "break dancing. Yeah!");
```

이벤트에 대한 모든 콜백을 제거하기 위해 우리는 단지 이벤트 이름( 예를 들어 `move` )을 이벤트가 붙어있는 객체의 `off()` 함수에 전달한다. 우리가 특정 이름의 콜백만을 제거하고 싶으면, 두번째 이름으로 콜백 이름을 전달할 수 있다:

```javascript
var ourObject = {};

// Mixin
_.extend(ourObject, Backbone.Events);

function dancing (msg) { console.log("We are dancing. " + msg); }
function jumping (msg) { console.log("We are jumping. " + msg); }

// 동일한 이벤트에 두개의 리스너를 추가한다
ourObject.on("move", dancing);
ourObject.on("move", jumping);

// 이벤트를 구동한다. 두개의 리스너가 호출된다.
ourObject.trigger("move", "Yeah!");

// 특정 리스너를 제거한다.
ourObject.off("move", dancing);

// 이벤트를 다시 구동한다. 하나의 리스너만 남아있다.
ourObject.trigger("move", "Yeah, jump, jump!");
```

결국, `trigger`는 특정 이벤트( 혹은 공백으로 구분된 이벤트 목록 )에 대한 콜백을 호출한다. 예제:

```javascript
var ourObject = {};

// Mixin
_.extend(ourObject, Backbone.Events);

function doAction (msg) { console.log("We are " + msg); }

// 이벤트 리스너들을 추가한다
ourObject.on("dance", doAction);
ourObject.on("jump", doAction);
ourObject.on("skip", doAction);

// 단일 이벤트
ourObject.trigger("dance", 'just dancing.');

// 복수 이벤트
ourObject.trigger("dance jump skip", 'very tired from so much action.');
```

`trigger`에 의해 지원되는 두번째 인자를 통해서 이벤트들의 각각( 모두 )에 추가 인자를 전달하는 것도 가능하다. 예제:

```javascript
var ourObject = {};

// Mixin
_.extend(ourObject, Backbone.Events);

function doAction (actionObj) {
  console.log("We are " + actionObj.action + ' for ' + actionObj.duration ); 
}

// 이벤트 리스너들을 추가한다
ourObject.on("dance", doAction);
ourObject.on("jump", doAction);
ourObject.on("skip", doAction);

// 단일 이벤트에 여러개의 인자를 전달한다.
ourObject.trigger("dance", {duration: "5 minutes", action: 'dancing'});

// 복수 이벤트에 여러가의 인자를 전달한다.
ourObject.trigger("dance jump skip", {duration: "15 minutes", action: 'on fire'});
```

## 라우터

Backbone에서 라우터는 어플리케이션 상태를 관리하고 어플리케이션 이벤트에 URL을 연결하기 위해 사용된다. 이것은 URL 조각으로 해쉬 태그를 사용하거나 브라우져의 pushState나 히스토리 API를 사용해서 수행된다. 라우터의 몇몇 예제를 아레에서 볼 수 있다:

```javascript
http://example.com/#about
http://example.com/#search/seasonal-horns/page2
```

메모: 어플리케이션은 보통 사용자가 특정 지점에 도달했을 때 무엇을 해야할지 결정하는 URL에 해당하는 적어도 하나의 경로를 가지고 있을 것이다. 이 관계는 다음과 같다.

```javascript
'route' : 'mappedFunction'
```

이제 우리는 `Backbone.Router`를 확장한 첫번째 라우터를 정의해보자.  이 안내서를 위해, 앞의 예제에 이어서 복잡한 TodoRouter를 필요로 하는 복잡한 할일 어플리케이션( 개인 다이어리같은 것 )을 만든다고 가정할 것이다.

우리가 라우터에 대한 단원의 나머지를 계속하기 위해서 아래 예제 코드의 주석을 주의깊게 봐라.

```javascript
var TodoRouter = Backbone.Router.extend({
    /* 이 라우터를 위한 지점과 함수의 맵을 정의한다. */
    routes: {
        "about" : "showAbout",
        /* 사용 예제: http://example.com/#about */

        "todo/:id" : "getTodo",
        /* 이것은 두 URL의 ( /로 구분된 ) 조각 사이에 어떤 컴포넌트와 일치하는
		":param" 변수를 사용하는 예제이다 */
        /* 사용 예제: http://example.com/#todo/5 */

        "search/:query" : "searchTodos",
        /* 우리는 동일한 함수에 맵핑되는 여러개의 지점을 정의할 수도 있고,
        이 경우에는 searchTodos()이다. 아래에서 우리가 인자를 주면 페이지 숫자가
		레퍼런스로 넘어가는 것을 주목해서 보라 */
        /* 사용 예제: http://example.com/#search/job */

        "search/:query/p:page" : "searchTodos",
        /* 알다시피, URL은 원하는 만큼 ":param"을 포함할 수 있다 */
        /* 사용 예제: http://example.com/#search/job/p1 */

        "todos/:id/download/*documentPath" : "downloadDocument",
        /* 이번에는 *splat을 사용한 예제이다. Splat은 다수의 URL 조각과
		매치할 수 있고 여러 ":param"*/ 로 결합될 수도 있다*/
        /* 사용 예제: http://example.com/#todos/5/download/files/Meeting_schedule.doc */

        /* 만일 기본 라우팅 이상의 것을 위해 splat을 사용하고 싶으면,
		URL의 끝에 splat을 두는 것도 좋은 생각일 것이다. 그렇지 않으면
		URL에 정규식을 적용해야만 할 지도 모른다 */

        "*other"    : "defaultRoute"
        /* 이것이 *splat끼지 사용한 기본 지점이다. 기본 지점은
		사용자가 지점 경로를 직접 부정확하게 입력한 경우
		일치하지 않는 URL에 대한 히든 카드로 생각해라. */
        /* 사용 예제: http://example.com/# <anything */
    },

    showAbout: function(){
    },

    getTodo: function(id){
        /*
        위의 지점에서 매치된 id가 이 함수의 인자로 넘어오는 것을 알아둬라
        */
        console.log("You are trying to reach todo " + id);
    },

    searchTodos: function(query, page){
        var page_number = page || 1;
        console.log("Page number: " + page_number + " of the results for todos containing the word: " + query);
    },

    downloadDocument: function(id, path){
    },

    defaultRoute: function(other){
        console.log('Invalid. You attempted to reach:' + other);
    }
});

/* 생성하기 위해 라우터 설정을 했다. */

var myTodoRouter = new TodoRouter();
```

Backbone 0.5버젼 이상에서, `window.history.pushState`를 통해서 HTML5의 pushState를 선택하는 것이 가능해졌다. 이것은 http://www.scriptjunkie.com/just/an/example과 같이 지점을 정의하는 것이 가능하도록 해준다. 사용자의 브라우져가 pushState를 지원하지 않을 때, 자동적으로 동작하지 않는다. 이 문서의 목적을 위해, 우리는 해쉬 태그 방법을 사용할 것이다.

#### 사용해야만 하는 라우터의 수는 제한되어 있는가?

Andrew de Andrade는 DocumentCloud가 보통 대부분의 어플리케이션에서 단 하나의 라우터만을 사용한다고 지적하였다. 당신은 당신의 프로젝트에서 어플리케이션 라우팅의 대부분이 다루기 어렵지 않아서 단일 라우터로 구성될 수 있기 때문에 한 두개 이상의 라우터를 필요로 할 것 같아 보이지 않는다.

#### Backbone.history

다음으로 `Backbone.history`가 어플리케이션 내의 `hashchange` 이벤트를 제어하기 때문에 이것을 초기화해야만 한다. 이것은 정의된 지점에 접근했을 때, 경로를 제어해서 콜백을 호출할 것이다.

다음 예제에서 `Backbone.history.start()` 메쏘드는 단순히 Backbone에 정상적으로 모든 `hashchange` 이벤트를 모니터링하기 시작했다고 말할 것이다:

```javascript
var TodoRouter = Backbone.Router.extend({
  /* 이 라우터에 대한 지점과 함수를 정의한다 */
  routes: {
    "about" : "showAbout",
    "search/:query" : "searchTodos",
    "search/:query/p:page" : "searchTodos"
  },

  showAbout: function(){},

  searchTodos: function(query, page){
    var page_number = page || 1;
    console.log("Page number: " + page_number + " of the results for todos containing the word: " + query);
  }
});

var myTodoRouter = new TodoRouter();

Backbone.history.start();

// 콘술을 확인해본다:
// http://localhost/#search/job/p3 출력: Page number: 3 of the results for todos containing the word: job
// http://localhost/#search/job 출력 : Page number: 1 of the results for todos containing the word: job 
// 등등 
```

메모: 마지막 예제를 테스트하기 위해서 이 책의 범위를 벗어나는 개인 개발 환경에서의 테스트를 위한 타이트 구축을 해야한다.

부수적으로 특정지점에서 URL에 어플리케이션의 상태를 저장하고 싶다면, `.navigate()` 메쏘드를 사용할 수 있다. 그 메쏘드는 `hashchange` 에벤트를 구동할 필요없이 단순히 URL을 갱신한다:

```javascript
/* 사용자가 하나의 할일 목록을 열 때, 특정 URL 부분이 수정되게 하고 싶다고 상상해보자 */
var TodoRouter = Backbone.Router.extend({
  routes: {
    "todo/:id": "viewTodo",
    "todo/:id/edit": "editTodo"
    // ... 다른 지점들
  },

  viewTodo: function(id){
    console.log("View todo requested.");
    this.navigate("todo/" + id + '/edit'); // 조각을 갱신하지만 그 지점을 구동하지 않는다.
  },
  editTodo: function(id) {
    console.log("Edit todo openned.");
  }
});

var myTodoRouter = new TodoRouter();

Backbone.history.start();

// 다음을 읽어라:
// http://localhost/#todo/4 url은 다음으로 변경된다: http://localhost/#todo/45/edit
// 하지만 그 지점에 매핑했음에도 불구하고 editTodo() 함수는 호출되지 않느다. 
//
// 출력: View todo requested.
```

`Router.navigate()`가 지점뿐만 아니라 URL 조각을 갱신하는 것도 가능하다.

```javascript
var TodoRouter = Backbone.Router.extend({
  routes: {
    "todo/:id": "viewTodo",
    "todo/:id/edit": "editTodo"
    // ... 다른 지점들
  },

  viewTodo: function(id){
    console.log("View todo requested.");
    this.navigate("todo/" + id + '/edit', true); // 조각을 갱신하고 지점도 구동한다
  },
  editTodo: function(id) {
    console.log("Edit todo openned.");
  }
});

var myTodoRouter = new TodoRouter();

Backbone.history.start();

// 다음을 읽어라:
// http://localhost/#todo/4 주소는 다음으로 갱신된다: http://localhost/#todo/45/edit
// 이번에는 editTodo() 함수가 호출된다.
// 
// 출력: 
// View todo requested.
// Edit todo openned. 
```

### Backbone의 동기화 API

Backbone.sync 메쏘드는 다른 서버단을 지원하기 위해 덮어써져있다. 이 기본 탑재 메쏘드는 RESTful JSON API의 속성에 맞춰져있다 - Backbone은 원래 루비 온 레일즈 어플리케이션에서 나왔는데, 그것은 PUT과 같은 HTTP 메쏘드를 동일한 방식으로 사용한다.

이것이 동작하는 방식은 모델과 컬렉션 클래스가 Backbone.sync를 호출하는 sync 메쏘드를 갖는 것이다. 모델과 컬렉션 둘다 항목을 조회하거나 저장하거나 삭제할 때, 내부적으로 this.sync를 호출할 것이다.

동기화 메쏘드는 세개의 파라미터로 호출된다:

* method: create, update, delete, read 중에 하나
* model: The Backbone 모델 객체
* options: 성공과 실패를 위한 메쏘드를 포함하고 있을 것이다.

새로운 sync 메쏘드를 구현하는 것은 다음 패턴을 사용할 수 있다:

```javascript
Backbone.sync = function(method, model, options) {
  var requestContent = {}, success, error;

  function success(result) {
    // MyAPI 에서의 결과를 처리한다
    if (options.success) {
      options.success(result);
    }
  }

  function error(result) {
    // MyAPI 에서의 결과를 처리한다
    if (options.error) {
      options.error(result);
    }
  }

  options || (options = {});

  switch (method) {
    case 'create':
      requestContent['resource'] = model.toJSON();
      return MyAPI.create(model, success, error);

    case 'update':
      requestContent['resource'] = model.toJSON();
      return MyAPI.update(model, success, error);

    case 'delete':
      return MyAPI.destroy(model, success, error);

    case 'read':
      if (model.attributes[model.idAttribute]) {
        return MyAPI.find(model, success, error);
      } else {
        return MyAPI.findAll(model, success, error);
      }
  }
};
```

이 패턴은 API 호출을 해 객체에 위입하는데, 그 객체는 이벤트를 지원하는 Backbone 스타일의 클래스일 수 있다. 이것이 독립적이고 잠재적으로 Backbone이 아닌 다른 라이브러리와의 조합을 안전하게 테스트할 수 있게 한다.

여기 몇개의 sync 구현체가 있다:

* Backbone localStorage
* Backbone offline
* Backbone Redis
* backbone-parse
* backbone-websql
* Backbone Caching Sync

### 충돌 관리

대부분의 클라이언트 프로젝트와 마찬가지로 Backbone.js는 모든 것을 직접 호출되는 함수표현식으로 감싼다:

```javascript
(function(){
  // Backbone.js
}).call(this);
```

이런 설정하는 동안 몇가지 일들이 일어난다. Backbone 네임스페이스가 생성되고 같은 페이지 상에 여러 버젼의 Backbone이 noConflict 모드를 통해 지원된다:

```javascript
var root = this;
var previousBackbone = root.Backbone;

Backbone.noConflict = function() {
  root.Backbone = previousBackbone;
  return this;
};
```

여러 버젼의 Backbone이 다음과 같이 noConflict를 호출함으로써 같은 페이지에서 사용될 수 있다:

```javascript
var Backbone19 = Backbone.noConflict();
// Backbone19는 최근에 로드된 버젼을 가리킨다.
// 그리고 `window.Backbone`은 전에 로드된 버젼에
// 저장될 것이다.
```

이런 초기 설정 코드 역시 CommonJS 모듈을 지원하므로 Backbone은 Node 프로젝트에 사용될 수도 있다:

```javascript
var Backbone;
if (typeof exports !== 'undefined') {
  Backbone = exports;
} else {
  Backbone = root.Backbone = {};
}
```

## 상속 & 결합

상속을 위해 Backbone은 내부적으로 구글이 구현한 Closure 라이브러리, `goog.inherits`에서 영감을 받은 `inherits` 함수를 사용한다. 그것은 기본적으로 연속된 프로토타입을 올바르게 설정하게 하는 함수이다.

```javascript
 var inherits = function(parent, protoProps, staticProps) {
      ...
```

여기에서 유일한 큰 차이점은 Backbone의 API가 “instance”와 “static” 메쏘드를 포함한 두개의 객체를 받는다는 것이다.

이 다음으로 상속을 목적으로 모든 Backbone의 객체는 다음과 같이 `extend` 메쏘드를 포함한다.

```javascript
Model.extend = Collection.extend = Router.extend = View.extend = extend;
```

Backbone으로 개발하는 대부분의 개발은 이들 객체를 상속하는 것을 기본으로 하고, 그것은 전통적인 객체 지향 구현을 흉내내도록 설계되어 있다.

이 말이 친근하게 들린다면, Backbone 그 자체가 Underscore로 많은 일을 한다고 할지라도, `extend`는 Underscore.js 유틸리티이기 때문이다. Underscore의 `extend`에 대해서 다음을 보라:

```javascript
each(slice.call(arguments, 1), function(source) {
  for (var prop in source) {
    obj[prop] = source[prop];
  }
});
return obj;
```

위의 코드는 어떤 객체어ㅅ 다른 객체로 특성들( 메쏘드와 값 )을 실제로 복사하기 때문에 ES5의 `Object.create`와 완전히 같지는 않다. 이것은 Backbone의 상속과 클래스 모델을 충분히 지원하지 못하기 때문에, 다음 단계가 수행된다:

* 생성자 특성이 있는지 알아보기 위해 객체 메쏘드들을 확인한다. 만일 있다면, 클래스의 생성자를 사용하고, 그렇지 않으면 부모의 생성자를 사용한다.( 즉, Backbone.Model)
* Underscore의 extend 메쏘드는 부모 클래스의 메쏘드를 새로운 자식 클래스에 추가하기 위해 호출된다.
* 빈 생성자 함수의 `prototype` 특성은 부모의 prototype으로 할당되고, 이 클래스의 새로운 객체는 자식의 `prototype` 특성에 지정된다.
Underscore의 extend 메쏘드는 자식 클래스에 static 메쏘드와 instance 메쏘드를 추가하기 위해 두번 호출된다.
* 자식의 prototype의 생성자와 `__super__` 특성이 할당된다.
* 이러한 패턴은 CoffeeScript에서 클래스에도 사용되기 때문에 Backbone 클래스는 CoffeeScript의 클래스와 호환된다.

`extend`는 좀 더 대단한 곳에 사용될 수 있고 결합을 좋아하는 개발자들은 `extend`를 사용할 수 있다는 것도 좋아할 것이다. 당신은 어떤 사용자 객체에 대해 기능을 정의하고 나서 모든 메쏘드와 특성을 그 객체에서 Backbone 객체로 단순하게 카피&페이스트 할 수 있다.

예제:

```javascript
 var MyMixin = {
  foo: 'bar',
  sayFoo: function(){alert(this.foo);}
}

var MyView = Backbone.View.extend({
 // ...
});

_.extend(MyView.prototype, MyMixin);

myView = new MyView();
myView.sayFoo(); //=> 'bar'
```

우리는 좀더 나아가서 이것을 가지고 뷰 상속에 적용할 수도 있다. 다음은 다른 뷰를 가지고 하나의 뷰를 확장하는 방법의 예제이다:

```javascript
var Panel = Backbone.View.extend({
});

var PanelAdvanced = Panel.extend({
});
```

하지만, Panel에 `initialize()` 메쏘드를 가지고 있고 PanelAdvanced에도 `initialize()` 메쏘드가 있다면 Panel의 메쏘드는 호출되지 않기 때문에, Panel의 initialize 메쏘드를 명시적으로 호출해야만 한다:

```javascript
var Panel = Backbone.View.extend({
   initialize: function(options){
      console.log('Panel initialized');
      this.foo = 'bar';
   }
});

var PanelAdvanced = Panel.extend({
    initialize: function(options){
      Panel.prototype.initialize.call(this, [options])
      console.log('PanelAdvanced initialized');
      console.log(this.foo); // Log: bar
    }
});

// 필요하다면 우리는 PanelAdvaned를 상속할 수도 있다
var PanelAdvancedExtra = PanelAdvanced.extend({
    initialize: function(options){
      PanelAdvanced.prototype.initialize.call(this, [options])
      console.log('PanelAdvancedExtra initialized');
    }
});

new Panel();
new PanelAdvanced();
new PanelAdvancedExtra();
```

이것은 당신이 Panel에서 상속된 많은 뷰들이 있다면 그 안에서 Panel의 initialize를 호출해야 하는 것을 기억해야만 하기 때문에 가장 우아한 해결책은 아니다.

현재는 Panel이 initialize 메쏘드를 갖지않지만 나중에 추가할 수도 있다면, 그때에는 모든 상속된 클래스에 가서 Panel의 initialize를 반드시 호출해 줘야하는 것도 기억해야 한다.

그래서 여기에 당신의 상속된 뷰가 Panel의 initialize 메쏘드를 호출할 필요없이 Panel을 정의하는 또 다른 방법이 있다.

```javascript
var Panel = function (options) {
  // 모든 Panel의 초기화 코드를 여기에 넣는다
  console.log('Panel initialized');
  this.foo = 'bar';

  Backbone.View.apply(this, [options]);
};

_.extend(Panel.prototype, Backbone.View.prototype, {
  // 여기에 Panel의 모든 메쏘드들을 넣는다. 예를 들어:
  sayHi: function () {
      console.log('hello from Panel');
  }
});

Panel.extend = Backbone.View.extend;

// 그리고나서 Panel에서 상속된 다를 클래스들은 다음과 같이 한다.
var PanelAdvanced = Panel.extend({
  initialize: function (options) {
    console.log('PanelAdvanced initialized');
    console.log(this.foo);
  }
});

var PanelAdvanced = new PanelAdvanced(); //출력: Panel initialized, PanelAdvanced initialized, bar
PanelAdvanced.sayHi(); // 출력: hello from Panel
```

Underscore의 `extend` 메쏘드를 적절히 쓸 때, 불필요한 코드를 작성하는 많은 시간과 노력을 절약할 수 있다.

( 이 팁을 알려준 [Alex Young](http://dailyjs.com), [Derick Bailey](http://stackoverflow.com/users/93448/derick-bailey) 그리고 [JohnnyO](http://stackoverflow.com/users/188740/johnnyo) 에게 감사한다. )

#### Backbone-Super

Lukas Olson이 만든 [Backbone-Super](https://github.com/lukasolson/Backbone-Super)은 [John Resig의 Inheritance script](http://ejohn.org/blog/simple-javascript-inheritance/)를 사용해서 *Backbone.Model*에 *_super* 메쏘드를 추가한다.
Backbone.js 문서에 있는대로 Backbone.Model.prototype.set.call을 사용하는 대신에 _super를 호출할 수도 있다:

```javascript
// 이것이 우리가 보통하는 방식이다
var OldFashionedNote = Backbone.Model.extend({
  set: function( attributes, options ) {
    // 부모의 메쏘드를 호출한다
    Backbone.Model.prototype.set.call(this, attributes, options);
    // 일반 코드가 여기 있고
    // ...
  }
});
```

이 플러그인을 사용하고 나서 당신은 다음의 문법으로 같은 일을 할 수 있다:

```javascript
// 이것이 Backbone-super 플러그인을 사용한 후 할 수 있는 방법이다
var Note = Backbone.Model.extend({
  set: function(attributes, options) {
    // 부모의 메쏘드를 호출한다
    this._super(attributes, options);
    // 일반 코드가 여기 있고
    // ...
  }
});
```

## 의존성

Backbone.js의 정규 [문서](http://backbonejs.org/)에서 말하기를:

>Backbone의 강한 의존성은 Underscore.js ( 1.3.1 이상 )이다. REST한 유지 계층을 위해, 히스토리는 Backbone.Router를 통해 지원되고, Backbone.View로 DOM 조작을 지원하고, json2.js와 jQuery( 1.4.2이상 )이나 Zepto을 포함한다.

*성능 개선을 포함하고 있는 Underscore의 한 갈래인 [Lo-dash](https://github.com/bestiejs/lodash)도 Backbone과 호환된다.*

이것이 의미하는 바는 당신이 모델외의 어떤 것을 할 필요가 있다면, jQuery나 Zepto같은 DOM 조작 라이브러리를 포함해야만 할 것이라는 뜻이다. Underscore는 유틸리티 메쏘드( Backbone은 매우 많이 의존성을 갖는다. )로 주로 사용될 것이고 Backbone.sync가 사용되면 과거의 브라우져를 위해 json2.js가 JSON을 지원할 것이다.

### DOM 조작

대부분의 개발자가 필요하지 않을지라도, Backbone은 다음 선택권 대신에 사용자 지정 DOM 라이브러리를 사용하도록 설정하도록 해준다. 소스는 다음과 같다:

```
// DOM 조작과 Ajax 호출을 위해 사용될 자바스크립트 라이브러리를 지정한다.
// ( `$` 변수로 알려저 있다. ) 기본적으로 Backbone은 다음을 사용할 것이다:
// jQuery, Zepto, 아니면 Ender; 하지만 `setDomLibrary()` 메쏘드가 당신이 
// 다른 자바스크립트 라이브러리를 선택할 수 있게 해준다.( 브라우져 밖에서
// 뷰를 테스트하기 위해 목 라이브러리를 선택하기도 한다. )

Backbone.setDomLibrary = function(lib) {
  $ = lib;
};
```

이 메쏘드를 호출하는 것은 당신이 어떤 DOM 조작 라이브러리라도 사용할 수 있게 해준다. 예제:

```
Backbone.setDomLibrary(aCustomLibrary);
```

### 유틸리티

Underscore.js는 Backbone에서 화면 뒤에서 객체 확장에서 이벤트 바인딩에 이르기까지 모든것에 주도적으로 사용된다. 전체 라이브러리가 보통은 포함되기 때문에, 우리는 필터링 `_.filter()`, 소팅 `_.sortBy()`, 매핑 `_.map()` 등등과 같은 Collections에 사용할 수 있는 많은 유용한 유틸리티에 자유로이 접근한다.

소스를 보자:

```
// Collection에 구현하고 싶은 Underscore 메쏘드들.
var methods = ['forEach', 'each', 'map', 'reduce', 'reduceRight', 'find',
    'detect', 'filter', 'select', 'reject', 'every', 'all', 'some', 'any',
    'include', 'contains', 'invoke', 'max', 'min', 'sortBy', 'sortedIndex',
    'toArray', 'size', 'first', 'initial', 'rest', 'last', 'without', 'indexOf',
    'shuffle', 'lastIndexOf', 'isEmpty', 'groupBy'];

// 각 Underscore 메쏘드는 Collection#models에 대한 프록시로 결합된다.
  _.each(methods, function(method) {
    Collection.prototype[method] = function() {
      return _[method].apply(_, [this.models].concat(_.toArray(arguments)));
    };
```
    
그러나, 지원되는 완전한 리스트를 위해 [공식 문서](http://backbonejs.org/#Collection-Underscore-Methods)를 보라.

### REST한 유지

Backbone에서 모델과 컬렉션은 `fetch`, `save`, 그리고 `destroy` 메쏘드를 사용해서 서버와 "동기화"될 수 있다. 이들 메쏘드들 모두는 `Backbone.sync` 함수로 다시 위임하는데, 이 함수는 실제로 Backbone의 모델에 각각의 유지 메쏘드를 위효 GET, POST, DELETE를 호출하는 jQuery나 Zepto의 `$.ajax` 함수를 감싸고 있다.

`Backbone.sync`의 코드:

```
var methodMap = {
    'create': 'POST',
    'update': 'PUT',
    'delete': 'DELETE',
    'read':   'GET'
  };
  
Backbone.sync = function(method, model, options) {
    var type = methodMap[method];
    options || (options = {});
    // ... Backbone.js의 많은 설정에 따라서 처리된다..
   return $.ajax(_.extend(params, options));
```

### 라우팅

`Backbone.History.start`를 호출하는 것은 jQuery나 Zepto가 `popState`나 `hashchange` 이벤트 리스너가 window 객체에 다시 바인딩되도록 한다.

`Backbone.history.start`의 소스:

```
// 우리가 pushState나 hashes를 사용할지 'onhashchange'가 지원될지
// 여부에 따라 URL 상태를 확인하는 방법이 결정된다.
if (this._hasPushState) {
        $(window).bind('popstate', this.checkUrl);
      } else if (this._wantsHashChange && ('onhashchange' in window) && !oldIE) {
        $(window).bind('hashchange', this.checkUrl);
      ...
```

`Backbone.History.stop`은 유사한 방식으로 이 이벤트 리스너를 뗗어내기 위해 DOM 조작 라이브러를 사용한다.



## 이름공간( Namespacing )

Backbone의 사용법을 배울 때, 학습서에서 중요하면서 공통으로 보이는 부분이 이름공간이다. 만일 당신이 자바스크립트에서 이름공간에 대한 경험이 있다면, 다음 부분은 당신이 알고 있는 개념을 Backbone에 어떻게 적용할지에 대한 약간의 조언을 제공하겠지만 나는 또한 모두가 같은 개념을 갖도록 하기 위해 초심자를 위한 설명도 할 것이다.

#### 이름공간이란 무엇인가?

이름공간의 기본생각은 전역공간에서 다른 객체나 변수가 충돌하는 것을 피하는 것이다. 이것은 당신이 동일한 변수명을 사용해서 페이지상의 다른 스크립트 이벤트에서 코드가 깨지는 것을 막는 가장 좋은 방법이기 때문에 중요하다. 전역공간의 좋은 '시민'으로서 당신이 다른 개발자의 스크립트가 동일한 문제를 야기하지 못하게 최선을 다할 의무도 있다. 

자바스크립트는 실제로 다른언어처럼 원래 가지고 있는 기능은 아니지만 유사한 효과를 나타내도록 사용할 수 있는 클로져를 가지고 있다.

이번 섹션에서 우리는 당신이 모델, 뷰, 라우터, 그외의 컴포넌트에 특별히 이름공간으로 나누는 방법에 대한 약간의 예제를 간단히 살펴볼 것이다. 우리가 시험할 패턴은 다음과 같다:

* 달일 전역 변수
* 객체 상수
* 중첩 이름공간

**단일 전연 변수**

자바스크립트에서 이름공간에 대한 인기있는 패턴중 하나는 단일 전역 변수에 대해 참조의 주요 객체로 선택하는 것이다. 함수와 특성을 가진 객체를 반환하는 기본 구현을 아래에서 확인할 수 있다:

```javascript
var myApplication = (function(){
    function(){
      // ...
    },
    return {
      // ...
    }
})();
```

당신은 아마 이전에 이런 테크닉을 보았을지도 모른다. Backbone 스타일의 예제는 다음과 같다:

```javascript
var myViews = (function(){
    return {
        TodoView: Backbone.View.extend({ .. }),
        TodosView: Backbone.View.extend({ .. }),
        AboutView: Backbone.View.extend({ .. });
        //etc.
    };
})();
```

여기에서 우리는 일련의 뷰 묶음을 반환하지만, 같은 방식으로 당신이 어플리케이션의 구조를 결정한 방식대로 모델, 뷰, 라우터들의 전체 묶음을 반환할 수 있다. 어떤 상황에서 이것이 동작한다 할지라도, 단일 전역 변수 패턴의 가장 큰 위험은 페이지 내에서 어떤 다른 누구도 동일한 전역 변수명을 쑤지 않도록 해야한다는 것이다.

Peter Michaux가 언급하기를 이에 대한 한가지 해결책은 접두사 이름공간을 사용하는 것이다. 그것은 핵심을 찌르는 간단한 개념이다. 이 생각은 당신이 공통으로 사용할 접두사명( 이번 예제에서는 myApplication_ )을 선택하고 어떤 메쏘드나 변수나 다른 객체를 접두사뒤에 정의하는 것이다.

```javascript
var myApplication_todoView = Backbone.View.extend({}),
    myApplication_todosView = Backbone.View.extend({});
```

이것은 전역 범위에 특정 변수가 존재할 확률을 낮춘다는 관점에서 효과적이다. 하지만 독특하게 이름지어진 객체도 역시 같은 효과를 가질 것이라는 점을 기억해라. 부수적으로 이 패턴의 가장 큰 논쟁거리는 어플리케이션이 커지기 시작하면 많은 전역 객체가 생겨날 수 있다는 점이다.

단일 전역 변수 패턴에 대한 Peter의 관점에 더 알고 싶다면, 그가 작성한 [포스팅](http://michaux.ca/articles/javascript-namespacing)을 읽어라.

메모: 단일 전역 변수 패턴의 몇가지 다른 변형들이 있지만, 몇개를 검토해보면서 나는 접두사를 쓰는 것이 Backbone에 가장 적합한 접근법이라고 느꼈다.

**상수 객체**

상수 객체는 전역공간을 훑지않아도 되는 장점이 있는데다가 코드와 파라미터를 논리적으로 묶는데 도음을 준다. 당신이 많이 중첩된는 것을 지원할 수 있는 가독성높은 구조를 만들고 싶다면 상수 객체는 이득이 된다. 단순한 전역 변수와 달리, 객체 상수는 종종 동일한 이름의 변수 존재를 위한 테스트를 고려하기도 한다. 이것은 충돌 확률을 줄여준다.

이 예제는 정의하기 전에 이름공간이 이미 있는지를 알아보기 위해 확인할 수 있는 두가지 방법을 보여준다. 다는 보통은 두번째 방식을 사용한다.

```javascript
/* myApplication의 존재를 확인하지 않는다 */
var myApplication = {};

/*
존재를 체크한다. 만일 정의되어 있으면, 그 인스턴스를 사용한다.
선택 1:   if(!myApplication) myApplication = {};
선택 2:   var myApplication = myApplication || {};
그리고 나서 우리는 모델, 뷰, 컬렉션( 실제로는 어떤 데이타라도 )을 지원하는 객체 상수를 정의할 수 있다:
*/

var myApplication = {
    models : {},
    views : {
        pages : {}
    },
    collections : {}
};
```

( 다음 예제에서는 뷰와 같은 ) 이름공간에 직접적으로 특성을 추가하는 방식을 선택할 수도 있다:

```javascript
var myTodosViews = myTodosViews || {};
myTodosViews.todoView = Backbone.View.extend({});
myTodosViews.todosView = Backbone.View.extend({});
```

이 패턴의 장점은 코드 확장을 위해서 모든 모델, 뷰, 라우터등을 깔끔하게 분리해서 단단한 기본 구조를 제공하는 방식으로 그것들을 손쉽게 감쌀 수 있다는 것이다. 

이 패턴은 많은 장점을 가진다. 어플리케이션의 기본 설정은 단순히 수정을 위해 전체 코드를 검색할 필요없이 쉽게 수정할수 있는 단 하나의 곳으로 분리하는 것은 종종 좋은 생각이다. 여기 어플리케이션의 설정을 저장하는 가상의 객체 상수의 예제가 있다:


```javascript
var myConfig = {
  language: 'english',
  defaults: {
    enableDelegation: true,
    maxTodos: 40
  },
  theme: {
    skin: 'a',
    toolbars: {
      index: 'ui-navigation-toolbar',
      pages: 'ui-custom-toolbar'
    }
  }
}
```

상수 객체와 표준 JSON 데이타셋사이에는 작은 문법적 차이만 있다는 것을 기억해라. 어떤 이유로( 예를 들어 서버에 보낼 때, 더 단순한 저장을 위해서 ) 설정을 저장하는데 JSON을 대신 사용한다면, 편한대로 해라.

객체 상수 패턴에 대해 좀 더 알고 싶다면, Rebecca Murphey의 [이 주제에 대한 좋은 글](http://rmurphey.com/blog/2009/10/15/using-objects-to-organize-your-code)을 읽기를 권한다.

**중첩 이름공간**

객체 상수 패턴의 확장이 중첩 이름공간이다. 그것은 최상위 이름공간이 존재하더라도 동일한 하위 이름 공간은 그렇지 않은 것이라는 사실에 기인해서 낮은 충돌 위험을 제공하는 또 다른 공통 패턴이다. 예를 들어 야후의 YUI는 중첩된 객체 이름공간 패턴을 확장해서 사용한다:

```javascript
YAHOO.util.Dom.getElementsByClassName('test');
```

야후의 YUI는 보통 중첩 객체 이름공간 패턴을 사용하고 심지어 DocumentCloud( Backbone의 창시자 )는 메인 어플리케이션에서 중첩 이름공간을 사용한다. Backbone으로 중첩 이름공간의 단순한 구현을 다음과 같이 볼 수 있다:

```javascript
var todoApp =  todoApp || {};

// 유사하게 중첩 하위 이름공간에 대한 확인을 수행한다
todoApp.routers = todoApp.routers || {};
todoApp.model = todoApp.model || {};
todoApp.model.special = todoApp.model.special || {};

// routers
todoApp.routers.Workspace   = Backbone.Router.extend({});
todoApp.routers.TodoSearch = Backbone.Router.extend({});

// models
todoApp.model.Todo   = Backbone.Model.extend({});
todoApp.model.Notes = Backbone.Model.extend({});

// special models
todoApp.model.special.Admin = Backbone.Model.extend({});
```

이 방식은 가독성이 높고, 구성이 명확하고 Backbone 어플리케이션을 이름공간으로 나누는 상대적으로 안전한 방법이다. 드러난 유일한 경고는 브라우져의 자바스크립트 엔진이 먼저 todoApp 객체를 설정하고나서, 호출하는 함수를 얻기 전에 하위 객체로 내려가야 한다는 점이다. 그러나, Juriy Zaytsev( kangax ) 같은 개발자들은 단일 객체 이름공간과 '중첩된' 이름공간 사이에 수행능력 차이를 테스트하고는 거의 무시할만한 것임을 알게되었다.

**추천**

위에서 이름공간 패턴을 살펴본 것처럼 Backbone 어플리케이션을 작성할 때 내가 선호하는 선택은 객체 상수보다는 중첩 객체 이름공간이다.

단일 전역 변수는 상대적으로 단순한 어플리케이션에서 잘 동작한다. 하지만, 이름공간과 하위 이름공간을 모두 필요로 하는 더큰 규모의 코드에서는 가독성이 높고 확장이 가능한 간결한 해결책을 필요로 한다. 나는 이 패턴이 이 목적을 달성하고 대부분의 Backbone 개발에 좋은 선택이라고 느낀다.


# 연습 1: 할일관리앱 - 첫번째 Backbone.js 앱

이제까지 우리가 기초를 살펴본 우리의 첫번째 Backbone.js 앱 - 할일 목록 어플리케이션을 작성하러 가보자. 할일 목록을 개발하는 것은 Backbone의 관습을 배우는 좋은 방법이다. 그것은 충분히 단순한 앱이지만, 바인딩, 모델 데이타 유지, 라우팅, 템플릿 렌더링같은 유용하고 흥미로운 문제들을 포함한다.


이번 챕터에서 우리는 [TodoMVC.com](http://todomvc.com)에 있는 Backbone.js 할일 앱을 만드는 방법을 배울 것이다.
![](img/todoapp.png)

상위 구조의 관점에서 우리에게 필요한 것을 생각해보자.

* 각각의 할일 항목을 표현하는 `Todo` 모델
* 할일들을 저장하고 유지하는 `TodoList` 컬렉션
* 할일들을 생성하는 방법
* 할일들을 보여주는 것
* 이미 있는 할일을 수정하는 것
* 할일을 완료하기
* 할일을 삭제하기
* 완료되거나 진행중인 함목들을 복마크하는 방법

기본적으로 고전적인 [CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) 방식아다. 시작해보자!

## 색인

첫번째 단계는 기본 어플리케이션의 의존성을 설정하는 것인데, 이번에는 다음과 같을 것이다: [jQuery](http://jquery.com), [Underscore](http://underscorejs.org), Backbone.js 그리고 [Backbone LocalStorage adapter](https://github.com/jeromegn/Backbone.localStorage). 이것들은 우리의 주( 사실 하나뿐인)HTML 파일인 index.html에서 로드될 것이다:


```html

<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
  <title>Backbone.js • TodoMVC</title>
  <link rel="stylesheet" href="assets/base.css">
</head>
<body>
  <script src="js/lib/jquery.min.js"></script>
  <script src="js/lib/underscore-min.js"></script>
  <script src="js/lib/backbone-min.js"></script>
  <script src="js/lib/backbone-localstorage.js"></script>
  <script src="js/models/todo.js"></script>
  <script type="text/template" id="item-template"></script>
  <script type="text/template" id="stats-template"></script>
  <script src="js/collections/todos.js"></script>
  <script src="js/views/todo.js"></script>
  <script src="js/views/app.js"></script>
  <script src="js/routers/router.js"></script>
  <script src="js/app.js"></script>
</body>
</html>

```

우리 어플리케이션의 많은 부분이 어떻게 쪼개지는지 보여주기 위해서 각각의 관심들은 모델, 뷰, 컬렉션, 라우터를 나타내는 폴더로 명확하게 구성된다. app.js 파일은 시작을 위해 사용된다.

메모: 당신이 따라해보고 싶다면, index.html에서 보는데로 디렉토리 구조를 생성해라. 그리고, assets 디렉토리에 [base.css](https://raw.github.com/addyosmani/todomvc/gh-pages/assets/base.css) 와 [bg.png](https://raw.github.com/addyosmani/todomvc/gh-pages/assets/bg.png) 모두가 필요할 것이다. 앞에서 말한대로 당신은 [TodoMVC.com](http://todomvc.com)에서 전체 어플리케이션을 확인할 수 있다.


## 어플리케이션 HTML

이제 우리 어플리케이션의 정적인 HTML을 보자. 우리는 새로운 할일들, 실제 할일을 보여주는 `<ul id="todo-list" />`, 완료된 할일들을 삭제하는 동작같은 것을 포함하는 부분이 필요할 것이다.

```html
  <section id="todoapp">
    <header id="header">
      <h1>todos</h1>
      <input id="new-todo" placeholder="무엇을 해야 하나요?" autofocus>
    </header>
    <section id="main">
      <input id="toggle-all" type="checkbox">
      <label for="toggle-all">모든 할일 완료하기</label>
      <ul id="todo-list"></ul>
    </section>
    <footer id="footer"></footer>
  </section>
  <div id="info">
    <p>할일을 수정하기 위해서는 더블 클릭을 하세요</p>
    <p><a href="https://github.com/addyosmani">Addy Osmani</a>에 의해 작성되었습니다</p>
    <p><a href="http://todomvc.com">TodoMVC</a>의 일부입니다</p>
  </div>

```

우리는 우리의 할일 목록을 찾아서 아직 완료되지 않은 항목들에 대한 상세 내용을 통계 부분에 추가할 것이다.

지금까지 잘되가고 있다. 이제 이 HTML을 우리 Backbone 할일 앱에 결합하기 위해서 기본( Todo 모델 )으로 돌아가야만 할 것이다.

## Todo 모델

`Todo` 모델은 매우 직관적이다. 우선 할일은 `title`과 그일이 끝났는지를 여부를 나타내는 `completed` 두 속성을 가진다. 이들 속성은 아래 예제에서 보듯이 기본으로 전달된다:

```javascript

  // js/models/todo.js

  var app = app || {};

  // Todo 모델
  // ----------
  // 기본 **Todo** 모델은 `title` 과 `completed` 속성을 갖는다.

  app.Todo = Backbone.Model.extend({

    // 할일에 대한 기본 속성
    // 생성된 각 할일은 `title` 과 `completed` 키를 갖게 한다.
    defaults: {
      title: '',
      completed: false
    },

    // 할일 항목의 `completed`상태를 전환한다.
    toggle: function() {
      this.save({
        completed: !this.get('completed')
      });
    }

  });

```

Todo 항목이 완료되었는지 여부를 지정하도록 하는 `toggle()` 함수가 있다.


## Todo 컬렉션


다음으로 우리는 모델을 몪는데 사용할 `TodoList` 컬렉션을 만든다. 이 컬렉션은 Backbone의 LocalStorage 어댑터를 통해 HTML5 로컬 스토리지에 Todo 기록을 자동적으로 유지하는 localStorage로 확장되기 때문에 그것들은 페이지 요청간에 저장될 것이다.

그리고 나서 `completed()`와 `remaining()`같은 정적 메쏘드를 만든다. 이 메쏘드들은 각각 완료된 할일들과 완료되지않은 할일들을 배열로 반환한다.

마지막으로 우리는 `nextOrder()` 함수를 만든다. 그겄은 Todo목록을 순서대로 유지시켜줄 뿐만 아니라 순서대로 항목을 정렬하는데 사용되는 `comparator()`이기도 하다.

```javascript

  // js/collections/todos.js

  var app = app || {};

  // Todo 컬렉션
  // ---------------

  // 외부의 서버 대신에 *localStorage*에 의해 저장되는
  // 할일들의 컬력션.
  var TodoList = Backbone.Collection.extend({

    // 이 컬렉션의 모델을 가리킨다.
    model: app.Todo,

    // `"todos-backbone"` 이름 공간의 할일 항목 모두를 저장한다.
    localStorage: new Backbone.LocalStorage('todos-backbone'),

    // 완료된 모든 할일 함목 목록을 필터링한다.
    completed: function() {
      return this.filter(function( todo ) {
        return todo.get('completed');
      });
    },

    // 완료되지 않은 할일 항목 목록을 필터링한다.
    remaining: function() {
      return this.without.apply( this, this.completed() );
    },

    // Todos는 데이타베이스에 정렬되지 않은 GUID순서로 저장될 지라도
	// 일련의 순서로 유지된다. 이것은 새로운 아이템의 다음 순서값을 생성한다.
    nextOrder: function() {
      if ( !this.length ) {
        return 1;
      }
      return this.last().get('order') + 1;
    },

    // Todos는 원래의 입력 순서대로 정렬한다.
    comparator: function( todo ) {
      return todo.get('order');
    }
  });

  // **Todos**의 전역 컬력션을 생성한다.
  app.Todos = new TodoList();

```

## 어플리케이션 뷰

어플리케이션 로직의 핵심인 뷰를 살펴보자. 각 할일은 그것과 관련된 약간의 로직을 갖고 있기 때문에, 우리는 요소 컨트롤러 패턴을 사용할 것이다 - 아이템의 컬렉션을 제어하는 뷰와 각 개별 항목을 다루는 다른 뷰, 두개의 뷰로 구성된다.

즉, 우리는 `AppView`를 가질 것인데, 그것은 새로운 할일들을 만들고 초기 할일 목록을 그리는 역할을 할 것이다. 그리고 나서 우리는 각 Todo 항목과 연결되어 있는 TodoView라고 불리는 다른 뷰 객체를 가질 것이다. Todo 객체는 연결되어 있는 할일을 수정하고 갱신하고 제거하는 역할을 할 것이다.

이러한 일들을 단순화하기 위해, 우리는 그 시점에는 읽기만 가능한 상태로 유지하고 할일은 생성하고 수정하고 삭제하는 기능을 제공하지 않을 것이다:

```javascript

  // js/views/app.js

  var app = app || {};

  // The Application
  // ---------------

  // **AppView**의 개략적인 모습은 UI의 상위 조각이다.
  app.AppView = Backbone.View.extend({

    // 새로운 요소를 생성하는 대신에 HTML에 이미
	// 존재하는 App 구조에 바인딩한다.
    el: '#todoapp',

    // 앱 아래부분에 통계에 대한 템플릿
    statsTemplate: _.template( $('#stats-template').html() ),

    // 초기화 시점에 우리는 항목이 추가되거나 변경될 때 관련된 이벤트를
	// `Todos` 컬렉션에 바인딩한다. *localStorage*에 저장되어 있을 이미
	// 존재하는 할일들을 로딩하는 것으로 시작한다.
    initialize: function() {
      this.input = this.$('#new-todo');
      this.allCheckbox = this.$('#toggle-all')[0];
      this.$footer = this.$('#footer');
      this.$main = this.$('#main');

      window.app.Todos.on( 'add', this.addOne, this );
      window.app.Todos.on( 'reset', this.addAll, this );
      window.app.Todos.on( 'all', this.render, this );

      app.Todos.fetch();
    },

    // 앱을 다시 그린다는 것은 단지 통계 부분을 갱신한다는 것을
	// 의미한다 - 앱의 나머지는 변경되지 않는다.
    render: function() {
      var completed = app.Todos.completed().length;
      var remaining = app.Todos.remaining().length;

      if ( app.Todos.length ) {
        this.$main.show();
        this.$footer.show();

        this.$footer.html(this.statsTemplate({
          completed: completed,
          remaining: remaining
        }));

      } else {
        this.$main.hide();
        this.$footer.hide();
      }

      this.allCheckbox.checked = !remaining;
    },

    // 할일 항목을 위한 뷰를 생성하고 `<ul>`에 뷰의 요소를
	// 추가함으로써 단일 할일 항목을 목록에 추가한다,
    addOne: function( todo ) {
      var view = new app.TodoView({ model: todo });
      $('#todo-list').append( view.render().el );
    },

    // 한번에 **Todos** 컬렉션에 모든 항목을 추가한다.
    addAll: function() {
      this.$('#todo-list').html('');
      app.Todos.each(this.addOne, this);
    }

  });

```


당신이 우리가 el( 요소 ), `statsTemplate`, 생성자, 뷰 특화된 메쏘드에 하고있는 일들을 알 수 있다. `el:` 키는 `todoapp` 아이디를 가진 요소에 대한 DOM 선택자이다. 이 값은 단지 문자열이며 Backbone은 #todoapp 선택자와 일치하는 요소( 아마도 여기에서는 HTML에서 정의한 `<section id="todoapp" />`가 될 것이다. ) 를 가리키는 참조를 생성한다.

내부적으로 이것은 우리가 컨트롤러의 내부에서 this.el을 참조할 수 있다는 것을 의미한다. this.el은 `<section id="todoapp" />` 요소이다. 알다시피, 우리는 요소를 리스트에 추가하면서 `addOne()`에서 el을 참조하고 있다.

이제 생성자 함수를 보자. 그것은 Todo 모델에 add, reset과 같은 이벤트를 바인딩한다. 여기에서는 우리가 `TodoView` 뷰에 갱신과 삭제의 제어를 위임하기 때문에, 우리는 거기에 대해서 걱정할 필요가 없다. 두가지 논리는 다음과 같다:

* 새로운 할일이 생성될 때, `addAll()`을 호출하는 `add` 이벤트가 구동될 것이다. 이것은 현재 우리 컬렉션안에 있는 모든 Todo들을 순회하면서 각 항목에 대하서 `addOne()`을 구동한다.( 이것은 짜증난다. )

* `addOne()`은 TodoView 뷰를 그리고 최종 요소를 Todo 목록에 추가하는 TodoView를 생성한다.

* `reset` 이벤트가 호출되면 ( 즉, 우리가 Local Storage로 부터 Todos가 로드될 때와 같이 대량으로 컬렉션을 갱신하고 싶다면 ), 유사한 방식으로 `addAll()` 다시 불린다. is similarly called again.

그리고 나서 우리는 새로운 할일을 생성하고 수정하고 완결여부에 따라 필터링하는 로직을 추가할 수 있다.

* 이벤트: 우리는 DOM 이벤트에 대한 선언적 콜백을 보함하는 이벤트 해쉬를 정의한다.
  * `createOnEnter()`: 사용자가 `<input/>` 필드 안에서 리턴을 눌렸을 때, 이 이벤트는 새로운 Todo 항목을 생성하고 다음 항목을 위해 `<input/>` 필드 값을 초기화한다.
  * `clearCompleted()`: 완료로 표시된 할일 목록에 항목들을 제거한다.
  * `toggleAllComplete()`: 사용자가 할일 목록의 모든 항목을 완료로 만든다.
  * `initialize()`:
    우리는 이미 존재하는 항목에 변경이 발생했다는 것을 알 수 있도록 change:completed 이벤트에 대한 콜백을 바인딩한다.
	우리는 필터 이벤트에 대해서도 콜백을 바인딩한다. 필더 이벤트는 addOne()과 addAll()과 조금 유사한 방식으로 동작한다. 그것의 기능은 할일 항목들이 (all, completed, remainging 같은 )UI에서 filterOne()과 filterAll()을 통해서 현재 선택된 필터에 기본해서 보이는 것을 전환하는 것이다.
  * `render()`:
    우리는 선택된 지점이 주목받게 하기 위해서 현재 선택된 필터에 기반해서 조건에 따라 CSS 스타일을 추가할 것이다.
  * `createOnEnter()`:
    사용자가 리턴키를 눌렀을 때, localStorage에 유지되는 새로운 Todo 모델을 생성한다. 이것은 newAttributes()를 통해 모델을 생성한다. 그것은 새로 추가할 항목의 제목, 순서, 완료 여부로 구성된 객체 상수이다.
  * `clearCompleted()`:
    완료로 표시된 모든 할일 항목들을 삭제한다

```javascript

  // js/views/app.js

  var app = app || {};

  // 어플리케이션
  // ---------------

  // **AppView**의 개략적인 모습은 UI의 상위 조각이다.
  app.AppView = Backbone.View.extend({

    // 새로운 요소를 생성하는 대신에 HTML에 이미
	// 존재하는 App 구조에 바인딩한다.
    el: '#todoapp',

    // 앱 아래부분에 통계에 대한 템플릿
    statsTemplate: _.template( $('#stats-template').html() ),

    // 새로운 함목들을 생성하고 완료된 항목들을 삭제하는 위임된 이벤트들
    events: {
      'keypress #new-todo': 'createOnEnter',
      'click #clear-completed': 'clearCompleted',
      'click #toggle-all': 'toggleAllComplete'
    },

    // 초기화 시점에 우리는 항목이 추가되거나 변경될 때 관련된 이벤트를
	// `Todos` 컬렉션에 바인딩한다. *localStorage*에 저장되어 있을 이미
	// 존재하는 할일들을 로딩하는 것으로 시작한다.
    initialize: function() {
      this.input = this.$('#new-todo');
      this.allCheckbox = this.$('#toggle-all')[0];
      this.$footer = this.$('#footer');
      this.$main = this.$('#main');

      window.app.Todos.on( 'add', this.addAll, this );
      window.app.Todos.on( 'reset', this.addAll, this );
      window.app.Todos.on( 'change:completed', this.filterOne, this );
      window.app.Todos.on( 'filter', this.filterAll, this );

      window.app.Todos.on( 'all', this.render, this );

      app.Todos.fetch();
    },

    // 앱을 다시 그린다는 것은 단지 통계 부분을 갱신한다는 것을
	// 의미한다 - 앱의 나머지는 변경되지 않는다.
    render: function() {
      var completed = app.Todos.completed().length;
      var remaining = app.Todos.remaining().length;

      if ( app.Todos.length ) {
        this.$main.show();
        this.$footer.show();

        this.$footer.html(this.statsTemplate({
          completed: completed,
          remaining: remaining
        }));

        this.$('#filters li a')
          .removeClass('selected')
          .filter('[href="#/' + ( app.TodoFilter || '' ) + '"]')
          .addClass('selected');
      } else {
        this.$main.hide();
        this.$footer.hide();
      }

      this.allCheckbox.checked = !remaining;
    },

    // 할일 항목을 위한 뷰를 생성하고 `<ul>`에 뷰의 요소를
	// 추가함으로써 단일 할일 항목을 목록에 추가한다,
    addOne: function( todo ) {
      var view = new app.TodoView({ model: todo });
      $('#todo-list').append( view.render().el );
    },

    // 한번에 **Todos** 컬렉션에 모든 항목을 추가한다.
    addAll: function() {
      this.$('#todo-list').html('');
      app.Todos.each(this.addOne, this);
    },

    filterOne : function (todo) {
      todo.trigger('visible');
    },

    filterAll : function () {
      app.Todos.each(this.filterOne, this);
    },

    // 새로운 Todo 항목에 속성을 생성한다.
    newAttributes: function() {
      return {
        title: this.input.val().trim(),
        order: app.Todos.nextOrder(),
        completed: false
      };
    },

    // 입력 필드에 리턴키를 누르면, *localStorage*에 유지되는
	// 새로운 **Todo** 모델을 생성한다.
    createOnEnter: function( e ) {
      if ( e.which !== ENTER_KEY || !this.input.val().trim() ) {
        return;
      }

      app.Todos.create( this.newAttributes() );
      this.input.val('');
    },

    // 모든 완료된 할일 항목들을 모델을 파굄함으로써 제거한다.
    clearCompleted: function() {
      _.each( window.app.Todos.completed(), function( todo ) {
        todo.destroy();
      });

      return false;
    },

    toggleAllComplete: function() {
      var completed = this.allCheckbox.checked;

      app.Todos.each(function( todo ) {
        todo.save({
          'completed': completed
        });
      });
    }
  });

```

## 각각의 Todo 뷰

이젠 `TodoView` 뷰를 보자. 이 뷰는 할일이 갱신될 때, 뷰도 갱신되도록 하면서 개별의 Todo를 책임지고 있을 것이다. 이 상호동작을 활성화하기 위해서 이벤트 리스너를 뷰에 추가해야 한다. 이벤트 리스너는 html에 나타나는 각각의 할일에 대한 이벤트를 감시할 것이다.

```javascript

  // js/views/todo.js

  var app = app || {};

  // 할일 항목 뷰
  // --------------

  // 할일 항목에 대한 DOM 요소
  app.TodoView = Backbone.View.extend({

    //... li 태그
    tagName:  'li',

    // 단일 아이템에 대한 템플릿 함수를 캐쉬한다.
    template: _.template( $('#item-template').html() ),

    // 항목에 지정된 DOM 이벤트
    events: {
      'dblclick label': 'edit',
      'keypress .edit': 'updateOnEnter',
      'blur .edit': 'close'
    },

    // TodoView는 다시 렌더링하기 위해서 모델의 변경을 감시한다.
    // 이 앱에서는 **Todo**와 **TodoView** 사이에 일대일 대응이 있기 때문에,
    // 편의상 모델에 직접적인 참조를 설정할 수 있다.
    initialize: function() {
      this.model.on( 'change', this.render, this );
    },

    // 할일 항목을 모델의 현재 상태로 다시 렌더링한다.
    // 그리고, 뷰안에 할일 수정 입력에 대한 참조를 갱신한다.
    render: function() {
      this.$el.html( this.template( this.model.toJSON() ) );
      this.input = this.$('.edit');
      return this;
    },

    // 이 뷰를 입력 필드를 보여주기 위해 `"editing"` 모드로 전환한다.
    edit: function() {
      this.$el.addClass('editing');
      this.input.focus();
    },

    // 할일에 대한 변경을 저장하기 위해 `"editing"` 모드를 끝낸다.
    close: function() {
      var value = this.input.val().trim();

      if ( value ) {
        this.model.save({ title: value });
      }

      this.$el.removeClass('editing');
    },

    // 항목을 수정하는 동안 `enter`를 누르면
    updateOnEnter: function( e ) {
      if ( e.which === ENTER_KEY ) {
        this.close();
      }
    }
  });

```


`initialize()` 생성자에서, 우리는 할일 모델에 대한 이벤트에 리스너를 설정할 것이다. 즉, 할일이 갱신되면, 그 변경을 반영하는 뷰를 재 렌더링하고 싶다.

`render()` 메쏘드 안에서, 우리는 `#item-template`으로 불리는 Underscore.js 자바스크립트 템플릿으로 렌더링한다. 그 템플릿은 이전에 Underscore.js의 `_.template()` 메쏘드를 사용해서 this.template으로 컴파일했다. 이 템플릿은 뷰의 현재 요소를 변경하기 위해 사용하는 HTML 조각을 반환한다. 즉, 렌더링 템플릿은 현제 `this.el` 밑에 존재하고 그것은 할일 목록에 추가될 수 있다.

이벤트 해쉬는 세개의 콜백을 포함한다:

* `edit()`: 사용자가 할일 목록에 있는 항목을 더블 클릭했을 때, 현재 뷰를 편집 모드로 바꾼다. 이것은 항목의 제목 속성의 존재하는 값을 바꾸도록 해준다.
* `updateOnEnter()`: 사용자가 리터/엔터 키를 눌렀는지 확인해서 close() 함수를 실행한다.
* `close()`: 빈 문자열( 즉 ‘’)을 포한하고 있는 경우에 더 처리하지 않도록 `<input/>` 필드의 현재 문자열 값을 트림한다. 유효한 값이 제공되면, 현재 할일 모델에 변경을 저장하고 대응되는 CSS 클래스를 제개함으로써 편집 모드를 종료한다.

## 설정

결국 우리는 두개의 뷰를 갖게 되었다: `AppView`와`TodoView`. 전자는 페이지가 로드될 때 생성되어야만 하고 어떤 코드들은 실제로 실행된다. 당신이 jQuery의 `ready()` 유틸리티를 이일을 하기엔 충분히 단순하다. 이 메쏘드는 DOM이 로드될 때, 함수를 실행하는 것이다.

```javascript

  // js/app.js

  var app = app || {};
  var ENTER_KEY = 13;

  $(function() {

    // **App**을 생성함으로써 시작한다.
    new app.AppView();

  });

```

## 동작

이제 우리는 제대로 동작하는지 확인하지 않고 너무 많이 왔다.

당신이 계속해서 index.html을 열면, ( 계획대로라면 ) 당신은 콘솔에 아무 에러도 보지 못해야 한다. (우리가 아직 어떤 할일도 만들지 않았으므로 ) 할일 목록은 비어있어야 할 것이고, 할일 목록은 아직 우리의 이벤트를 가로채지 않기 때문에 아무 동작도 아지않는다. 그러나, 우리는 콘솔에서 Todo를 생성할 수 있다.

입력: `window.app.Todos.create({ title: 'My first Todo item'});` 리턴을 누른다.

![](img/todoconsole.png)

당신이 콘솔에서 위의 명력을 실행하면, 할일 컬렉션에 방금 추가한 새로운 할일을 (콘솔 출력으로) 보여야만 한다. 생성된 할일은 Local Storage에 저장되고 페이지 갱신이 될 것이다.

위에서 사용된 `window.app.Todos.create()`는 컬렉션 정의에 전달한 타입의 새로운 모델 항목을 생성하는 컬렉션 메쏘드(`collection.create(attributes, [options])`)이다. 우리의 경우에는 `app.Todo` 타입을 생성한다:

```javascript

  var TodoList = Backbone.Collection.extend({

      model: app.Todo // 컬렉선에 새로운 모델을 생성하기 위해 collection.create()이 사용하는 모델
      ...
  )};

```

확인하기 위해서 다음을 실행한다:

`var secondTodo = window.app.Todos.create({ title: 'My second Todo item'});`

`secondTodo instanceof app.Todo`

![](img/todoconsole2.png)

## 템플릿


`TodoView` 뷰에서 사용된 `#item-template`가 정의를 필요로 하기 때문에 정의해 보자. 페이지내에 템플릿을 포함하는 한가지 방법은 사용자 정의 script 태그를 사용하는 것이다. 이 태그는 브라우져가 처리하지 않는다. 브라우져는 그것을 일반 문자열로 해석한다. 그리고나서 Underscore 마이크로 템플릿등은 HTML 조각을 그리기 위해 그 템플릿에 접근할 수 있다.

```html
  <!-- index.html -->

  <script type="text/template" id="item-template">
    <div class="view">
      <input class="toggle" type="checkbox" <%= completed ? 'checked' : '' %>>
      <label><%= title %></label>
      <button class="destroy"></button>
    </div>
    <input class="edit" value="<%= title %>">
  </script>
```

위에서 보여준 `<%=`과 같은 템플릿 태그들은 Underscore.js에 특화된 것이고 Underscore 사이트에 문서화되어 있다. 당신이 만들 어플리케이션에서 Mustache나 Handlebars같은 템플릿 라이브러리를 선택할 수 있다. Backbone은 상관없으니 쓰고 싶은 것을 써라.

이제 `TodoView` 뷰 안에서 `_.template( $('#item-template').html() )`가 호출될 때, 템플릿은 정상적으로 렌더링할 것이다.


우리는 또한 얼마나 많은 항목들이 완료되었는지 보여줄 뿐만 아니라 사용자가 이 항목들을 제거하게 해주는데 사용하는 #stats-template 템플릿도 정의해야만 한다.

```html
  <!-- index.html -->

  <script type="text/template" id="stats-template">
    <span id="todo-count"><strong><%= remaining %></strong> <%= remaining === 1 ? 'item' : 'items' %> left</span>
    <ul id="filters">
      <li>
        <a class="selected" href="#/">All</a>
      </li>
      <li>
        <a href="#/active">Active</a>
      </li>
      <li>
        <a href="#/completed">Completed</a>
      </li>
    </ul>
    <% if (completed) { %>
    <button id="clear-completed">Clear completed (<%= completed %>)</button>
    <% } %>
  </script>
```


## 동작

이제 index.html을 갱신하면 우리가 작업한 결과가 보여야만 한다.

앞서 콘솔을 통해 추가한 할일들이 Local Storage에서 취합되어 목록에 나타나야만 한다. 또한 우리는 할일 이름을 입력하고 새로운 할일을 생성하기 위해 리턴을 눌러서 폼을 제출할 수 있어야만 한다.

![](img/todocompleted.png)


엄청난 과정을 거쳤지만 할일을 완료하고 삭제하는 것은 어떤가?

## 할일의 완료와 삭제


그래서 우리 안내서의 다음 부분은 할일을 완료하고 삭제하는 것을 다룬다. 이 두가지 동작은 각 Todo 항목에 특화되어 있어서 이 기능은 TodoView 뷰에 추가해야만 한다.

이것의 핵심은 우리가 추가한 두 이벤트 처리자이다. 하나는 할일의 체크박스에 붙은 togglecompleted 이벤트이고 다른 하나는 할일의 `<button class="destroy" />` 버튼에 붙은 클릭 이벤트이다.

체크박스의 togglecompleted 이벤트는 toggle() 함수를 호출하는데, 이 함수는 todo 모델의 완료 상태를 전환하고 할일을 다시 저장한다 - 매우 직관적이다!
버튼 클릭 이벤트는 `clear()`를 실행하는데, 이 함수는 단순히 todo 모델을 파괴한다.


이게 거기에 붙어있는 다있다. 우리가 변경 이벤트를 바인딩했기 때문에, todo 모델이 변경될 때마다 체크박스가 선택되거나 안 선택되면서 뷰는 자동적으로 다시 그려질 것이다. 유사한 방식으로 todo 모델이 삭제될 때, 우리가 destroy 이벤트를 바인딩했기 때문에 뷰에서 할일이 제거되하기 위해 모델의 `destroy()` 함수가 호출될 것이다.

우리가 할일 항목의 보여줌 상태를 제어하기 위해 visible 이벤트도 바인딩한 것도 여러번 말했다. 이것이 어떤 지점에서 필터링과 컬렉션을 결합하는데 사용되기 때문에 우리는 현재 필터로 완료 상태인 항목만 볼 수 있는 것이다.

이 안내서가 길어지기 때문에, 우리는 즉시 수정과 갱신은 다루지 않는다. 만일 그에 대한 예제를 원한다면, [complete source](https://github.com/addyosmani/todomvc/tree/master/architecture-examples/backbone/)를 보아라.

```javascript

  // js/view/todos.js

  // 할일 항목 뷰
  // --------------

  // 할일 항목에 대한 DOM 요소...
  app.TodoView = Backbone.View.extend({

    //... li 태그
    tagName:  'li',

    // 단일 아이템에 대한 템플릿 함수를 캐쉬한다.
    template: _.template( $('#item-template').html() ),

    // 항목에 지정된 DOM 이벤트
    events: {
      'click .toggle':  'togglecompleted',
      'dblclick label': 'edit',
      'click .destroy': 'clear',
      'keypress .edit': 'updateOnEnter',
      'blur .edit':   'close'
    },

    // TodoView는 다시 렌더링하기 위해서 모델의 변경을 감시한다.
    // 이 앱에서는 **Todo**와 **TodoView** 사이에 일대일 대응이 있기 때문에,
    // 편의상 모델에 직접적인 참조를 설정할 수 있다.
    initialize: function() {
      this.model.on( 'change', this.render, this );
      this.model.on( 'destroy', this.remove, this );
      this.model.on( 'visible', this.toggleVisible, this );
    },

    // 할일 항목의 제목을 다시 그린다.
    render: function() {
      this.$el.html( this.template( this.model.toJSON() ) );
      this.$el.toggleClass( 'completed', this.model.get('completed') );

      this.toggleVisible();
      this.input = this.$('.edit');
      return this;
    },

    toggleVisible : function () {
      this.$el.toggleClass( 'hidden',  this.isHidden());
    },

    isHidden : function () {
      var isCompleted = this.model.get('completed');
      return ( // hidden cases only
        (!isCompleted && app.TodoFilter === 'completed')
        || (isCompleted && app.TodoFilter === 'active')
      );
    },

    // 모델의 `"completed"` 상태를 전환한다.
    togglecompleted: function() {
      this.model.toggle();
    },

    // 이 뷰를 입력 필드를 보여주기 위해 `"editing"` 모드로 전환한다.
    edit: function() {
      this.$el.addClass('editing');
      this.input.focus();
    },

    // 할일에 대한 변경을 저장하기 위해 `"editing"` 모드를 끝낸다.
    close: function() {
      var value = this.input.val().trim();

      if ( value ) {
        this.model.save({ title: value });
      } else {
        this.clear();
      }

      this.$el.removeClass('editing');
    },

    // 항목을 수정하는 동안 `enter`를 누르면
    updateOnEnter: function( e ) {
      if ( e.which === ENTER_KEY ) {
        this.close();
      }
    },

    // 항목을 제거하고, *localStorage*에서 모델을 삭제하고, 그 뷰를 제거한다.
    clear: function() {
      this.model.destroy();
    }
  });

```



## 할일 라우팅

마지막으로 우리는 라우팅에 도달했다. 그것은 우리가 활성화된 아이템 목록뿐만 아니라 완료된 아이템 목록도 손쉽게 북마크할 수 있게 해준다. 우리는 다음 지점을 지원할 것이다:

```javascript
#/ (all - default)
#/active
#/completed
```

![](img/todorouting.png)

지점은 필터가 적용된 할일 목록을 변경할 때, 필터에 대한 모델 수준과 필터 링크에 적용된 selected 클래스가 전환될 것이다. 필터링된 동안 항목이 갱신되면, 그에 때라 갱신될 것이다.
즉 필터가 active이고 항목이 완료상태이면, 그 항목은 숨겨질 것이다. active 필터는 리로드에도 유지된다.

```javascript

  // js/routers/router.js

  // 할일 라우터
  // ----------

  var Workspace = Backbone.Router.extend({
    routes:{
      '*filter': 'setFilter'
    },

    setFilter: function( param ) {
      // 현재 필터를 사용중인 것으로 설정한다
      window.app.TodoFilter = param.trim() || '';

      // Todo 뷰 항목을 보이거나 숨기기 위해
	  // 컬렉션에 필터 이벤트를 구동한다.
      window.app.Todos.trigger('filter');
    }
  });

  app.TodoRouter = new Workspace();
  Backbone.history.start();

```

`window.app.Todos.trigger('filter')` 줄에서 보듯이, 문자열 필터가 설정되면 단순히 항목들을 보이고 안보이게 하기 위해 컬렉션 수준에서 필터를 구동한다.

결국, 우리는 페이지 로딩동안 초기 URL을 우회하기 위해 `Backbone.history.start()`를 호출한다.

## 결론

우리는 이젠 첫번째 완전한 Backbone.js 어플리케이션을 개발하는 방법을 배웠다. 전체 앱은 온라인상에서 언제라도 볼 수 있고, 소스는 [TodoMVC](http://www.todomvc.com)에서 볼 수 있다.

이 책의 후반부에서 우리는 RequireJS를 사용해서 어플리케이션을 더욱 모듈화하고 유지 계층을 데이타베이스로 바꾸고, 결국에는 몇 개의 테스팅 프레임워크로 어플리케이션을 단위테스트 하는 것을 배울 것이다.

# 연습 2: 책 도서관 - 첫번째 REST한 Backbone.js 앱


*작성자: Björn Ekengren, Addy Osmani*

##파트 1

이번 연습에서 우리는 Backbone을 사용해서 디지탈 책을 관리하는 도서과 어플리케이션을 만들 것이다.


###설정

우서 우리는 프로젝트를 위한 단순한 폴더 구조가 필요하다. css, img 그리고 js 디렉토리를 프로젝트 루트 폴더에 만들어라.

Backbone과 Underscore와 jQuery 라이브러리를 다운받아서 js 폴더에 복사해로. 아래 이미지는 img폴더에 저장한다:

![](http://codebyexample.info/wp-content/uploads/2012/03/placeholder.png)

새로운 index.html 파일을 프로젝트의 루트에 생성하고 다음을 입력해라:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8"/>
    <title>Backbone.js Library</title>
    <link rel="stylesheet" href="css/screen.css">
</head>
<body>
<div id="books">
    <div class="bookContainer">
        <img src="img/placeholder.png"/>
        <ul>
            <li>Title</li>
            <li>Author</li>
            <li>Release date</li>
            <li>Keywords</li>
        </ul>
    </div>
</div>
<script src="js/jquery-1.7.1.js"></script>
<script src="js/underscore.js"></script>
<script src="js/backbone.js"></script>
<script src="js/app.js"></script>
</body>
</html>
```

부라우져에서 이 파일을 열면 다음과 같이 보여야한다:

![](http://codebyexample.info/wp-content/uploads/2012/03/Screen-Shot-2012-03-05-at-12.57.08-AM1.png)

뭐 대단할 건 없다. 이 문서는 CSS 안내서는 아니지만 약간 이쁘게 할 필요는 있다. css 폴더에 screen.css 파일을 생성하고, 다음을 입력해라:

```css
body {
    background-color: #eee;
}

.bookContainer {
    border: 1px solid #aaa;
    width: 300px;
    height: 130px;
    background-color: #fff;
    float: left;
    margin: 5px;
}
.bookContainer img {
    float: left;
    margin: 10px;
}
.bookContainer ul {
    list-style-type: none;
}
```
이제 좀 나아 보인다:

![](http://codebyexample.info/wp-content/uploads/2012/03/Screen-Shot-2012-03-05-at-1.06.15-AM.png)


이것은 우리가 보고 싶어하는 최종 결과물이지만, 더 많을 책들이 보일 것이다. 계속 진행해보면, 그 모습이 어떻게 보이는지 알고 싶다면, bookContainer div를 몇개 복사해봐라. 이제 우리는 실제 어플리케이션을 개발할 준비가 되었다. app.js를 열고 다음을 입력해라:

```js
(function ($) {

    var Book = Backbone.Model.extend({
        defaults:{
            coverImage:"img/placeholder.gif",
            title:"Some title",
            author:"John Doe",
            releaseDate:"2012",
            keywords:"JavaScript Programming"
        }
    });

})(jQuery);
```

이것은 책에 대한 우리 모델이다. 우리가 모델이 포함했으면 하는 모든 값에 대한 기본값을 할당하는 기본 특성을 포함하고 있다. “jQuery” 인자로 스스로 실행되는 함수로 모든 것을 감쌌다는 것을 알아둬라. 이것은 전역 범위를 오염시키는 것을 막고, $ 변수의 충돌을 피하는 표준적인 방식이다. 그안에서 모델은 그다지 유용하지 않기 때문에 우리는 i와 뷰를 쌍으로 묶어야만 한다. 뷰에서 템플릿이 필요하면, index.html을 열고 이미 만들어 놓은 bookContainer에 템플릿을 생성한다.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8"/>
    <title>Backbone.js Library</title>
    <link rel="stylesheet" href="css/screen.css">
</head>
<body>
<div id="books">
    <div class="bookContainer">
        <img src="img/placeholder.png"/>
        <ul>
            <li>Title</li>
            <li>Author</li>
            <li>Release date</li>
            <li>Keywords</li>
        </ul>
    </div>
    <script id="bookTemplate" type="text/template">
        <img src="<%= coverImage %>"/>
        <ul>
            <li><%= title %></li>
            <li><%= author %></li>
            <li><%= releaseDate %></li>
            <li><%= keywords %></li>
        </ul>
    </script>
</div>
<script src="js/jquery-1.7.1.js"></script>
<script src="js/underscore.js"></script>
<script src="js/backbone.js"></script>
<script src="js/app.js"></script>
</body>
</html>
```

그러면 여기에서 무슨일이 있어나냐고? 글쎄, 나는 템플릿을 “text/template” 타입의 script 태그로 감쌌다. 이렇게 함으로써 프라우져는 타입을 인식하지 않고 렌더링하지 않을 것이다. 하지만 우리는 여전히 자바스크립트로 모든 요소에 접근할 수 있다. Backbone( 원문에는 템플릿 엔진( Underscore )이 생성한다고 되어있지만 이것은 틀린 말이다.)이 생성할 것이기 때문에, 감싸고 있던 div 태그를 제거하였다. 다양한 항목에 대해서 Underscore가 찾아서 실제 데이타로 대치할 <%= 항목 %>을 입력하였다. 이제 뷰를 생성하는데 쓸 템플릿을 갖게 되었다. 다시 app.js로 넘어가자:

```js
(function ($) {

    var Book = Backbone.Model.extend({
        defaults:{
            coverImage:"img/placeholder.gif",
            title:"Some title",
            author:"John Doe",
            releaseDate:"2012",
            keywords:"JavaScript Programming"
        }
    });

    var BookView = Backbone.View.extend({
        tagName:"div",
        className:"bookContainer",
        template:$("#bookTemplate").html(),

        render:function () {
            var tmpl = _.template(this.template); //tmpl은 JSON객체를 받아서 html을 반환하는 함수이다.

            this.$el.html(tmpl(this.model.toJSON())); //this.el은 tagName에 정의된 것이다. jQuery html() 함수를 사용하기 위해서는 $el을 쓴다.
            return this;
        }
    });

})(jQuery);
```

그래서 뷰는 extend 함수를 써서, 그것 특성들을 전달하는 모델과 같이 동작한다. tagName 특성은 뷰의 컨테이너를, 또 template은 뷰에 대한 템플릿을 정의한다. render 함수는 하나의 인자( index.html에 있는 템플릿 )로 Underscore의 template 함수를 호출함으로써 tmpl 함수를 생성한다. 그리고 나서 모델을 사용해서 `tmpl` 함수를 호출한다… 잠깐 기다려라. 무슨 모델이냐고? 글쎄, 이것은 뷰 생성자를 호출할 때 인자로 전달되어야만 하는 것이다. 지금보니 뷰는 html 페이지의 어떤 요소에도 연결되어 있지 않다. 이제 그것을 관리해보자:

```js
(function ($) {

    var Book = Backbone.Model.extend({
        defaults:{
            coverImage:"img/placeholder.gif",
            title:"Some title",
            author:"John Doe",
            releaseDate:"2012",
            keywords:"JavaScript Programming"
        }
    });

    var BookView = Backbone.View.extend({
        tagName:"div",
        className:"bookContainer",
        template:$("#bookTemplate").html(),

        render:function () {
            var tmpl = _.template(this.template); //tmpl은 JSON객체를 받아서 html을 반환하는 함수이다.

            this.$el.html(tmpl(this.model.toJSON())); //this.el은 tagName에 정의된 것이다. jQuery html() 함수를 사용하기 위해서는 $el을 쓴다.
            return this;
        }
    });

    var book = new Book({
        title:"Some title",
        author:"John Doe",
        releaseDate:"2012",
        keywords:"JavaScript Programming"
    });

    bookView = new BookView({
        model: book
    });

    $("#books").html(bookView.render().el);

})(jQuery);
```

여기에서 Book의 생성자를 부르고 원하는 속성을 전달해서 새 Book 모델을 생성한다. 그 이후에 모델은 BookView를 생성할 때 사용된다. 마지막에 bookView가 렌더링되고 페이지에 추가된다. 그것은 다음처럼 보인다:

![](http://codebyexample.info/wp-content/uploads/2012/03/Screen-Shot-2012-03-05-at-10.53.34-PM.png)


잘 보인다면, 이제는 잘 돌아가는 Backbone 어플리케이션을 갖게된 것이다. 도서과이 책 한권만 가지고 있는 것은 아니기 때문에 우리는 좀더 만들어야만 한다. 컬렉션을 한번 보자. 컬렉션은 모델들의 묶음을 포함한다. 모델들은 동일한 종류여야만 한다. 즉 같은 컬렉션에 사과와 오렌지를 섞어서 넣을 수 없다. 컬렉션은 너무 단순해서 아래와 같이 컬렉션이 담고 있는 모델의 종류를 적는 것 외에 할 것이 없다:

```js
var Library = Backbone.Collection.extend({
    model:Book
});
```

계속해서 app.js에 코드를 입력해라. 다음에 살펴볼 것은 Library 컬렉션에 대한 새 뷰이다. 이 뷰는 앞에서 본 BookView보다 조금 복잡하다:

```js
var LibraryView = Backbone.View.extend({
        el:$("#books"),

        initialize:function(){
            this.collection = new Library(books);
            this.render();
        },

        render: function(){
            var that = this;
            _.each(this.collection.models, function(item){
                that.renderBook(item);
            }, this);
        },

        renderBook:function(item){
            var bookView = new BookView({
                model: item
            });
            this.$el.append(bookView.render().el);
        }
    });
```

무엇을 하는지 내가 설명할 수 있도록 몇줄 추가했다. 두번째 줄에 “el” 특성을 지정했다. 뷰는 `BookView` 에서 본 것처럼 tagName을 가지거나 el을 가질 수 있다. tagName을 쓰면, 뷰는 요소를 생성하겠지만, 페이지에 넣는 것은 우리 몫이다. 우리가 el을 사용할 때는 우리는 페이지에 이미 존재하는 요소를 지정해서 뷰가 직접적으로 페이지의 지정한 요소에다 쓸 것이다. 이 경우에는 id가 ”books”인 div를 선택하였다.

다음으로 네번째 줄에서 initialize 함수가 있다. 이 함수는 뷰 생성자가 호출될 때, Backbone이 호출한다. 다섯번째 줄에서 우리는 새로운 Library( Book 모델의 컬렉션 )을 생성하고 “collection”라는 지역 특성에 저장한다. 여섯번째 줄에서 자신의 render 함수를 호출하는데, `LibraryView` 생성자가 호출되자마자 렌더링하려고 하기 때문에 이것은 스스로 렌더링하는 뷰이다. 뷰가 스스로 렌더링하도록 만드는 것이 필수는 아니지만 일반적인 형태이다.

render 함수안의 열번째 줄에서 현재 객체의 참조( 역자주: `this` )를 “that” 변수에 저장하고나서 (열한번째 줄에서) Underscore의 each 함수를 써서 컬렉션내의 모든 모델( Books )을 순회한다. “each”의 첫번째 인자는 순회할 배열이다. 두번째 인자는 배열을 각 객체에 적용할 함수이다. 이 경우의 함수는 현재 모델을 인자로 갖는 renderBook을 호출한다. “this”를 사용하면 그것은 함수 그 자체를 참조하기 때문에 잘 돌아가기 위해서 “that”을 사용해야만 한다. ( 열세번째 줄의 ) 세번째 인자는 각각이 실행되는 컨택스트이다.

열여섯번째 줄에서 우리는 모델( Book )을 인자로 갖는 `renderBook` 함수를 정의하고 `BookView`를 생성하는데 사용한다. 그리고 나서 `bookView`가 렌더링되고 ( 두번째 줄에서 ) el 특성에 지정되었던 뷰 컨테이너에 추가된다.

다섯번째 줄에서 “books” 인자로 Library 생성자를 호출하는 것을 유심히 보아야 한다. Library는 Book 모델을 생성하는데 사용할 수 있는 객체 배열을 받는 Backbone 컬렉션이다. 우리는 아직 books 변수를 정의하지 않았으니까 더 진행해보자:

```js
var books = [{title:"JS the good parts", author:"John Doe", releaseDate:"2012", keywords:"JavaScript Programming"},
        {title:"CS the better parts", author:"John Doe", releaseDate:"2012", keywords:"CoffeeScript Programming"},
        {title:"Scala for the impatient", author:"John Doe", releaseDate:"2012", keywords:"Scala Programming"},
        {title:"American Psyco", author:"Bret Easton Ellis", releaseDate:"2012", keywords:"Novel Splatter"},
        {title:"Eloquent JavaScript", author:"John Doe", releaseDate:"2012", keywords:"JavaScript Programming"}]
```

이제 우리는 거의 Backbone 도서과의 첫번째 버젼을 시험할 준비가 됐다. 다음 코드를 수정해라:

```js
    var book = new Book({
        title:"Some title",
        author:"John Doe",
        releaseDate:"2012",
        keywords:"JavaScript Programming"
    });

    bookView = new BookView({
        model: book
    });

    $("#books").html(bookView.render().el);
```

다음 코드를 추가한다:

var `libraryView = new LibraryView();`
브라우져에서 index.html을 보면, 이렇게 보일 것이다.

![](http://codebyexample.info/wp-content/uploads/2012/03/Screen-Shot-2012-03-06-at-9.58.03-AM.png)

최종적인 app.js는 다음과 같다:

```js
(function ($) {
    var books = [{title:"JS the good parts", author:"John Doe", releaseDate:"2012", keywords:"JavaScript Programming"},
        {title:"CS the better parts", author:"John Doe", releaseDate:"2012", keywords:"CoffeeScript Programming"},
        {title:"Scala for the impatient", author:"John Doe", releaseDate:"2012", keywords:"Scala Programming"},
        {title:"American Psyco", author:"Bret Easton Ellis", releaseDate:"2012", keywords:"Novel Splatter"},
        {title:"Eloquent JavaScript", author:"John Doe", releaseDate:"2012", keywords:"JavaScript Programming"}];

    var Book = Backbone.Model.extend({
        defaults:{
            coverImage:"img/placeholder.gif",
            title:"Some title",
            author:"John Doe",
            releaseDate:"2012",
            keywords:"JavaScript Programming"
        }
    });

    var Library = Backbone.Collection.extend({
       model:Book
    });

    var BookView = Backbone.View.extend({
        tagName:"div",
        className:"bookContainer",
        template:$("#bookTemplate").html(),

        render:function () {
            var tmpl = _.template(this.template); //tmpl은 JSON객체를 받아서 html을 반환하는 함수이다.

            this.$el.html(tmpl(this.model.toJSON())); //this.el은 tagName에 정의된 것이다. jQuery html() 함수를 사용하기 위해서는 $el을 쓴다.
            return this;
        }
    });

 var LibraryView = Backbone.View.extend({
        el:$("#books"),

        initialize:function(){
            this.collection = new Library(books);
            this.render();
        },

        render: function(){
            var that = this;
            _.each(this.collection.models, function(item){
                that.renderBook(item);
            }, this);
        },

        renderBook:function(item){
            var bookView = new BookView({
                model: item
            });
            this.$el.append(bookView.render().el);
        }
    });

    var libraryView = new LibraryView();

})(jQuery);
```

여기에서 무슨 일이 일어나는지 다시 살펴보자:

* Line 58: LibraryView 생성자가 호출된다
* Line 36: LibraryView는 html의 books div와 연결된다.
* Line 39: Book 모델의 컬렉션을 생성하기 위해, 두번째 줄의 책 속성 배열로 Library 생성자가 호출된다.
* Line 43: render 함수는 Book 컬렌션을 순회하면서 각 Book 모델에 대해서 마흔여섯번째 줄에서 renderBook을 호출한다.
* Line 51: renderBook 함수는 주어진 Book 모델에서 새로운 BookView를 생성한다.
* Line 54: BookView의 render 함수가 호출되고 그 결과물은 html의 books div에 추가된다.

당신은 이제 Backbone의 기본 컴포넌트인 모델, 뷰, 그리고 컬렉션을 알게되었다. 다음 파트에서 우리의 Library를 좀더 상호동작하도록 발전시킬 것이다.

이 안내서의 코드들은 [여기](https://dl.dropbox.com/u/70775642/workshop-practical/code.zip)에서 사용가능하다.

##파트 2

첫번째 파트에서 나는 Backbone의 기본인 모델, 뷰, 컬렉션을 다뤘다. 이 파트는( 역자주: tutorial이라고 언급되는 것으로 보아 원문은 분리된 Article이었던 것같다. ) 첫번째 파트를 기초로 작성되었기 때문에, 다음을 진행하기에 앞서 읽지 않았다면 읽어보기를 권한다. 이번 파트에서는 모델을 컬렉션에 어떻게 추가하고 삭제하는지를 볼 것이다.

###모델 추가하기

새로운 책을 추가하기 위해서 일련의 입력 폼이 있어야 한다. index.html에 추가해보자

```html
<div id="books"><form id="addBook" action="#">
<div><label for="coverImage">CoverImage: </label><input id="coverImage" type="file" />
 <label for="title">Title: </label><input id="title" type="text" />
 <label for="author">Author: </label><input id="author" type="text" />
 <label for="releaseDate">Release date: </label><input id="releaseDate" type="text" />
 <label for="keywords">Keywords: </label><input id="keywords" type="text" />
 <button id="add">Add</button></div>
</form></div>
```

나는 나중에 다시 맵핑할 필요가 없도록 하기 위해서 인풋의 아이디를 Book 모델의 속성과 맞추었다. screen.css에 아래보이는 코드를 추가해라

```css
#addBook label {
    width:100px;
    margin-right:10px;
    text-align:right;
    line-height:25px;
}
 
#addBook label, #addBook input {
    display:block;
    margin-bottom:10px;
    float:left;
}
 
#addBook label[for="title"], #addBook label[for="releaseDate"] {
    clear:both;
}
 
#addBook button {
    display:block;
    margin:5px 20px 10px 10px;
    float: right;
    clear: both;
}
 
#addBook div {
    width: 550px;
}
 
#addBook div:after {
    content:"";
    display:block;
    height:0;
    visibility:hidden;
    clear:both;
    font-size:0;
    line-height:0;
}
```

이제 책을 추가하는 함수를 작성해보자. 그 함수를 가장 상위의 뷰( LibraryView )에 render 함수 뒤쪽에 넣자.

```js
addBook: function(){
    var formData = {};
 
    $("#addBook").children("input").each(function(i, el){
        formData[el.id] = $(el).val();
    });
 
    books.push(formData);
 
    this.collection.add(new Book(formData));
},
```

여기에서 나는 폼의 입력 요소 모두를 선택해서 jQuery의 each를 써서 순회한다. 우리가 폼에서 Book 모델의 키와 동일한 아이디를 같은 이름으로 썼기 때문에, 단순히 formData에 바로 저장해서는 books 배열에 추가할 수 있다. 그리고나서 우리는 새로운 Book 모델을 생성하고 컬렉션에 추가한다. 이제 이 함수를 폼의 Add 버튼에 연결하자. 우리는 LibraryView에 이벤트 리스너를 추가해서 이작업을 한다.

```js
events:{
    "click #add":"addBook"
},
```

기본적으로 Backbone은 함수에 이벤트 객체를 전달할 것이다. 폼이 실제로 전송되어서 페이지가 리로드되는 것을 막고 싶기 때문에 이런 방식은 이 경우에 유용하다. addBook 함수에 preventDefault 구문을 추가한다.

```js
addBook: function(e){
    e.preventDefault();
 
    var formData = {};
 
    $("#addBook").children("input").each(function(i, el){
        formData[el.id] = $(el).val();
    });
 
    books.push(formData);
 
    this.collection.add(new Book(formData));
},
```

이 코드가 잘 돌아가면, books 배열과 컬렉션에 책을 추가할 것이다. 하지만 BookView의 render 함수를 호출하지 않았기 때문에 보지지는 않을 것이다. 모델이 컬렉션에 추가될 때, 컬렉션이 add 이벤트를 발동할 것이다. 만일 이 이벤트를 감시하면, renderBook 함수를 호출할 수 있을 것이다. 이 바인딩은 initialize에서 이뤄진다.

```js
initialize:function () {
    this.collection = new Library(books);
    this.render();
 
    this.collection.on("add", this.renderBook, this);
},
```

이제 어플리케이션을 돌려볼 준비가 되었다.

![](http://codebyexample.info/wp-content/uploads/2012/04/Screen-Shot-2012-04-05-at-1.24.51-AM.png)

미리 말했다시피, 필드를 비워두면, 생성된 뷰도 비어있을 것이다. 이건 우리가 원하는 바가 아니다. 우리는 기본값이 채워져있길 바란다. 그렇게 하기 위해서 약간의 로직을 추가해야만 한다. 또한 표지 이미지를 위한 파일 입력도 동작하지 않는 것도 알아두기만 하고 독자의 숙제로 남겨두겠다.

```js
addBook:function (e) {
    e.preventDefault();
 
    var formData = {};
 
    $("#addBook div").children("input").each(function (i, el) {
        if ($(el).val() !== "") {
            formData[el.id] = $(el).val();
        }
    });
 
    books.push(formData);
 
    this.collection.add(new Book(formData));
},
```

여기에 ( 일곱번째 줄에 ) 함목의 값이 비어있는지를 확인하도록 추가했다. 그 경우에 모델 데이타에 추가하지 않도록 했다. 그때에는 Book의 나머지 특성을 위한 기본값을 추가하자.

```js
var Book = Backbone.Model.extend({
    defaults:{
        coverImage:"img/placeholder.png",
        title:"No title",
        author:"Unknown",
        releaseDate:"Unknown",
        keywords:"None"
    }
});
```

이젠 더 나은 기본 동작을 한다.

![](http://codebyexample.info/wp-content/uploads/2012/04/Screen-Shot-2012-04-05-at-11.41.59-AM1.png)

###모델 삭제하기

이제 Books를 제거하는 방법을 보자. 우리는 먼저 index.html의 템플릿에 삭제 버튼을 추가해보자.

```html
<script id="bookTemplate" type="text/javascript">// <![CDATA[
    <img src="<%= coverImage %>"/>
<ul>
    <li><%= title%></li>
 
    <li><%= author%></li>
 
    <li><%= releaseDate%></li>
 
    <li><%= keywords%></li>
 
</ul>
 
    <button class="delete">Delete</button>
// ]]></script>
```

우리는 이쁘게 보기 위한 css도 추가한다. 존재하는 ul의 여백이 위쪽으로 좀더 붙도록했다.

```css
.bookContainer ul {
    list-style-type: none;
    margin-bottom: 0;
}
 
.bookContainer button {
    float:right;
    margin: 10px;
}
```

잘 되었다!

![](http://codebyexample.info/wp-content/uploads/2012/04/Screen-Shot-2012-04-05-at-11.59.54-AM.png)

이제 우리는 로직에 버튼을 붙여야 한다. 이것은 add 버튼과 같은 방식으로 한다. deleteBook 함수를 BookView에 생성해보자

```js
var BookView = Backbone.View.extend({
    tagName:"div",
    className:"bookContainer",
    template:$("#bookTemplate").html(),
 
    render:function () {
		var tmpl = _.template(this.template); //tmpl은 JSON객체를 받아서 html을 반환하는 함수이다.
 
		this.$el.html(tmpl(this.model.toJSON())); //this.el은 tagName에 정의된 것이다. jQuery html() 함수를 사용하기 위해서는 $el을 쓴다.
        return this;
    },
 
    deleteBook:function () {
        //모델을 삭제한다.
        this.model.destroy();
 
        //뷰를 삭제한다.
        this.remove();
    }
});
```

그리고 나서 삭제버튼에 이벤트 리스너를 추가한다.

```js
var BookView = Backbone.View.extend({
    tagName:"div",
    className:"bookContainer",
    template:$("#bookTemplate").html(),
 
    render:function () {
		var tmpl = _.template(this.template); //tmpl은 JSON객체를 받아서 html을 반환하는 함수이다.
 
		this.$el.html(tmpl(this.model.toJSON())); //this.el은 tagName에 정의된 것이다. jQuery html() 함수를 사용하기 위해서는 $el을 쓴다.
        return this;
    },
 
    events: {
        "click .delete": "deleteBook"
    },
 
    deleteBook:function () {
        //모델을 삭제한다.
        this.model.destroy();
 
        //뷰를 삭제한다.
        this.remove();
    }
});
```

테스트하면, 잘 돌아가는 것을 보게 될 것이다. 하지만 아직 끝난 것은 아니다. 우리가 삭제 버튼을 누르면, 모델과 뷰는 삭제될 것이지만, books 배열의 데이타는 아니다. 이것은 우리가 LibraryView를 다시 렌더링하면, 삭제된 책들이 다시 보인다는 것을 의미한다. Backbone 컬렉션은 똑똑해서, 그 안에 모델이 삭제될 때, “remove” 이벤트가 구동되는 것을 알려준다. 이것은 우리가 LibraryView에 감시하고 동작하는 함수를 두게한다. LibraryView의 initialize에ㅓ 리스너를 추가해라.

```js
initialize:function () {
    this.collection = new Library(books);
    this.render();
 
    this.collection.on("add", this.renderBook, this);
    this.collection.on("remove", this.removeBook, this);
},
```

여기에서는 컬렉션에서 remove 이벤트가 발생할 때, removeBook 함수가 호출되도록 지정했으니 이 함수를 생성하자. 컬렉션은 삭제된 모델을 이벤트의 인자로 전달하는 것을 알아둬라.

```js

removeBook: function(removedBook){
    var removedBookData = removedBook.attributes;
 
    _.each(removedBookData, function(val, key){
        if(removedBookData[key] === removedBook.defaults[key]){
            delete removedBookData[key];
        }
    });
 
    _.each(books, function(book){
        if(_.isEqual(book, removedBookData)){
            books.splice(_.indexOf(books, book), 1);
        }
    });
},
```

기본값은 books 배열에 저장되지 않기 때문에, 일치하는 것을 찾기 위해 그 값들은 빼야한다. 우리는 삭제된 Book 모델의 특성을 순회해서 기본값과 일치하는 특성을 삭제하기 위해 Underscore의 each 함수를 사용한다. Underscore의 each 함수도 배열의 객체들을 순회할 수 있기 때문에 삭제된 Book 데이타를 찾기위해 books 배열의 객체들을 순회하는데 다시 쓴다. 일치하는 것을 찾기 위해서 객체의 깊은 비교( deep comparison )을 수행하는 Underscore의 isEqual을 사용한다. 유사하게 indexOf도 복잡한 객체들을 찾는다. 그것은 splice를 사용해서 책 데이타를 제거할 때 사용한다.

###요약

이 안내서에서 우리는 컬렉션에 모델을 어떻게 추가하고 제거하는지 보았다. 우리는 또한 어떻게 이벤트 처리자를 사용해서 뷰, 모델, 컬렉션을 같이 묶는지도 보았다. 우리는 유용한 Underscore 함수인 each, indexOf, isEqual 함수도 보았다. 이 안내서에 관심이 간다면, 더 많은 내용들을 만들 것이다. 여전히 Backbone에서 다룰 많은 것들이 남아있다.

이 파트에 대한 코드는 [여기](https://dl.dropbox.com/u/70775642/workshop-practical/code.zip)에서 볼 수 있다.

##파트 2.5

이 시리즈의 앞 두 파트에서 우리는 Backbone 어플리케이션의 기본 구조와 모델을 추가하고 삭제하는 방법을 살펴보았다. 세번째 파트에서는 모델을 서버와 어떻게 동기화하는지를 살펴볼 것이다. 하지만, 그렇게 하기 위해서 우회해서 서버를 REST api로 설정할 필요가 있다. 그것이 이번 파트에서 우리가 할 일이다. 이것은 자바스크립트 안내서이기 때문에, node.js를 사용해서 서버를 만드는데 자바스크립트를 쓸 것이다. 당신이 다른 언어로 REST 서버를 설정하는 것이 더 편하다면, 따라야만 하는 API는 다음과 같다:

```
url HTTP 메쏘드 동작
/api/books  GET 모든 책의 배열을 얻는다.
/api/books/:id  GET 아이디가 :id인 책을 얻는다.
/api/books  POST  새로운 책을 추가하고 아이디가 추가된 그 책을 반환한다.
/api/books/:id  PUT 아이디가 :id인 책을 수정한다.
/api/books/:id  DELETE  아이디가 :id인 책을 삭제한다.
```

이 안내서에 대한 개략적인 내용은 다음과 같다:

* node.js, npm 그리고 MongoDB의 설치
* node 모듈들의 설치
* 디렉토리 구조 생성
* 단순한 웹서버 생성
* 데이타베이스 연결
* REST API 작성


nodejs.org에서 node.js를 다운로드하고 설치해라. 노드 패키지 매니져( npm )도 설치될 것이다.

mongo.org에서 MongoDB를 다운로드해서 설치해라. MongoDB를 설치할 때, MongoDB를 실행하기 위한 설정을 복사하는 명령을 날려라. OSX상에서 다음과 같다:

```
sudo cp /usr/local/Cellar/mongodb/2.0.4-x86_64/mongod.conf /usr/local/etc/mongod.conf
```

일단 설치만 된다면, 그것을 실행할 수 있다. 내 컴퓨터에서는 다음과 같다:

```
mongod run --config /usr/local/Cellar/mongodb/2.0.4-x86_64/mongod.conf
```

###node 모듈들의 설치

먼저 이 프로젝트를 위해서 새로운 폴더를 생성해라. 터미널을 사용해서 프로젝트 폴더로 이동해서 다음 명령을 실행한다:

```
npm install express@2.5.9
npm install path
npm install mongoose
```

express의 @2.5.9에 주의해라. 현재 안정화 버젼은 3.0.3이고 2.5.9와 다른 API를 가지고 있지만, 우리는 2.5.9버젼을 사용할 겄이다.

###디렉토리 구조 생성

프로젝트 루트 폴더에서 server.js 파일을 생성해라 - 서버 코드가 있을 곳이다. 그리고 나서 public 폴더를 생성한다. public 폴더안에 것들은 express 웹 서버에 의해서 클라이언트에 정적 자원으로 제공될 것이다. 이제 계속해서 파트 2의 모든 것을 public 폴더에 복사한다. 다 하고 나면 플더 구조는 다음과 같을 것이다:

```
node_modules/
  .bin/
  express/
  mongoose/
  path/
public/
  css/
  img/
  js/
  index.html
server.js
package.json
```

###단순한 웹서버 생성

server.js를 열고 다음을 입력한다:

```js
// 모듈 의존성
var application_root = __dirname,
    express = require("express"), //웹 프레임워크
    path = require("path"), //파일 패쓰를 다루는 유틸리티들
    mongoose = require('mongoose'); //MongoDB 통합
 
// 서버를 생성한다
var app = express.createServer();
 
// 서버를 설정한다
app.configure(function () {
    app.use(express.bodyParser()); //요청 바디를 파싱해서 req.body를 만든다
    app.use(express.methodOverride()); //HTTP 메쏘드를 덮어쓰기 위해서 req.body를 확인한다
    app.use(app.router); //url과 HTTP 메쏘드에 기반한 라우팅을 수행한다
    app.use(express.static(path.join(application_root, "public"))); //정적 자원을 제공하는 곳
    app.use(express.errorHandler({ dumpExceptions:true, showStack:true })); //개발시점에 모든 에러를 보여준다
});
 
// 서버를 구동한다
app.listen(4711, function () {
    console.log("Express server listening on port %d in %s mode", app.address().port, app.settings.env);
});
```

이 프로젝트에 필요한 모듈을 로딩하는 것으로 시작한다: HTTP 서버를 생성하기 위해 Express, 파일 경로를 다루는 Path, 데이타베이스와 연결하기 위한 mongoose. Express 서버를 생성하고 익명 함수를 사용해서 설정한다. 이것은 표준적인 설정이고 우리 어플리케이션을 위해서 methodOverride 부분은 실제로 필요하지 않다. 이것은 폼은 보통 GET과 POST만 지원하기 때문에 폼에서 바로 PUT과 DELETE HTTP 요청을 오는 것을 위해 사용된다. 마지막으로 listen 함수를 실행함으로써 서버를 구동한다. 사용된 포트 번호( 이 경우는 4711 )는 시스템의 어떤 남는 포트라도 될 수 있다. 그것은 임의의 숫자이기 때문에 단순히 4711를 썼다. 우리는 첫번째 서버를 구동할 준비가 되었다:

```js
node server.js
```

당신이 localhost:4711로 브라우져를 열면, 다음과 같은 모습이 보여야만 한다:

![](http://codebyexample.info/wp-content/uploads/2012/04/Screen-Shot-2012-04-05-at-11.59.54-AM1.png)

파트 2에서 해논 것과 같지만 지금은 직접 파일에서 대신에 서브를 돌리고 있다. 대단할 일이지 않는가! 우리는 이제 서버가 반을할 지점( URL )을 정의할 수 있다. 이 URL이 우리의 REST API가 될 것이다. app을 사용함으로써 정의된 지점은 HTTP 용어인 get, put, post 그리고 delete 중에 하나 뒤에 붙는다. 그것은 Create, Read, Update 그리고 Delete와 대응한다. server.js로 돌아가서 단순한 지점을 정의해라:

```js
// Routes
app.get('/api', function(req, res){
    res.send('Library API is running');
});
```

get 함수는 URL을 첫번째 인자로 가지고 함수를 두번째 인자로 가질 것이다. 그 함수는 request와 response 객체로 호출될 것이다. 이제 당신은 node를 재시작하고 그 URL로 가보자:

![](http://codebyexample.info/wp-content/uploads/2012/04/Screen-Shot-2012-04-23-at-10.09.35-AM.png)


###데이타베이스 연결

환상적이다. 이제 우리는 MongoDB에 데이타를 저장하고 싶으니까 스키마를 정의해야만 한다. 다음을 server.js에 추가해라:

```js
// 데이타베이스에 접속한다
mongoose.connect('mongodb://localhost/library_database');
 
// 스키마
var Book = new  mongoose.Schema({
    title:String,
    author:String,
    releaseDate: Date
});
 
// 모델
var BookModel = mongoose.model('Book', Book);
```

알다시피, 스키마 정의는 매우 직관적이다. 그것이 더 진보적이지만 이것이 우리를 위해 할 일이다. 나는 또한 Mongo에서 모델( BookModel )을 추출했다. 이것이 사용하는 방법이다. 다음으로는 전체 책을 반환하는 REST API를 위한 get 동작을 정의한다:

```js
// 모든 책 목록을 얻는다
app.get('/api/books', function (req, res) {
    return BookModel.find(function (err, books) {
        if (!err) {
            return res.send(books);
        } else {
            return console.log(err);
        }
    });
});
```

모델의 find 함수는 다음과 같이 정의된다: function find (conditions, fields, options, callback) – 하지만 우리는 모든 책을 반환하는 함수를 원하기 때문에, callback 인자만 필요하다. callback은 error 객체와 발견된 객체들의 배열을 인자로 호출될 것이다. 에러가 없으면, res 객체의 send 함수를 사용해서 클라이언트로 객체 배열을 반환하고 그렇지 않으면 콘솔에 에러를 출력한다.

우리 API를 테스트하기 위해서는 자바스크립트 콘솔에서 약간을 입력해야만 한다. node를 재시작하고 브라우져로 localhost:4711로 가본다. 자바스크립트 콘솔을 열어라. 구글 크롬을 사용한다면, 메뉴에서 View->Developer->JavaScript Console을 실행한다. 파이어폭스를 쓴다면, Firebug를 설치하고 View->Firebug를 실행한다. 다른 브라우져를 쓰고 있다면, 다른 어디선가 콘솔을 찾을 거라고 생각한다. 콘솔에서 다음을 입력해라:

```js
jQuery.get("/api/books/", function (data, textStatus, jqXHR) {
    console.log("Get resposne:");
    console.dir(data);
    console.log(textStatus);
    console.dir(jqXHR);
});
```

… 그리고 엔터를 누르면 다음이 보여야만 한다:

![](http://codebyexample.info/wp-content/uploads/2012/04/Screen-Shot-2012-04-29-at-12.50.32-AM.png)


페이지에 이미 로드되어 있기 때문에, 여기에서 나는 REST API를 호출하기 위해서 jQuery를 썼다. 반환된 배열은 비어있는 것이 확실하다. 왜냐하면 아직 데이타베이스에 아무것도 넣지 않았기 때문이다. 계속해서 server.js에서 데이타를 넣을 수 있는 POST 지점을 생성해라:

```js
// 새 책을 추가한다
app.post('/api/books', function (req, res) {
    var book = new BookModel({
        title:req.body.title,
        author:req.body.author,
        releaseDate:req.body.releaseDate
    });
    book.save(function (err) {
        if (!err) {
            return console.log('created');
        } else {
            return console.log(err);
        }
    });
    return res.send(book);
});
```

우선 제목, 작가, 출간일 속성을 전달해서 새로운 BookModel를 생성해보자. 데이타는 req.body에서 수집된다. 이것은 API로 이 동작을 호출하는 누구라도 제목, 작가, 출간일을 포함하는 JSON 객체를 제공해야 한다는 것을 의미한다. 우리가 어떤 것도 필수값으로 지정하지 않았기 때문에 실제로 호출하는 사람은 속성의 일부나 전체를 생략할 수 있다.

우리는 이전의 get 지점과 동일한 방식으로 에러 처리릴 의한 익명 함수를 전달하는 BookModel의 save 함수를 호출한다. 마지막으로 우리는 저장된 BookModel를 반환한다. 우리가 단순히 “success”나 유사한 문자열이 아닌 BookModel을 반환하는 이유는 BookModel니 저장되었을 때 MongoDB에서 _id 속성을 얻을 것이다. 그 속성은 특정 책을 갱신하거나 삭제할 때 클라이언트가 필요로 하는 것이다. 다시 테스트해보자. node를 재시작하고 콘솔로 돌아가서 다음을 타이핑해라:

```js
jQuery.post("/api/books", {
  "title": "JavaScript the good parts",
  "author": "Douglas Crockford",
  "releaseDate": new Date(2008, 4, 1).getTime()
}, function(data, textStatus, jqXHR) {
    console.log("Post response:"); console.dir(data); console.log(textStatus); console.dir(jqXHR);
});
```

..그리고 나면

```js
jQuery.get("/api/books/", function (data, textStatus, jqXHR) {
    console.log("Get response:");
    console.dir(data);
    console.log(textStatus);
    console.dir(jqXHR);
```

이제 서버에서 다시 사이즈가 1인 배열을 얻어져야만 한다. 당신은 이 줄에 좀 궁금해 할지 모르겠다:

```js
"releaseDate": new Date(2008, 4, 1).getTime()
```

MongoDB는 UNIX 타입 형태( 1970년 1월 1일부터 지난 밀리세컨드 )를 기대하기 때문에 우리는 post를 호출하기 전에 날짜를 변환해야만 한다. 그러나 우리가 다시 가져온 객체는 자바스크립트 날짜 객체를 포함한다. 반환된 객체의 _id 속성도 유심히 보아라.

![](http://codebyexample.info/wp-content/uploads/2012/04/Screen-Shot-2012-04-29-at-1.16.58-AM.png)


계속해서 server.js에 단일 책을 얻어오는 get을 만들자:

```js
app.get('/api/books/:id', function(req, res){
    return BookModel.findById(req.params.id, function(err, book){
        if(!err){
            return res.send(book);
        } else {
            return console.log(err);
        }
    });
});
```

여기서 우리는 지점의 이부분이 동적이라는 것을 표현하기 위해 콜론 표식(:id)을 사용한다. 우리는 단일 결과를 얻기 위해서 BookModel의 findById 함수도 사용한다. 이제 당신은 다음과 같이 URL에 아이디를 추가함으로써 하나의 책을 얻을 수 있다:

```js
jQuery.get("/api/books/4f95a8cb1baa9b8a1b000006", function (data, textStatus, jqXHR){
    console.log("Get resposne:");
    console.dir(data);
    console.log(textStatus);
    console.dir(jqXHR);
});
```

다음과 같이 PUT( 갱신 ) 함수를 만들자:

```js
app.put('/api/books/:id', function(req, res){
    console.log('Updating book ' + req.body.title);
    return BookModel.findById(req.params.id, function(err, book){
        book.title = req.body.title;
        book.author = req.body.author;
        book.releaseDate = req.body.releaseDate;
        return book.save(function(err){
            if(!err){
                console.log('book updated');
            } else {
                console.log(err);
            }
            return res.send(book);
        });
    });
});
```

이것은 이전 것보다 좀 더 크지만, 꽤 직관적이어야 한다 - 우리는 아이디로 책을 찾고, 그 속성을 갱신하고, 저장하고 클라이언트에 다시 보낸다.

이것을 테스트하기 위해서, 우리는 좀더 일반적인 jQuery ajax 함수를 사용할 수 있다( 그 함수는 우리가 GET 요청에서 얻은 것으로 아이디를 대체한다 );

```js
jQuery.ajax({
  url:"/api/books/4f95a8cb1baa9b8a1b000006",
  type:"PUT",
  data:{
    "title": "JavaScript The good parts",
    "author": "The Legendary Douglas Crockford",
    "releaseDate": new Date(2008, 4, 1).getTime()
  },
  success: function(data, textStatus, jqXHR) {
    console.log("Post resposne:"); console.dir(data); console.log(textStatus); console.dir(jqXHR);
  }});
  
```

마지막으로 우리는 삭제 지점을 생성한다:

```js
app.delete('/api/books/:id', function(req, res){
    console.log('Deleting book with id: ' + req.params.id);
    return BookModel.findById(req.params.id, function(err, book){
        return book.remove(function(err){
            if(!err){
                console.log('Book removed');
                return res.send('');
            } else {
                console.log(err);
            }
        });
    });
});
```

…그리고 나서 테스트해라:

```js
jQuery.ajax({
  url:'/api/books/4f95a5251baa9b8a1b000001',
  type: 'DELETE',
  success:function(data, textStatus, jqXHR){
    console.log("Post resposne:");
    console.dir(data);
    console.log(textStatus);
    console.dir(jqXHR);
  }
});
```

이제 REST API가 완성되었다 - 우리는 모든 HTTP 메쏘드를 지원한다. 다음은 무엇을 해야 하는가? 글쎄, 이제까지 나는 책의 키워드 부분을 남겨두었다. 책이 몇가지 키워드를 가지고 있고 그것을 문자열이 아닌 문자열의 배열로 표현하고 싶기 때문에 조금 더 복잡하다. 앞으로 할 일은 또 다른 스키마를 필요로 하는 것이다. 키워드 스키마를 Book 스키마 바로 위에 추가해라:

```js
// 스키마
var Keywords = new mongoose.Schema({
    keyword: String
});
```

존재하는 스키마에 하위 스키마를 추가하기 위해, 우리는 브라켈 표식을 다음과 같이 사용한다:

```js
var Book = new mongoose.Schema({
    title:String,
    author:String,
    releaseDate:Date,
    keywords: [Keywords]
});
```

POST와 PUT도 수정해라

```js
app.post('/api/books', function (req, res) {
    var book = new BookModel({
        title:req.body.title,
        author:req.body.author,
        releaseDate:req.body.releaseDate,
        keywords: req.body.keywords
    });
    book.save(function (err) {
        if (!err) {
            return console.log('created');
        } else {
            return console.log(err);
        }
    });
    return res.send(book);
});
 
app.put('/api/books/:id', function(req, res){
    return BookModel.findById(req.params.id, function(err, book){
        book.title = req.body.title;
        book.author = req.body.author;
        book.releaseDate = req.body.releaseDate;
        book.keywords = req.body.keywords;
        return book.save(function(err){
            if(!err){
                console.log('book updated');
            } else {
                console.log(err);
            }
            return res.send(book);
        });
    });
});
```

우리가 필요로 하는 모든 것이 여기에 있다. 이제 우리는 콘솔에서 테스트할 수 있다:

```js
jQuery.post("/api/books", {
  "title": "Secrets of the JavaScript Ninja",
  "author": "John Resig",
  "releaseDate": new Date(2008, 3, 12).getTime(),
  "keywords":[{
     "keyword":"JavaScript"
   },{
     "keyword": "Reference"
   }]
}, function(data, textStatus, jqXHR) {
    console.log("Post response:"); console.dir(data); console.log(textStatus); console.dir(jqXHR);
});
```

이제 기능적으로 완전한 REST 서버를 갖게되었다. 우리는 도서과 어플리케이션이 유지되게( persistent ) 하기 위해서 이것을 안내서의 다음 파트에서 이용할 것이다.

##파트 3

이 파트에서 우리는 Backbone 어플리케이션을 REST API를 통해서 서버에 연결하는 것을 다룰 것이다. 이 파트는 앞의 두 파트에 기초해서 만들어졌기 때문에, 이 파트에서 완전히 이해해기 위해서 앞 파트들을 읽기를 추천한다.


갱신: 어떤 이유로 당신이 서버를 사용할 수 없다면, Backbone.Localstorage 플러그인( Localstorage를 지원하는 브라우져가 필요할 것이다 )을 사용할 수 있다. 이것을 하기 위해, 여기서 플러그인을 다운로드하고 그것을 Backbone 밑에 스크립트 태그로 html 페이지를 추가하고 다음과 같이 컬렉션에서 그것을 초기화해라:

```js
var Library = Backbone.Collection.extend({
    localStorage: new Backbone.LocalStorage("LibraryStorage"),
    model: Book,
    url: '/api/books'
});
```

Backbone 어플리케이션을 서버에 동기화하기 위해, JSON 형태로 통신하는 REST API를 가진 서버가 필요하다. 파트 2.5에서 내가 생성한 서버가 우리 요건에 맞지만, 당신이 다른 언어로 자신만의 서버를 생성한다면 당신은 API 정의를 얻기 위해 안내서를 읽고 싶을 지도 모른다. Backbone이 서버와 모델을 유지하기 위해 sync 함수를 사용하도록 해준다. 당신은 보통 이 함수를 직접적으로 사용하지 않지만, 대신 Backbone이 동기화할 곳을 알려주는 url 속성을 컬렉션( 혹은 모델이 컬렉션안에 없으면 모델에 )에 지정한다. 그리고 Library 컬렉션에 url 속성을 추가해라:

```js
var Library = Backbone.Collection.extend({
    model:Book,
    url:'/api/books'
});

```

이런식으로 Backbone은 API가 다음과 같다고 가정할 것이다:

```
url HTTP Method Operation
/api/books  GET 모든 책의 배열을 얻는다
/api/books/:id  GET 아이디가 :id인 책을 얻는다
/api/books  POST  새 첵을 추가하고 추가된 아이디 속성이 있는 책을 반환한다
/api/books/:id  PUT 아이디가 :id인 책을 갱신한다
/api/books/:id  DELETE  아이디가 :id인 책을 삭제한다

```

우리 어플리케이션이 페이지 로드시에 서버에서 Book 모델을 얻기 위해서 LibraryView를 갱신해야만 한다. Backbone 문서에서는 페이지가 로드될 때, 클라이언트 쪽에서 모델을 가져오는 것보다 페이지가 생성될 때, 서버에서 모든 모델이 추가되는 것을 추천한다. 이 안내서는 당신에게 서버와 어떻게 통신하는지에 대한 더 완벽한 그림을 주기 위해서 그 추천을 무시할 것이다. app.js에 LibraryView로 가서 다음 수정을 적용해라:

```js
var LibraryView = Backbone.View.extend({
    el:$("#books"),
 
    initialize:function () {
        //this.collection = new Library(books);
        this.collection = new Library();
        this.collection.fetch();
        this.render();
 
        this.collection.on("add", this.renderBook, this);
        this.collection.on("remove", this.removeBook, this);
        this.collection.on("reset", this.render, this);
    },
```

여기에서 나는 this.collection.fetch()를 사용해서 내부 배열로 부터 컬렉션을 생성하는 줄을 수정했다. 나는 또 reset 이벤트에 리스너도 추가했다. 모델 조회가 비동기적이고 페이지가 렌더링된 후 일어나기 때문에 이렇게 해야만 한다. 조회가 끝났을 때, Backbone은 reset 이벤트를 구동할 것이다. 그 이벤트는 우리가 감시하고 뷰를 다시 렌더링한다. 이제 당신이 페이지를 리로드하면 당신은 서버에 저장되어 있는 모든 책을 보게 될 것이다:

![](http://codebyexample.info/wp-content/uploads/2012/04/Screen-Shot-2012-04-30-at-12.27.32-AM.png)


보다시피 날짜와 키워드가 조금 이상해 보인다. 서버에서 온 날짜는 자바스크립트 날짜 객체로 변환되고 Underscore 템플릿에 적용할 때, 표시하기 위해서 toString() 함수를 사용할 것이다. 자바스크립트에 날짜를 포맷팅하는데 잘 지원하지 않기 때문에 이것을 수정하기 위해 dateFormat jQuery 플러그인을 사용할 것이다. 여기에서 그것을 다운로드해서 js 폴더에 넣는다. 그리고나서 index.html을 다음과 같이 바꾼다:

```html

<body>
<div id="books">
    <form id="addBook" action="#">
        <div>
            <label for="coverImage">CoverImage: </label><input id="coverImage" type="file">
            <label for="title">Title: </label><input id="title">
            <label for="author">Author: </label><input id="author">
            <label for="releaseDate">Release date: </label><input id="releaseDate">
            <label for="keywords">Keywords: </label><input id="keywords">
            <button id="add">Add</button>
        </div>
    </form>
</div>
<script id="bookTemplate" type="text/template">
    <img src="<%= coverImage %>"/>
    <ul>
        <li><%= title%></li>
        <li><%= author%></li>
        <li><%= $.format.date(new Date(releaseDate), 'dd/MM/yyyy') %></li>
        <li><%= keywords %></li>
    </ul>
    <button class="delete">Delete</button>
</script>
<script src="js/jquery-1.7.1.js"></script>
<script src="js/jquery.dateFormat-1.0.js"></script>
<script src="js/underscore.js"></script>
<script src="js/backbone.js"></script>
<script src="js/app.js"></script>
</body>
```

그래서 스물다섯번째 줄에서 jquery.dateFormat-1.0.js 파일을 추가하고 열아홉번째 줄에서 dd/MM/yyyy 포맷으로 날짜를 프린트하기 위해 dateFormat을 사용한다. 이제 페이지상의 날짜를 좀더 좋게 보인다. 키워드는 어떠한가? 우리가 키워드를 배열의 형태로 받았기 때문에 나뉘어진 키워드 문자열을 만드는 코드를 실행해야만 한다. 그렇게하기 위해서, 우리는 아무것도 출력하지 않는 코드를 실행하는 템플릿 테그안에 = 문자를 생략할 수 있다:

```html
<script id="bookTemplate" type="text/template">
    <img src="<%= coverImage %>"/>
    <ul>
        <li><%= title%></li>
        <li><%= author%></li>
        <li><%= $.format.date(new Date(releaseDate), 'dd/MM/yyyy') %></li>
        <li><% _.each(keywords, function(keyobj){%> <%= keyobj.keyword %><% }); %></li>
    </ul>
    <button class="delete">Delete</button>
</script>
```

여기에서 each 함수를 써서 키워드 배열을 순회하고 각 키워드를 출력한다. 나는 <%= 태그를 사용해서 키워드를 출력하는 것을 기억해 둬라. 이것은 공백을 사이에 두고 출력될 것이다. 당신이 “new age”같이 키워드 안에 공백을 지원하고 싶으면 콤마로 구분할 수 있다( 키워드내에 콤마를 넣는 이상한 사람은 없지 않는가? ). 그것은 다음과 같이 우리가 마지막 키워드후에 콤마를 제거하는 코드를 더 작성하게 만든다:

```html
       <li>
       <% _.each(keywords, function(keyobj, index, list){%>
        <%= keyobj.keyword %>
          <% if(index < list.length - 1){ %>
          <%= ', ' %>
        <% }}); %>
       </li>
```

페이지를 리로딩하는 것은 다음처럼 보여야만 한다:

![](http://codebyexample.info/wp-content/uploads/2012/04/Screen-Shot-2012-04-30-at-1.02.14-AM.png)

이제 책을 삭제하고 페이지를 리로드해라: 짠! 삭제된 책이 돌아와있네! 허접하네, 왜이러지? 이것은 우리가 서버에서 BookModels을 가져왔을 때 _id속성( _가 있는것을 기억해라)을 가지고 있지만, Backbone은 id속성( _가 없다 )을 기대하기 때문이다. id 속성이 없기 때문에 Backbone은 이 모델을 새로운 것으로 보고, 새 모델을 삭제하는 것은 동기화할 필요가 없다. 이것을 고치기 위해, 우리는 서버 응답을 바꿀 수도 있지만 우리는 대신 Backbone.Model의 parse 함수를 보자. parse 함수는 모델 생성자에 전달되기 전에 당신이 서버 응답을 수정하게 해준다. 다음과 같이 Book 모델을 갱신해라:

```js
var Book = Backbone.Model.extend({
    defaults:{
        coverImage:"img/placeholder.png",
        title:"No title",
        author:"Unknown",
        releaseDate:"Unknown",
        keywords:"None"
    },
    parse:function (response) {
        console.log(response);
        response.id = response._id;
        return response;
    }
});
```

나는 단순히 필요한 id 속성에 _id의 값을 복사한다. 당신이 페이지를 리로드하면, 삭제 버튼을 눌렀을 때 모델이 서버 상에서 실제로 삭제되는 것을 볼 수 있을 것이다.

메모: Backbone이 _id를 단일한 아이디로 인식하도록 해주는 더 단순한 방법은 다음과 같이 모델의 idAttribute를 지정하는 것이다:

```js
var Book = Backbone.Model.extend({
    defaults:{
        coverImage:"img/placeholder.png",
        title:"No title",
        author:"Unknown",
        releaseDate:"Unknown",
        keywords:"None"
    },
    idAttribute: "_id"
});
```

당신이 폼을 써서 새 책을 추가하려고 하면, 삭제와 같은 이야기임을 알게 될 것이다 - 모델은 서버상에서 유지되지 않는다. 이것이 Backbone.Collection.add가 자동으로 동기화하지 않는 이유이지만, 쉽게 바꿀 수 있다. app.js의LibraryView에 다음을 바꿔라:

```js
this.collection.add(new Book(formData));
```

…이렇게 바꿔라:

```js
this.collection.create(formData);
```

이제 새로이 생성된 책들은 유지될 것이다. 날짜를 입력하면, 아마도 실제로 유지되지 않을 것이다. 서버는 날짜가 UNIT 타임스탬프 형태( 1970년 1월 1일부터 지난 밀리세컨드 )로 기대한다. 서버가 ‘keyword’ 속성에 객체 배열을 기대하기 때문에 당신이 입력한 키워드도 저장되지 않는다.

우리는 날짜 문제 수정을 시잔한다. 우리는 진짜로 사용자가 날짜를 특정 형태로 직접 입력하도록 하게 하고 싶지 않기 때문에 jQuery UI의 기본적인 datepicker를 사용할 것이다. 여기의 datepicker를 포함하고 있는 사용자 정의 jQuery UI 생성해라. css와 js 파일은 index.html에 추가해라:

```html
<head>
    <meta charset="UTF-8"/>
    <title>Backbone.js Web App</title>
    <link rel="stylesheet" href="css/screen.css">
    <link rel="stylesheet" href="css/cupertino/jquery-ui-1.8.19.custom.css">
</head>
```

그리고 jQuery 뒤에 js 파일을 추가한다:

```html
<script src="js/jquery-1.7.1.js"></script>
<script src="js/jquery-ui-1.8.19.custom.min.js"></script>
<script src="js/jquery.dateFormat-1.0.js"></script>
<script src="js/underscore.js"></script>
<script src="js/backbone.js"></script>
<script src="js/app.js"></script>
```

이제 app.js 앞부분에서 datepicker를 releaseDate 항목에 바인딩한다.

```js
(function ($) {
    $( "#releaseDate" ).datepicker();
 
    var books = [
        {title:"JS the good parts", author:"John Doe", releaseDate:"2012", keywords:"JavaScript Programming"},

```
        
당신은 이제 releaseDate 필드를 클릭함으로써 날짜를 선택할 수 있다:

![](http://codebyexample.info/wp-content/uploads/2012/04/Screen-Shot-2012-04-30-at-1.34.19-AM.png)

이제 LibraryView의 addBook 함수로 가서 다음과 같이 수정해라:

```js
addBook:function (e) {
    e.preventDefault();
 
    var formData = {};
 
    $("#addBook div").children("input").each(function (i, el) {
        if ($(el).val() !== "") {
            if (el.id === 'releaseDate'){
                formData[el.id] = $('#releaseDate').datepicker("getDate").getTime();
            } else {
                formData[el.id] = $(el).val();
            }
        }
    });
 
    books.push(formData);
 
    //this.collection.add(new Book(formData));
    this.collection.create(formData);
},
```

여기에서 나는 현재 요소가 releaseDate 입력 필드인지 확인한다. 그 경우이면, 날짜 객체를 주는 datePicker(“getDate”)를 사용하고 나서 밀리쎄컨드로 시간을 주는 getTime 함수를 사용할 것이다. 키워드 이슈도 수정해보자:

```js
addBook:function (e) {
    e.preventDefault();
 
    var formData = {};
 
    $("#addBook div").children("input").each(function (i, el) {
        if ($(el).val() !== "") {
            if (el.id === 'keywords') {
                var keywordArray = $(el).val().split(',');
                var keywordObjects = [];
                for (var j = 0; j < keywordArray.length; j++) {
                    keywordObjects[j] = {"keyword":keywordArray[j]};
                }
                formData[el.id] = keywordObjects;
            } else if (el.id === 'releaseDate'){
                formData[el.id] = $('#releaseDate').datepicker("getDate").getTime();
            } else {
                formData[el.id] = $(el).val();
            }
        }
    });
 
    books.push(formData);
 
    //this.collection.add(new Book(formData));
    this.collection.create(formData);
},
```

여기에서 나는 현재 요소가 키워드 필드인지 확인한다. 그 경우에 문자열을 콤마로 나누고 키워드 객체들로 새 배열을 생성한다. 즉 키워드는 콤마로 분리되어 있다고 가정하기 때문에 폼에서 책에 대한 주석을 더 잘 쓸 수 있다. 이제 당신은 출간일과 키워드 모두를 가지고 있는 새첵을 생성할 수 있다!

![](http://codebyexample.info/wp-content/uploads/2012/04/Screen-Shot-2012-05-01-at-8.57.51-PM.png)

### 요약

이 안내서에서 우리는 어플리케이션을 REST API를 사용해 서버에 연결함으로써 유지가능하게 만들었다. 또한, 데이타를 직렬화하고 역직렬화할 때 발생할 수 있는 문제와 그 해결책도 살펴보았다. 우리는 dateFormat과 datepicker jQuery 플러그인을 살펴보고 Underscore 템플릿에서 좀 더 진보된 것을 하는 방법도 살펴보았다. 코드는 [여기](https://dl.dropbox.com/u/70775642/workshop-practical/code.zip)에서 볼 수 있다.



# Backbone 보일러플레이트와 Grunt의 BBB

[Backbone Boilerplate](https://github.com/tbranyen/backbone-boilerplate/)는 Backbone.js 어플리케이션을 만드는 최고의 예제와 유틸리티 묶음이다. 그것은 Backbone 기여자[Tim Branyen](https://github.com/tbranyen)이 만들었다. 그는 Bocoup에서 Backbone을 사용해서 일년이 넘게 앱을 만들면서 마주친 발견, 어려움 그리고 공통된 작업으로부터 보일러플레이트를 구성했다. 이것은 [StartupDataTrends.com](http://startupdatatrends.com)같은 앱들을 포함하고 있다.

스캐폴딩과 최소화, 파일 결합, 서버, 템플릿 컴파일과 같은 미리 포함된 빌드 작업으로 Backbone 보일러플레이트( 그리고 관련 프로젝트 [Grunt-BBB](https://github.com/backbone-boilerplate/grunt-bbb))들은 모든 수준의 개발자를 위한 좋은 선택이다. 개발을 위한 설정을 할 때, 나는 그것들이 당신에게 엄청난 시작점을 주기 때문에 사용해 보기를 강력 추천한다. 그것들은 또한 또다른 시간 절약이기도 한 많은 주석들도 포함하고 있기도 하다.

기본적으로, Backbone 보일러플레이트는 당신에게 다음을 제공한다:

* [HTML5 보일러플레이트](http://html5boilerplate.com)를 가지고 있는 Backbone, [Lodash](https://github.com/bestiejs/lodash) (an [Underscore.js](http://underscorejs.org/) alternative) 그리고 [jQuery](http://jquery.com)
* 보일러플레이트 모듈 코드
* 템플릿 전컴파일과 모든 라이브러리, 어플리케이션, CSS의 결합과 최소화를 위한 윈도우/맥/리눅스 빌드 툴
* 모듈, 컬렉션 등에 대한 보일러플레이트를 작성하는 시간을 최소화하는 ( grunt-bbb - [B]ackbone [B]oilerplate [B]uild 를 통한) 스캐폴딩 지원.
* 경량화된 node.js 웹서버
* 삶을 더 쉽게 만들어주는 많은 Backbone.js 스니펫들

## 시작해보자

### Backbone 보일러플레이트

보일러플레이트를 어플리케이션을 생성하기 시작하는데 사용할 수 있지만 우선은 그것을 설치해야 할 것이다. 보일러플레이트 저장소를 직접 클론함으로써 최신의 버젼을 얻어서 설치할 수 있다:

```shell
$ git clone git://github.com/tbranyen/backbone-boilerplate.git
```

아니면 또 다른 방법으로, 다음과 같이 최신의 tarball을 얻어올 수 있다:

```shell
$ curl -C - -O https://github.com/tbranyen/backbone-boilerplate/zipball/master
```

### Grunt-BBB

Tim이 보일러플레이트 문서에서 다룬 것처럼, 그가 추천한 빌드툴과 grunt-bbb 보조 프로그램을 사용하고 싶다면 [Grunt](http://gruntjs.com)를 설치해야만 한다.

Grunt는 또 다른 [Bocoup](http://bocoup.com)의 개발자 ([Ben Alman](http://benalman.com))가 만든 뛰어난 노드기반의 자바스크립트 빌드 툴이다. 그것은 [Ant](http://ant.apache.org/)나 [Rake](https://github.com/jimweirich/rake)와 유사하게 생각된다. 보일러플레이트를 작성할 필요없이 당신의 프로젝트를 스캐폴딩하기 위한 Backbone 특화된 유틸리티를 제공하기 때문에 grunt-bbb 보조 프로그램도 유용하다.

NPM을 통해서 grunt와 grunt-bbb를 설치하기 위해:

```shell
# first run
$ npm install -g grunt

# followed by
$ npm install -g bbb

# finally create a new project
$ bbb init
```

이게 다이다. 우리는 이제 출발할 준비가 되었다.

grunt-bbb를 사용하기 위한 전형적인 순서, 나중에 사용할 수도 있다:

* 새 프로젝트를 초기화한다(`bbb init`)
* 새 모듈과 템플릿을 추가한다(`bbb init:module`)
* 미리 포함된 서브를 개발에 이용한다(`bbb server`)
* 빌드 툴을 실행한다(`bbb build`)
* 제품 자산으로 배포하고 매핑한다(using `bbb release`)

## 새 프로젝트 생성

프로젝트를 위한 폴더를 생성하고, 시작하기 위해서 `bbb init`를 실행해라. 모든 것이 잘 설치되었다면, 이것은 우리를 위해 일련의 프로젝트 디렉토리와 파일들을 대신 생성할 것이다. 생성된 것을 살펴보자.

### index.html

이것은 페이지의 아랫부분에 [RequireJS](http://requirejs.org)을 포함하는 특이사항을 가진 꽤 표준적인 HTML5 보일러플레이트이다.

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
  <meta name="viewport" content="width=device-width,initial-scale=1">

  <title>Backbone Boilerplate</title>

  <!-- Application styles. -->
  <link rel="stylesheet" href="/assets/css/index.css">
</head>

<body>
  <!-- Main container. -->
  <div role="main" id="main"></div>

  <!-- Application source. -->
  <script data-main="/app/config" src="/assets/js/libs/require.js"></script>
</body>
</html>
```

RequireJS는 [AMD](https://github.com/amdjs/amdjs-api/wiki/AMD) (비동기적인 모듈 정의) 모듈이며 스크립트 로더이다. 그것은 어플리케이션 내의 모듈을 관리하는 것을 도와줄 것이다. 우리는 이 책의 후반부에 더 자세히 다루겠지만, 여기에서는 다음 특정 부분이 하는 것을 상위 수준에서 다루자:

```
<script data-main="app/config" src="/assets/js/libs/require.js"></script>
```

`data-main` 속성은 RequireJS가 로딩이 끝난 후에 `app/config.js` (설정 객체)를 로드하라고 알려주는데 사용된다. RequireJS가 자동적으로 붙여주기 때둔에 여기에서 우리가 `.js` 확장자를 생략했다고 말하겠지만 RequireJS는 경로를 확장자를 포함하든 관계없이 다룰 것이다. 이제 참조된 설정을 보자.

### config.js

RequireJS 설정 객체는 우리가 자주 참조하는( 예를 들어 jQuery ) 의존성에 대한 축약명칭와 경로를 지정하고 기본 어플리케이션이나 AMD 내부에서 지원하지 않는 `shim` 라이브러리같은 특성을 가지고 실행되게 해준다.

이것이 Backbone 보일러플레이트의 설정 파일의 형태이다:

```javascript
// 어플리케이션을 위한 RequireJS 설정을 지전한다
require.config({

  // main 어플리케이션 파일로 어플리케이션을 초기화한다.
  deps: ['main'],

  paths: {
    // 자바스크립트 폴더들.
    libs: '../assets/js/libs',
    plugins: '../assets/js/plugins',

    // 라이브러리들.
    jquery: '../assets/js/libs/jquery',
    lodash: '../assets/js/libs/lodash',
    backbone: '../assets/js/libs/backbone'
  },

  shim: {
    // Backbone 라이브러리는 lodash and jQuery에 의존성을 갖는다.
    backbone: {
      deps: ['lodash', 'jquery'],
      exports: 'Backbone'
    },

    // Backbone.LayoutManager는 Backbone에 의존성을 갖는다.
    'plugins/backbone.layoutmanager': ['backbone']
  }

});
```

위의 설정에서 정의된 첫번째 옵션을 `deps: ['main']`이다. 이것은 RequireJS가 main.js 파일을 로드한다는 것을 알려준다. 그 파일은 어플리케이션의 시작 지점으로 생각된다. 당신은 우리가 `main`을 위한 다른 경로도 지정하지 않았음을 알아차릴 것이다.

이것은 위ㄹ가 `baseUrl` 옵션을 사용해서 스크립트에 경로를 덮어쓰지 않았기 때문에, Require는 이것을 index.html의 `data-main` 속성의 경로를 사용할 것으로 추측된다. 즉, 우리의 `baseUrl`은 `app/`이고 필요한 다른 스크립트들은 이 위치에 상대 경로로 로드될 것이다.

다음 부분은 `paths`인데, `baseUrl`의 상대 경로를 지정할 수도 있고 일반적으로 참조하는 의존성에 대한 경로나 축약명으로도 지정할 수 있다.

```javascript
  paths: {
    // 자바스크립트 폴더
    libs: '../assets/js/libs',
    plugins: '../assets/js/plugins',

    // 라이브러리
    jquery: '../assets/js/libs/jquery',
    lodash: '../assets/js/libs/lodash',
    backbone: '../assets/js/libs/backbone'
  },
```

그 다음에는 `shim` 설정이 있다:

```javascript
  shim: {
    // Backbone 라이브러리는 lodash 과 jQuery에 의존성이 있다.
    backbone: {
      deps: ['lodash', 'jquery'],
      exports: 'Backbone'
    },

    // Backbone.LayoutManager 는 Backbone에 의존성이 있다.
    'plugins/backbone.layoutmanager': ['backbone']
  }
```

`shim`은 AMD 호환성이 없는 라이브러리를 로드하도록 하는 RequireJS 설정의 중요한 부분이다. 여기에서 중요한 생각은 AMD에 대한 지원을 구현한 모든 라이브러리가 필요한 것이 아니라는 점이다. `shim`은 우리를 위해 힘든 작업을 관리한다.

예를 들어 아래 블럭에서, Backbone.js가 로드되기 전에 로드되어야하는 Lodash( Underscore.js 의 클론 )과 jQuery에 의존성이 있다고 지정한다. 그것들이 로드되면, 우리는 전역 export `Backbone`을 모듈값으로 쓴다.

```javascript
    backbone: {
      deps: ['lodash', 'jquery'],
      exports: 'Backbone'
    }
```

마지막으로, 우리는 RequireJS에게 Backbone [LayoutManager](https://github.com/tbranyen/backbone.layoutmanager) 플러그인( 템플릿과 레이아웃 관리자도 포함되어 있다 )이 로드되기 전에 Backbone이 로드되어야 한다고 알려준다.

```javascript
    // Backbone.LayoutManager는 Backbone에 의존성이 있다.
    'plugins/backbone.layoutmanager': ['backbone']
```

이것 전체 설정은 우리 스크립트가 우리가 원하는 순서로 올바르게 로드되도록 해준다.

### main.js

다음으로, 우리는 `main.js`를 만든다. 그것은 우리 어플리케이션의 시작점이다. 우리는 어플리케이션인 `app.js`와 라우터인 `router.js`와 같은 필요한 다른 스크립트의 배열을 로드하는 전역 메쏘드 `require()`를 사용한다. 대부분의 시간에 우리는 어플리케이션을 구동하기 위한 `require()`와 그 외의 용도로 `define()`를 호출하는 유사한 메쏘드만 사용할 것이다.

의존성 배열 뒤에 정의된 함수는 그 스크립트가 로드되기 전까지 호출되지 않는 콜백이다. 우리가 어떻게	지역적으로 "app"와 "router"를 `app`와 `Router`로 편리하게 축약 참조로 부를 수 있게하는지 주목해라.

```javascript
require([
  // 어플리케이션.
  'app',

  // 주 라우터.
  'router'
],

function(app, Router) {

  // 어플리케이션 이름공간상에 주 라우터를 정의하고
  // 이 인스턴스에서 모든 이동을 호출한다.
  app.router = new Router();

  // 시작점을 호출하고 HTML5의 History API를 지원하도록 한다.
  // 기본적으로 '/'를 루트 폴터로 지정한다. app.js를 변경한다.
  Backbone.history.start({ pushState: true, root: app.root });

  // 상대적인 모든 이동은 라우터에 의해 처리되게 하기 위해서
  // navigate 메쏘드를 통해 전달되어야만 한다. 링크가
  // `data-bypass` 속성을 가지면, 완전히 위임한다.
  $(document).on('click', 'a:not([data-bypass])', function(evt) {
    // 앵커 href의 절대 경로를 얻는다.
    var href = $(this).attr('href');

    // href가 있고 해쉬 지점이면, Backbone을 통해 실행한다.
    if (href && href.indexOf('#') === 0) {
      // 링크가 패이지를 갱신하지 않도록 기본 이벤트를
	  // 중단시킨다
      evt.preventDefault();

      // `Backbone.history.navigate`는 모든 라우터를 위해 중요하다.
	  // 그것은 올바른 이벤트를 구동시킨다. 라우터 내부의 `navigate`
	  // 메쏘드는 항상 이 메쏘드를 호출한다. 그 조각이 루트에서 쪼개져있다.
      Backbone.history.navigate(href, true);
    }
  });

});
```

중간에 Backbone 보일러플레이트는 라우터가 HTML5 History API와 다른 이동 시나리오를 지원하도록 초기화하는 보일러플레이트 코드를 포함하기 때문에 우리는 할 필요가 없다.

### app.js

이제 `app.js` 모듈을 보자. 전형적으로, Backbone 보일러플레이트가 아닌 어플리케이션에서 `app.js` 파일은 앱을 시작할 때 필요한 주요 로직이나 모듈 참조를 가지고 있을 것이다.

그러나 이 경우에, 이 파일은 템플릿과 레이아웃 설정뿐만 아니라 레이아웃을 사용하는 유틸리티를 정의하는데 사용된다. 초심자에게, 이것은 이해할 많은 코드처럼 보이지만, 좋은 소식은 기본 앱에서는 이부분을 크게 수정할 필요는 없어 보인다는 것이다. 대신, 당신은 앱의 모듈에 더 관심을 가져야 한다. 다음에 우리는 이것을 살펴볼 것이다.

```javascript
define([

  // 라이브러리들
  'jquery',
  'lodash',
  'backbone',

  // 플러그인들
  'plugins/backbone.layoutmanager'

],

function($, _, Backbone) {

  // 설정과 모듈 생성을 위한 전역 위치를
  // 제공한다
  var app = {
    // 어플리케이션을 실행할 루트 경로
    root: '/'
  };

  // 새 자바스크립트 템플릿 객체를 지역화해서 생성한다.
  var JST = window.JST = window.JST || {};

  // LayoutManager를 Backbone 보일러플레이트의 기본값으로 설정한다.
  Backbone.LayoutManager.configure({
    paths: {
      layout: 'app/templates/layouts/',
      template: 'app/templates/'
    },

    fetch: function(path) {
      path = path + '.html';

      if (!JST[path]) {
        $.ajax({ url: app.root + path, async: false }).then(function(contents) {
          JST[path] = _.template(contents);
        });
      }

      return JST[path];
    }
  });

  // Backbone.Events, modules, 그리고 레이아웃 관리를 app 객체에 모두 넣는다.
  return _.extend(app, {
    // 중청된 뷰 객체로 사용자 정의 객체를 생성한다.
    module: function(additionalProps) {
      return _.extend({ Views: {} }, additionalProps);
    },

    // 레이아웃 사용을 위한 유틸리티
    useLayout: function(name) {
      // 이미 이 레이아웃을 사용하고 있으면 DOM에 다시 삽입하지 않는다.
      if (this.layout && this.layout.options.template === name) {
        return this.layout;
      }

      // 레이아웃이 존재하면 DOM에서 제거한다.
      if (this.layout) {
        this.layout.remove();
      }

      // 새로운 레이아웃을 생성한다.
      var layout = new Backbone.Layout({
        template: name,
        className: 'layout ' + name,
        id: 'layout'
      });

      // DOM에 삽입한다.
      $('#main').empty().append(layout.el);

      // 레이아웃을 그린다.
      layout.render();

      // 참조를 캐쉬한다.
      this.layout = layout;

      // 연속 호출을 위해 레이아웃을 반환한다.
      return layout;
    }
  }, Backbone.Events);

});
```

### Backbone 보이러플레이트 모듈 생성하기

단순히 AMD 모듈이기만 한 것과 혼동하지 않기 위해서 Backbone 보일러플레이트 `module`은 다음으로 구성된 스크립트이다:

* 모델
* 컬렉션
* ( 필요한 경우 ) 뷰

우리는 `grunt-bbb`에 다시 한번 `init`을 사용해서 쉽게 새로운 보일러플레이트 모듈을 생성할 수 있다:

```shell
# 새 모듈을 생성한다
$ bbb init:module

# Grunt 프롬프트
Please answer the following:
[?] Module Name foo
[?] Do you need to make any changes to the above before continuing? (y/N) n

Writing app/modules/foo.js...OK

Initialized from template "module".
```

이것은 모듈 `foo.js`를 다음과 같이 생성할 것이다:

```javascript
define([
  // 어플리케이션
  'app'
],

// 위의 배열에 의존성을 매핑한다.
function(app) {

  // 새 모듈을 생성한다.
  var Foo = app.module();

  // 기본 모델.
  Foo.Model = Backbone.Model.extend({

  });

  // 기본 컬렉션.
  Foo.Collection = Backbone.Collection.extend({
    model: Foo.Model
  });

  // AMD 호환을 위해 모듈을 반환한다.
  return Foo;

});

```

어떤식으로 우리의 모델과 컬렉션을 위한 보일러플레이트 코드가 이미 작성되어 있을 뿐만 아니라 레이아웃을 유틸리티를 사용하는 코드도 `app.js`에 정의되어 있는지 살펴봐라.

이제, 당신은 뷰가 어디에서 어떻게 설정되는지 궁금할 것이다. Backbone 보일러플레이트가 기본적으로 생성된 모듈에 뷰를 포함하고 있지 않긴 하지만, 우리는 필요에 따라 쉽게 추가할 수 있다.

예제:

```javascript
define([
  // Application.
  'app',

  // Views
  'modules/foo/views'
],

// 위의 배열에 의존성을 매핑한다.
function(app, Views) {

  // 새 모듈을 생성한다.
  var Foo = app.module();

  // 기본 모델.
  Foo.Model = Backbone.Model.extend({

  });

  // 기본 컬렉션.
  Foo.Collection = Backbone.Collection.extend({
    model: Foo.Model
  });

  // 기본 뷰.
  Foo.Views = Views;

  // AMD 호환을 위해 모듈을 반환한다.
  return Foo;

});
```

어떨때 우리는 Backbone LocalStorage나 Offline 어댑터와 같은 플러그인 참조를 포함하고 싶을지도 모른다. 위의 보일러플레이트에서 플러그인을 포함하는 한가지 깔끔한 방법은 다음과 같다:

```javascript
define([
  'app',

  // 라이브러리
  'backbone',

  // 플러그인
  'plugins/backbone-localstorage'
],

function(app, Backbone, Views) {
  // 새 모듈을 생성한다.
  var Foo = app.module();

  // 기본 모델.
  Foo.Model = Backbone.Model.extend({

  });

  // 기본 컬렉션.
  Foo.Collection = Backbone.Collection.extend({
    model: Foo.Model,

    // `"foo"` 이름 공간 아래에	모든 항목을 저장한다.
    localStorage: new Store('foo-backbone'),
  });

  // 기본 뷰
  Foo.Views = Views;

  // AMD 호환을 위해 모듈을 반환한다.
  return Foo;
});
```

당신은 우리 모듈 샘플에서 우리가 단지 View가 아닌 복수형인 "Views"을 사용하고 있는 것을 발견했을지도 모른다. 이것은 View 모듈이 필요한 만큼의 뷰들에 대한 참조를 포함하기 때문이다. 위에서 `/modules/foo/views.js` 파일은 다음과 같을 것이다:

```javascript
define([
  'app',

  // Libs
  'backbone'
],

function(app, Backbone) {

  var Views = {};

  Views.Bar = Backbone.View.extend({
    template: 'foo/bar',
    tagName: 'li',
    ...
   });

  Views.Baz = Backbone.View.extend({
    template: 'foo/baz',
    tagName: 'li',
    ...
   });

   return Views;

});
```

Views에서 `template` 이 참조하는 곳은 `app/templates` 디렉토리의 파일에 대응한다. 예를 들어 `foo/bar`는 `app/templates/foo/bar.html`에 있고, 그것은 Lodash/Underscore.js의 마이크로 템플릿팅 로직을 담고 있는 HTML 템플릿이다.


### router.js

마지막으로, 이동을 관리하는데 사용하는 어플리케이션 라우터를 살펴보자. Backbone 보일러플레이트가 생성하는 기본 라우터는 지정된 지점이 없는 정상적인 기본을 포함하고 있다.

```javascript
define([
  // 어플리케이션
  'app'
],

function(app) {

  // 어플리케이션 라우터를 정의하기 위해, 우리는 여기에서 하위 라우터를 붙인다.
  var Router = Backbone.Router.extend({
    routes: {
      '': 'index'
    },

    index: function() {

    }
  });

  return Router;

});
```

그러나 우리가 페이지가 로드될 때 모듈 특화된 로직을 실행하고 싶으면( 즉, 사용자가 기본 지점에 도달할 때 ), 모듈을 의존성으로 옮기고 Views를 레이아웃에 붙이기 위해 Backbone LayoutManager를 사용할 수 있다:

```javascript
define([
  // 어플리케이션
  'app',

  // 모듈
  'modules/foo'
],

function(app, Foo) {

  // 어플리케이션 라우터를 정의하기 위해 여기에서 하위 라우터를 붙일 수 있다.
  var Router = Backbone.Router.extend({
    routes: {
      '': 'index'
    },

    index: function() {
            // 새로운 컬렉션을 생성한다.
            var collection = new Foo.Collection();

            // 'main' 레이아웃을 사용하고 설정한다
            app.useLayout('main').setViews({
                    // bar 뷰를 content 뷰에 붙인다
                    '.bar': new Foo.Views.Bar({
                            collection: collection
                    })
             }).render();
    }
  });

  // 데이타를 가져온다. ( 예를들면 localStorage에서 )
  collection.fetch();

  return Router;

});
```

## 결론

이 섹션에서 우리는 Backbone 보일러플레이트를 살펴보았고 어플리케이션을 스캐폴딩하게 해주는 BBB 툴을 어떻게 쓰는지 배웠다.

만일 이 프로젝트가 어떻게 앱을 구조화하는데 도움을 주는지 더 배우고 싶다면, BBB에는 학습을 위해 쉽게 생성할 수 있는 몇개의 미리 준비된 보일러플레이트 샘플 앱이 있다.

이 것들은 보일러플레이트 안내서 프로젝트(`bbb init:tutorial`) 와 [TodoMVC](http://todomvc) 프로젝트 (`bbb init:todomvc`)의 구현을 포함하고 있다. 나는 그것들이 당신에게 Backbone 보일러플레이트, 템플릿 등등이 웹 앱의 전체 설정에 어떻게 녹아드는지 더 완변한 그림을 제공하기 때문에 확인해 볼 것을 추천한다.

Grunt-BBB에 대해 더 알고 싶다면, 정식 프로젝트 [저장소](https://github.com/backbone-boilerplate/grunt-bbb)를 볼 것을 기억해 둬라. 더 많이 읽고 싶으 사람들을 위해서 관련된 [slide-deck](https://dl.dropbox.com/u/79007/talks/Modern_Web_Applications/slides/index.html)도 있다.

## 관련된 툴과 프로젝트

보다시피 스케폴딩 툴은 프로젝트에 필요한 기본 파일들을 신속하게 자동 생성함으로써 새로운 어플리케이션을 얼마나 빨리 시작하게 하는데 도움을 줄 수 있다. 당신이 그런 툴에 고마움을 느끼면, [Yeoman](http://yeoman.io) (내가 기여하는 프로젝트중 하나)과 [Brunch](https://github.com/brunch/brunch)를 확인해보는 것도 추천한다.

Brunch는 Backbone, Underscore, jQuery 그리고 CoffeeScript와 잘 맞고 Red Bull과 Jim Beam과 같은 회사에서 사용되기도 한다. 당신은 이것을 사용해서 제3의 의존성( 예를들면 최신의 jQuery나 Zepto같은 것 )을 갱신해야만 할지도 모른다. 그것이 모듈로 사용하기에 충분히 안전한지는 별게의 것이다.

Brunch는 node.js의 패키지 관리자를 통해서 설치될 수 있고 그것은 시작하기 쉽다. Vim이나 Textmate를 에디터로 선택해서 사용하고 있다면, 그 둘에서 사용가능한 Brunch 번들이 있다는 것을 알면 기쁠 것이다.


# 일반적인 문제점과 해결책

이번 섹션에서, 우리는 Backbone을 사용한 상대적으로 덜 평범한 프로젝트의 작업을 시작하면 자주 겪는 많은 일반적인 문제뿐만 아니라 현재 잠재적인 해결책도 알아볼 것이다.

아마도 이런 질문 중에 가장 자주 나오는 것은 뷰로 무언가를 더 하는 방법에 관한 것일 것이다. 당신이 중첩 뷰로 작업 방법, 뷰의 제거와 상속을 배우는 방법을 알고 싶어 한다면, 이 섹션은 당신이 그 방법을 알려줄 것이다.


#### 중첩: Backbone.js에서 하위 뷰를 렌더링하고 추가하는 가장 좋은 접근법은 무엇인가?

중첩은 보통 유지보수할 수 있는 코드를 작성하기 위해 계층적인 뷰를 유지보수하는 좋은 방법으로 생각되어 왔다. 초심자들은 다음과 같이 하위 뷰( 예를들면 내부 뷰 )에 매우 간단한 설정을 하려고 한다:

```javascript

// 앞에서 뷰를 정의한 곳에
// 부모뷰 안에 하위 뷰를 정의한다.

...
initialize : function () {

    this.innerView1 = new Subview({options});
    this.innerView2 = new Subview({options});
},

render : function () {

    this.$el.html(this.template());

    this.innerView1.setElement('.some-element').render();
    this.innerView2.setElement('.some-element').render();
}
```

이것은 DOM 요소를 추가할 때, 그 순서를 유지하는 것을 걱젓할 필요없이 동작한다. 뷰는 이미 초기화되어 있고, render() 메쏘드는 한번에 너무 많은 기능을 가질 필요가 없다. 불행이도, 요소의 `tagName`과 재위임해야만 하는 이벤트를 설정하는 기능을 가지고 있지 않다는 것은 downside이다.

재위임 문제를 겪지 않는 또 다른 접근법은 다음과 같이 작성될 수 있다:

```javascript

initialize : function () {

},

render : function () {

    this.$el.empty();

    this.innerView1 = new Subview({options});
    this.innerView2 = new Subview({options});


    this.$el.append(this.innerView1.render().el, this.innerView2.render().el);
}

```

이 버젼에서 우리는 빈 공간을 포함하는 템플릿은 필요하지도 않고 `tagName`의 문제는 다시 한번 정의함으로써 해결된다.

로직을 `onRender` 이벤트로 옮기는 변형은 약간의 사소한 변화를 가지고 작성될 수 있다:


```javascript

initialize : function () {
    this.on('render', this.onRender);
},

render : function () {

    this.$el.html(this.template);

    // 로직

    return this.trigger('render');
},

onRender : function () {
    this.innerView1 = new Subview();
    this.innerView2 = new Subview();
    this.innerView1.setElement('.some-element').render();
    this.innerView2.setElement('.some-element').render();
}
```

만일 어플리케이션에 중첩 뷰를 발견했다면, 초기화, 렌더링 그리고 하위 뷰를 추가하는데 사용할 만한 더 많은 최적의 접근법이 있다. 그 예가 다음에 있다:

```javascript

var OuterView = Backbone.View.extend({
    initialize: function() {
        this.inner = new InnerView();
    },

    render: function() {
        this.$el.html(template); // 템플릿이 없으면 this.$el.empty()
        this.$el.append(this.inner.$el);
        this.inner.render();
    }
});

var InnerView = Backbone.View.extend({
    render: function() {
        this.$el.html(template);
        this.delegateEvents();
    }
});

```

이것은 몇가지 특정한 설계상의 결정을 방해한다:

* 실제로 당신이 하위 요소를 추가하는 순서
* OuterView는 InnerView에 설정되는 HTML 요소를 포함하지 않는다. 그것은 내부뷰에 여전히 tagName을 지정할 수 있다는 것을 의미한다.
* render() 는 InnerView 요소가 DOM에 들어간 후에 호출된다. InnerView의 render() 메쏘드가 다른 요소와의 배열에 기초해서 페이지상의 요소를 크기를 바꾸면, 이것은 유용하다. 이것은 일반적인 사용례이다.

두번째 잠재적인 해결책은 이것이다. 깔끔하게는 보이지만 현실적으로 성능에 영향을 주는 경우가 있다:

```javascript

var OuterView = Backbone.View.extend({
    initialize: function() {
        this.render();
    },

    render: function() {
        this.$el.html(template); // 템플릿이 없으면 this.$el.empty()
        this.inner = new InnerView();
        this.$el.append(this.inner.$el);
    }
});

var InnerView = Backbone.View.extend({
    initialize: function() {
        this.render();
    },

    render: function() {
        this.$el.html(template);
    }
});
```

복수개의 뷰가 템플릿 상의 특정 위치에 중첩되어야만 한다면, 하위 뷰의 cid들에 의해 인덱싱되는 하위 뷰의 해쉬가 생성되어야만 한다. 템플릿에서 각 뷰가 놓일 요소를 생성하기 위해 `data-view-cid`라는 HTML 속성을 사용해라. 템플릿이 렌더링되어서 그 결과가 상위 뷰에 추가되면, 각 요소인 뷰의 `$el`은 하위 뷰의 `el`을 질의할 수도 있고 대체될 수도 있다.

단일 하위 뷰를 갖는 샘플 구현:

```javascript

var OuterView = Backbone.View.extend({
    initialize: function() {
        this.children = {};
        var child = new Backbone.View();
        this.children[child.cid] = child;
    },

    render: function() {
        this.$el.html('<div data-view-cid="' + this.child.cid + '"></div>');        
        _.each(this.children, function(view, cid) {
            this.$('[data-view-cid="' + cid + '"]').replaceWith(view.el);
        }, this);
    }
};

```

보통은 더 많은 개발자들이 첫번째 해결책을 다음과 같이 선택한다:

* 다수의 뷰가 이미 render() 메쏘드에서 DOM에 의존성을 갖고 있다
* OuterView가 다시 렌더링될 때, 재 초기화는 잠재적인 메모리 누수와 이미 바인딩된 이벤트 문제가 있어서 다시 초기화는 하지 않는다

[Marionette](#marionette)와 [Thorax](#thorax)는 중첩된 뷰에 대한 로직을 제공해서 각 항목이 연결된 뷰를 가지는 컬렉션을 렌더링한다. Thorax가 Handlebars 템플릿 유틸리티를 제공하는 반면, Marionette는 자바스크립트 API들을 제공한다.

(이런 팁을 알려준 [Lukas](http://stackoverflow.com/users/299189/lukas)와 [Ian Taylor](http://stackoverflow.com/users/154765/ian-storm-taylor)에게 감사한다 ).

#### 중접 뷰에서 모델을 관리하는 가장 좋은 방법은 무엇인가?

중접된 설정에서 관련된 모델의 속성에 접근하기 위해서 관련된 모델은 이것이 어떤 모델을 참조하고 있는지 미리 알고 있어야만 한다. Backbone.js는 관계와 중첩을 자동적으로 관리하지 않는데, 모델이 서로에 대해 알게하는 것은 우리에게 달렸다는 뜻이다.

한가지 방법은 각각의 자식 모델이ㅣ 'parent' 속성을 갖게하는 것이다. 당신이 중첩 모델을 순회하는 방법은 우선 부모로 올라갔다가 그리고 나서 알고 있는 어떤 동기 모델로 내려가는 것이다. 우리가 modelA, modelB, modeC를 모델로 갖는다고 가정해보자:

```javascript

// modelA를 초기화할 때, 부모 모델에 대한 연결점을 설정할 것을 제안한다
// 이것을 할때, 다음과 같다:

ModelA = Backbone.Model.extend({

    initialize: function(){
        this.modelB = new modelB();
        this.modelB.parent = this;
        this.modelC = new modelC();
        this.modelC.parent = this;
    }
}
```

이것은 당신이 this.parent를 사용해서 자식 모델의 함수에서 부모 모델에 접근할 수 있게 해준다.

중첩된 Backbone.js 뷰가 필요할 때, 각각의 뷰가 tagName 설정을 써서 하나의 HTML 태그를 표현하게 하는 것이 더 쉽다는 것을 알게 될 것이다. 이것은 다음과 같이 작성된다:

```javascript
ViewA = Backbone.View.extend({

    tagName: 'div',
    id: 'new',

    initialize: function(){
       this.viewB = new ViewB();
       this.viewB.parentView = this;
       $(this.el).append(this.viewB.el);
    }
});

ViewB = Backbone.View.extend({

    tagName: 'h1',

    render: function(){
        $(this.el).html('Header text'); // 혹은 this.options.headerText같은 것을 사용해라
    },

    funcB1: function(){
        this.model.parent.doSomethingOnParent();
        this.model.parent.modelC.doSomethingOnSibling();
        $(this.parentView.el).shakeViolently();
    }

});
```

그리고나서 어플리케이션 초기화 코드에서 ViewA를 초기화하고 그 요소를 body 요소안에 넣을 것이다.

또 다른 방법은 [Backbone-Forms](https://github.com/powmedia/backbone-forms)이라는 확장을 사용하는 것이다. 앞에서 우리가 사용했던 것과 유사한 schema를 사용해서, 중첩은 다음과 같이 수행된다:

```javascript
var ModelB = Backbone.Model.extend({
    schema: {
        attributeB1: 'Text',
        attributeB2: 'Text'
    }
});

var ModelC = Backbone.Model.extend({
    schema: {
        attributeC: 'Text',
    }
});

var ModelA = Backbone.Model.extend({
    schema: {
        attributeA1: 'Text',
        attributeA2: 'Text',
        refToModelB: { type: 'NestedModel', model: ModelB, template: 'templateB' },
        refToModelC: { type: 'NestedModel', model: ModelC, template: 'templateC' }
    }
});
```

이 기술에 대한 더 많은 정보를 [GitHub](https://github.com/powmedia/backbone-forms#customising-templates)에서 찾아 볼 수 있다.

(이 팁을 알려준 [Jens Alm](http://stackoverflow.com/users/100952/jens-alm)와 [Artem Oboturov](http://stackoverflow.com/users/801466/artem-oboturov)에게 감사한다 )

#### 어떤 Backbone.js 뷰가 다른 뷰를 갱신하도록 하는 것이 가능한가?


중개자 패턴은 이 문제의 해결책은 구현하는 훌륭한 선택이다.

패턴에 대해 너무 깊게 들어갈 필요없이, 이것은 당신이 이벤트를 발행하고 구독하게 해주는 이벤트 관리자를 효율적으로 쓰게 해준다. ApplicationViewA는 'selected' 이벤트를 구독하고, ApplicationViewB가 'selected' 이벤트를 발행하도록 한다.

내가 이것을 좋아하는 이유는 뷰간에 직접적으로 묶이지 않으면서 당신이 뷰간에 이벤트를 보내게 해주기 때문이다.

예제:

```javascript

// 구현에 대해서는 http://addyosmani.com/largescalejavascript/#mediatorpattern
// 를 보거나 또다른 대안으로 http://thejacklawson.com/Mediator.js/
// 를 통해 더많이 알 수 있다.

var mediator = new Mediator();

var ApplicationViewB = Backbone.View.extend({
    toggle_select: function() {
        ...
        mediator.publish('selected', any, data, you, want);
        return this;
    }
});

var ApplicationViewA = Backbone.View.extend({
    initialize: function() {
        mediator.subscribe('selected', this.delete_selected)
    },

    delete_selected: function(any, data, you, want) {
        ... do something ...
    },
});
```

이러한 방식에서 ApplicationViewA은 'selected' 이벤트를 발행한 것이 ApplicationViewB이든 FooView이든 상관하지 않고 이벤트가 발생했다는 것만 관심을 갖는다. 사실 어플리케이션의 구성부분들 사이에 뷰가 아닌 이벤트를 관리하는 것이 더 유지보수하기 좋다는 것을 알게 될 겄이다.

( 이 팁과 내의 대규모 자바스크립트 글에 대해서 [John McKim](http://stackoverflow.com/users/937577/john-mckim)에게 감사를 전한다 ).

#### 어떻게 하위 뷰가 상위 뷰를 렌더링하는가?

당신이 다른 뷰를 포함하는 뷰( 예를들어 모델 뷰를 포함하는 메인 뷰 )가 있고 자식 뷰에서 부모 뷰를 렌더링 또는 재렌더링하고 싶다고 한다면, 이것은 매우 쉽다.

그 시나리오상에서 당신은 특정 이벤트가 발생했을 때, 렌더링을 수행하고 싶을 것이다. 예를들어, 이 이벤트 'somethingHappened'를 호출해보자. 부모 뷰는 그 이벤트가 발생할 때, 알도록 자식뷰에 이벤트를 바인딩할 수 있다. 그러면 스스로 렌더링할 수 있다.

부모 뷰:

```javascript
// 부모 초기화
this.childView.on('somethingHappened', this.render, this);

// 부모 제거
this.childView.off('somethingHappened', this.render, this);
```

자식 뷰:

```javascript

// 이벤트가 발생한 후
this.trigger('somethingHappened');

```

자식이 "somethingHappened" 이벤트를 발생한 후, 부모의 render 함수가 호출될 것이다.

( 이 팁을 알려준 Tal [Bereznitskey](http://stackoverflow.com/users/269666/tal-bereznitskey) 에게 감사한다 )



#### 어떻게 메모리 누수없이 뷰를 제거하는가?

어플리케이션이 커져감에 따라, 사용되지않지만 살아있는 뷰들이 점점 관리하기 어려워진다. 대신, 더이상 필요하지 않은 뷰들을 없애고 필요하면 새로 만드는 것이 더 좋다는 것을 알게 된다.

이것을 하게 도와주는 해결책은 당신의 뷰가 상속받을 BaseView를 만드는 것이다. 여기의 아이디어는 당신의 뷰가 제거될 때, 모든 이벤트가 자동적으로 언바인딩되기 위해서, 뷰가 구독중인 모든 이벤트의 참조를 가지고 있는 것이다.

샘플 구현:

```javascript
var BaseView = function (options) {

    this.bindings = [];
    Backbone.View.apply(this, [options]);
};

_.extend(BaseView.prototype, Backbone.View.prototype, {

    bindTo: function (model, ev, callback) {

        model.bind(ev, callback, this);
        this.bindings.push({ model: model, ev: ev, callback: callback });
    },

    unbindFromAll: function () {
        _.each(this.bindings, function (binding) {
            binding.model.unbind(binding.ev, binding.callback);
        });
        this.bindings = [];
    },

    dispose: function () {
        this.unbindFromAll(); // 이 뷰가 바인딩한 모든 이벤트를 언바인딩한다.
        this.unbind(); // 이 뷰의 이벤트를 감시하는 모든 감시자를 언바인딩한다. 뷰가 가비지 컬렉트될 것이기 때문에 불필요할 수도 있다.
        this.remove(); // this.el을 DOM에서 제거하고 DOM 이벤트를 제거하는 기본적인 Backbone.View.remove() 메쏘드
    }

});
```

```javascript
BaseView.extend = Backbone.View.extend;
```

그리고 나면, 모델이나 컬렉션의 이벤트에 바인딩되어야만 할 때면, bindTo 메쏘드를 사용할 것이다. 예:

```
var SampleView = BaseView.extend({

    initialize: function(){
        this.bindTo(this.model, 'change', this.render);
        this.bindTo(this.collection, 'reset', this.doSomething);
    }
});
```

뷰를 제거할 때, 간단하게 모든 것이 자동적으로 정리되는 dispose() 메쏘드를 호출해라.

```javascript
var sampleView = new SampleView({model: some_model, collection: some_collection});
sampleView.dispose();
```

( 이 팁을 알려준 to [JohnnyO](http://stackoverflow.com/users/188740/johnnyo)에게 감사한다 )

#### 부모나 자식 뷰에서 뷰의 제거를 어떻게 다루는가?

마지만 질문에서, 우리는 메모리 사용을 줄이기 위해( 일종의 가비지 컬렉션 ) 어떻게 뷰를 효과적으로 삭제할지를 보았다.

어플리케이션이 다수의 부모 자식 뷰로 설정되어 있는 상황에서 더이상 필요없을때, 뷰와 연결된 DOM 요소를 제거하는 것뿐만 아니라 자식 요소에 붙은 이벤트 처리자를 언바인딩하고 싶어하는 것도 일반적이다.

마지막 질문의 해결책이 이 경우를 다루는데 충분하지만, 자식 뷰를 다루는 더 명시적인 예제를 필요로하면, 아래를 보아라:

```javascript
Backbone.View.prototype.close = function() {
    if (this.onClose) {
        this.onClose();
    }
    this.remove();
    this.unbind();
};

NewView = Backbone.View.extend({
    initialize: function() {
       this.childViews = [];
    },
    renderChildren: function(item) {
        var itemView = new NewChildView({ model: item });
        $(this.el).prepend(itemView.render());
        this.childViews.push(itemView);
    },
    onClose: function() {
      _(this.childViews).each(function(view) {
        view.close();
      });
    }
});

NewChildView = Backbone.View.extend({
    tagName: 'li',
    render: function() {
    }
});
```

여기에서 뷰의 close() 메쏘드는 더이상 필요가 없거나 초기화가 필요할 때, 뷰를 제거하도록 구현되었다. 대부분의 경우에 어떤 모델에도 영향이 가지 않도록 하기 위해서 뷰 제거는 뷰단에서 이루어진다.

예를들어, 당신이 블로그 어플리케이션을 작업하고 있고 코멘트의 뷰를 제거하면, 아마도 앱의 다른 뷰가 코멘트의 선택을 보여주고 컬렉션을 초기화하는 것이 이 뷰에 영향을 줄것이다.

( 이 팁을 알려준 [dira](http://stackoverflow.com/users/906136/dira)에게 감사한다 )

#### 뷰들이 서로 결합하고 추가하는 가장 좋은 방법은 무엇인가?




컬렉션의 각 항목이 자체로 컬렉션인 컬렉션을 가지고 있다고 해보자. 컬렉션의 각 항목을 렌더링할 수 있고, 자체가 컬렉션인 항목도 실제로 렌더링 할 수 있다. 우리가 가지고 있는 문제는 HTML이 데이타 구조의 계층성을 표현하도록 어떻게 이 구조를 렌더링할 것이가 이다.

이문제에 접근하는 가장 단순한 방법은 Derick Baileys [Backbone.Marionette](https://github.com/marionettejs/backbone.marionette)같은 프레임워크를 쓰는 것이다. 이 프레임워크에는 CompositeView라 불리는 일종의 뷰가 있다.

CompositeView의 기본 생각은 같은 뷰에서 모델과 컬렉션을 렌더링할 수 있다는 점이다.

그것은 템플릿으로 단일 모델을 렌더링할 수 있다. 또한, 그 모델의 컬렌션을 가져와서 그 컬렉션안의 각 모델에 대해서 뷰를 렌더링한다. 기본적으로 그것은 컬렉션의 각 모델을 렌더링하기 위해 당신이 정의한 동일한 복합 뷰 타입을 사용한다. 이것을 하기 위해서 뷰 인스턴스에 initialize 메쏘드를 통해 컬렌션이 어디에 있는지 말해주기만 하면, 반복적이고 계층적이 그려진다.

[온라인](http://jsfiddle.net/derickbailey/AdWjU/)상에서 실제로 돌아가는 데모가 있다.

그리고 [Marionette](https://github.com/marionettejs/backbone.marionette)에 대한 소스코드와 문서도 얻을 수 있다.

#### 더 나은 모델 특성 검증

우리가 책의 앞부분에서 배운 것처럼, 모델의 `validate` 메쏘드는 `set`과 `save`가 호출되기 전에 호출되고, 그 메쏘드는 값을 갱신한 모델 속성을 전달한다.

기본적으로 우리가 따로 `validate` 메쏘드를 정의하면, Backbone은 어떤 모델 속성이 설정되는지 관계없이 매번 이 검증을 통해 모델의 모든 속성을 전달한다.

이것은 특정 함목이 설정되었는지 확인하거나 설정되지 않은 다른 것에 관심없이 검증하는 것이 부담이 될 수 있다는 뜻이다.

이 문제를 더 잘 보기 위해서 전형적인 등록 폼의 경우를 보자:

* 폼 항목은 blur 이벤트를 사용해서 검증한다
* 다른 모델 속성( 다른 폼 데이타 )이 유효한지 안한지에 관계없이 각각의 항목을 검증한다.

여기 올바른 사용례가 있다:

우리는 사용자가 포커스하너나 포커스를 빼앗을 수 있는 아무것도 채워지지 않은 이름, 성, 이메일 입력 박스를 갖고 있다. 각 폼 항목 옆에 "this field is required" 라는 메시지가 나타나야만 한다.

HTML:

```
<!doctype html>
<html>
<head>
  <meta charset=utf-8>
  <title>Form Validation - Model#validate</title>
  <script src='http://code.jquery.com/jquery.js'></script>
  <script src='http://underscorejs.org/underscore.js'></script>
  <script src='http://backbonejs.org/backbone.js'></script>
</head>
<body>
  <form>
    <label>First Name</label>
    <input name='firstname'>
    <span data-msg='firstname'></span>
    <br>
    <label>Last Name</label>
    <input name='lastname'>
    <span data-msg='lastname'></span>
    <br>
    <label>Email</label>
    <input name='email'>
    <span data-msg='email'></span>
  </form>
</body>
</html>
```

이 폼에 적용되는 현재의 Backbone `validate` 메쏘드를 사용해서 작성된 간단한 검증은 다음과 같이 구현될 수 있다:


```javascript
validate: function(attrs) {

    if(!attrs.firstname) return 'first name is empty';
    if(!attrs.lastname) return 'last name is empty';
    if(!attrs.email) return 'email is empty';

}
```

불행이도, 이 메쏘드는 어떤 항목이라도 포커스를 잃을 때마다 이름 에러만 발동되어서 이름 함목 옆에 에러 메시지만 보인다.

이문제의 한가지 해결책은 모든 필드를 검사한 후 모든 에러를 반환하는 것이다:

```javascript
validate: function(attrs) {
  var errors = {};

  if (!attrs.firstname) errors.firstname = 'first name is empty';
  if (!attrs.lastname) errors.lastname = 'last name is empty';
  if (!attrs.email) errors.email = 'email is empty';

  if (!_.isEmpty(errors)) return errors;
}
```

이것은 폼의 각 입력에 대한 Field  모델을 정의하는 완전한 해결책으로 바뀌어서 우리 경우의 인자들을 다음과 같이 동작한다:

```javascript

$(function($) {

  var User = Backbone.Model.extend({
    validate: function(attrs) {
      var errors = this.errors = {};

      if (!attrs.firstname) errors.firstname = 'firstname is required';
      if (!attrs.lastname) errors.lastname = 'lastname is required';
      if (!attrs.email) errors.email = 'email is required';

      if (!_.isEmpty(errors)) return errors;
    }
  });

  var Field = Backbone.View.extend({
    events: {blur: 'validate'},
    initialize: function() {
      this.name = this.$el.attr('name');
      this.$msg = $('[data-msg=' + this.name + ']');
    },
    validate: function() {
      this.model.set(this.name, this.$el.val());
      this.$msg.text(this.model.errors[this.name] || '');
    }
  });

  var user = new User;

  $('input').each(function() {
    new Field({el: this, model: user});
  });

});

```


이것은 각 개별 속성에 대한 유효성을 검증하고 정상적으로 포커스를 잃은 항목에 다한 메시지를 설정하는 방법으로 잘 동작한다. [@braddunbar](http://github.com/braddunbar)가 만든 위의 [데모](http://jsbin.com/afetez/2/edit)도 돌려볼 수 있다.

하지만 불행히도 폼의 항목 모두를 매번 검증해야 한다.
우리가 특정 경우에 다수의 클라이언트 검증 메쏘드를 가지고 있다면, 우리는 매번 모든 속성에 각 검증 메쏘드를 호출되어야만 하길 원하지 않기 때문에, 여러분에게 이 해결책은 이상적이지 않다.

위의 방법의 잠재적으로 더 나은 대안은 [@gfranko](http://github.com/@franko)의 [Backbone.validateAll](https://github.com/gfranko/Backbone.validateAll) 플러그인을 쓰는 것이다. 그것은 다른 모델 특성( 혹은 폭 항목 )의 검증을 고려할 필요없이 특정 모델 특성( 혹은 폼 항목 )을 검증하기 위해 특별히 만들어졌다.

여기에서는 어떻게 이 플러그인을 사용해서 부부전인 User 모델과 validate 메쏘드를 설정해서 우리 예제에 적용하는지 보여준다:


```javascript

// Create a new User Model
var User = Backbone.Model.extend({

      // 정규식
      patterns: {

          specialCharacters: '[^a-zA-Z 0-9]+',

          digits: '[0-9]',

          email: '^[a-zA-Z0-9._-]+@[a-zA-Z0-9][a-zA-Z0-9.-]*[.]{1}[a-zA-Z]{2,6}$'
      },

      // Validators
      validators: {

          minLength: function(value, minLength) {
            return value.length >= minLength;

          },

          maxLength: function(value, maxLength) {
            return value.length <= maxLength;

          },

          isEmail: function(value) {
            return User.prototype.validators.pattern(value, User.prototype.patterns.email);

          },

          hasSpecialCharacter: function(value) {
            return User.prototype.validators.pattern(value, User.prototype.patterns.specialCharacters);

          },
         ...

    // 우리는 속성이 널인지 비교함으로써 어떤 속성이
	// 유효한지 결정할 수 있다.

        validate: function(attrs) {

          var errors = this.errors = {};

          if(attrs.firstname != null) {
              if (!attrs.firstname) {
                  errors.firstname = 'firstname is required';
                  console.log('first name isEmpty validation called');
              }

              else if(!this.validators.minLength(attrs.firstname, 2))
                errors.firstname = 'firstname is too short';
              else if(!this.validators.maxLength(attrs.firstname, 15))
                errors.firstname = 'firstname is too large';
              else if(this.validators.hasSpecialCharacter(attrs.firstname)) errors.firstname = 'firstname cannot contain special characters';
          }

          if(attrs.lastname != null) {

              if (!attrs.lastname) {
                  errors.lastname = 'lastname is required';
                  console.log('last name isEmpty validation called');
              }

              else if(!this.validators.minLength(attrs.lastname, 2))
                errors.lastname = 'lastname is too short';
              else if(!this.validators.maxLength(attrs.lastname, 15))
                errors.lastname = 'lastname is too large';
              else if(this.validators.hasSpecialCharacter(attrs.lastname)) errors.lastname = 'lastname cannot contain special characters';

          }
```


이 방법은 validate 메쏘드 내부 로직이 어떤 폼 항목이 현재 설정되고 검증되고 있는지를 결정하도록 해서 설정하려고 하지 않는 다른 모델 특성에 신경쓰지 않도록 해준다.

그것은 사용하기에도 꽤 쉽다. 우리는 단순히 새로운 모델 객체를 정의할 수 있고, 그리고나서 플러그인에 의해 정의된 동작을 사용하는 모델의 `validateAll` 옵션을 사용해서 데이타를 설정한다:



```javascript
var user = new User();
user.set({ 'firstname': 'Greg' }, {validateAll: false});

```


끝났다!.

Backbone.validateAll 로직은 기본적으로 기본 Backbone 로직을 덮어쓰지 않는다. 그래서 그것은 우리가 그다지 관심갖지 않는 항목 검증의 [성능](http://jsperf.com/backbone-validateall)에  대해서도 더 잘 관리하는 시나리오를 사용할 수 있다. 그러나 이 섹션의 두 해결책 모두 잘 동작할 것이다.


# Backbone 확장


## Backbone.Marionette

*Derick Bailey & Addy Osmani에 의해 만들어졌음*

알다시피, Backbone은 자바스크립트 어플리케이션에 많은 개발 조각을 제공한다. 그것은 작은 크기에서 중간 크기의 앱을 개발하거나, jQuery DOM 이벤트를 구성하거나, 모바일 기기와 대규모의 기업 요건을 지원하는 단일 페이지 앱을 만들거나 하는데 필요한 주요 조각을 제공한다. 하지만 Backbone은 완벽한 프레임워크는 아니다. 그것은 메모리 관리, 뷰 관리 등등을 포함해서 어플리케이션의 설계, 구조, 확장성을 개발자에게 남겨둔 개발조각이다.

[Backbone.Marionette](http://marionettejs.com) ( 혹은 단지 "Marionette" )는 위에서 Backbone이 제공하는 일반적이지 않은 어플리케이션의 개발자가 요구하는 많은 특성들을 제공한다. 대규모의 어플리케이션 제작을 단순화를 목적으로 하는 복합적인 어플리케이션 라이브러리이다. 그것은 개발자인 [Derick Bailey](http://lostechies.com/derickbailey/)와 많은 다른 [기여자](https://github.com/marionettejs/backbone.marionette/graphs/contributors)들이 Backbone 앱을 개발하는데 사용해왔던 어플리케이션에서 발견되는 공통 설과와 구현 패턴들을 제공한다.

Marionette의 주요 장점은 다음과 같다:

* 어플리케이션을 모듈화되고 이벤트 주도적인 구조로 확장한다.
* 뷰 렌더링을 위해 Underscore 템플릿을 사용하는 것같은 상식적인 기본값
* 어플리케이션의 특정한 요건을 맞추기 위해 수정하기 쉽다
* 특화된 뷰타입으로 뷰의 보일러플레이트를 줄인다
* 어플리케이션의 모듈 구조와 그것에 붙는 모듈 상에서 개발한다
* Region과 Layout으로 런타임에 어플리케이션의 렌더링하는 컴포넌트를 구성한다
* 눈에 보이는 영역 안에 중첩 뷰와 레이아웃을 둔다
* 내장된 메모리 관리와 뷰, 영역, 레이아웃 내의 좀비를 제거한다
* EventBinder로 내장된 이벤트를 제거한다
* EventAggregator로 이벤트 주도 구조를 만든다
* 필요한 것을 뽑아내고, 선택하도록 해주는 유연한 "as-needed" 구조
* 등등

마리오네트는 서로 독립적으로 사용될 수 있거나 개발자이인 우리를 위해 큰 이익을 가져다 주기 위해 함께 사용할 수 있는 컴포넌트를 제공한다는 점에서 Backbone과 유사한 철학을 지향한다. 하지만, 그것은 Backbone의 구조적인 컴포넌트 위에서 발전하고, 어플리케이션에 수십개의 컴포넌트와 개발 조각을 제공한다.

마리오네트의 컴포넌트는 제공되는 특성상 크게 차이가 있지만, 모든 컴포넌트들은 보일러플레이트 코드를 줄이고, 많이 사용되는 어플리케이션 구조를 제공할 수 있는 복합적인 어플리케이션 계층을 만들기 위해 함께 사용된다. 주요 컴포넌트는 다음과 같다:

* [**Backbone.Marionette.Application**](https://github.com/marionettejs/backbone.marionette/blob/master/docs/marionette.application.md): 초기화 객체를 통해 앱을 시작하게 해주는 어플리케이션 객체
* [**Backbone.Marionette.Application.module**](https://github.com/marionettejs/backbone.marionette/blob/master/docs/marionette.application.module.md): 어플리케이션내의 모듈과 하위 모듈을 생성한다.
* [**Backbone.Marionette.AppRouter**](https://github.com/marionettejs/backbone.marionette/blob/master/docs/marionette.approuter.md): 라우터를 설정만으로 줄여준다.
* [**Backbone.Marionette.View**](https://github.com/marionettejs/backbone.marionette/blob/master/docs/marionette.view.md): ( 직접적으로 사용되지는 않지만 ) 다른 마리오네트 뷰가 상속하는 기본 뷰 타입
* [**Backbone.Marionette.ItemView**](https://github.com/marionettejs/backbone.marionette/blob/master/docs/marionette.itemview.md): 단일 항목을 렌더링하는 뷰
* [**Backbone.Marionette.CollectionView**](https://github.com/marionettejs/backbone.marionette/blob/master/docs/marionette.collectionview.md): 컬렉션을 순회하여 각 모델에 대한 각각의 `ItemView` 객체를 렌더링하는 뷰
* [**Backbone.Marionette.CompositeView**](https://github.com/marionettejs/backbone.marionette/blob/master/docs/marionette.compositeview.md): 종단 혹은 복합 모델 계층을 렌더링하기 위한 컬렉션 뷰와 항목 뷰
* [**Backbone.Marionette.Region**](https://github.com/marionettejs/backbone.marionette/blob/master/docs/marionette.region.md): 어플리케이션에서 내용을 보이고 안보이는 것을 포함한 가시적인 영역을 관리한다
* [**Backbone.Marionette.Layout**](https://github.com/marionettejs/backbone.marionette/blob/master/docs/marionette.layout.md): 레이아웃을 렌더링하고 그 내부 영역을 관리하는 영역 관리자를 생성하는 뷰
* [**Backbone.Marionette.EventAggregator**](https://github.com/marionettejs/backbone.marionette/blob/master/docs/marionette.eventaggregator.md): 이벤트 유도 혹은 발행-구독 툴로 사용되는 Backbone.Events의 확장
* [**Backbone.Marionette.EventBinder**](https://github.com/marionettejs/backbone.marionette/blob/master/docs/marionette.eventbinder.md): 이벤트를 바인딩하고 언바인딩을 도와주는 이벤트 바인딩 관리자
* [**Backbone.Marionette.Renderer**](https://github.com/marionettejs/backbone.marionette/blob/master/docs/marionette.renderer.md): 데이터를 가진 템플릿이든 안가진 템플릿이든 견고하고 일반적인 방식으로 렌더링한다.
* [**Backbone.Marionette.TemplateCache**](https://github.com/marionettejs/backbone.marionette/blob/master/docs/marionette.templatecache.md): `<script>` 블럭에 저장된 템플릿을 빠른 후속처리를 위해 캐쉬한다.
* [**Backbone.Marionette.Callbacks**](https://github.com/marionettejs/backbone.marionette/blob/master/docs/marionette.callbacks.md): 콜백 메쏘드들을 관리하고 필요에 따라 호출한다.

하지만 Backbone과 같이 단지 마리오네트 컴포넌트 몇몇을 쓰고 싶다면, 전체 컴포넌트를 쓸 필요는 없다. 때에 따라서 쓰고 싶은 특성을 선택해서 뽑아 쓸 수 있다. 이것은 다른 Backbone 프레임워크와 플러그인들과 매우 쉽게 연동하도록 해준다. 이것은 또한 마리오네트를 사용하기 위해서 전체를 수정하지 않아도 된다는 것을 의미한다.

### 보일러플레이트 렌더링 코드

Backbone과 Underscore로 뷰를 일반적으로 렌더링할 필요가 있는 코드를 상상해보라. 우리는 렌더링한 템플릿이 필요하다. 그 템플릿이 DOM에 직접적으로 있고, 그 템플릿을 사용하는 뷰를 정의하는 자바스크립트가 필요하다. 그리고, 모델의 데이타로 템플릿을 적용해야만 한다.

```
<script type="text/html" id="my-view-template">
  <div class="row">
    <label>First Name:</label>
    <span><%= firstName %></span>
  </div>
  <div class="row">
    <label>Last Name:</label>
    <span><%= lastName %></span>
  </div>
  <div class="row">
    <label>Email:</label>
    <span><%= email %></span>
  </div>
</script>
</pre>
```

```javascript
var MyView = Backbone.View.extend({
  template: $('#my-view-template').html(),

  render: function(){

    // Underscore.js 템플릿을 컴파일한다.
    var compiledTemplate = _.template(this.template);

    // 모델 데이타로 템플릿을 렌더링한다
    var data = this.model.toJSON();
    var html = compiledTemplate(data);

    // 렌더링된 html로 뷰에 적용한다
    this.$el.html(html);
  }
});
```

일단 작성된 대로라면, 뷰를 생성하고 모델을 전달해야만 한다. 그리고나서, 뷰의 `el`을 가져다가 뷰를 보여주는 순서에 따라 DOM에 추가한다.

```javascript
var myModel = new MyModel({
  firstName: 'Derick',
  lastName: 'Bailey',
  email: 'derickbailey@gmail.com'
});

var myView = new MyView({
  model: myModel
})

myView.render();

$('#content').html(myView.el)
```

이것은 Backbone으로 뷰를 정의하고, 작서하고, 렌더링하고, 보여주기 위한 기본 설정이다. 이것은 또한 우리가 "보일러플레이트 코드" ( 같은 기능의 모든 프로젝트와 구현에서 반복되는 코드 )라고 부르는 것이다. 그것은 금새 지겹고 반복된다.

마리오네트의 `ItemView`로 입문하라 - 뷰를 정의하는 보일러플레이트를 줄여주는 단순한 방법이다.

### Marionette.ItemView로 보일러플레이트 경감

( `Marionette.View`를 제외하고 )모든 마리오네트 뷰 타입은 핵심적인 렌더링 로직을 다루는 내장 `render` 메쏘드를 가지고 있다. `Backbone.View`에서 상속된 `MyView`를 바꿈으로써, 이 장점을 가질 수 있다. 뷰를 위한 자체적인 `render` 메쏘드를 제공하는 대신에 마리오네트가 렌더링할 수 있게 한다. 우리는 여전히 동일한 Underscore.js 템플릿과 렌더링 메커니즘을 사용하지만, 그 구현은 우리 눈에 숨겨졌다. 결국, 우리는 뷰에 필요한 코드량을 줄일 수 있다.

```javascript
var MyView = Backbone.Marionette.ItemView.extend({
  template: '#my-view-template'
});
```

이것이 다이다 - 이전 뷰 구현과 정확히 동일한 동작을 하도록 하기 위해 당신이 해야할 모두이다. `Backbone.View.extend`를 `Backbone.Marionette.ItemView.extend`로 바꾸고 나서 `render` 메쏘드를 제거해라. 이전에 했던 같은 방법으로 여전히 `model`로 뷰 객체를 생성할 수 있고 뷰 객체의 `render` 메쏘드를 호출할 수 있고, DOM에 뷰를 보여줄 수 있다. 하지만, 뷰 정의는 템플릿을 위한 단 한줄의 설정으로 줄었다.

### 메모리 관리

뷰를 정의하는데 필요한 코드를 줄이는 것 뿐만 아니라, 마리오네트는 모든 뷰내에 뷰 객체와 이벤트 핸들러를 쉽게 제거하는 진보된 메모리 관리 기능을 포함한다.

다음 뷰 구현을 생각해 보자:

```javascript
var ZombieView = Backbone.View.extend({
  template: '#my-view-template',

  initialize: function(){

    // 뷰를 다시 렌더링하기 위해서 모델을 change 이벤트에 바인딩한다
    this.model.on('change', this.render, this);

  },

  render: function(){

    // 이 알람이 문제를 표시할 것이다.
    alert('We`re rendering the view');

  }
});
```

우리가 동일한 변수명으로 이 뷰에 대해서 두 객체를 생성해서 모델의 값을 변경하면, 알람 창을 몇번 보게 될까?

```javascript
var myModel = new MyModel({
  firstName: 'Jeremy',
  lastName: 'Ashkenas',
  email: 'jeremy@example.com'
});

// 첫번째 뷰 객체를 생성한다.
var zombieView = new ZombieView({
  model: myModel
})

// 동일한 변수명을 사용해서
// 두번째 뷰 객체를 생성한다
zombieView = new ZombieView({
  model: myModel
})

myModel.set('email', 'jeremy@gmail.com');
```

우리가 두 객체를 위해서 같은 `zombieView` 변수를 재사용하고 있기 때문에, 두번째 객체가 성성된 후 바로 첫번째 뷰 객체가 스코프에서 없어질 것이다. 이것은 자바스크립트 가비지콜렉트가 구동되어서 제거할 것이다. 그것은 첫번째 뷰객체는 더이상 활성화되지 않고 모델의 "change" 이벤트에 반응하지 않음을 의미한다.

하지만 우리가 이코드를 실행하면, 우리는 알람창이 두번 보여지는 것을 알게된다!

문제는 뷰의 `initialize` 메쏘드에서 모델의 이벤트 바인딩 때문이다. 우리가 `this.render`를 모델의 `on` 이벤트 바인딩에 콜백 메쏘드로 전달할 때, 모델 그 자체가 뷰 객체에 대한 직접 참조가 주어진다. 이제는 모델이 뷰객체에 대한 참조를 잡고 있기 때문에 `zombieView` 변수를 새로운 뷰 객체로 대체하는 것이 원래 뷰를 스코프에서 제거되게 하지 않는다. 모델이 여전히 참조를 가지고 있기 때문에, 뷰는 여전히 스코프에 남아있다.

원 뷰가 스코프에 남아있고 두번째 뷰 객체도 스코프에 있기 때문에, 모델의 데이타를 바꾸는 것은 양쪽 뷰 객체가 반응하도록 할 것이다.

그래도 이것을 고치는 것은 쉽다. 뷰가 그 동작을 다하고 삭제될 때, `off`를 호출하기만 하면 된다. 이렇게 하기 위해서 뷰에 `close` 메쏘드를 추가해라.

```javascript
var ZombieView = Backbone.View.extend({
  template: '#my-view-template',

  initialize: function(){
    // 뷰를 다시 렌더링하기 위해서 모델을 change 이벤트에 바인딩한다
    this.model.on('change', this.render, this);
  },

  close: function(){
    this.model.off('change', this.render, this);
  },

  render: function(){

    // 이 알람이 문제를 표시할 것이다.
    alert('We`re rendering the view');

  }
});
```

그리고나서 더이상 필요하지 않을 때, 첫번째 객체의 `close`를 호출하면, 단 하나의 뷰 객체만 살아남을 것이다.

```javascript
var myModel = new MyModel({
  firstName: 'Jeremy',
  lastName: 'Ashkenas',
  email: 'jeremy@example.com'
});

// 첫번째 뷰 객체를 생성한다.
var zombieView = new ZombieView({
  model: myModel
})
zombieView.close(); // 두번 확인한다.

// 동일한 변수명을 사용해서
// 두번째 뷰 객체를 생성한다
zombieView = new ZombieView({
  model: myModel
})

myModel.set('email', 'jeremy@gmail.com');
```

이제 우리는 이 코드를 실행할 때 한번의 알림창만 보게 될 것이다.

그러나 이벤트 처리자들을 수동으로 제거해야만 하기 보다는 마리오네트가 하도록 할 수 있다

```javascript
var ZombieView = Backbone.Marionette.ItemView.extend({
  template: '#my-view-template',

  initialize: function(){

    // 뷰를 다시 렌더링하기 위해서 모델을 change 이벤트에 바인딩한다
    this.bindTo(this.model, 'change', this.render, this);

  },

  render: function(){

    // 이 알람이 문제를 표시할 것이다.
    alert('We`re rendering the view');

  }
});
```

이 경우에 우리가 `bintTo`라는 메쏘드를 사용하고 있는 것을 눈여겨보아라. 이 메쏘드는 마리오네트의 `EventBinder` 객체에서 왔고, 모든 마리오네트 뷰 타입에 추가된다. `bindTo` 메쏘드의 모양은 이벤트를 구동하는 객체를 첫번째 인자로 전달하는 것을 제외하면 `on` 메쏘드와 유사하다.

마리오네트의 뷰는 또한 `close` 이벤트를 제공하는데, `bintTo`로 설정된 이벤트 바인딩은 자동으로 그 안에서 제거될 것이다. 이것은 우리가 더이상 직접 `close` 메쏘드를 정의할 필요가 없다는 쓰이며, `bindTo` 메쏘드를 쓸 때, 우리 이벤트가 없어져서 뷰는 좀비가 되지 않을 것이라는 것을 알게 된다.

하지만, 실제 어플리케이션에서 뷰에 `close`를 호출하는 것은 어떻게 자동화하는가? 그것을 언제 어디서 호출할 것인가? `Marionette.Region`( 각 뷰의 생명주기를 관리하는 객체 )에 들어가 보자.

### 영역 관리

뷰가 생성된 후, 일반적으로 보여지기 위해 DOM에 들어가야만 한다. 그동작은 일반적으로 jQuery의 선택자와 그 결과 객체의 `html()` 설정에 의해 이루어진다:

```javascript
var myModel = new MyModel({
  firstName: 'Jeremy',
  lastName: 'Ashkenas',
  email: 'jeremy@gmail.com'
});

var myView = new MyView({
  model: myModel
})

myView.render();

// DOM에 뷰를 보여준다
$('#content').html(myView.el)
```

이것은 또다시 보일러플레이트 코드이다. 우리가 직접 `render`를 호출하고 뷰를 보여주기 위해 DOM 객체를 선택하지 말아야 한다. 더 나아가서, 이 코드는 스스로 우리가 적용하고 싶은 DOM 요소에 붙어 있었던 이전 뷰 객체를 닫도록 하고 있지않다. 그리고, 우리는 이미 좀비 뷰의 위험을 보지 않았는가.

이 문제를 풀기위해서, 마리오네트는 `Region` 객체( 특정 DOM 요소에 보여지는 각 뷰의 생명주기를 관리하는 객체 )를 제공한다.

```javascript
// 관리할 DOM 요소가 어떤 것인지 지정한 영역 객체를 생성한다
var myRegion = new Backbone.Marionette.Region({
  el: '#content'
});

// 영역에 뷰를 보여준다.
var view1 = new MyView({ /* ... */ });
myRegion.show(view1);

// 코드의 다른 부분에서
// 다른 뷰를 보여준다
var view2 = new MyView({ /* ... */ });
myRegion.show(view2);
```

여기에서 주의할 것이 몇가지있다. 첫번째, 우리는 영역에 `el`을 지정함으로써 관리할 DOM 요소가 무엇인지 알려줬다. 두번째, 우리는 뷰의 `render` 메쏘드를 더이상 호출하지 않는다. 마지막으로 우리는 뷰상에 `close`를 호출하지도 않지만 이것은 후출된다.

우리가 뷰의 생명주기를 관리하고 DOM에 뷰를 보여주기 위해 영역을 사용할 때, 영역 스스로는 이들 관심사항을 제어한다. 영역의 `show` 메쏘드로 뷰 객체를 전달함으로써 영역은 뷰에 있는 render 메쏘드를 호출할 것이다. 그것은 뷰의 최종 `el`을 가져다가 DOM 요소에 적용할 것이다.

다음에 영역의 `show` 메쏘드를 호출하면, 영역은 뷰가 현제 보여지고 있다는 것을 기억하고 있다. 영역은 뷰의 `close` 메쏘드를 호출해서 DOM에서 제거하고 계속해서 전달된 새로운 뷰에 대해 렌더링하고 보여주는 코드를 실행한다.

영역이 `close` 호출을 제어하고 뷰 객체 내의 `bintTo` 이벤트 바인더를 사용하기 때문에 우리는 더이상 어플리케이션에 좀비 뷰에 대해 걱정할 필요가 없다.


### 마리오네트 할일 앱

마리오네트의 상위 개념을 배웠으니, 그것을 사용해서 우리의 첫 연습으로 만든 할일 어플리케이션을 리팩토링해보자. 이 어플리케이션의 전체 코드는 Derick의 TodoMVC [fork](https://github.com/derickbailey/todomvc/tree/master/labs/architecture-examples/backbone_marionette_modules/js)에서 찾을 수 있다.

우리의 최종 구현은 겉으로 보기에나 기능적으로 아래와 같이 원래 앱과 동일하다.

![](img/marionette_todo0.png)

우선, 기본 TodoMVC 앱을 나타내는 어플리케이션 객체를 정의한다. 이것은 조기화 코드를 포함하고 우리 앱의 기본 레이아웃 영역들을 정의한다.

**TodoMVC.js:**

```javascript
var TodoMVC = new Backbone.Marionette.Application();

TodoMVC.addRegions({
  header : '#header',
  main   : '#main',
  footer : '#footer'
});

TodoMVC.on('initialize:after', function(){
  Backbone.history.start();
});
```

영역들은 특정 요소들 안에 보여지는 내용을 관리하는데 사용되고, `TodoMVC` 객체의 `addRegions` 메쏘드는 단지 `Region` 객체를 생성하는 축약일 뿐이다. 우리는 관리할 각 영역에 대한 jQuery 선택자( 예를들어 `#header`, `#main`, `#footer` )를 지정하고, 그 영역 내에 다양한 Backbone 뷰를 보여주기 위해 영역을 알려준다.

![](img/marionette_todo1.png)

어플리케이션 객체가 초기화되면, 초기 URL로 이동하기 위해, `Backbone.history.start()`을 호출한다.

다음으로, 우리는의 레이아웃들을 정의한다. 레이아웃은 `Marionette.ItemView`에서 직접 상속된 특별한 종류의 뷰이다. 이것은 단일 템플릿을 렌더링하하거나, 템플릿과 연관된 모델( 혹은 `item` )이 없다는 것을 의미한다.

레이아웃과 `ItemView` 사이의 주요 차이점중에 하나는 레이아웃은 영역을 가지고 있다는 것이다. 레이아웃을 정의할 때, 우리는 `template`으로 제공하지만 템플릿이 가지고 있는 영역들도 제공한다. 레이아웃이 렌더링된 후, 우리는 정의된 영역들을 사용하는 레이아웃내의 다른 뷰들을 보여줄 수 있다.

아래의 TodoMVC 레이아웃 모둘에서 우리는 다음과 같이 레이아웃을 정의한다:

* Header: 우리가 새로운 할일을 생성할 수 있는 곳
* Footer: 얼마나 많은 징행중/완료된 할일이 있는지 요약해 주는 곳

이 부부은 이전에 `AppView`와 `TodoView`에 있었던 뷰 로직의 일부가 담겨있다.

아래와 같은 마리오네트 모듈은 마리오네트 앱내에서 개인정보와 구현은닉을 만드는데 사용되는 단순한 모듈 시스템을 제공하는 것을 기억해라. 하지만 이런 것들이 사용될 필요는 없지만, 대신 이 섹션의 후반부에 RequireJS와 AMD를 사용한 또다른 구현에 대한 링크를 줄 것이다.


**TodoMVC.Layout.js:**

```javascript
TodoMVC.module('Layout', function(Layout, App, Backbone, Marionette, $, _){

  // 레이아웃 Header 뷰
  // ------------------

  Layout.Header = Backbone.Marionette.ItemView.extend({
    template : '#template-header',

    // UI 바인딩은 jQuery  선택자 객체를 가르키는
	// 캐쉬된 속성을 생성한다
    ui : {
      input : '#new-todo'
    },

    events : {
      'keypress #new-todo':   'onInputKeypress'
    },

    onInputKeypress : function(evt) {
      var ENTER_KEY = 13;
      var todoText = this.ui.input.val().trim();

      if ( evt.which === ENTER_KEY && todoText ) {
        this.collection.create({
          title : todoText
        });
        this.ui.input.val('');
      }
    }
  });

  // 레이아웃 Footer 뷰
  // ------------------
  
  Layout.Footer = Backbone.Marionette.Layout.extend({
    template : '#template-footer',

    // UI 바인딩은 jQuery  선택자 객체를 가르키는
	// 캐쉬된 속성을 생성한다
    ui : {
      count   : '#todo-count strong',
      filters : '#filters a'
    },

    events : {
      'click #clear-completed' : 'onClearClick'
    },

    initialize : function() {
      this.bindTo(App.vent, 'todoList:filter', this.updateFilterSelection, this);
      this.bindTo(this.collection, 'all', this.updateCount, this);
    },

    onRender : function() {
      this.updateCount();
    },

    updateCount : function() {
      var count = this.collection.getActive().length;
      this.ui.count.html(count);

      if (count === 0) {
        this.$el.parent().hide();
      } else {
        this.$el.parent().show();
      }
    },

    updateFilterSelection : function(filter) {
      this.ui.filters
        .removeClass('selected')
        .filter('[href="#' + filter + '"]')
        .addClass('selected');
    },

    onClearClick : function() {
      var completed = this.collection.getCompleted();
      completed.forEach(function destroy(todo) { 
        todo.destroy(); 
      });
    }
  });

});

```

다음으로, 우리는 페이지내의 보이거나 혹은 안보이는 레이아웃을 제어하는 것같은 어플리케이션 라우팅과 흐름을 방해한다.

마리오네트는 라우팅을 단순화하기 위해 AppRouter의 개념을 사용한다. 이것은 라우터 이벤트를 다루는 보일러플레이트를 줄여주고 라우터가 객체의 메쏘드를 직접 호출하도록 설정해 준다. 우리는 `appRoutes`를 사용해서 AppRouter를 설정한다.

이것은 원래 Workspace 라우터에 정의된 `'*filter': 'setFilter'` 지점을 아래 보듯이 바꾼다:

```javascript
        var Workspace = Backbone.Router.extend({
                routes:{
                        '*filter': 'setFilter'
                },

                setFilter: function( param ) {
                        // 사용된 현재 필터를 지정한다
                        window.app.TodoFilter = param.trim() || '';

                        // 컬렉션의 reset/addAll 를 구동한다.
                        window.app.Todos.trigger('reset');
                }
        });
```

TodoList 컨트롤러는 매우 가독성높은 레이아웃을 사용하기는 하지만 원래 `AppView`와 `TodoView`에 있었던 나머지 보여주는 로직을 다룬다.

**TodoMVC.TodoList.js:**

```javascript
TodoMVC.module('TodoList', function(TodoList, App, Backbone, Marionette, $, _){

  // TodoList 라우터
  // ---------------
  //
  // 활성화, 완료된 할일 항목을 보여주는 지점을 다룬다

  TodoList.Router = Marionette.AppRouter.extend({
    appRoutes : {
      '*filter': 'filterItems'
    }
  });

  // TodoList 컨트롤러 (중계자)
  // ------------------------------
  //
  // 위의 뷰와 모델의 상세 구현에서 어플리케이션 수준에
  // 존재하는 흐름과 로직을 제어한다.
  
  TodoList.Controller = function(){
    this.todoList = new App.Todos.TodoList();
  };

  _.extend(TodoList.Controller.prototype, {

    // 적절할 뷰들을 보여주고 만일 있다면,
	// 할일 항목들을 조회함으로써 앱을 시작한다.
    start: function(){
      this.showHeader(this.todoList);
      this.showFooter(this.todoList);
      this.showTodoList(this.todoList);

      this.todoList.fetch();
    },

    showHeader: function(todoList){
      var header = new App.Layout.Header({
        collection: todoList
      });
      App.header.show(header);
    },

    showFooter: function(todoList){
      var footer = new App.Layout.Footer({
        collection: todoList
      });
      App.footer.show(footer);
    },

    showTodoList: function(todoList){
      App.main.show(new TodoList.Views.ListView({
        collection : todoList
      }));
    },

    // 완료 또는 전체 항목을 보여주는 필터를 설정한다.
    filterItems: function(filter){
      App.vent.trigger('todoList:filter', filter.trim() || '');
    }
  });

  // TodoList 초기화 객체
  // --------------------
  //
  // 어플리케이션이 시작할 때,
  // TodoList를 시작하고 존재하는 할일 항목을
  // 모아서 보여주는 중계자를 초기화한다.
  
  TodoList.addInitializer(function(){

    var controller = new TodoList.Controller();
    new TodoList.Router({
      controller: controller
    });

    controller.start();

  });

});

```

####컨트롤러

이 앱에서 컨트롤러는 전체 흐를에 많이 기여하지 않는 것을 기억하라. 하지만 일반적으로 라우터에 대한 마리오네트의 철학은 라우터들이 어플리케이션의 구현에서 나중에 고려해야만 하는 것이다라는 것이다. 아주 자주, 우리는 라우터를 전체 어플리케이션의 흐름과 로직의 단일 컨트롤러로 만드는 Backbone의 라우팅 시스템을 남용하는 개발자들의 나쁜 예를 많이 볼 것이다.

이것은 부득이하게 라우터 메쏘드에 모든 가능한 코드 조합( 뷰 생성, 모델 로딩, 앱의 다른 부분과 결합 등등 )을 짜집기하게한다. Derick과 같은 개발자는 이것을 [단일 책임 원치](http://en.wikipedia.org/wiki/Single_responsibility_principle) (SRP)과 관심분리의 위반으로 본다.

Backbone의 라우터와 히스토리는 브라우져의 특정 관점을 다루기 위해 존재한다 - 앞으로 가기와 뒤로 가기 버튼 관리. 마리오네트는 이동에 의해 실행되는 코드로 다른곳으로 가능 데에 제한되어야 한다고 생각한다. 이것은 어플리케이션이 라우터를 사용하거나 사용하지 않게 해준다. 우리는 버튼 클릭이나 어플리케이션 이벤트 처리자나 라우터로 부터 컨트롤러의 "show"를 호출하고 어떻게 호출했는지 상관없이 결국 같은 어플리케이션 상태가 되게 할 것이다.

Derick은 이 주제에 대한 자신의 생각을 확장해서 글을 썼고, 그 블로그에서 좀 더 읽을 수 있다:

* [http://lostechies.com/derickbailey/2011/12/27/the-responsibilities-of-the-various-pieces-of-backbone-js/](http://lostechies.com/derickbailey/2011/12/27/the-responsibilities-of-the-various-pieces-of-backbone-js/)
* [http://lostechies.com/derickbailey/2012/01/02/reducing-backbone-routers-to-nothing-more-than-configuration/](http://lostechies.com/derickbailey/2012/01/02/reducing-backbone-routers-to-nothing-more-than-configuration/)
* [http://lostechies.com/derickbailey/2012/02/06/3-stages-of-a-backbone-applications-startup/](http://lostechies.com/derickbailey/2012/02/06/3-stages-of-a-backbone-applications-startup/)

#### 복합뷰

그리고 나서 우리는 TodoMVC 어플리케이션에서 할일 항목들과 할일 항목 리스트에 대한 실제 뷰를 정의한다. 이를 위해서, 우리는 마리오네트의 `복합뷰 - CompositeView`들을 사용한다. 복합뷰 뒤의 개념은 잎( 혹은 노드 )와 가지의 재귀적이고 계층적인 구조의 모습을 표현하는 것이다.

이 뷰들을 부모-자식 모델의 계층이며 기본적으로 재귀적이라고 생각해보라. 복합뷰가 다루는 컬렉션내의 각 항목에 대해서, 같은 복합뷰 타입이 그 항목을 렌더링하는데 사용될 것이다. 재귀적이지 않은 계층에 대해서도 `itemView` 속성을 정의함으로써 항목 뷰를 덮어쓸 수 있다.

우리의 할일 목록 항목 뷰에 대해서, 우리가 그것을 ItemView로 정의하면 우리의 할일 목록 뷰는 컬렉션의 각 항목의 할일 목록 항목 뷰를 사용할 `itemView`설정이 덮어써진 복합뷰가 된다.

TodoMVC.TodoList.Views.js

```javascript
TodoMVC.module('TodoList.Views', function(Views, App, Backbone, Marionette, $, _){

  // 할일 목록 항목 뷰
  // -------------------
  //
  // 각 할일 항목을 보여주고, 완료 마크를
  // 포함해서 항목의 변경에 대응한다.

  Views.ItemView = Marionette.ItemView.extend({
    tagName : 'li',
      template : '#template-todoItemView',

      ui : {
        edit : '.edit'
      },

      events : {
        'click .destroy' : 'destroy',
        'dblclick label' : 'onEditClick',
        'keypress .edit' : 'onEditKeypress',
        'click .toggle'  : 'toggle'
      },

      initialize : function() {
        this.bindTo(this.model, 'change', this.render, this);
      },

      onRender : function() {
        this.$el.removeClass('active completed');
        if (this.model.get('completed')) this.$el.addClass('completed');
        else this.$el.addClass('active');
      },

      destroy : function() {
        this.model.destroy();
      },

      toggle  : function() {
        this.model.toggle().save();
      },

      onEditClick : function() {
        this.$el.addClass('editing');
        this.ui.edit.focus();
      },

      onEditKeypress : function(evt) {
        var ENTER_KEY = 13;
        var todoText = this.ui.edit.val().trim();

        if ( evt.which === ENTER_KEY && todoText ) {
          this.model.set('title', todoText).save();
          this.$el.removeClass('editing');
        }
      }
  });

  // 항목 목록 뷰
  // --------------
  //
  // 보여주기 위한 활성/완료 항목을 필터링하는 것을 포함해서
  // 항목의 목롤을 렌더링하는 것을 제어한다.

  Views.ListView = Backbone.Marionette.CompositeView.extend({
    template : '#template-todoListCompositeView',
      itemView : Views.ItemView,
      itemViewContainer : '#todo-list',

      ui : {
        toggle : '#toggle-all'
      },

      events : {
        'click #toggle-all' : 'onToggleAllClick'
      },

      initialize : function() {
        this.bindTo(this.collection, 'all', this.update, this);
      },

      onRender : function() {
        this.update();
      },

      update : function() {
        function reduceCompleted(left, right) { return left && right.get('completed'); }
        var allCompleted = this.collection.reduce(reduceCompleted,true);
        this.ui.toggle.prop('checked', allCompleted);

        if (this.collection.length === 0) {
          this.$el.parent().hide();
        } else {
          this.$el.parent().show();
        }
      },

      onToggleAllClick : function(evt) {
        var isChecked = evt.currentTarget.checked;
        this.collection.each(function(todo){
          todo.save({'completed': isChecked});
        });
      }
  });

  // 어플리케이션 이벤트 처리자
  // --------------------------
  //
  // 다양한 CSS 클래스들의 사용을 통해 보여주고 숨기는 것으로
  // 항목의 목록 필터링을 처리한다.
  
  App.vent.on('todoList:filter',function(filter) {
    filter = filter || 'all';
    $('#todoapp').attr('class', 'filter-' + filter);
  });

});

```

마지막 코드블럭의 끝에, `vent`를 사용하는 이벤트 처리자도 알아볼것이다. 이것은 TodoList 컨트롤러에서 구동된 `filterItem`을 처리하게 해주는 이벤트 수집자이다.

마지막으로, 우리는 할일 항목을 표현하는 모델과 컬렉션을 정의한다. 의미적으로 첫번째 연습에서 사용한 원래 버젼과 크게 다르지 않고 Derick이 선호하는 코딩 스타일에 더 잘 맞게 재작성되었다.

**Todos.js:**

```javascript
TodoMVC.module('Todos', function(Todos, App, Backbone, Marionette, $, _){

  // 할일 모델
  // ----------
  
  Todos.Todo = Backbone.Model.extend({
    localStorage: new Backbone.LocalStorage('todos-backbone'),

    defaults: {
      title     : '',
      completed : false,
      created   : 0
    },

    initialize : function() {
      if (this.isNew()) this.set('created', Date.now());
    },

    toggle  : function() {
      return this.set('completed', !this.isCompleted());
    },

    isCompleted: function() { 
      return this.get('completed'); 
    }
  });

  // 할일 컬렉션
  // ---------------

  Todos.TodoList = Backbone.Collection.extend({
    model: Todos.Todo,

    localStorage: new Backbone.LocalStorage('todos-backbone'),

    getCompleted: function() {
      return this.filter(this._isCompleted);
    },

    getActive: function() {
      return this.reject(this._isCompleted);
    },

    comparator: function( todo ) {
      return todo.get('created');
    },

    _isCompleted: function(todo){
      return todo.isCompleted();
    }
  });

});

```

우리는 결국 주 어플리케이션 객체의 `start`를 호출함으로써 어플리케이션 index 파일의 모든 것을 시작한다:

Initialisation:

```javascript
      $(function(){
        // ( js/TodoMVC.js에 정의된 ) TodoMVC를 시작한다.
        TodoMVC.start();
      });
```

다 끝났다!

### 할일 앱의 마리오네트 구현이 더 유지보수하기 좋은가?

Derick은 유지보수성은 모듈화와 관심분리( SRP와 SoC ), 그리고 관심이 서로 섞이지 않도록 하는 또다른 연관 패턴으로 이어진다고 생각한다. 그러나, 개념을 추출해서 추상화하고 나누기 위해 모듈을 가장 작은 조각으로 나누기 위해서 단순히 개념을 추출하는 것은 어려울 수 있다.

단일 책임 이론(SRP)은 완전히 반대로 말한다. - 상황이 바뀌는 문맥에서 이해할 필요가 있다. _이_ 시스템에서 어떤 부분이 항상 같이 바뀌는가? 어느 부분이 독립적으로 바뀔 수 있는가? 이것을 모르고는, 컴포넌트와 모듈을 분리하는 것과 동일 모듈이나 객체에 함께 담는 것 사이의 고민으로 어느 부분이 떼어내어져야하는지 할지 못한디ㅏ.

Derick이 앱을 모듈로 구성한 방법은 각 레벨에서 개념의 명세를 만드는 것이었다. 상위의 모듈은 책임을 모으는 것같은 상위의 관심이다. 각 책임은 하위 모듈에 의해 구현되는 노출되는 API 묶음으로 쪼개진다( Dependency Inversion Principle ). 이것들은 중개자를 통해 결합된다 - 중개자는 일반적으로 모듈에서 컨트롤러로 취급된다.

Derick이 파일을 구성한 방법도 유지보수성에 직접 영향을 주었고, 올바른 어플리케이션 폴더 구조를 유지하는 것의 중요성에 대한 글( 읽어보길 추천한다 )도 썼다:

* [http://lostechies.com/derickbailey/2012/02/02/javascript-file-folder-structures-just-pick-one/](http://lostechies.com/derickbailey/2012/02/02/javascript-file-folder-structures-just-pick-one/)
* [http://hilojs.codeplex.com/discussions/362875#post869640](http://hilojs.codeplex.com/discussions/362875#post869640)

### 마리오네트와 유연성

마리오네트는 Backbone과 매우 유사하게 유연성있는 프레임워크이다. 그것은 Backbone위에서 어플리케이션 구조를 생성하고 구성하는데 도움을 주는 다양한 도구를 제공하지만, Backbone과 같이, 당신이 어느 하나를 쓰기 위해 전체를 다 도입하도록 강요하지 않는다.

마리오네트의 유연성과 다기능성은 비교를 목적으로 만든 TodoVMC의 세가지 버젼을 살펴봄으로써 매우 이해하기 쉽다:

* [Simple](https://github.com/jsoverson/todomvc/tree/master/labs/architecture-examples/backbone_marionette) - Jarrod Oversion이 작성
* [RequireJS](https://github.com/jsoverson/todomvc/tree/master/labs/dependency-examples/backbone_marionette_require) - Jarrod가 또 작성
* [Marionette modules](https://github.com/derickbailey/todomvc/tree/master/labs/architecture-examples/backbone_marionette_modules/js) - Derick Bailey이 작성

**The simple version**: 이버젼은 마리오네트의 다양한 뷰 종류와 어플리케이션 객체와 이벤트 수집자들의 직접적이 사용을 보여준다. 전역 이름공간에 직접 생성되고 추가된 객체들은 꽤 단순하다. 이것은 어떻게 마리오네트로 모든 것을 재작성할 필요없이 이미 있는 코드를 증대하는데 사용할 수 있는지에 대한 좋은 예이다.

**The RequireJS version**: RequireJS와 마리오네트를 함께 사용하는 것은 모듈화( 자바스크립트 어플리케이션을 확장하는데 매우 중요한 개념 )된 어플리케이션 구조를 만드는데 도움을 준다. RequireJS는 마리오네트를 기존보다 더 유연하게 만들어 주면서 큰 이득을 줄 수 있는 강력한 도구들을 제공한다.

**The Marionette module version**: 그러나 RequireJS가 모듈화된 어플리케이션 구조를 만드는 유일한 방법은 아니다. 모듈과 이름공간에 어플리케이션을 만들고 싶하는 사람들을 위해 마리오네트는 내장된 모듈 및 이름공간 구조를 제공한다. 이 예제 어플리케이션은 어플리케이션의 단순한 버젼을 가져다가 모든 조각을 함께 가지고 있는 어플리케이션 컨트롤러( 중개자 / 흐름 객체 )를 사용해서 이름공간화된 어플리케이션으로 재작성하였다.

마리오네트는 확실히 Backbone 어플리케이션이 어떻게 설계되어야 하는지에 대한 공통적인 대안을 제공한다. 모듈, 뷰 타입, 이벤트 수집자, 어플리케이션 객체 등등의 조합은 이 대안에 기초해서 매우 강력하고 유연한 구조를 만드는데 사용될 수 있다.

하지만, 알다시피 마리오네트는 완전히 견고한( 독자적이거나 최선의 ) 프레임워크는 아니다. 그것은 AMD나 이름공간과 같은 다른 구조적인 스타일과 섞거나 맞출 수 있는 어플리케이션 기반의 많은 요소를 제공하거나 뷰를 렌더링하는 보일러플레이트 코드를 줄임으로써 이미 있는 프로젝트에 단순한 인자화를 제공한다.

어플리케이션의 필요에 따라 마리오네트의 사용정도를 조절할 수 있기 때문에, 이 유연성은 마리오네트가 당신과 당신의 프로젝트에 가치를 창출할 더 많은 기회를 만들어낸다.

### 그외

이것은 단지 마리오네트의 빙산의 일각일 뿐이다 - 심지어 우리가 살펴본 `ItemView`와 `Region`에 대해서도. 이런 객체들 모두에 사용할 수 있는 너무 많은 기능과 특성, 유연성과 변형이 있다. 이제 우리는 마리오네트가 현행화와 확장점등을 제공하는 수십개의 컴포넌트를 가지고 있다 - 그 컴포넌트는 내부에 스스로의 동작을 가지고 있다.

마리오네트와 그 컴포넌트, 그것들이 제공하는 특성과 사용법을 더 배우기 위해서 마리오네트 문서, 위키, 소스코드, 프레젝트 핵심 기여자 등등을 [http://marionettejs.com](http://marionettejs.com)에서 확인해라.


<p>&nbsp;</p>
<p>&nbsp;</p>



## Thorax

*Ryan Eastridge와 Addy Osmani가 만듬*

Backbone의 매력 중에 한 부분은 뷰 쪽을 보면 특히 독단적이지 않은 구조를 보통 제공한다는 것이다. Thorax는 템플릿 기능으로 Handlebars를 사용하도록 독단적인 결정을 한다. 마리오네트에서 본 몇가지 패턴이 Thorax에서도 보인다. 마리오네트는 그 패턴 대부분은 자바스크립트 API로 노출하는 반면, Thorax에서는 템플릿 헬퍼로 종종 노출된다. 이 챕터는 독자가 Handlebars에 대해 알고 있다고 가정한다.

Thorax는 월마트의 모바일 웹 어플리케이션을 만들기 위해 Ryan Eastridge와 Kevin Decker에 의해 만들어졌다. 이 챕터는 Thorax를 채택하든 말든 상관없이 어플리케이션에서 도움이 될 Thorax의 템플릿 특성과 구현된 패턴에 국한할 것이다. Thorax에서 구현된 다른 특징을 더 알고, 보일러플레이트 프로젝트를 다운로드하고 싶다면 [Thorax website](http://walmartlabs.github.com/thorax)를 방문해라.

### Hello World

`Thorax.View`는 `options` 객체가 없다는 점에서 `Backbone.View`와 다른다. 생성자에 전달된 모든 인자는 뷰의 특성이 되고, `template`에서 사용할 수 있게 된다:

```javascript
    var view = new Thorax.View({
        greeting: 'Hello',
        template: '{{greeting}} World!'
    });
    view.render();
    $('body').append(view.el);
```

이 챕터의 대부분의 예제에서 `template` 특성이 지정될 것이다. 보일러플레이트를 포함하는 큰 프로젝트는 Thorax 웹사이트상에서 `name` 특성이 대신 사용되고, 프로젝트상의 동일한 파일 이름의 `템플릿`이 자동적으로 뷰에 할당될 것이다.

`model`이 뷰에 설정되면, 그 속성도 템플릿에서 사용할 수 있게 된다:

    var view = new Thorax.View({
        model: new Thorax.Model({key: 'value'}),
        template: '{{key}}'
    });

### 내부 자식 뷰

뷰 헬퍼는 뷰안에 다른 뷰를 넣도록 해준다. 자식 뷰는 뷰의 특성으로 지정될 수 있다:

```javascript
    var parent = new Thorax.View({
        child: new Thorax.View(...),
        template: '{{view child}}'
    });
```

아니면 초기화하는 자식 뷰의 이름을 지정할 수도 있다( 전달할 어떤 선택적인 특성도 같이 지정할 수 있다 ). 이 경우에 자식 뷰는 `extend`와 `name` 특성으로 미리 생성되어야만 한다:

```javascript
    var ChildView = Thorax.View.extend({
        name: 'child',
        template: ...
    });
  
    var parent = new Thorax.View({
        template: '{{view "child" key="value"}}'
    });
```

뷰 헬퍼는 블럭 헬퍼로 사용되기도 한다. 블럭 헬퍼는 블럭이 자식 뷰의 `template` 특성에 할당되는 경우이다:

```handlebars
    {{#view child}}
        child will have this block
        set as it's template property
    {{/view}}
```

`Backbone.View` 객체가 DOM `el`을 갖는 반면, Handlebars는 문자열 기본이다. 우리가 구체적인 내용을 섞어 보자면 다음과 같이 뷰를 내장하는 것은 `뷰` 헬퍼가 전달된 뷰를 `children` 해쉬에 추가하고 나서 플레이스홀더 HTML을 템플릿으로 집어넣는 플레이스홀더 구조로 동작한다:

```html
    <div data-view-placeholder-cid="view2"></div>
```

부모 뷰가 렌더링되면, 우리가 생성한 모든 플레이스홀더 검색과 자식 뷰의 `el` 교체를 위해 DOM을 뒤진다:

```javascript
    this.$el.find('[data-view-placeholder-cid]').forEach(function(el) {
        var cid = el.getAttribute('data-view-placeholder-cid'),
            view = this.children[cid];
        view.render();
        $(el).replaceWith(view.el);
    }, this);
```

### 뷰 헬퍼

Thorax에서 가장 유용한 것중에 하나는 `Handlebars.registerViewHelper`이다 ( `Handlebars.registerHelper`와는 다르다). 이 메쏘드는 생성할 블럭 헬퍼와 블럭이 설정된 `template`을 가진 내장된 `HelperView` 객체를 등록한다. `HelperView` 객체는 템플릿내에서 부모의 컨택스트를 가진다는 점에서 보통의 자식 뷰 객체와 다르다. 다른 자식 뷰들과 똑같이 선언하는 뷰 객체를 설정하는 `parent` 특성을 가지고 있다. `collection` 헬퍼를 포함해서 Thorax의 많은 내장 헬퍼들이 이런 방식으로 만들어져 있다.

간단한 예는 부모 뷰에 선언된 이벤트가 구동될 때마다 생성된 `HelperView` 객체를 다시 렌더링하는 `on` 헬퍼일 것이다:

    Handlebars.registerViewHelper('on', function(eventName, helperView) {
        helperView.parent.on(eventName, function() {
            helperView.render();
        });
    });

이 사용예는 버튼이 클릭될 때마다 각 횟수를 증가하는 카운터이다. 이 예제는 클릭될 때 메쏘드를 호출하는 버튼을 쉽게 만들어주는 Thorax의 `button` 헬퍼를 사용하였다:

```handlebars
    {{#on "incrimented"}}{{i}}{/on}}
    {{#button trigger="incrimented"}}Add{{/button}}
```

그리고 대응하는 뷰 클래스:

```javascript
    new Thorax.View({
        events: {
            incrimented: function() {
                ++this.i;
            }
        },
        initialize: function() {
            this.i = 0;
        },
        template: ...
    });
```

### 컬렉션 헬퍼

`collection` 헬퍼는 컬렉션의 각 항목에 대해서 뷰를 생성하고 항목이 추가되거나 삭제되거나 변경될 때 갱신하는 `CollectionView` 객체를 생성하고 내장한다:

```handlebars
    {{#collection kittens}}
      <li>{{name}}</li>
    {{/collection}}
```

그리고 대응하는 뷰:

```javascript
    new Thorax.View({
      kittens: new Thorax.Collection(...),
      template: ...
    });
```

이 경우에 블럭은 생성된 각 항목뷰에 대한 `template`으로 할당되고 컨택스트는 주어진 모델의 `attributes`가 될 것이다. 이 헬퍼는 임의의 HTML 속성이 될 수 있는 컬렉션을 포함하는 태그의 타입을 지정하는 `tag`나 다음 하나를 설정한다:

- `item-template` - 각 모델을 보여주는 템플릿. 블럭이 지정되면, item-template이 될 것이다
- `item-view` - 각 항목 뷰가 생성될 때 사용하는 뷰 클래스
- `empty-template` - 컬렉션이 비어있을 때 보여주는 템플릿. inverse나 else 블럭이 지정되면 empty-template이 될 것이다
- `empty-view` - 컬렉션이 비어있을 때 보여줄 뷰

설정과 블럭은 조함해서 사용할 수 있다. 이 경우, 컬렉션의 각 고양이에 대한 블럭을 `template`에 설정한 `KittenView` 클래스를 만들었다:

```handlebars
    {{#collection kittens item-view="KittenView" tag="ul"}}
      <li>{{name}}</li>
    {{else}}
      <li>No kittens!</li>
    {{/collection}}
```

뷰마다 여러개의 컬렉션이 사용될 수 있고 컬렉션이 중첩될 수 있다는 것을 기억해라. 이겄은 컬렉션을 담는 모델을 담는 컬렉션을 담고 있는 모델... 이 있을 때 유용하다.

```handlebars
    {{#collection kittens}}
      <h2>{{name}}</h2>
      <p>Kills:</p>
      {{#collection miceKilled tag="ul"}}
        <li>{{name}}</li>
      {{/collection}}
    {{/collection}}
```

### 사용자정의 HTML 데이타 속성

Thorax는 동작에 자용자정의 데이타 속성을 잘 사용한다. 어떤 것들은 Thorax에게만 유효한 반면, 어떤 것들은 일반적인 디버깅을 위한 함수를 만드는 어떤 Backbone 프로젝트에서도 꽤 유용하다. Thorax를 사용하지 않는 프로젝트에서 어떤 뷰를 추가하기 위해서, 기본 뷰 클래스에 `setElement` 메쏘드를 덮어써라:

```javascript
  MyApplication.View = Backbone.View.extend({
    setElement: function() {
        var response = Backbone.View.prototype.setElement.apply(this, arguments);
        this.name && this.$el.attr('data-view-name', this.name);
        this.$el.attr('data-view-cid', this.cid);
        this.collection && this.$el.attr('data-collection-cid', this.collection.cid);
        this.model && this.$el.attr('data-model-cid', this.model.cid);
        return response;
    }
  });
```

인스펙터 상에서 어플리케이션을 좀 더 즉각적으로 이해할 수 있도록 하는 것 이상으로 주어진 요소에 대한 닫히 뷰, 모델, 컬렉션을 찾는 함수로 jQuery나 Zepto를 확장할 수 있다. 잘 동작하게 만들기 위해서, `_configure` 메쏘드를 덮어써서 본인의 기본 뷰에서 생성된 각 뷰의 참조를 저장해라:

```javascript
    MyApplication.View = Backbone.View.extend({
        _configure: function() {
            Backbone.View.prototype._configure.apply(this, arguments);
            Thorax._viewsIndexedByCid[this.cid] = cid;
        },
        dispose: function() {
            Backbone.View.prototype.dispose.apply(this, arguments);
            delete Thorax._viewsIndexedByCid[this.cid];
        }
    });
```

그리고 나서 jQuery나 Zepto를 확장할 수 있다:

```javascript
    $.fn.view = function() {
        var el = $(this).closest('[data-view-cid]');
        return el && Thorax._viewsIndexedByCid[el.attr('data-view-cid')];
    };

    $.fn.model = function(view) {
        var $this = $(this),
            modelElement = $this.closest('[data-model-cid]'),
            modelCid = modelElement && modelElement.attr('[data-model-cid]');
        if (modelCid) {
            var view = $this.view();
            return view && view.model;
        }
        return false;
    };
```

어플리케이션에서 무작위로 찾기 위해서 모델의 참조를 저장하는 대신에 이제 주어진 DOM 이벤트가 발생할 때, `$(element).model()`를 사용할 수 있다. Thorax에서는 컬렉션내의 각 `모델`에 대한 뷰 클래스를 ( `model` 특성을 이용해서 ) 생성하는 `collection` 헬퍼와 결합해서 특히 유용하게 사용될 수 있다. 예제 템플릿:

```handlebars
    {{#collection kittens tag="ul"}}
      <li>{{name}}</li>
    {{/collection}}
```

그리고 대응되는 뷰 클래스:

```javascript
    Thorax.View.extend({
      events: {
        'click li': function(event) {
          var kitten = $(event.target).model();
          console.log('Clicked on ' + kitten.get('name'));
        }
      },
      kittens: new Thorax.Collection(...),
      template: ...
    });  
```

Backbone 어플리케이션에서 일반적인 안티 패턴은 단일 뷰 클래스에 'className'을 할당하는 것이다. 여러번 사용될 것에 대해서 CSS 클래스를 줄이고 CSS 선택자 대신에 'data-view-name' 속성을 사용하는 것을 고려해봐라.

```css
  [data-view-name="child"] {

  }
```

### Thorax 자원

Backbone관련된 안내서가 할일 어플리케이션없이 완성되지 않았다. 이 단일 Handlebars 템플릿으로 작성된 아주 단순한 예제뿐만 아니라 [TodoMVC에 대한 Thorax 구현](http://todomvc.com/labs/architecture-examples/thorax/)이 이용 가능하다:

```handlebars
  {{#collection todos tag="ul"}}
    <li{{#if done}} class="done"{{/if}}>
      <input type="checkbox" name="done"{{#if done}} checked="checked"{{/if}}>
      <span>{{item}}</span>
    </li>
  {{/collection}}
  <form>
    <input type="text">
    <input type="submit" value="Add">
  </form>
```

그리고 대응되는 자바스크립트:

```javascript
  var todosView = Thorax.View({
      todos: new Thorax.Collection(),
      events: {
          'change input[type="checkbox"]': function(event) {
              var target = $(event.target);
              target.model().set({done: !!target.attr('checked')});
          },
          'submit form': function(event) {
              event.preventDefault();
              var input = this.$('input[type="text"]');
              this.todos.add({item: input.val()});
              input.val('');
          }
      },
      template: '...'
  });
  todosView.render();
  $('body').append(todosView.el);
```

대형 사이트에서 Thorax의 동작을 보기 위해서는 안드로이드나 iOS 장치로 walmart.com를 방문해라. 자원들을 완전한 목록을 보고 싶으면 [Thorax website](http://walmartlabs.github.com/thorax)를 방문해라.
<p>&nbsp;</p>
<p>&nbsp;</p>

# 모듈화된 개발


## 소개

우리가 어플리케이션이 모듈화되어있다고 할때는 보통은 어플리케이션이 모듈들 안에 매우 독립적이고 구분되는 기능 조각들로 구성되었음을 의미한다. 알다시피, 결합도를 낮추는 것은 가능한 의족성을 제거함으로써 앱의 더 쉬운 유지보수성을 제공한다. 모듈화가 효과적으로 구현될 때, 시스템의 일부의 변화가 다른 곳에 어떻게 영향을 주는지 알기 쉽다.

그러나 다른 전통적인 프로그래밍 언어와 달리, 현자 자바스크립트 버젼은 개발자에게 깔끔하고 조직화된 방식으로 모듈을 가져오는 방법을 제공하지 않는다. 그것은 더 복잡한 자바스크립트 어플리케이션에 대한 필요가 나타난 최근 몇년까지는 큰 고민이 필요하지 않았던 명세사항중 하나였다.

대신 현재의 개발자들은 모듈이나 객체 상수 패턴의 변형을 다시 가져다 쓰곤한다. 이걸들 대부분으로 모듈 스크립트들은 단일 전역 객체로 표현되는 이름공간으로 DOM에 묶인다. 그것은 당신의 설계 구조상에서 이름 충돌을 야기할 가능성이 있다. 직접적인 노력이나 다른 툴없이 의존성 관리를 제어할 깔끔한 방법도 없다.

이문제에 대한 근본적인 해결책이 ES Harmony에 도달할 때까지, 좋은 소식은 모듈화된 자바스크립트 작성은 결코 쉬워지지도 않았지만, 오늘날 당신은 그것을 할 수 있다.

책의 다음 부분에서 우리는 어플리케이션의 코드 조각들을 관리가능한 모듈로 깔끔하게 감싸기 위한 AMD 모듈들과 RequireJS를 사용하는 방법과 언제 모듈이 로드되는지를 결정하기 위해 경로를 사용하는 또 다른 방법을 볼 것이다.

## RequireJS와 AMD를 사용하여 모듈 구성하기

당신이 전에 사용한 적이 없다면, [RequireJS](http://requirejs.org)는 James Burke에 의해 작성된 유명한 스크립트 로더이다. 그는 나중에 잠깐 다룰 AMD 모듈의 형태를 구성하는데 도와준 유능한 개발지이다. RequireJS의 기능은 여러 스크립트 파일을 로드하고, 의존성을 가진 모듈을 정의하고, 텍스트 파일과 같은 스크립트가 아닌 의존성으로 로드하는 것이다.

그래서 왜 Backbone과 함께 RequireJS를 쓰는가? Backbone이 어플리케이션에 깔끔한 구조를 제공는데 뛰어지나지만, 몇가지 추가적인 도움이 있을 수 있는 곳에서 몇가지 중요한 점이 있다:

1) Backbone은 모듈화된 개발에 특별한 방법을 지지하지 않는다. 앱을 구조화하는데 모듈 패턴과 객체 상수같은( 둘다 잘 동작한다 ) 고전적인 패턴을 선택하는 개발자에게 제한이 없음을 의미하지만, 그것은 또한 개발자가 의존성 관리와 같은 다른 관심이 생길때, 가장 좋은 동작이 무엇인지 확신하지 못한다는 것을 의미한다.

RequireJS는 AMD (Asynchronous Module Definition) 포맷과 호환성이 있다. 그 포맷은 '암묵적으로 의존성을 갖는 스크립트 태그를 작성하고 그것을 수동으로 관리'하는 개발 방법보다 더 나은 방식으로 개발하려는 바램에서 시작하였다. AMD는 당신이 깔끔하게 의존성을 선언하도록 해줄 뿐만 아니라 브라우져에서도 잘 돌아가고, 같은 파일의 다수의 모듈을 정의했을 때 의존성을 위한 문자열 아이디도 지원하고, 전역 이름공간을 오염시키지 않는 사용하기 쉬운 도구도 제공한다.

2) 직접 의존성 관리를 한다면 잘 하는 것도 실제로는 꽤 힘든 일이기 때문에 의존성 관리에 대해서 조금더 논의해 보자. 우리가 자바스크립트로 모듈을 작성할 때, 이상적으로는 코드 단위를 지능적으로 재사용할 수 있길 원하고 때로는 보통 때는 어플리케이션을 처음 시작할 때 큰 로딩 비용을 피하기 위해서 동적으로 동작하는 반면, 런타임에는 다른 모듈을 가져오는 것을 의미한다.

잠깐동안 GMail 웹 클라이언트를 생각해봐라. 사용자가 처음에 페이지를 로드할 때, 구글은 사용자가 사용하고 싶다고 ( 'expand'를 클릭해서 ) 명령하기 전까지 채팅 모듈같은 위젯을 숨긴다. 그리고나서 구글은 페이지가 초기화될 때 모든 사용자가 로드하지 않고 동적 의존성 로드를 통해 단지 채팅 모듈만 로드하게 된다. 이 방법은 실행 속도와 로딩 시간을 개선할 수 있고, 큰 어플리케이션을 개발할 때 유용하다는 것을 확실히 증명할 수 이다.

당신이 이 주제를 더 알고 싶은 경우를 위해 나는 전에 AMD와 다른 모듈 포맷과 스크립트 로더를 다루는 [상세한 기사](http://addyosmani.com/writing-modular-js)를 썼었다. 남은 것은 적합한 스크립트로더와 깔끔한 모듈 형태없이 어플리케이션을 개발하는 것은 완변하게 좋을지라도 어플리케이션 개발에 이런 도구를 사용하는 것을 고련하는 것이 큰 이득이 될 수도 있다는 것이다.

### RequireJS으로 AMD 모듈 작성하기

위에서 논의한 대로, AMD 포맷의 전체 목표는 오늘날의 개발자가 사용할 수 있는 모듈화된 자바스크립트를 위한 해결책을 제공하는 것이다. 스크립트 로더로 모듈을 사용할 때 알아두어야하는 두개의 주요 개념은 모듈 정의를 도와주는 `define()` 메쏘드와 의존성 로드를 제어하는 `require()` 메쏘드이다. `define()`은 명세에 따라 다음 메쏘드 서명을 사용해서 이름이 있는 모듈이나 없는 모듈을 정의하는데 사용된다:

```javascript
define(
    module_id /*optional*/,
    [dependencies] /*optional*/,
    definition function /*모듈이나 객체를 생성하는 함수*/
);
```

소스내의 주석으로 보았다 시피, `module_id`는 AMD가 아닌 결합 도구가 사용될 때( 유용한 상황에서 몇가지 다른 예가 있기다 하다 )만 필요한 선택적인 인자이다. 이 인자가 비어있을 때, 우리는 모듈이 '익명'으로 부른다. 익명 모듈로 동작할 때, 모듈의 구분자 개념은 DRY해야 한다. 그것은 파일 이름과 코드의 중복을 피하는 것이 당연하게 해준다.

메쏘드 성명으로 돌아가서, 의존성 인자는 정의한 모듈에서 필요로하는 의존성의 배열을 포현하고, 세번째인자( 'definition function' )은 모듈을 생성하기 위해 실행하는 함수이다. ( RequireJS와 호환되는 ) barebone 모듈은 `define()`를 사용해서 아래와 같이 정의될 수 있다:

```javascript
// 모듈 아이디를 생략해서 모듈을 익명으로 만들어졌다.

define(['foo', 'bar'],
    // 모듈 정의 함수
    // 의존성(foo와 bar)은 함수 파라미터로 맵핑된다.
    function ( foo, bar ) {
        // 모듈을 내보내기ㅇ 위해 정의한 값을 반환한다
        // ( 즉 우리가 사용하는 쪽에 노출하고 싶어하는 기능 )

        // 여기에서 모듈을 생성한다.
        var myModule = {
            doStuff:function(){
                console.log('Yay! Stuff');
            }
        }

        return myModule;
});
```

#### 또다른 사용법
의존성을 `require()`을 사용해서 의존성을 지역 변수로 선언하게 해주는 `define()`의 [편리한 버젼](http://requirejs.org/docs/whyamd.html#sugar) 도 있다. 이것은 노드를 사용했었던 사람에게 친근하게 느껴진다. 그것은 의존성을 추가하거나 제거하는데 더 쉽다.
이전 코드 예제에 대한 또다른 문법이 여기있다:

```javascript
// 모듈 아이디를 생략해서 모듈을 익명으로 만들어졌다.

define(function(require){
    // 모듈 정의 함수
    // 의존성(foo와 bar)은 함수 파라미터로 맵핑된다.
    var foo = require('foo'),
        bar = require('bar');

        // 모듈을 내보내기ㅇ 위해 정의한 값을 반환한다
        // ( 즉 우리가 사용하는 쪽에 노출하고 싶어하는 기능 )

        // 여기에서 모듈을 생성한다.
        var myModule = {
            doStuff:function(){
                console.log('Yay! Stuff');
            }
        }

        return myModule;
});
```

`require()` 메쏘드는 일반적으로 최상위 자바스크립트 파일이나 모듈에서 코드를 로드하는데 사용된다. 사용예는 다음과 같다:

```javascript
// 'foo'와 'bar'는 두 개의 외부 모듈이라고 생각하자.
// 이 예제에서 두개 모듈에서 로드된 'exports'가
// 함수의 인자로 콜백에 ( foo와 bar) 전달되어서
// 유사하게 접근될 수 있다.

require(['foo', 'bar'], function ( foo, bar ) {
        // 기타 코드
        foo.doSomething();
});
```


**AMD로 모듈, 뷰 그리고 다른 컴포넌트 감싸기**

우리가 AMD 모듈들을 어떻게 정의하는지 보았으니, 뷰와 컬렉션같은 컴포넌트가 필요한 어플리케이션의 어떤 부분에 대한 의존성으로 쉽게 로드할 수 있게 하기 위해, 그것들을 감싸는 방법에 대해 살펴보자. 정말 단순하게 Backbone 모델은 단지 Backbone과 Underscore.js를 필요로한다. 이것들을 그 의존성으로 고려하고, AMD 모델 모듈을 작성하기 위해 우리는 단순히 다음과 같이 했다:

```javascript
define(['underscore', 'backbone'], function(_, Backbone) {
  var myModel = Backbone.Model.extend({

    // 기본 속성
    defaults: {
      content: 'hello world',
    },

    // 빈 초기화 메쏘드
    initialize: function() {
    },

    clear: function() {
      this.destroy();
      this.view.remove();
    }

  });
  return myModel;
});
```

우리가 AMD이 아닌 코드를 이 모듈 포맷을 써서 바꾸는 것은 매우 당연하게 만들면서 어떻게 Underscore.js의 객체를 `_`로, Backbone을 `Backbone`으로 매핑했는지 보아라. jQuery와 같은 다른 의존성을 필요로 하는 뷰에 대해서, 이것은 다음과 같이 유사하게 된다:

```javascript
define([
  'jquery',
  'underscore',
  'backbone',
  'collections/mycollection',
  'views/myview'
  ], function($, _, Backbone, myCollection, myView){

  var AppView = Backbone.View.extend({
  ...
```

달라 표시( `$` )로 축약했기 때문에, AMD를 사용해서 원하는 어플리케이션의 부분을 감추는 것을 매우 쉽게 해준다.


## RequireJS와 텍스트 플러그인을 사용해서 템플릿을 외부에 두기

[Underscore/Mustache/Handlebars] 템플릿을 외부 파일로 옮기는 것은 실제로 꽤 쉽다. 이 어플리케이션이 RequireJS를 사용하기 때문에, 특정 스크립트 로더를 사용해서 외부 템플릿을 구현하는 방법에 대해서만 논의할 것이다.

RequireJS는 텍스트 파일 의존성으로 로드하는데 사용하는 text.js라 불리는 플러그인이 있다. text 플러그인을 사용하기 위해, 다음의 간단한 단계를 따라라:

1. http://requirejs.org/docs/download.html#text 에서 플러그인을 다운로드해서 어플리케이션의 주 JS파일과 같은 디렉토리나 적당한 하위 디렉토리에 놓아라.

2. 다음으로, text.js 플러그인을 초기 RequireJS 설정 옵션에 포함시켜라. 아래 예제 코드에서, 우리는 RequireJS는 이 코드 예제가 실행되기 이전에 페이지 안에 포함되었다고 가정한다. 로드된 다른 스크립트들은 예제를 위해 그냥 놓아두었다.

```javascript
require.config( {
    paths: {
        'backbone':         'libs/AMDbackbone-0.5.3',
        'underscore':       'libs/underscore-1.2.2',
        'text':             'libs/require/text',
        'jquery':           'libs/jQuery-1.7.1',
        'json2':            'libs/json2',
        'datepicker':       'libs/jQuery.ui.datepicker',
        'datepickermobile': 'libs/jquery.ui.datepicker.mobile',
        'jquerymobile':     'libs/jquery.mobile-1.0'
    },
    baseUrl: 'app'
} );
```

3. `text!` 접두어가 의존성을 위해 사용될 때, RequireJS는 자동적으로 텍스트 플러그인을 로드해서 의존성을 텍스트 자원으로 다룰 것이다. 이것에 대한 전형적인 예제 동작은 다음과 같이 보일 것이다..

```javascript
require(['js/app', 'text!templates/mainView.html'],
    function(app, mainView){
        // mainView 파일에 대한 내용은
		// 사용을 위해 mainView로 로드된다.
    }
);
```

4. 마지막으로 우리는 템플릿을 목적으로 로드된 텍스트 자원을 사용할 수 있다. 당신은 아마 어떤 구분자로 스크립트를 사용해서 HTML 템플릿 코드를 저장하는데 사용할 것이다.

Underscore.js의 마이크로 템플릿(과 jQuery)으로 보통은 다음과 같을 것이다:

HTML:

	<script type="text/template" id="mainViewTemplate">
	    <% _.each( person, function( person_item ){ %>
	        <li><%= person_item.get('name') %></li>
	    <% }); %>
	</script>


JS:

```javascript
var compiled_template = _.template( $('#mainViewTemplate').html() );
```

그러나 RequireJS와 텍스트 플러그인으로, 사용하는 것은 템플릿을 외부 텍스트 파일( 말하자면 `mainView.html` )로 저장하는 것만큼 쉽고 다음과 같다:

```javascript
require(['js/app', 'text!templates/mainView.html'],
    function(app, mainView){

        var compiled_template = _.template( mainView );
    }
);
```

이게 다이다! 이제 당신은 Backbone에서 다음과 같이 템플릿을 뷰에 적용할 수 있다:

```javascript
collection.someview.$el.html( compiled_template( { results: collection.models } ) );
```


모든 템플릿 솔루션은 템플릿 컴파일을 위한 자신만의 메쏘드를 가질 것이지만, 당신이 위의 내용을 이해한다면 Underscore의 마이크로 템플릿팅을 다른 솔루션으로 바꾸는 것은 매우 사소한 것이다.

**주의:** 당신은 [RequireJS tpl](https://github.com/ZeeAgency/requirejs-tpl)을 보고 싶을 수도 있다. 그것은 더 나은 성능과 eval연산이 없는 최적화( 미리 컴파일된 템플릿 )된 Underscore 템플릿팅 시스템의 AMD 호환 버젼이다. 나는 아직 써보지 않아지만, 그것은 추천할 만한 것으로 여겨진다.


## RequireJS 최적화기로 제품화를 위해 Backbone 앱 최적화하기

숙련된 개발자라면 알겠지만, 크고 작은 자바스크립트 웹 어플리케이션을 작성할 때 중요한 마지막 과정은 빌드 과정이다. 대다수 단일 페이지 앱은 한두개 이상의 스크립트로 구성되기 때문에 제품화하기 앞서 스크립트의 최적화, 압축, 파일 결합 과정은 사용자가 더 적은 수의 스크립트 파일을 다운로드하도록 할 것이다.

메모: 이전에 빌드 과정을 본 적이 없고 이번이 처음 듣는 것이면, [이 주제에 대한 내 글과 스크린 샷](http://addyosmani.com/blog/client-side-build-process/)이 유용할 것이다.

다른 구조적인 자바스크립트 프레임워크로 내가 추천하는 것은 보통 YUI 압축기나 구글의 클로져 컴파일러 툴을 사용하는 것이지만 당신이 RequireJS를 사용중이면, 그것이 Backbone과 결합할 때 사용가능한 조금더 우아한 방법이 있다. RequireJS는 다음 기능을 포함해서 많은 기능을 가진 r.js라고 하는 커멘드 라인 최적화기를 가지고 있다:

* 동적 모듈 로드 기능을 유지하면서 특정 스크립트들을 결합하고 최적화된 브라우져 전달을 위해 UglifyJS( 기본으로 사용된다 )와 구글의 클로져 컴파일러같은 외부툴을 사용해서 압출할 수 있다.
* @import를 사용해 가져온 CSS 파일들을 파일내에 내장하고 주석을 제거하여 CSS와 스타일시트를 최적화한다.
* 노드와 라이노( 나중에 더 설명할 것이다. )를 사용하여 AMD 프로젝트를 실행할 수 있다.

첫번째 동그라미 문장에서 '특정' 이라는 단어를 언급했다는 것을 알아차릴 것이다. RequireJS 최적화기는 오직 최상위( 하위는 제외 ) require와 define 호출에 전달된 문자 상수의 배열로 지정된 모듈 스크립트들만 결합한다. [최적화기 문서](http://requirejs.org/docs/optimization.html)에서 명확히 밝혔다시피 이것은 Backbone 모듈들이 다음과 같이 정의되는 것을 의미한다:

```javascript
define(['jquery','backbone','underscore', 'collections/sample','views/test'],
    function($,Backbone, _, Sample, Test){
        //...
    });
```

잘 결합되지만 다음의 내장 의존성은 :

```javascript
var models = someCondition ? ['models/ab','models/ac'] : ['models/ba','models/bc'];
```

무시될 것이다. 이것은 최적화 후라고 할 지라도 동적으로 의존성/모듈 로딩은 여전히 유효하게 만들어주도록 설계되어 있다.

RequireJS 최적화기가 노드와 자바환경 모두에서 잘 동작한다 하더라도, 노드에서 더 빨리 돌기 때문에 노드에서 돌릴 것을 강력히 추천한다. 내 경험에서, 양쪽 환경에서 설정하는 장점은 편하게 생각되는 것쪽으로 갈 수 있다는 것이다.

r.js를 시작하기 위해 [RequireJS 다운로드 페이지](http://requirejs.org/docs/download.html#rjs)나 [NPM을 통해](http://requirejs.org/docs/optimization.html#download) r.js를 얻어라. 이제 RequireJS 최적화기는 단일 스크립트와 CSS파일들에 대해서 잘 동작하지만 실제로 대부분의 경우, 전체 Backbone 프로젝트를 최적화하고 싶을 것이다. 당신은 커맨드 라인에서 모든 것을 할 *수* 있지만 cleaner 옵션은 빌드 프로파일을 사용한다.

아래는 이 책의 후반부에 볼 모듈화된 jQuery 모바일 애에서 가져온 빌드 파일의 예이다. **빌드 프로파일** ( 보통 `app.build.js`로 이름지어진다 )은 RequireJS에게 `appDir`의 모든 내용을 `dir`( 이경우, `../release` )에 정의된 디렉토리로 복사하도록 알려준다. 이것은 릴리즈 폴더내에 모든 필요한 최적화를 적용할 것이다. `baseUrl`은 모듈을 위한 경로를 해석하는데 사용된다. 그것은 이상적으로 `appDir`에 상대 경로여야 한다.

예제 파일의 아래부근에 `modules`라는 배열이 보일 것이다. 이것은 당신이 최적화하고 싶은 모듈 이름들을 지정하는 곳이다. 이 경우에 우리는 'app'라고 불리는 주 어플리케이션을 최적하한다. 'app'는 `appDir/app.js`로 매핑된다.

```javascript
({
    appDir: './',
    baseUrl: './',
    dir: '../release',
    paths: {
       'backbone':          'libs/AMDbackbone-0.5.3',
        'underscore':       'libs/underscore-1.2.2',
        'jquery':           'libs/jQuery-1.7.1',
        'json2':            'libs/json2',
        'datepicker':       'libs/jQuery.ui.datepicker',
        'datepickermobile': 'libs/jquery.ui.datepicker.mobile',
        'jquerymobile':     'libs/jquery.mobile-1.0'
    },
    optimize: 'uglify',
    modules: [
        {
            name: 'app',
            exclude: [
                // 어떤 라이브러리를 포함하고 싶지 않은면, 그것을 여기에 적는다
            ]
        }
    ]
})
```

r.js의 빌드 시스템이 동작하는 방식은 app.js( 전달할 모듈 무엇이든 )을 순회하면서 의존성을 해석해서 그것들을 최종 `release`( 디렉토리 ) 폴더로 결합한다. CSS도 동일한 방법으로 처리한다.

빌드 프로파일은 보통 프로젝트의 'scripts'나 'js' 디렉토리 안에 놓인다. 그러나 문서에 따라, 이 파일은 당신이 원하는 어디든 존재할 수 있지만, 그에 따라 빌드 프로파일의 내용을 수정해야만 할 것이다.

마지막으로 빌드를 실행하기 위해, `appDir`이나 `appDir/scripts` 디렉토리 내에서 다음 명령을 한번 실행해라:

```javascript
node ../../r.js -o app.build.js
```

다 끝났다. 당신이 UglifyJS나 클로져 설정을 옳바르게 한 이상, r.js는 단지 몇번의 키입력으로 전체 Backbone 프로젝트를 쉽게 최적화할 수 있어야만한다. 빌드 프로파일에 대해서 더 배우고 싶다면, James Burke에게 사용가능한 거의 모든 옵션을 사용한 [많은 주석을 가진 예제 파일](https://github.com/jrburke/r.js/blob/master/build/example.build.js)이 있다.


## 패키지를 사용한 RequireJS으로 Backbone.js 자바스크립트 어플리케이션을 최적화하고 빌드하기

*[Bill Heaton](https://github.com/pixelhandler)이 기여하였음*

자바스크립트 어플리케이션이 너무 복잡하거나 커서 단일 파일로 빌드할 수 없을 때, 어플리케이션 컴포넌트를 패키지로 묶는 것은 스크립트 의존성이 동시에 다운로드되게 해주고, 사이트가 일련의 의존성을 필요로 할 때 **패키지된** 것과 모듈 코드만을 로딩하게 한다.

( 자바스크립트 ) 모듈 로딩 라이브러리인 RequireJS는 자바스크립트 기반의 어플리케이션을 빌드하는 [최적화기](http://requirejs.org/docs/optimization.html 'RequireJS optimizer')를 가지고 있고 다양한 옵션을 제공한다. 빌드 프로파일은 ANT로 프로젝트를 빌드하는데 사용되는 build.xml과 매우 유사한, 빌드를 위한 방법 명세서이다. **r.js**로 빌드하는 잇점은 최소화된 코드로 빠른 스크립트 로딩뿐만 아니라 어플리케이션의 패키지 컴포넌트를 패키지하는 방법도 제공한다.

* [하나의 자바스크립트 파일 최적화](http://requirejs.org/docs/optimization.html#onejs 'Optimizing one JavaScript file')
* [전체 프로젝트 최적화](http://requirejs.org/docs/optimization.html#wholeproject 'Optimizing a whole project')
* [레이어나 패키지내에서 프로젝트 최적화](http://requirejs.org/docs/faq-optimization.html#priority 'Optimizing a project in layers or packages')

복잡한 어플리케이션에서, *패키지들*의 코드를 조직화하는 것은 매력적인 빌드 정책이다. 이 글의 빌드 프로파일은 개발중인 현재 테스트 어플리케이션에 기반하였다( 파일 목록은 아래에 있다 ). 어플리케이션 프레임워크는 오픈 소스 라이프러리로 개발되었다. 이 빌드 프로파일의 주 목적은 [Asynchronous Module Definition (AMD)](https://github.com/amdjs/amdjs-api/wiki/AMD 'Asynchronous Module Definition (AMD) wiki page') 포맷에 따라 모듈화 코드를 사용해서 [Backbone.js](http://documentcloud.github.com/backbone/ 'Backbone.js')으로 개발된 어플리케이션을 최적화하는 것이다. AMD와 RequireJS는 의존성을 가진 모듈 코드를 작성하기 위한 구조를 제공한다. Backbone.js는 모델, 뷰, 컬렉션을 개발하기 위한 코드 조직화와 REST한 API를 통한 연동은 제공한다.

아래는 어플리케이션 파일 조직화의 개략도이다. 모듈화된( 혹은 패키지화된 ) 계층을 빌드하기 위한 빌드 프로파일가 그것을 따른다.

#### 파일 조직화

app.build.js를 ( 소스와 릴리즈 디렉토리 모두에 같은 레벨로 ) 빌드 프로파일로 가지며 다음 디렉토리와 파일 구조를 가정하자. 아레 *section*이라는 이름을 가진 파일들은 어플리케이션의 어떤 컴포넌트가 될수 있다는 것을 알아두라( 예를 들면 *header*, *login* ).

```text
.-- app.build.js
|-- app-release
`-- app-src
    |-- collections
    |   |-- base.js
    |   |-- sections-segments.js
    |   `-- sections.js
    |-- docs
    |   `--docco.css
    |-- models
    |   |-- base.js
    |   |-- branding.js
    |   `-- section.js
    |-- packages
    |   |-- header
    |   |   |-- models
    |   |   |   |-- nav.js
    |   |   |   `-- link.js
    |   |   |-- templates
    |   |   |   |-- branding.js
    |   |   |   |-- nav.js
    |   |   |   `-- links.js
    |   |   `-- views
    |   |       |-- nav.js
    |   |       |-- branding.js
    |   |       `-- link.js
    |   |-- header.js
    |   `-- ... more packages here e.g. cart, checkout ...
    |-- syncs
    |   |-- rest
    |   |   `-- sections.js
    |   |-- factory.js
    |   `-- localstorage.js
    |-- test
    |   |-- fixtures
    |   |   `-- sections.json
    |   |-- header
    |   |   |-- index.html
    |   |   `-- spec.js
    |   |-- lib
    |   |   `-- Jasmine
    |   |-- models
    |   |-- utils
    |   |-- global-spec.js
    |-- utils
    |   |-- ajax.js
    |   |-- baselib.js
    |   |-- debug.js
    |   |-- localstorage.js
    |   `-- shims.js
    |-- vendor
    |-- |-- backbone-min.js
    |   |-- jquery.min.js
    |   |-- jquery.mobile-1.0.min.js
    |   |-- json2.js
    |   |-- modernizr.min.js
    |   |-- mustache.js
    |   |-- require.js
    |   |-- text.js
    |   `-- underscore.js
    |-- views
    |   |-- base.js
    |   `-- collection.js
    |-- application.js
    |-- collections.js
    |-- index.html
    |-- main.js
    |-- models.js
    |-- syncs.js
    |-- utils.js
    |-- vendor.js
    `-- views.js
```

#### 패키지를 구성하는 코드로 모듈 의존성을 최적화는 빌드 프로파일

빌드 프로파일은 [어플리케이션의 다양한 부분을 위해 다중 다운로드로 나누어](http://requirejs.org/docs/faq-optimization.html#priority 'optimize modular dependencies in packages') 구성될 수도 있다.

설명했던 이 정책은 기본적인 혹은 사이트 전체의 base.js에 있는 적당한 Backbone 메소드( 예를 들면 Backbone.Model )를 상속한 ( 핵심적인 ) *모델*, *뷰*, 컬렉션의 그룹을 빌드한다. *packages* 디렉토리는 section이나 responsibility의 코드가 모인다. 예를 들면, cart, checkout등등. 예제의 *header* 패키지안에 디렉토리 구조가 앱 루트 디렉토리 파일 구조와 유사한 것을 기억해둬라. ( 모듈화된 코드의 ) *패키지*가 어플리케이션의 일반 라이브러리와 의존성을 갖고 있고, 패키지 실행에 대한 특별한 코드도 가지고 있다; 다른 패키지들은 다른 패키지 의존성을 필요로 하지 말아야한다. *utils* 디렌토리는 어플리케이션을 지원하는 코드조각, 헬퍼, 공통 라이브러리를 가지고 있다. REST한 API나 localStorage와 퍼시스턴스를 정의하기 위해 *syncs* 디렌토리가 있다. *vender* 라이브러리는 빌드되지 않을 것이고 그럴 필요도 없고 단지 CDN을 사용할지를 결정해도 된다( 그러면 이 경로들을 : *[empty:](http://requirejs.org/docs/optimization.html#empty 'empty:')* 에 지정해라). 그리고 마지만으로 [Jasmine](http://pivotal.github.com/jasmine/ 'Jasmine is a behavior-driven development framework for testing your JavaScript code') 단위 테스트 명세를 위한 *test* 디렉토리가 있다. 그것도 당신이 선택하면 빌드에서 무시된다.

디렌토리와 같은 이름의 .js 파일도 있다는 것도 알아둬라. 그 파일들은 paths에 기술된 파일들이다. 이들은 빌드할 파일들을 묶는 정책이다. 예제는 아래의 빌드 프로파일을 따른다.

```javascript
({
    appDir: './app-src',
    baseUrl: './',
    dir: './app-build',
    optimize: 'uglify',
    paths: {
        // 외부 코드는 빌드하지 않을 것이다. 이미 빌드되어 있다.
        'text'         : 'vendor/text',
        'json2'        : 'vendor/json2.min',
        'modernizr'    : 'vendor/modernizr.min',
        'jquery'       : 'vendor/jquery-1.7.1',
        'jquerymobile' : 'vendor/jquery.mobile.min.js',
        'underscore'   : 'vendor/underscore',
        'mustache'     : 'vendor/mustache',
        'backbone'     : 'vendor/backbone',
        // 의존성을 정의한 파일들...
        // 벤터 라이브러리들은 무시하지만, 그렇게 하기 위해서 묶음이 필요하다.
        'vendor'       : 'vendor',
        // 어플리케이션 모듈/패키지 이 파일들은 의존성을 정의하고,
        // 각 파일보다는 묶음에서 필요로 하는 모듈을
		// 객체로 묶기도 한다.
        'utils'        : 'utils',
        'models'       : 'models',
        'views'        : 'views',
        'collections'  : 'collections',
        // 빌드할 패키지들
        'header'       : 'packages/header'
        //... 더 많은 패키지들
    },
    modules: [
        // 공통 라이브러리, 유틸리티, 동기화, 모델, 뷰, 컬렉션
        {
            name: 'utils',
            exclude: ['vendor']
        },
        {
            name: 'syncs',
            exclude: ['vendor', 'utils']
        },
        {
            name: 'models',
            exclude: ['vendor', 'utils', 'syncs']
        },
        {
            name: 'views',
            exclude: ['vendor', 'utils', 'syncs', 'models']
        },
        {
            name: 'collections',
            exclude: ['vendor', 'utils', 'syncs', 'models', 'views']
        },
        // 패키지들
        {
            name: 'header',
            exclude: ['vendor', 'utils', 'syncs', 'models', 'views', 'collections']
        }
        // ... 기타 등등 ...
    ]
})
```

위의 빌드 프로파일은 확장성과 성능의 균형을 맞춰 설계되었다

**코드 의존성들을 묶은 예제**

패키지에 빌드되지 않은 vendor.js의 내용은 *no conflict* 호출도 사용한다

```javascript
// 벤더 라이브러리 목록. 예를 들면, jQuery, Underscore, Backbone 등등
// 이 모듈은 빌드 중에 r.js 최적화 도구와 함께 사용된다.
// @see <http://requirejs.org/docs/faq-optimization.html>
define([ 'jquery', 'underscore', 'backbone', 'modernizr', 'mustache' ],
function ($,        _,            Backbone,   Modernizr,   Mustache) {
    // $의 여러 버젼을 사용할 필요도 있다면 no conflict을 호출해라.
    $.noConflict();
    _.noConflict();
    Backbone.noConflict();
});
```

어플리케이션을 위한 공통 라이브러리 코드.

```javascript
// List of utility libraries,
define([ 'utils/ajax', 'utils/baselib', 'utils/localstorage', 'utils/debug', 'utils/shims' ],
function (ajax,         baselib,         localstorage,         debug) {
    return {
        'ajax' : ajax,
        'baselib' : baselib,
        'localstorage' : localstorage,
        'debug' : debug
    };
    // 필요할 때면( 예를 들어 객체 생성시 ) 자바스크립트를 확장한 구문
});
```

다른 패키지 파일에서 공통 모델을 필요로 할 때의 예제

```javascript
// 모델 목록
// 이 디렉토리의 모델들은 사이트 전반에 사용된다
// 이 모듈( 객체 )의 사이트 전반의 모델을 묶는 것은
// ( 빌드 ) 최적화기가 실행될 때,
// 성능을 최적화하고 결합된 의존성을 유지한다.
define([ 'models/branding', 'models/section' ],
function (Branding,          Section) {
    return {
        'Branding' : Branding,
        'Section'  : Section
    };
});
```

#### 코드 표준의 간단한 메모

위의 예제에서 파라미터가 소문자나 대문자로 시작할 수 있음을 주의해라. *대문자*로 시작하는 파라미터 변수명은 *생성자*이고 *소문자* 변수명은 그렇지 않고 생성자에 의해 성성된 객체일 수도 있고 혹은 *new*를 사용하지 않는 객체나 함수일 수도 있다.

추천하는 스타일은 생성자에는 대문자로 시작하는 카멜 노테이션을 사용하고, 다른 곳에는 소문자 카멜 노테이션을 사용하는 것이다.

#### 모듈의 코드를 최적화할 때, 일반적인 위험

순환 의존성을 정의하지 않도록 주의해라. 예를들어, 공통 *모델들* 패키지( models.js ) 의존성이 모델 디렉토리의 파일을 기정하고 있다.

    define([ 'models/branding', 'models/section' ], function (branding, section)
    // ...
    return { 'branding' : branding, 'section', section }

그리고 나서 다른 패키지가 공통 모델을 필요로 한다면, 공통 models.js에서 모델 객체를 다음과 같이 접근할 수 있다..

    define([ 'models', 'utils' ], function (models, utils) {
    var branding = models.branding, debug = utils.debug;

아마 모델을 몇번 쓰고난 후, "모델"을 습관적으로 사용한다. 나중에 당신은 이미 정의된 모델을 extends로 다른 공통 모델로 추가할 필요가 있다. 당신이 새로운 모델을 모델 디렉토리에 추가하고 model.js에 이 모델의 참조를 추가해서 위험은 시작된다:

    define([ 'models/branding', 'models/section', 'models/section-b' ], function (branding, section)
    // ...
    return { 'branding' : branding, 'section', section, 'section-b' : section-b }

하지만 *model/section-b.js* 파일에서 모델을 객체로 다음과 같이 반환하는 model.js를 사용하는 의존성을 정의한다...

    define([ 'models' ], function (models, utils) {
    var section = models.section;

위에서 models.js내에 실수가 있다. models/section-b를 위한 의존성이 추가되었다. section-b에서 모델을 위한 의존성이 정의되었다. 새로운 models/section-b.js는 *모델*을 필요로 하고, model.js는 *models/section-b.js*를 필요로 한다 - 순환 의존성이다. 이것은 RequireJS에서 로드 시즘에 에러를 내지만 순환 의존성에 대해 말하지 않는다.

다른 실수들에 대허서는 RequireJS 사이트의 [COMMON ERRORS](http://requirejs.org/docs/errors.html 'RequireJS common errors page') 페이지를 보라.

#### r.js로 빌드 실행하기

당신이 다음과 같이 노드의 npm( 패키지 관리자 )로 r.js를 설치했다면...

    > npm install requirejs

...커맨드 라인상에서 빌드를 실행할 수 있다:

    > r.js -o app.build.js


## 연습: AMD와 RequireJS로 모듈화된 Backbone 앱 빌드하기

이번 챕터에서 우리는 우리의 첫번째 Backbone과 RequireJS 프로젝트를 볼 것이다 - 모듈화된 할일 어플리케이션을 빌드하는 방법. 어플리케이션은 우리가 새로운 할일을 추가하고, 할일 항목을 수정하고, 완료로 표시된 할일 항목 모두를 지울 수 있게 한다. 더 발전된 예를 위해 모바일 Backbone 개발의 섹션을 보라.

어플리케이션에 대한 전체 코드는 이 저장소의 `practicals/modular-todo-app` 폴더에서 찾을 수 있다.( Thomas Davis와 J&eacute;r&ocirc;me Gravel-Niquet 에게 감사한다 ). 아니면, AMD와 AMD가 아닌 버젼 모두가 있는 내 부수 프로젝트 [TodoMVC](https://github.com/addyosmani/todomvc) 에서 복사본을 가져가라.

**주의:** Thomas는 이 연습에 대한 어떤 것들을 [backbonetutorials.com](http://backbonetutorials.com)에 더 자세히 다루기도 하지만, 이 섹션에서 나는 내가 핵심 개념이라고 생각되는 것을 다룰 것이다.

### 개략도

'모듈화된' Backbone 어플리케이션을 작성하는 것은 간단한 과정일 수도 있다. 그러나 여러 선택 중에 AMD를 모듈 포맷으로 사용하려고 한다면 알게 될 주요한 개념적인 차이점들이 있다:

* AMD가 자바스크립트나 브라우져의 표준적인 특성이 아니기 때문에, 모듈 포맷을 사용해서 컴포넌트와 모듈을 정의하도록 하기 위해서는 ( RequireJS나 curl.js와 같은 ) 스크립트 로더를 반드시 써야한다. 우리가 이미 봤다시피, 여기해서 AMD뿐만 아니라 RequireJS를 사용한 많은 장점들이 있다.
* 모델, 뷰, 컨트롤러, 라우터는 AMD 형태를 *사용해서* 은닉화되어야만 한다. 이것은 Backbone 어플리케이션의 각 컴포넌트가 AMD가 Backbone이 아닌 모듈에 하듯이 깔끔하게 종속성( 예를 들면, 뷰는 컬렉션을 필요로 한다 )을 관리하게 해준다.
* ( 유틸리티나 어플리케이션 헬퍼같은 ) Backbone이 아닌 컴포넌트나 모듈도 AMD를 사용해서 은닉될 수 있다. 나는 이것이 다른곳에서 재사용성을 증가시키기 때문에 당신이 Backbone 코드에 독립적으로 사용되기도 하고 테스트되기도 하는 방식으로 이들 모듈을 개발해보게 한다.

우리는 기본을 봤기 때문에, 어플리케이션 개발을 보자. 참고로 앱의 구조는 다음과 같다:

```
index.html
...js/
    main.js
    .../models
            todo.js
    .../views
            app.js
            todos.js
    .../collections
            todos.js
    .../templates
            stats.html
            todos.html
    ../libs
        .../backbone
        .../jquery
        .../underscore
        .../require
                require.js
                text.js
...css/
```

### 마크업

어플리케이션의 마크업은 상대적으로 단순하고 세개의 주요 부분으로 구성된다: 새로운 할일 항목을 입력하는 입력부( `create-todo` ), ( 그자리에서 바로 편집도 할 수 있는 ) 이미 존재하는 항목들을 보여주는 목록부( `todo-list` ), 마지막으로 얼마나 많은 항목이 완료로 남아있는지 요약해주는 부분( `todo-stats` ).

```
<div id="todoapp">

      <div class="content">

        <div id="create-todo">
          <input id="new-todo" placeholder="What needs to be done?" type="text" />
          <span class="ui-tooltip-top">Press Enter to save this task</span>
        </div>

        <div id="todos">
          <ul id="todo-list"></ul>
        </div>

        <div id="todo-stats"></div>

      </div>

</div>
```

안내서의 나머지 부분은 실제의 자바스크립트 부분에 촛점을 맞출 것이다.

### 설정 옵션

당신이 AMD에 관한 이전 챕터를 읽었다면, Backbone 모듈( 뷰, 컬렉션, 혹은 다른 모듈 )이 필요로 하는 각 의존성을  명시적으로 정의해야하기 때문에 조금은 지루할 수 있다. 그러나, 이것은 개선될 수 있다.

단순히 어플리케이션의 모듈이 사용하는 공통 경로를 참조하기 위해서, 우리는 RequireJS [configuration object](http://requirejs.org/docs/api.html#config)를 사용한다. 그건은 일반적으로 최상위 스크립트 파일로 정의된다. 설정 객체는 많은 유용한 기능이 있는데, 가장 유용한 것은 이름 매핑이다. 이름 매핑은 기본적으로 키:값 쌍이다. 이때, 키는 경로에 대해 사용하고 싶은 축약이름이고, 값은 경로의 실제 위치를 나태낸다.

아래 코드 예제에서, `backbone`, `underscore`, `jquery` 그리고 선택에 따라 텍스트 자산을 템플릿으로 로딩하도록 도와주는 RequireJS `text` 플러그인을 포함하는 공통 이름 매핑을 볼 수 있다.

**main.js**

```javascript
require.config({
  baseUrl:'../',
  paths: {
    jquery: 'libs/jquery/jquery-min',
    underscore: 'libs/underscore/underscore-min',
    backbone: 'libs/backbone/backbone-optamd3-min',
    text: 'libs/require/text'
  }
});

require(['views/app'], function(AppView){
  var app_view = new AppView;
});
```

main.js 파일의  끝에 있는 `require()`는 단순해서 우리는 어플리케이션( `view/app.js` )의 주 뷰를 로드해서 객체화할 수 있다. 우리는 보통 프로젝트 최상위 스크립트 파일에 포함된 이것과 설정 객체 모두를 보게될 것이다.

이름 매핑을 제한할 뿐만 아니라, 설정 객체는 `waitSeconds`( 스크립트 로딩전에 기다리는 초 단위 시간 )같은 부수적인 특성을 정의하는데 사용될 수도 있다. 당신은 다른 언어에 대해서 국제화 번들을 로드하고 싶을 것이다. `baseUrl`은 단순히 모듈을 찾는데 사용되는 경로이다.

설정 객체에 대한 더 많은 정보를 위해서는 [RequireJS 문서](http://requirejs.org/docs/api.html#config)에 있는 안내서를 자유로이 확인해봐라.


### 모델, 뷰, 컬렉션을 모듈화하기

우리가 Backbone 컴포넌트의 AMD로 싼 버젼에 들어가기 전에, AMD가 아닌 뷰의 예제를 살펴보자. 다음 뷰는 자신의 모델( Todo 항목 )의 변경을 감시해서 사용자가 항목의 값을 수정하면 다시 렌더링한다.

```javascript
var TodoView = Backbone.View.extend({

    //... li 태그
    tagName:  'li',

    // 단일 항목에 대한 템플릿 함수를 캐쉬한다.
    template: _.template($('#item-template').html()),

    // 아이템에 지정된 DOM 이벤트.
    events: {
      'click .check'              : 'toggleDone',
      'dblclick div.todo-content' : 'edit',
      'click span.todo-destroy'   : 'clear',
      'keypress .todo-input'      : 'updateOnEnter'
    },

    //  TodoView는 모델의 변경을 감시해서 다시 렌더링한다.
    // 이 앱에서는 **Todo**와 **TodoView** 사이에 1:1 대응이 있기 때문에,
    // 편의상 모델을 직접적으로 참조시킨다.
    initialize: function() {
      this.model.on('change', this.render, this);
      this.model.view = this;
    },
    ...
```

 템플릿팅에 대해서 어떻게 아이디( 혹은 다른 선택자 )로 스크립트를 참조하고 그 값을 얻는지에 대한 일반적인 방법이 사용되었다. 이번 코스는 접근되는 템플릿이 마크업 안에 암묵적으로 정의되어야만 한다. 다음은 위에서 참조되고 있는 템플릿의 '내장' 버젼이다:

```
<script type="text/template" id="item-template">
      <div class="todo <%= done ? 'done' : '' %>">
        <div class="display">
          <input class="check" type="checkbox" <%= done ? 'checked="checked"' : '' %> />
          <div class="todo-content"></div>
          <span class="todo-destroy"></span>
        </div>
        <div class="edit">
          <input class="todo-input" type="text" value="" />
        </div>
      </div>
</script>
```

템플릿에 아무런 이상이 없는 동안, 우리가 일단 여러 템플릿을 필요로 하는  큰 어플리케이션의 개발을 시작한다면, 템플릿 모두를 페이지 로드에 포함하는 것은 빠르게 관리하기도 어렵고 실행 비용도 늘어나게 된다. 우리는 잠깐동안 이 문제를 해결하는 것을 볼 것이다.

이제 뷰의 AMD 버젼을 보자. 앞서 논의한대로, '모듈'은 AMD의 뷰가 필요로 하는 의존성을 지정하는 `define()`을 사용해서 감싸졌다. 'jquery' 등에 매핑된 경로를 사용하는 것은 공통 의존성을 참조하는 것을 단순화하고 의존성 객체는 우리가 접근할 수 있는 지역 변수( 예를 들어 'jquery'는 `$` )로 매핑된다.

**views/todo.js**

```javascript
define([
  'jquery',
  'underscore',
  'backbone',
  'text!templates/todos.html'
  ], function($, _, Backbone, todosTemplate){
  var TodoView = Backbone.View.extend({

    //... li 태그.
    tagName:  'li',

    // 단일 항목에 대한 템플릿 함수를 캐쉬한다.
    template: _.template(todosTemplate),

     // 아이템에 지정된 DOM 이벤트.
    events: {
      'click .check'              : 'toggleDone',
      'dblclick div.todo-content' : 'edit',
      'click span.todo-destroy'   : 'clear',
      'keypress .todo-input'      : 'updateOnEnter'
    },

    //  TodoView는 모델의 변경을 감시해서 다시 렌더링한다.
    // 이 앱에서는 **Todo**와 **TodoView** 사이에 1:1 대응이 있기 때문에,
    // 편의상 모델을 직접적으로 참조시킨다.
    initialize: function() {
      this.model.on('change', this.render, this);
      this.model.view = this;
    },

    // 할일 항목의 내용을 다시 렌더링한다.
    render: function() {
      this.$el.html(this.template(this.model.toJSON()));
      this.setContent();
      return this;
    },

    // 할일 항목의 내용을 설정하기 위해서 `jQuery.text`를 사용한다.
    setContent: function() {
      var content = this.model.get('content');
      this.$('.todo-content').text(content);
      this.input = this.$('.todo-input');
      this.input.on('blur', this.close);
      this.input.val(content);
    },
    ...
```

유지보수 관점에서, 펨플릿에 접근하는 것만 제외하면, 뷰에서 차이점은 없다.

( 의존성은 `text`로 표시된는 ) RequireJS의 텍스트 플러그인을 사용해서 우리는 실체로 이전에 외부 파일( todos.html )에서 본 템플릿의 모든 내용을 저장할 수 있다.

**templates/todos.html**

```html
<div class="todo <%= done ? 'done' : '' %>">
    <div class="display">
      <input class="check" type="checkbox" <%= done ? 'checked="checked"' : '' %> />
      <div class="todo-content"></div>
      <span class="todo-destroy"></span>
    </div>
    <div class="edit">
      <input class="todo-input" type="text" value="" />
    </div>
</div>
```

템플릿의 내용을 지역변수( 이경우 `todosTemplate` )로 매핑할 수 있기 때문에 더이상 템플릿의 아이디에 관심가질 필요가 없다. 그리고나서 우리가 보통 템플릿 스크립트의 값을 얻은 방식대로 그것을 Underscore.js의 템플릿팅 함수인 `_.template()`에 전달한다.

다음으로, 어떻게 모델을 컬렉션에서 필요로 하는 의존성으로 정의하는지 보자. 여기 AMD 호환가능한 모델 모듈이 있는데, 그것은 두개의 기본값을 갖는다: Todo 항목의 내용을 위한 `content` 속성과 항목이 완료되었는지 아닌지를 알게해주는 `done` 상태값.

**models/todo.js**

```javascript
define(['underscore', 'backbone'], function(_, Backbone) {
  var TodoModel = Backbone.Model.extend({

    // 할일에 대한 기본값.
    defaults: {
      // 각 항목은 `content`를 가져야만 한다.
      content: 'empty todo...',
      done: false
    },

    initialize: function() {
    },

    // 이 할일 항목의 `done` 상태를 전환한다.
    toggle: function() {
      this.save({done: !this.get('done')});
    },

    // *localStorage*에서 제거하고 그 뷰도 삭제한다.
    clear: function() {
      this.destroy();
      this.view.remove();
    }

  });
  return TodoModel;
});
```

다른 종류의 의존성마다 우리가 우리 모델 모듈을 지역변수( 이경우 `Todo` )로 쉽게 매핑할 수 있기 때문에 `TodosCollection`을 위해 사용하는 모델로 참조될 수 있다. 이 컬렉션도 완료된 Todo 항목들만 걸러주는 `done()` 필터와 완료되지 않은 항목들을 위한 `remaining()` 필터를 간단하기 지원한다.

**collections/todos.js**

```javascript
define([
  'underscore',
  'backbone',
  'libs/backbone/localstorage',
  'models/todo'
  ], function(_, Backbone, Store, Todo){

    var TodosCollection = Backbone.Collection.extend({

    // 이 컬렌션의 모델에 대한 참조
    model: Todo,

    // `todo` 이름 공간 내에 모든 할일 항목을 저장한다.
    localStorage: new Store('todos'),

    // 완료된 모든 할일 항목들만 필터링한다.
    done: function() {
      return this.filter(function(todo){ return todo.get('done'); });
    },

    // 완료되지 않은 할일 항목들만 필트링한다.
    remaining: function() {
      return this.without.apply(this, this.done());
    },
    ...
```

사용자가 ( 컬렉션의 모델들로 삽입한 ) 뷰의 새로운 할일 목록을 추가하는 것뿐만 아니라, 이상적으로 얼마나 많은 항목들이 완료되고 얼마나 많은 항목들이 남아있는지 보여주길 원한다. 우리는 이미 위의 컬렉션에 이정보를 제공하는 필터를 정의했기 때문에 주 어플리케이션 뷰에서 그 정보를 이용해보자.

**views/app.js**

```javascript
define([
  'jquery',
  'underscore',
  'backbone',
  'collections/todos',
  'views/todo',
  'text!templates/stats.html'
  ], function($, _, Backbone, Todos, TodoView, statsTemplate){

  var AppView = Backbone.View.extend({

    // 새로운 요수를 생성하는 대신에 HTML에 표시되어 있는
    // 이미 있는 App의 골력에 바인딩한다.
    el: $('#todoapp'),

    // 앱의 바닥에 통계줄을 위한 템플릿
    statsTemplate: _.template(statsTemplate),

    // ...이벤트, initialize()등은 전체 파일에서 볼 수 있다.

    // 앱을 재 렌더링하는 것은 단지 통계부분만 갱신한다 - 앱의
    // 나머지는 변하지 않는다.
    render: function() {
      var done = Todos.done().length;
      this.$('#todo-stats').html(this.statsTemplate({
        total:      Todos.length,
        done:       Todos.done().length,
        remaining:  Todos.remaining().length
      }));
    },
    ...
```

위에서, 우리는 이 프로젝트를 위한 두번째 템플릿으로 `templates/stats.html`을 `statsTemplate`에 매핑한다, 그것은 전체의 `done`과 `remaingin` 상태를 렌더링하는데 사용된다. 이겄은 단순히 템플릿에 전체의 Todos 컬렉션의 길이( `Todos.length` - 지금까지 생성된 Todo 항목의 수 )와 완료된 항목의 수( `Todos.done().length` )와 남은 항목의 수( `Todos.remaining().length )를 전달해서 동작한다.

`statsTemplate`의 내용은 아래에서 볼 수 있다. 그리 복잡할 것은 없지만, 특정 상태에 "1 item"이나 "2 item<i>s</i>"이 있다고 기술해야 하는지 계산하는 삼항 조건식을 사용한다.

```
<% if (total) { %>
        <span class="todo-count">
          <span class="number"><%= remaining %></span>
          <span class="word"><%= remaining == 1 ? 'item' : 'items' %></span> left.
        </span>
      <% } %>
      <% if (done) { %>
        <span class="todo-clear">
          <a href="#">
            Clear <span class="number-done"><%= done %></span>
            completed <span class="word-done"><%= done == 1 ? 'item' : 'items' %></span>
          </a>
        </span>
      <% } %>
```



할일 앱에 대한 나머지 소스는 주로 사용자와 어플리케이션의 이벤트를 처리하는 코드로 구성되어 있지만, 이 예제에 대한 핵심 개념의 대부분은 살펴보았다.

전체가 어떻게 묶이는지 보기 위해서는 자유롭게 이 저장소를 클론해서 소스를 가져가고 더 배우기 위해서 [온라인](https://github.com/addyosmani/backbone-fundamentals/tree/master/practicals/modular-todo-app)을 돌아다녀 보아라. 도움이 되길 바란다!

**주의:** 이 첫번째 예제가 RequireJS 최적화기에 대한 챕터에서 본 빌드 프로파일을 사용하지 않는 반면 모바일 Backbone 어플리케이션을 개발하는 섹션에서는 사용할 것이다.


## 모듈 로딩에 기반한 라우터

이번 섹션은 Kevin Decker이 만든 [Lumbar](http://walmartlabs.github.com/lumbar)에 구현된 대로 모듈 로딩의 접근법에 기반한 지점에 대해 논의할 것이다. RequireJS와 같이 Lumbar도 모듈화된 빌드 시스템이지만 로딩 지점에 대해 구현한 패턴은 어떤 빌드 시스템에서도 사용할 수 있다.

Lumbar 빌드 툴의 기능 명세는 이 책에서 논의되지 않을 것이다. 로더와 빌드 시스템으로 완전한 Lumbar 기반의 프로젝트를 보기 위해서는 Lumbar를 포함한 다양한 환경에 대한 보일러플레이트 프로젝트를 제공하는 [Thorax](http://walmartlabs.github.com/thorax)를 보아라.

### JSON 기반 모듈 설정

Lumbar는 각 정의된 모듈에 대해서 하나의 자바스크립트 파일을 만들기 위해 중앙의 JSON 설정 파일에서 각 모듈에 대한 파일 목록을 정의하는 반면, RequireJS는 파일당 의존성을 정의한다. Lumbar는 기본 모듈을 제외한 각 모듈이 단일 라우터와 지점의 목록을 정의할 것을 필요로 한다. 예제 파일은 다음과 같다:

     {
        "modules": {
            "base": {
                "scripts": [
                    "js/lib/underscore.js",
                    "js/lib/backbone.js",
                    "etc"
                ]
            },
            "pages": {
                "scripts": [
                    "js/routers/pages.js",
                    "js/views/pages/index.js",
                    "etc"
                ],
                "routes": {
                    "": "index",
                    "contact": "contact"
                }
            }
        }
    }

모듈에 정의된 모든 자바스크립트 파일은 모듈을 위한 `name`과 `routes`를 포함하고 있는 범위의 `모듈` 객체를 가질 것이다. `js/routers/pages.js`에 `pages` 모듈에 대한 Backbone 라우터를 다음과 같이 정의한다:

    new (Backbone.Router.extend({
        routes: module.routes,
        index: function() {},
        contact: function() {}
    }));

### 모듈 로더 라우터

`Backbone.Router`의 가끔 사용되는 특징은 동일 지점들을 감시하는 다수의 라우터를 생성하는 기능이다. Lumbar는 어플리케이션의 모든 지점을 감시하는 라우터를 생성하는 이 특징을 사용한다. 지점이 일치할 때, 이 주 라우터는 필요한 모듈이 로드되었는지 아닌지를 체크한다. 모듈이 이미 로드되었으면, 주 라우터는 아무런 동작도 취하지않고 모듈에 정의된 라우터가 지점을 제어한다. 필요한 모듈이 아직 로드되어 있지 않았으면 로드하고 나서 `Backbone.history.loadUrl`이 호출될 것이다. 이것은 지점을 다시 로드하고, 주 라우터가 더 이상 동작하지 않게 만들고, 라우터는 응답하는 새로 로드된 모듈에 정의된다.

예제 구현은 아래에 제공된다. `설정` 객체는 위의 예제 설정 JSON 파일의 데이타를 포함해야만 하고, `loader` 객체는 `isLoaded`와 `loadModule` 메쏘드를 구현해야만 한다. Lumbar는 이들 구현 모두를 지공하고 있는 것을 기억하라. 예제는 자체적인 구현을 만들기 위해서 제공된다.

    // 주 라우터를 위한 프로토타입으로 
    // 사용되는 객체를 생성한다.
    var handlers = {
        routes: {}
    };

    _.each(config.modules, function(module, moduleName) {
        if (module.routes) {
            // 모듈을 위한 로딩 콜백을 생성한다
            var callbackName = "loader_" moduleName;
            handlers[callbackName] = function() {
                if (loader.isLoaded(moduleName)) {
                    // 모듈이 로드된다면 아무것도 하지 않는다
                    return;
                } else {
                    // 모듈은 로드되어야만 한다
                    loader.loadModule(moduleName, function() {
                        // 라우터를 리로딩하는 것이
			// 모듈의 라우터의 콜백을
			// 구동하기 위해 모듈이 로드된다.
                        Backbone.history.loadUrl();
                    });
                }
            };
            // 모듈의 각 지점은 로딩 콜백을 
	    // 구동해야만 한다.
            _.each(module.routes, function(methodName, route) {
                handlers.routes[route] = callbackName;
            });
        }
    });

    // 주 라우터를 생성한다
    new (Backbone.Router.extend(handlers));

### pushState를 제어하기 위한 Node의 사용

사용자가 지점들 중에 어디에선든 앱을 진입할( 혹은 pushState URL로 이동후 리프레쉬를 누를 ) 수 있기 때문에, ( 해쉬 태그없이 Backbone 지점을 제공해주는 ) `window.history.pushState` 지원은 서버가 Backbone 어플리케이션이 다루는 URL이 무엇인 알아야만 한다.

단일 위치에 모든 지점을 정의하는 다른 잇점은 각 지점을 감시하기 위해 위에서 제공되는 같은 JSON 설정 파일이 서버에서 로드될 수도 있다는 것이다. NodeJS와 Express에서의 예제 구현:

    var fs = require('fs'),
        _ = require('underscore'),
        express = require('express'),
        server = express.createServer(),
        config = JSON.parse(fs.readFileSync('path/to/config.json'));

    _.each(config.modules, function(module, moduleName) {
        if (module.routes) {
            _.each(module.routes, function(methodName, route) {
                server.get(route, function(req, res) {
                      res.sendFile('public/index.html');
                });
            });
        }
    });

이것은 index.html이 Backbone 어플리케이션을 제공할 것이라고 가정한다. `Backbone.History` 객체는 `root` 설정이 지정되는 한 나머지 지점을 처리할 수 있다. 루트에 있는 간단한 어플리케이션을 위한 예제 설정은 다음과 같다:

    Backbone.history || (Backbone.history = new Backbone.History());
    Backbone.history.start({
      pushState: true,
      root: '/'
    });

## 중개자와 퍼사드 패턴으로 Bacbone을 분리하기

이 섹션에서 우리는 [대규모 자바스크립트 어플리케이션 개발](http://addyosmani.com/largescalejavascript)의 내 글에서 다룬 어떤 개념을 Backbone에 적용할 것이다.

*나중에, 당신은 [Aura](http://github.com/addyosmani/aura) 를 한번 보고 싶어할 지 모르겠다 - 이번 섹션에서 다룰 많은 개념에 기반한 내가 만든 인기 있는 위젯 기반의 Backbone.js 확장 프레임워크.*

### 요약

상위 수준에서 보면, 그런 어플리케이션에서 동작하는 구조는 다음 중에 하나이다:

* **매우 낮은 의존성**: 모듈들이 서로 직접 통신하는 것보다 관심있는 이벤트를 발행하고 구독만 하게 한다. 이것은 우리가 어떤 코드 조각도 강하게 서로 묶이지 않고 더 쉽게 재사용될 수 있는 어플리케이션을 만들게 도와준다.
* **모듈 단위 보안의 지원**: 그것으로 모듈은 허용된 동작만을 실행할 수 있다. 어플리케이션 보안은 자바스크립트 어플리케이션에서 종종 간과되지만, 유연한 방법으로 매우 쉽게 구현되는 영역이다.
* **실패 극복 지원**: 특정 모듈이 에러가 나더라도 어플리케이션이 계속 동작하게 해준다. 내가 제시하는 이에 대한 전형적인 예제는 GMail 채팅 위젯이다. 페이지상의 한 위젯( 예를 들어 채팅 )이 에러가 나면 어플리케이션의 나머지( 메일 )가 영향받지 않고 계속 동작하는 방식으로 어플리케이션을 만들 수 있다고 상상해봐라.

이것은 과거에 ( 모듈화된 홈페이지를 위해서 ) Yahoo!를 포함해서 많은 다른 회사들에 의해 구현된 구조이다.

이 구조를 가능하게 하는 세개의 설계 패턴은:

* **모듈 패턴**: 함수와 변수가 공개나 비공개로 유지할 수 있는 곳의 특정 코드 블럭을 은닉하는데 사용된다( 물론 자바스크립트에서 'private'은 진짜 보호는 아니기 때문에 보호를 흉내낸다 )
* **중개자 패턴**: 모듈들 간의 통신이 복잡하지만 잘 정의될 때, 사용된다. 시스템이 코드상의 모듈간에 너무 많은 관계를 가지면, 제어의 중앙집중점을 가지는데 시간이 걸리기도 한다. 그건은 패턴이 잘 맞는 상황이다
* **퍼사드 패턴**: 많은 량의 코드에 실제 내부의 복잡성을 숨기고 편리한 상위 레벨 인터페이스를 제공하는데 사용된다

이 구조에는 다음의 역할이 있다.

* **모듈**: 모듈을 정의하는 것에 대한 대략 두 개의 개념이 있다. AMD 모듈을 감싸는 역할로 사용되기 때문에, 기술적으로 각 모델, 뷰, 컬렉션이 모듈로 간주될 수 있다. 우리는 단지 MVC나 MV*의 외부에 구분되는 코드 블럭이 되는 모듈 개념을 가지고 있다. 나중에 이런 종류의 '모듈'은 서로 간에 직접 통신하기 보다는 발행과 구독으로만 다뤄진다. 그것은 중개자 패턴을 통해 가능해진다.
* **중개자**: 중개자는 당신이 구현하고 싶은 방식에 따라 다양한 역할을 하게 된다. 내가 쓴 글에서, 중개자를 마음대로 모듈을 시작하고 끝내는 기능을 가진 모듈 관리자로 사용하는 것을 언급했었지만 그것이 Backbone으로 오면 발행/구독 기능을 제공하는 중앙의 '컨트롤러'로 단순화하는 것으로 충분하다고 느껴진다. 물론 모듈 시작, 정지, 잠시 멈춤 등을 지원하는 모듈 시스템을 만드는 관점에서 모든 노력을 다하지만, 이 범위는 본 챕터의 것이 아니다.
* **퍼사드**: 이것은 어플리케이션 코어( 중개자 )를 추상화하면서 모듈이 중개자에 다시 메시지를 중계하는 안전한 중간 계층으로 동작해서, 모듈 간에 직접적으로 접촉하지 않는다. 퍼사드는 어플리케이션 보안 경비의 역할도 수행한다: 전달된 행동을 실행하도록 해주면 모듈의 요청이 처리되도록 설정( permissions.js, 나중에 살펴볼 것이다. )으로 모듈에서의 이벤트 통지를 확인한다.


### 연습

이 챕터의 연습 섹셕을 위해, 우리는 위에서 언급한 세가지 패턴을 사용해서 잘 알고 있는 Backbone 할일 어플리케이션을 확장할 것이다.

어플리케이션은 어플리케이션 수준의 모듈을 통해 Backbone 모델의 모든 것을 다루는 AMD 모듈로 쪼개진다. 뷰는 어플리케이션의 나머지에 관련된 이벤트를 발행하고, 그리고나서 모듈은 이 이벤트 통지를 구독할 수 있을 것이다.

모듈의 구독은 퍼사드( 혹은 샌드박스 )를 통해 수행된다. 이것이 하는 일은 구독자 이름과 구독하려는 'channel/notification' 을 대조하는 것이다. 채널이 ( permissions.js를 통해 지정된 것에) 구독을 허용하지 *않으면*, 구독은 허용되지 않는다.


**중개자**

`aura/mediator.js`에 나타난다.

아래는 Ryan Florence가 이전에 작업한 것에 기초한 중개자 패턴의 아주 간단한 AMD 로 감싼 구현이다. 그것은 객체의 입력으로 받아들여지는데, `publish()`와 `subscribe()` 메쏘드를 붙인다. 큰 어플리케이션에서 중개자는 모듈 초기화, 구동, 정지를 위한 처리자같은 추가적인 유틸리티를 포함할 수 있지만, 데모를 목적으로 우리 요건을 위해서 이 두개의 메쏘드만 잘 동작하면 된다.

```javascript
define([], function(obj){

  var channels = {};
  if (!obj) obj = {};

  obj.subscribe = function (channel, subscription) {
    if (!channels[channel]) channels[channel] = [];
    channels[channel].push(subscription);
  };

  obj.publish = function (channel) {
    if (!channels[channel]) return;
    var args = [].slice.call(arguments, 1);
    for (var i = 0, l = channels[channel].length; i < l; i++) {
      channels[channel][i].apply(this, args);
    }
  };

  return obj;

});
```


**퍼사드**

`aura/facade.js`에 나타난다.

다음으로 퍼사드 패턴의 구현이다. 이제 자바스크립트에 적용된 고전적인 퍼사드 패턴은 다음과 같이 보일 것이다:

```javascript

var module = (function() {
    var _private = {
        i:5,
        get : function() {
            console.log('current value:' + this.i);
        },
        set : function( val ) {
            this.i = val;
        },
        run : function() {
            console.log('running');
        },
        jump: function(){
            console.log('jumping');
        }
    };
    return {
        facade : function( args ) {
            _private.set(args.val);
            _private.get();
            if ( args.run ) {
                _private.run();
            }
        }
    }
}());

module.facade({run: true, val:10});
// 출력 current value: 10, running
```

지원 메쏘드의 인터페이스를 단순히 반환하는 대신에 API가 더 단순한 것을 반환하면서 동일한 동작의 실제 구현을 완전히 숨길 수 있는 상황에서 그것은 효과적인 모듈 패턴의 변형이다. 이것은 최종 사용자가 경험하는 것은 설정을 전달하는 단순화된 API( 우리의 경우, 단한나의 메쏘드 추상화가 노출되었다 )가 전부인 반면, 뒤에서 수행되는 로직이 필요한 만큼 복잡해지게 한다. 이것이 쉽게 사용할 수 있는 API를 제공하는 아름다운 방법이다.

즉, 단순화하기 위해서 AMD 호환되는 퍼사드 구현은 프록시와 더 유사하게 동작할 것이다. 모듈은 중개자의 `publicsh()`와 `subscribe()` 메쏘드를 접근하여 퍼사드를 통해 직접 통신하겠지만, 중개자를 직접 건드리지는 못한다. 이것은 퍼사드가 어플리케이션 수준에서 구독과 발행의 검증을 하게 해준다.

우리가 ( 아래에서 보듯이 ) 허용되었는지 아닌지를 알기 위해 권한 설정을 통해 구동을 검증하는 단순하지만 유연한 권한 검증기를 구현하도록 하게도 해준다.


```javascript
define([ '../aura/mediator' , '../aura/permissions' ], function (mediator, permissions) {

    var facade = facade || {};

    facade.subscribe = function(subscriber, channel, callback){

        // 주의: 권한 및 안전을 제어하는 것은 여기에서 부수적인 것이다
        // 중개자를 직접 사용하기 위해서만
	// 권한 체크는 제거될 수 있다.

        if(permissions.validate(subscriber, channel)){
            mediator.subscribe( channel, callback );
        }
    }

    facade.publish = function(channel){
        mediator.publish( channel );
    }
    return facade;

});
```

**권한**

`aura/permissions.js`에 나타난다.

우리의 간단한 권한 설정에서, 우리는 명확한지 아닌지 만들어낸 구독 요청을 비교하도록 한다. 이것은 어플리케이션을 위한 유연한 보안 계층을 적용한다.

이것이 어떻게 동작하는지 가시적으로 보기 위해서, permissions -> renderDone -> todoCounter를 false가 되도록 변경하는 것을 생각해보자. 이것은 ( 그 이벤트 통지를 구독하지 않도록 하기 때문에 ) 어플리케이션이 남겨진 할일 항목들을 위한 카운트 컴포넌트를 렌더링하거나 보여주는 기능을 완전히 비활성화할 것이다. 하지만 할일 앱의 나머지 부분은 여전히 문제없이 사용된다.

그것은 어플리케이션 보안을 위해 매운 무건은 예제이지만, 많은 가시적인 위젯을 가진 큰 앱에서 얼마나 강력한지 상상해보라.

```javascript
define([], function () {

    // 권한

    // 권한 구조는 그것이 명확하게 되기
    // 이전에 구독을 비교한다. 이것은
    // 어플리케이션을 위한 유연한
    // 보안을 적용한다.

    var permissions = {

        newContentAvailable: {
            contentUpdater:true
        },

        endContentEditing:{
            todoSaver:true
        },

        beginContentEditing:{
            editFocus:true
        },

        addingNewTodo:{
            todoTooltip:true
        },

        clearContent:{
            garbageCollector:true
        },

        renderDone:{
            todoCounter:true //switch to false to see what happens :)
        },

        destroyContent:{
            todoRemover:true
        },

        createWhenEntered:{
            keyboardManager:true
        }

    };

    permissions.validate = function(subscriber, channel){
        var test = permissions[channel][subscriber];
        return test===undefined? false: test;
    };

    return permissions;

});
```



**구독자**

`subscribers.js`에 나타난다.

구독자 '모듈'은 퍼사드를 통해 중개자에와 다시 통신하고 특정 이름의 이벤트가 발행될 때 동작을 수행한다.

예를들어, 사용자가 할일 항목을 위해 몇개의 텍스트를 입력하고 '엔터'를 누를 때, 어플리케이션은 두가지를 말하는 통지를 발행한다: a) 새로운 할일 항목이 사용 가능하고 b) 새로운 항목의 텍스트 내용은 X이다.  원하는 것 무엇이든 이 정보로 하는 것은 어플리케이션의 나머지에 남겨진 것이다.

주로 발행/구독을 사용하는 Backbone 어플리케이션을 갱신하기 위해서 당신이 결국 해야 하는 많은 작업은 특정 뷰내의 의존성 높은 로직을 반응하는 뷰 외부의 모듈로 옮기는 것이다.

예제로 `todoSaver`를 봐라 - 그 기능은 'newContentAvailable'이라고 불리는 `notificationName`이 구동되면 새로운 할일 항목을 모델에 저장하는 것이다. 당신이 마지막 예제 코드에서 권한 구조를 보았다면, 'newContentAvailable'이 거기 있다는 것을 알아챘을 것이다. 내가 구독자가 통지를 구독하는 것을 막고 싶으면, 단순히 설정값을 `false`로 지정한다.

다시, 이것은 권한 구조를 얼마나 진보시키는가에 대한 엄청난 단순화이지만, 어플리케이션의 어떤 부분이 언제라도 특정 모듈에 의해 접근될 수 있게 하거나 막는 것을 제어하는 확실한 방법중 하나이다.

```javascript
define(['jquery', 'underscore', 'aura/facade'],
function ($, _, facade) {

    // 뷰에 대한 구독 '모듈'. 이것들은 
    // facade.subscribe( subscriberName, notificationName , callBack )같은 형태를 취한다.

    // 최근 할일 내용으로 뷰를 갱신한다.
    // 구독대상: newContentAvailable

    facade.subscribe('contentUpdater', 'newContentAvailable', function (context) {
        var content = context.model.get('content');
        context.$('.todo-content').text(content);
        context.input = context.$('.todo-input');
        context.input.bind('blur', context.close);
        context.input.val(content);
    });


    // 사용자가 편집을 끝냈을 때 모델을 저장한다.
    // 구독대상: endContentEditing
    facade.subscribe('todoSaver','endContentEditing', function (context) {
        try {
            context.model.save({
                content: context.input.val()
            });
            context.$el.removeClass('editing');
        } catch (e) {
            //console.log(e);
        }
    });


    // 사용자가 더이상 할일을 필요로 하지 않을 때 삭제한다.
    // 구독대상: destroyContent
    facade.subscribe('todoRemover','destroyContent', function (context) {
        try {
            context.model.clear();
        } catch (e) {
            //console.log(e);
        }
    });


    // 사용자가 새로운 항목을 추가할 때, 툴팁을 보여준다.
    // 구독대상: addingNewTodo
    facade.subscribe('todoTooltip','addingNewTodo', function (context, todo) {
        var tooltip = context.$('.ui-tooltip-top');
        var val = context.input.val();
        tooltip.fadeOut();
        if (context.tooltipTimeout) clearTimeout(context.tooltipTimeout);
        if (val == '' || val == context.input.attr('placeholder')) return;
        var show = function () {
                tooltip.show().fadeIn();
            };
        context.tooltipTimeout = _.delay(show, 1000);
    });


    // 내용 편집으로 모드를 바꾸면 편집 UI로 갱신한다.
    // 구독대상: beginContentEditing
    facade.subscribe('editFocus','beginContentEditing', function (context) {
        context.$el.addClass('editing');
        context.input.focus();
    });


    // 새로운 할일 항목을 생성한다
    // 구독대상: createWhenEntered
    facade.subscribe('keyboardManager','createWhenEntered', function (context, e, todos) {
        if (e.keyCode != 13) return;
        todos.create(context.newAttributes());
        context.input.val('');
    });



    // 할일과 남아있는 항목 계수기
    // 구독대상: renderDone
    facade.subscribe('todoCounter','renderDone', function (context, Todos) {
        var done = Todos.done().length;
        context.$('#todo-stats').html(context.statsTemplate({
            total: Todos.length,
            done: Todos.done().length,
            remaining: Todos.remaining().length
        }));
    });


    // clearContent가 구동될 때, 완료 할일 모두를 지운다
    // 구독대상: clearContent
    facade.subscribe('garbageCollector','clearContent', function (Todos) {
        _.each(Todos.done(), function (todo) {
            todo.clear();
        });
    });


});
```

이것이 이 센션에 대한 모두이다. 당신이 다룬 개념에 대해 호기심이 일어난다면, jQuery Summit의 대규모 JS에 대한 내 [슬라이드](http://addyosmani.com/blog/large-scale-javascript-application-architecture/)나 그 주제에 대한 좀더 긴 [글](http://addyosmani.com/largescalejavascript)을 보길 고려해라.


## Backbone.js의 페이지 요청과 컬렉션

페이징은 우리가 웹상에서 쉽게 발견하는 풀어야만 하는 흔한 문제이다. 서버쪽의 API와 그것을 사용하는 자바스크립트가 많이 포함된 클라이언트를 만들 때, 매우 그러할 것이다.

이 주제에서, 우리는 Backbone.js를 위해 작성된 **페이징 컴포넌트**들을 경험해 볼 것이다. 그것은 당신이 이 분제를 해결해야만 하는 어플리케이션 작업을 한다면 유용할 것이다. 그것들은 [Backbone.Paginator](http://github.com/addyosmani/backbone.paginator)라 불리는 확장의 일부분이다.

Backbone.js와 같은 구조적인 프레임워크로 작업할 때, 동작하길 바라는 세가지 종류의 페이징이 있다:

**서비스 계층의 요청(API)** - 예를 들면 'Brendan' 이라는 단어가 포함된 결과에 대한 쿼리 - 만일 5000개의 결과가 유효하지만 ( 이동할 수 있는 250개의 결과 페이지는 놓아둔 채 ) 페이지당 20개의 결과만 보여준다면.

이 문제는 실제로 UI에서 사용자의 검색 설정에 기초해서 바뀌는 ( 예를들어 sort, query, order 와 같은 ) 다른 URL 인자의 퍼시스턴스를 유지하는 것과 같은 것 이상의 것을 다룬다. 페이징까지 뷰를 가로채는 깔끔한 방법을 생각해야만 하기 때문에 ( 예를 들어, 처음으로, 마지막으로, 다음으로, 첫번째, 두번째, 세번째 같은 ) 페이지 간에 쉽게 이동도 하고 페이지당 보여지는 결과의 수같은 것도 관리할 수 있다.

**반환된 데이타의 더 클라이언트 치중된 페이징** - 예를들어 100개의 결과를 포함하는 JSON 응답을 반환한다. 사용자에게 100개를 보여주기 보다는 브라우져에서 이동할 수 있는 UI와 함께 결과중에서 20개만 보여준다.

요청 문제와 유사하게 클라이언트 페이징은 ( 다음, 이전, 첫번째, 두번째, 세번째같은 ) 재이동, 정렬, 순서, 페이지동 보이는 결과수의 변경에 문제가 있을 수 있다.

**무한 결과** - 페이스 북같은 서비스에서, 숫자에 기반한 페이징 개념은 '더 읽기'나 '더 보기' 버튼으로 대체된다. 이것을 구동하는 것은 보통 N개의 결과 다음 '페이지'를 조회하는 것이지만, 이전에 로드된 결과를 대체하는 것이 아니라 대신 그것에 단순히 추가하는 것이다.

각 새로운 조회를 대체하기 보다는 뷰에 그 결과를 단순히 추가하는 요청 페이지 관리자는 효율적인 '무한' 페이지 관리자이다.

**이제 우리가 외부에서 얻을 것이 무엇인지 정확히 보자:**

*페이징은 Backbone.js를 사용해서 데이타의 컬렉션을 페이지 수를 매기는 독립적인 컴포넌트이다. 그것은 서버로의 요청( 예를들면 API )을 페이징하는 것을 도와주는 해결책과 우리가 N개의 결과 컬렉션을 뷰 안에서 M개의 페이지로 더 페이징하고 싶을 때 한번의 데이타 로드를 페이지로 나누는 해결책 모두를 제공하는 것이 목적이다. *


### 페이지 관리자의 조각

Backbone.Paginator는 주요 페이징 컴포넌트를 지원한다:

* **Backbone.Paginator.requestPager**: 클라이언트와 서버쪽 API 사이에 페이징 요청을 위한 것이다
* **Backbone.Paginator.clientPager**: 서버에서 반환된 데이타를 UI를 통해 더 페이지하고 싶을 때를 위한 것이다. ( 예를들어 60개의 결과가 반환되었을 때 20개씩 3개의 페이지로 페이지를 메기는 경우 )


### 실제 예제

아래에 Netflix API를 사용한 두 페이징 컴포넌트의 실제 미리보기가 있다. 이 예제를 더 시험해 보기 위해서 저장소를 복제하라.

* [Backbone.Paginator.requestPager()](http://addyosmani.github.com/backbone.paginator/examples/netflix-request-paging/index.html)
* [Backbone.Paginator.clientPager()](http://addyosmani.github.com/backbone.paginator/examples/netflix-client-paging/index.html)
* [Infinite Pagination (Backbone.Paginator.requestPager())](http://addyosmani.github.com/backbone.paginator/examples/netflix-infinite-paging/index.html)
* [Diacritic Plugin](http://addyosmani.github.com/backbone.paginator/examples/google-diacritic/index.html)

### Paginator.requestPager

이 섹션에서 우리는 requestPager를 사용해서 실제로 돌려볼 것이다.

#### 1. 새로운 페이징되는 컬렉션을 생성한다

우선, 우리는 아래와 같이 `Backbone.Paginator.requestPager()`를 사용하는 새로운 페이징되는 컬렉션을 만든다.

```javascript
var PaginatedCollection = Backbone.Paginator.requestPager.extend({
```

#### 2: 보통때와 같이 컬렉션을 위한 모델을 지정한다.

그리고나서 컬렉션 안에, 보통때처럼 데이타를 제공하는 서비스( 예를들어 Netflix API )를 위한 URL ( 혹은 기본 URL )밑에 이 컬렉션으로 사용되는 모델을 지정한다.

```javascript
        model: model,
```

#### 3. 기본 URL과 요청의 종류를 설정한다.

우리는 기본 URL을 설정해야만 한다. 요청의 `type`는 기본적으로 `GET`이고, `dataType`은 다른 도메인의 요청도 가능하도록 `jsonp`이다.

```javascript
    paginator_core: {
      // 요청의 종류( 기본적으로 GET )
      type: 'GET',

      // 응답의 종류( 기본적으로 jsonp )
      dataType: 'jsonp',

      // 서비스에 대한 URL( 혹은 기본 URL )
      url: 'http://odata.netflix.com/Catalog/People(49446)/TitlesActedIn?'
    },
```

#### 4. 라이브러리가 결과를 어떻게 보여줄지 설정한다.

우리는 라이브러리에게 페이지당 얼마나 많은 항목을 보여줄지 같은 것들을 알려줘야만 한다...

```javascript
    paginator_ui: {
      // API가 접근할 수 있는 가장 낮은 페이지 번호
      firstPage: 0,

      // 페이지 관리자가 시작할 페이지
      // ( 페이지 관리자가 있을 실제 페이지이기도 하다 )
      currentPage: 0,

      // 페이지동 얼마나 많은 항목을 보여줄지
      perPage: 3,

      // 사용하는 API나 서비스가 전체 페이지 수를
      // 알려주지 않는 경우의 질의에 대한
      // 기본 총 페이지 수
      // 서비스가 total을 반환하지 않는 경우에 10이 기본이다.
      totalPages: 10
    },
```

#### 5. 서버에 전달하고 싶은 인자를 설정한다.

대부분의 경우에 기본 URL로만 충분치 않기 때문에, 서버에 더 많은 인자를 전달할 수 있다.
하드코딩된 값 대신에 함수를 사용할 수 있고, `paginator_ui`에 지정한 값을 참조할 수도 있다는 것을 알아둬라.

```javascript
    server_api: {
      // 요청에 대한 질의 항목
      '$filter': '',

      // 요청( 페이지 )당 반환된는 항목의 수
      '$top': function() { return this.perPage },

      // 필요에 따라 바꾸기 위해 요청이 건너뛸 결과의 수
      // Netflix API의 경우, 페이지마다 page * number 수만큼의
      // 결과를 건너뛰어야 할 필요가 있다.
      '$skip': function() { return this.currentPage * this.perPage },

      // 정렬할 항목
      '$orderby': 'ReleaseYear',

      // 요청 결과의 받고 싶은 형태
      '$format': 'json',

      // 사용자 인자
      '$inlinecount': 'allpages',
      '$callback': 'callback'
    },
```

#### 6. 마지막으로, Collection.parse()를 설정하면 끝이다.

해야할 마지막 일은 컬렉션의 `parse()` 메쏘드를 설정하는 것이다. 우리는 컬렉션에 적용될 데이타를 포함하는 JSON응답의 정상적인 부분을 반환하게 하고 싶다. 그것은 아래의 ( Netflix API를 위한 ) `response.d.results`과 같다.

당신은 `this.totalPages`가 API에 의해 반환된 전체 페이지 수로 설정되는 것을 알아차렸을 지도 모른다. 이것은 UI에서 명확히 보여주기 위해서 우리가 현재나 마지막 요청에 대해 유용한 최대 ( 결과 ) 페이지 수를 정의하게 해준다. 그것은 또한 우리가 클릭 즉 '다음' 버튼이 요청을 할지 안할지에 대해 영향을 주기도 한다.

```javascript
        parse: function (response) {
            // 결과가 어떻게 구조화되어있는지에 따라 바뀌어야만 한다
	    // ( 예를들어 d.results는 Netflix 에서 정한 것이다 )
            var tags = response.d.results;
            // 보통은 this.totalPages는 response.d.__count과 같지만
            // 이 특정 NetFlix 요청은 검색에 대한 전체 항목수만 반환하기
	    // 때문에, 우리는 나누기를 해야 한다.
            this.totalPages = Math.floor(response.d.__count / this.perPage);
            return tags;
        }
    });

});
```

#### 편의 메쏘드:

편의를 위해, 다음 메쏘드가 `requestPager`와 상호작용하는 뷰에서 사용 가능하다:

* **Collection.goTo( n, options )** - 특정 페이지로 이동
* **Collection.requestNextPage( options )** - 다음 페이지로 이동
* **Collection.requestPreviousPage( options )** - 이전 페이지로 이동
* **Collection.howManyPer( n )** - 페이지당 보여지는 항목의 수 지정

**requestPager** 컬렉션의 메쏘드들 `.goTo()`, `.requestNextPage()`, `.requestPreviousPage()`는 모두 원 [Backbone Collection.fetch() method](http://documentcloud.github.com/backbone/#Collection-fetch)의 확장이다. 그렇기 때문에, 그것들 모두 같은 설정 객체를 인자로 가질 수 있다.

이 설정 객체는 서버 응답 후에 실행하기 위한 함수를 전달하기 위한 `success`와 `error` 인자를 사용할 수 있다.

```javascript
Collection.goTo(n, {
  success: function( collection, response ) {
    // 새버 요청이 성공하면 호출된다
  },
  error: function( collection, response ) {
    // 서바 요청이 실패하면 호출된다
  }
});
```

콜백을 관리하기 위해, 우리는 콜백을 관리하는 메쏘드들에 의해 반환되는 [jqXHR](http://api.jquery.com/jQuery.ajax/#jqXHR)도 사용할 수 있다.

```javascript
Collection
  .requestNextPage()
  .done(function( data, textStatus, jqXHR ) {
    // 서버 요청이 성공하면 호출된다
  })
  .fail(function( data, textStatus, jqXHR ) {
    // 서버 요청이 실패하면 호출된다
  })
  .always(function( data, textStatus, jqXHR ) {
    // 서버 요청이 완료된 후 어떤것을 한다
  });
});
```

현재 컬렉션의 내용을 대체하는 대신에 현재 컬렉션에 들어온 모델을 추가하고 싶으면, 이 메쏘드에 설정으로 `{add: true}`을 전달해라.

```javascript
Collection.requestPreviousPage({ add: true });
```

### Paginator.clientPager

`clientPager`는 설정값이 UI 수준에서 이미 반환된 데이타의 페이징에 영향을 준다는 것만 제외하면 `requestPager`와 유사하게 동작한다. ( 아직 ) 보이지는 않지만 `clientPager`와 엮인 더 많은 UI 로직이 있다. 이 예제는 'views/clientPagination.js'에서 볼 수 있다.

#### 1. 모델과 URL을 사용해서 새로운 페이징되는 컬렉션을 만든다.
우선 `requestPager`로 model을 갖는 새로운 페이징되는 `Backbone.Paginator.clientPager` 컬렉션을 만든다:

```javascript
    var PaginatedCollection = Backbone.Paginator.clientPager.extend({

        model: model,
```

#### 2. 기본 URL과 요청 종류를 설정한다.

우리는 기본 URL을 설정해야만 한다. 요청의 `type`는 기본적으로 `GET`이고, `dataType`은 다른 도메인의 요청도 가능하도록 `jsonp`이다.

```javascript
    paginator_core: {
      // 요청의 종류( 기본적으로 GET )
      type: 'GET',

      // 응답의 종류( 기본적으로 jsonp )
      dataType: 'jsonp',

      // 서비스에 대한 URL( 혹은 기본 URL )
      url: 'http://odata.netflix.com/v2/Catalog/Titles?&'
    },
```

#### 3. 라이브러리가 결과를 어떻게 보여줄지 설정한다.

우리는 라이브러리에게 페이지당 얼마나 많은 항목을 보여줄지 같은 것들을 알려줘야만 한다...

```javascript
    paginator_ui: {
      // API가 접근할 수 있는 가장 낮은 페이지 번호
      firstPage: 1,

      // 페이지 관리자가 시작할 페이지
      // ( 페이지 관리자가 있을 실제 페이지이기도 하다 )
      currentPage: 1,

      // 페이지동 얼마나 많은 항목을 보여줄지
      perPage: 3,

      // 사용하는 API나 서비스가 전체 페이지 수를
      // 알려주지 않는 경우의 질의에 대한
      // 기본 총 페이지 수
      // 서비스가 total을 반환하지 않는 경우에 10이 기본이다.
      totalPages: 10
    },
```

#### 4. 서버에 전달하고 싶은 인자를 설정한다.

대부분의 경우에 기본 URL로만 충분치 않기 때문에, 서버에 더 많은 인자를 전달할 수 있다.
하드코딩된 값 대신에 함수를 사용할 수 있고, `paginator_ui`에 지정한 값을 참조할 수도 있다는 것을 알아둬라.

```javascript
    server_api: {
      // 요청에 대한 질의 항목
      '$filter': 'substringof(\'america\',Name)',

      // 요청( 페이지 )당 반환된는 항목의 수
      '$top': function() { return this.perPage },

      // 필요에 따라 바꾸기 위해 요청이 건너뛸 결과의 수
      // Netflix API의 경우, 페이지마다 page * number 수만큼의
      // 결과를 건너뛰어야 할 필요가 있다.
      '$skip': function() { return this.currentPage * this.perPage },

      // 정렬할 항목
      '$orderby': 'ReleaseYear',

      // 요청 결과의 받고 싶은 형태
      '$format': 'json',

      // 사용자 인자
      '$inlinecount': 'allpages',
      '$callback': 'callback'
    },
```

#### 5. 마지막으로, Collection.parse()를 설정하면 끝이다.

그리고 마지막으로 우리는 `parse()` 메쏘드가 있다. 그것은 이 경우에 UI에서 데이타를 페이징하기 위한 자체적인 전체 페이지 수를 갖고 있기 때문에 서버에서 가용한 총 결과 페이지수에 관심이 없다. 

```javascript
    parse: function (response) {
            var tags = response.d.results;
            return tags;
        }

    });
```

#### 편의 메쏘드:

언급한 대로, 뷰가 UI 페이징 데이타를 이동하는 많은 편의 메쏘드를 가로챈다. `clientPager`을 위한 것은 다음과 같다:

* **Collection.goTo(n)** - 특정 페이지로 이동
* **Collection.previousPage()** - 다음 페이지로 이동
* **Collection.nextPage()** - 이전 페이지로 이동
* **Collection.howManyPer(n)** - 페이지당 보여지는 항목의 수 지정
* **Collection.setSort(sortBy, sortDirection)** - 현재 뷰의 정렬을 갱신. 숫자( 문자열로 저장되어 있더라도 )를 정렬하려고 하면, 정렬은 자동으로 감지해서 잘 동작할 것이다.
* **Collection.setFilter(filterFields, filterWords)** - 현재 뷰의 필더. 필터 기능은 순서없이 여러 단어를 지원하기 때문에 기본적으로 전체 문제 검색 기능을 가지고 있다. 또한, 당신이 모델의 한 항목이나 항목의 배열을 전달할 수 있고, 그 모두는 걸러질 것이다. 마지막 옵션은 비교 메쏘드와 규칙을 포함하는 객체를 전달하기 위한 것이다. 현재는 ```levenshtein``` 메쏘드만 사용가능하다.

```javascript
  this.collection.setFilter(
    {'Name': {cmp_method: 'levenshtein', max_distance: 7}}
    , 'Amreican P' // 'r'과 'e'가 바꿔었고 'Pie'의 'P'에 주의해라
  );
```

플러그인이 ```useLevenshteinPlugin``` 변수를 사용해서 로드되고 활성화된다는 점도 주의해라.

마지막으로 중요한 것: Levenshtein 비교 동작은 문자열 사이의 ```거리```를 반환한다. 그것이 긴 문자열 *검색*을 하게 해주지는 않는다.

두 문자열 사이의 거리는 문자열이 같아지기 위해 추가되거나 삭제되거나 왼쪽 혹은 오른쪽으로 이동한 글자의 숫자를 의미한다.

"This is a test that could show something"에 대해서 "Something" 비교하는 것은 32를 반환한다는 것을 의미하는데, 그것은 "Something"와 "ABCDEFG"의 비교( 9 )보다 크다.

( 제목, 이름 등등 같은 ) 짧은 문장에서만 levenshtein을 사용해라.

* **Collection.doFakeFilter(filterFields, filterWords)** - ```Collection.setFilter```을 가짜로 호출한 뒤의 모델의 수를 반환한다.

* **Collection.setFieldFilter(rules)** - 인자로 전달한 `rules`에 따라 각 모델의 값들을 거른다. 예제: 당신은 '발행 연도'와 '작가'를 가진 책의 컬렉션을 가지고 있다. 당신은 1999년과 2003년 사이에 발행된 책들만 거를 수 있다. 그리고 나서 이들 책을 'A'로 시작하는 이름을 가진 작가들만 거르는 또다른 `rule`을 추가할 수 있다. 가능한 규칙: function, required, min, max, range, minLength, maxLength, rangeLength, oneOf, equalTo, pattern.


```javascript

  my_collection.setFieldFilter([
    {field: 'release_year', type: 'range', value: {min: '1999', max: '2003'}},
    {field: 'author', type: 'pattern', value: new RegExp('A*', 'igm')}
  ]);

  //규칙:
  //
  //var my_var = 'green';
  //
  //{field: 'color', type: 'equalTo', value: my_var}
  //{field: 'color', type: 'function', value: function(field_value){ return field_value == my_var; } }
  //{field: 'color', type: 'required'}
  //{field: 'number_of_colors', type: 'min', value: '2'}
  //{field: 'number_of_colors', type: 'max', value: '4'}
  //{field: 'number_of_colors', type: 'range', value: {min: '2', max: '4'} }
  //{field: 'color_name', type: 'minLength', value: '4'}
  //{field: 'color_name', type: 'maxLength', value: '6'}
  //{field: 'color_name', type: 'rangeLength', value: {min: '4', max: '6'}}
  //{field: 'color_name', type: 'oneOf', value: ['green', 'yellow']}
  //{field: 'color_name', type: 'pattern', value: new RegExp('gre*', 'ig')}

```

* **Collection.doFakeFieldFilter(rules)** - ```Collection.setFieldFilter```을 가짜로 호출한 뒤 모델의 수를 반환한다.

#### 구현에 관한 주요점:

당신은 페이지 관리자의 실제 상태를 보여주는 ```뷰```에서 몇몇 변수를 사용할 수 있다.

```totalUnfilteredRecords``` - 어떤 식으로든 걸러진 전체 항목까지 포함한 항목의 수를 포함한다.( ```clientPager``` 에서만 사용가능 )

```totalRecords``` - 항목의 수를 포함한다.

```currentPage``` - 페이지 관리자가 있는 실제 페이지.

```perPage``` - 페이지 관리자가 페이지마다 보여주는 항목의 수.

```totalPages``` - 전체 페이지 수.

```startRecord``` - 현재 페이지에서 보여지는 첫번째 항목의 위치( 예를 들면 2000개의 항목에서 41에서 50 ) ( ```clientPager``` 에서만 사용가능 )

```endRecord``` - 현재 페이지에서 보여지는 마지막 항목의 위치( 예를 들면 2000개의 항목에서 41에서 50 ) ( ```clientPager``` 에서만 사용가능 )

### 플러그인

**Diacritic.js**

(ă,ş,ţ 등등 같은) 발음 기호를 가장 근접한 문자로 바꿔주는 Backbone.Paginator을 위한 플러그인. 이것은 필터링에 특히 유용하다.

플러그인을 활성화하기 위해서, 아래의 예제에서 보듯이 `this.useDiacriticsPlugin`를 true로 지정해라:

```javascript
Paginator.clientPager = Backbone.Collection.extend({

    // 정렬, 혹은 필터링할 때( 또는 동시에 사용할 때 ), 사용하는 기본값Default values used when sorting and/or filtering.
    initialize: function(){
      this.useDiacriticsPlugin = true; // 가능하면 diacritics 플러그인을 사용한다.
    ...
```

 [1]: http://github.com/addyosmani/backbone.paginator
 [2]: http://addyosmani.github.com/backbone.paginator/
 [3]: http://addyosmani.github.com/backbone.paginator/examples/netflix-request-paging/index.html
 [4]: http://addyosmani.github.com/backbone.paginator/examples/netflix-client-paging/index.html
 [5]: http://addyosmani.github.com/backbone.paginator/examples/netflix-infinite-paging/index.html
 [6]: http://github.com/addyosmani/backbone.paginator/issues
 [7]: https://github.com/cowboy/grunt


# 모바일 어플리케이션

## Backbone & jQuery Mobile

### 라우팅 충돌 해결

개발자가 jQuery Mobile로 Backbone 어플리케이션을 만들 때, 만나는 전형적인 첫번째 주요 관문은 두 프레임워크가 어플리케이션 이동을 제어하는 방법에 있어서 자신만의 방안을 가지고 있다는 것이다.

Backbone의 라우터는 `Backbone.Router`를 통해 사용자가 이동 지점을 정의하는 명시적인 방식을 제안하는 반면, jQuery Mobile은 분리된 '페이지들'이나 동일 문서의 뷰를 참조하기 위한 URL 해쉬 조각의 사용을 권장한다. jQuery Mobile도 '#photo/id'에서 가리키는 링크가 실제로 하는 것에 대한 많은 내부 프레임워크 혼동이 될 수도 있는 XHR 호출을 통해 링크의 외부 내용을 자동적으로 가져오는 것을 지원한다.

이 문제를 회피하기 위해 이전에 제안된 몇가지 해결책은 직접 수정된 Backbone이나 jQuery Mobile을 포함하는 것이다. 나는 새로운 배포본이 반영되었을 때, 프레임워크를 직접 수정해야만 하기 때문에 이런 방식을 선호하지 않는다.

이 문제를 다르게 해결하려고 하는 [jQueryMobile 라우터](https://github.com/azicchetti/jquerymobile-router)도 있지만, 나는 내가 제안하는 해결책이 더 단순하면서 두 프레임워크가 서로 확장할 필요도 없이 평화롭게 양립할 수 있게 해준다고 생각한다. 우리가 추구하는 것은 해쉬 변경을 처리하기 위해 하나의 프레임워크( 예를 들어 `Backbone.Router` )에 완전히 의존하기 위해서 다른 하나의 프레임워크가 해쉬 변경을 감시하지 않도록 하는 방식이다.

jQuery Mobile을 사용해서 다음 설정을 적용한다:

```javascript
$.mobile.hashListeningEnabled = false;
```

다른 코드가 초기화되기 전에 하라.

나는 정식 문서에는 없지는 jQuery Mobile 커밋을 통해 발견한 이 방법을 알아내고 지금에 더 자세한 것은 여기 http://jquerymobile.com/test/docs/api/globalconfig.html에서 찾을 수 있어서 기쁘다.

생각다는 다음 질문은 만일 jQuery Mobile이 URL 해쉬 변경을 감시하지 못하도록 막으면 지원되는 내장된 이동과 효과를 사용해서 문서내의 다른 섹션으로 이동할 수 있는 장점을 어떻게 살릴 것인가? 이다. 좋은 질문이다. 이것은 단순히 다음과 같이 `$.mobile.changePage()`를 호출함으로써 해결할 수 있다:

```javascript
var url = '#about',
    effect = 'slideup',
    reverse = false,
    changeHash = false;

$.mobile.changePage( url , { transition: effect}, reverse, changeHash );
```

위의 예제에서, `url`은 이동할 URL이나 해쉬 아이디를 참조할 수 있고, `effect`는 페이지가 움직이는 단순한 이동이고, 마지막 두 인자는 이동( `reverse` ) 방향과 주소창에 해쉬가 갱신( `changeHash` )되어야 하는지 아닌지 이다. 후자의 관점에서, 나는 보통 해쉬 갱신의 두 원본 관리를 피하기 위해 false를 설정하지만 당신이 편하다면 자유로이 true로 설정해도 된다.

**주의:** jQuery Mobile Router 플르그인을 Backbone과 함께 돌리기 위한 방법을 알아보기 위해 같이 해야할 작업을 위해, [https://github.com/Filirom1/jquery-mobile-backbone-requirejs](https://github.com/Filirom1/jquery-mobile-backbone-requirejs)을 확인하고 싶을지도 모르겠다.


### 연습: jQuery Mobile을 사용한 Backbone, Require.js/AMD 앱

**주의:** 이 연습을 위한 코드는 `practicals/modular-mobile-app`에서 찾을 수 있다.

### 시작하기

일단 당신이 [Backbone fundamentals](http://msdn.microsoft.com/en-us/scriptjunkie/hh377172.aspx)이 편하게 느껴지면, 만들고 싶은 앱의 대충의 설계도를 모으고 어플리케이션 구조에 대해 생각해기 시작해라. 이상적으로 당신은 가능한 미래에 앱을 유지보수하기 쉽게 하기 위해 논리적으로 관심을 분리하고 싶다.

**이름공간**

이 어플리케이션을 위해서, 나는 중첩된 이름 공간 패턴을 선택하였다. 정확히 구현하였다면 이것은 앱에서 참조되는 항목들이 뷰인지 다른 모듈인지 그외인지 명확히 구분하게 해준다. 이 초기 구조는 ( 당신이 분리된 파일로 관리하는 것을 선호하지 않는다면 ) 어플리케이션 기본도 포함하고 있는 올바른 것이다.

```javascript
window.mobileSearch = window.mobileSearch || {
    views: {
        appview: new AppView()
    },
    routers:{
        workspace:new Workspace()
    },
    utils: utils,
    defaults: {
        resultsPerPage: 16,
        safeSearch: 2,
        maxDate:'',
        minDate:'01/01/1970'
    }
}
```

**모델**

flickly 어플리케이션에는 최소한 모델이 되어야만하는 두개의 독특한 데이타 타입이 있다 - 검색 결과와 개별 사진, 둘다 사진 제목과 같은 추가적인 메타 정보를 포함하고 있다. 당신이 이것을 단순화한다면, 검색 결과는 실제로 적당한 사직 묶음들이기 때문에 어플리케이션은 단지 다음의 것만 필요로 한다:

* 단일 모델( 사진 혹은 '결과' 항목 )
* 검색 결과를 위한 ( 결과 항목들을 포함하는 ) 결과 컬렉션
* 각각의 사진 혹은 하나 이상의 사진들을 위한 ( 하나 이상의 결과 항목을 포함하는 ) 사진 컬렉션

**뷰**

우리가 필요로 하는 뷰는 어플리케이션 뷰, 검색 결과 뷰, 사진 뷰이다. 페이지에 동적인 요소를 필요로 하지 않는 단일 페이지 어플리케이션의 정적 뷰나 페이지( 예를 들면 'about' 페이지 )는 Backbone과 관계없이 문서의 마크업으로 쉽게 작성될 수 있다.

**라우터**

많은 가능한 지점은 신중하게 선택되어야만 한다:

* 기본 검색 질의 `#search/kiwis`
* ( 예를들어 정렬이나 페이징같은 ) 추가적인 인자를 갖는 검색 질의 `#search/kiwis/srelevance/p7`
* 특정 사진을 위한 질의 `#photo/93839`
* 기본 지점( 인자는 전달되지 않음 )


이 안내서는 데모 어플리케이션을 완전히 다루기 위해 간단히 확장될 것이다. 중간에, Backbone과 jQuery Mobile 사이에 이전에 논의했던 라우터 해결법을 보여주는 전체 어플리케이션을 위해서는 practicals 폴더를 보세요.


### jQuery Mobile: 모바일 어플리케이션 개발을 뛰어 넘기

내가 제풍으로 본 jQM 앱의 대다수는 모바일 장치에서 사용자에기 최적의 경험을 주는 것을 목적으로 개발되었다. 프레임워크가 이런 목적을 위해 개발되었다고 가정하면, 기본적으로 잘못된 것은 없지만, 많은 개발자들이 jQM이 jQuery와 다르지 않은 UI 프레임워크라는 것을 잊는다. 그것은 위젯 팩토리를 사용하고 우리가 허용한 것 이상을 위해 사용될 수 있다.

당신이 데스크탑 브라우져에서 Flickly를 연다면, 당신은 Google.com과 비슷한 이미지 검색 UI를 얻을 것이지만, 잠깐동안 페이지상의 컴포넌트( 버튼, 텍스트 입력, 탭 )를 살펴보자. 내가 여전히 모파일 컴포넌트를 테마로 하기 위해서 jQM을 쓰고 있지만, 데스크탑 UI는 모바일 어플리케이션같이 보이지 않는다: 탭, 날짜 선택기, 슬라이더 - 데스크탑 UI의 모든 것은 jQM이 사용자에게 모바일 장치에서 제공하는 것을 재사용하고 있다. 미디어 쿼리 덕분에, 컴포넌트 블럭을 확장하고 또 다른 레이아웃을 제공하면서 데스크탑 UI는 공백을 최적으로 사용할 수 있는 반면 여전히 jQM을 컴포넌트 프레임워크로 사용할 수 있다.

그 장점은 그 특징의 잇점을 가지는 jQuery UI를 따로 가져갈 필요가 없다는 점이다. 최근 ThemeRoller 덕분에 내 컴포넌트는 정확히 내가 원했던 것대로 이쁘게 보이고 앱 사용자들은 다른 모든 것에 대해서 낮은 해상도와 jQM스러운 jQM UI를 가질 수 있다.

여기서 얻을 것은 당신이 ( matchMedia.js등을 사용해서 ) 화면 해상도에 따른 조건적인 스크립트/스타일 로딩의 문제를 ( 이미 ) 겪지 않았다면, 여러장치를 지원하는 컴포넌트 테마를 가지게 하는 더 단순한 방법이 있다는 것을 기억하는 것이다.


# 단위 테스트


## Jasmine을 사용해서 Backbone 어플리케이션을 단위 테스트하기

## 소개

단위 테스트에 대한 한가지 정의는 어플리케이션에서 테스트할 수 있는 코드의 가장 작은 조각을 가지고 코드의 나머지 부분과 분리하고 그것이 예상대로 동작하는지 결정하는 과정이다. 이 섹션에서, 우리는 Pivotal Labs에서 만든 [Jasmine](http://pivotal.github.com/jasmine/) 이라는 인기있는 자바스크립트 테스트 프레임워크를 사용해서 Backbone 어플리케이션을 테스트하는 방법을 볼 것이다.

어플리케이션이 '잘' 테스트되었다고 간주되기 위해서 구분되는 기능은 이상적으로 당신이 돌아가리라고 기대되는 다른 조건에 대해 테스트 되는 자신만의 구분된 단위 테스트를 가져야만 한다. 모든 테스트는 기능이 '완성'되었다고 생각되기 전에 통과해야 한다. 이것은 개발자가 이 변경이 어떤 문제도 야기하지 않는다는 신뢰성을 가지고 코드 단위와 의족성 모두를 수정하게 해준다.

개발자가 sum 함수에 특정값을 전달하는 것이 옳은 결과가 반환되는지 검증하고 싶어한다고 할 때 단위 테스트의 기본 예제이다. 이 책과 관련된 더 많은 예제에 대해서 우리는 사용자가 새로운 할일 항목을 리스트에 추가한 것이 Todos 컬렉션에 특정 타입의 모델을 올바르게 추가하는지를 검증하고 싶다.

현대적인 웹 어플리케이션을 만들 때, 일반적으로 자동화된 단위 테스트를 개발 과정의 일부로 포함하는 것이 가장 좋은 사례로 생각되고 있다. 우리가 이에 대한 해결책으로 Jasmine에 관심을 가지고 있는 반면, QUnit을 포함해서 고려할 만한 수많은 대안들이 있다.

## Jasmine

Jasmine은 자신을 자바스크립트 코드를 위한 행동 주도적인 개발( BDD ) 프레임워크로 묘사한다. 우리는 프레임워크가 어떻게 동작하는지 보기 전에 [BDD](http://en.wikipedia.org/wiki/Behavior_Driven_Development)가 무엇인지 정확히 이해하는 것이 유용하다.

BDD는 소프트웨어의 동작을 테스트하려는 ( BDD의 저작권자인 ) [Dan North](http://dannorth.net/introducing-bdd/)에 의해 처음으로 언급된 차세대 테스트 방법론이다. 차세대는 어자일 과정에서 초기에 많이 헷갈리는 질문에 답해줌으로써 팀이 고품질의 소프트웨어를 배포하도록 하기 위해 도메인 주도 설계( DDD )와 린 소프트웨어 개발의 개념을 합쳐서 나온 것으로 생각된다. 그런 질문은 문서화와 테스팅에 관련된 것을 포함한다.

당신이 만일 BDD에 관한 책을 읽었다면, 'outside-in and pull-based'라는 표현도 좋아할 것이다. 그 이유는 올바른 소프트웨어 솔루션은 a) 시스템의 예상 결과에 집중하고 b) 이 결과를 만들어 냄으로써 작성되도록 하는 린 생산의 pull 특징의 개녕을 빌려온 겄이기 때문이다.

BDD는 보통 프로젝트에 많은 투자자가 있지만 시스템에 비정형적인 한명의 사용자가 없다는 것을 알아차렸다. 이런 다른 그룹들은 다른 방식으로 만들어진 소프트웨어에 영향을 받고 시스템상에서 그들에게 의미있는 품질에 대한 다양한 의견을 가지고 있을 것이다. 소프트웨어가 당신에게 가져다 주는 가치가 무엇이고 언제 그것들이 가치있는지를 이해하는 것이 중요한 이유이다.

마지막으로, BDD는 자동화에 의지한다. 당신이 일단 예상되는 품질을 정의하면, 당신 팀은 일반적으로 만들어지는 솔류션의 기능상 확인하고 예상되는 결과와 비교하고 싶을 것이다. 이 것을 효율적으로 지원하기 위해서, 과정은 자동화되어야만 한다. BDD는 명세에 기반한 테스트의 자동화에 매우 의존하며 Jasmine은 이것을 도와주는 툴이다.

BDD는 개발자와  비기술적인 투자자 모두를 도와준다:


* 풀려는 문제의 모델에 대해 더 잘 이해하고 설명한다
* 개발자가 아닌 사람이 읽을 수 있는 언어로 지원되는 테스트 케이스를 설명한다
* 작성된 기술 코드와 비즈니스에서 말하는 업계 용어의 변역을 최소화하는데 집중한다

이것이 의미하는 것은 개발가가 Jasmine 단위 테스트를 프로젝트 투자자에게 보여줄 수 있고, ( 상위 수준에서 사용되는 일반적인 단어 덕분에 ) 그들은 이상적으로 그 코드가 지원하는 것을 이해할 수 있어야만 한다는 것이다.

개발자는 종종 [TDD](http://en.wikipedia.org/wiki/Test-driven_development)로 알려진 다른 테스트 패러다임과 똑같이 BDD를 구현한다. TDD뒤의 핵심 생각은 다음과 같다:

* 당신 코드가 지원할 것같은 기능을 표현하는 단위 테스트를 작성한다
* 이 테스트가 실패하는 것을 보아라( 그 기능을 지원하는 코드가 아직 작성되지 않았으니까 )
* 테스트가 통과하도록 코드를 작성하라.
* 문제를 해결하고 반복하고 리팩토링해라

이 챕터에서 우리는 Backbone 어플리케이션을 위한 단위 테스트를 작성하기 위해서 BDD( 와 TDD )를 사용할 것이다.

***주의:*** 나는 많은 개발자들이 코드를 작성한 후 코드의 동작을 검증하는 테스트를 작성하는 것을 좋아하기도 하는 것을 알고 있다. 이것도 좋지만, 코드가 문제를 일으킬 수 밖에 없는 동작이 아니라 올바르게 동작하는 것만 테스트하는 위험이 있을 수 있다는 것을 알아둬라.


## 스위트, 명세, 그리고 스파이

Jasmine을 사용할 때, 스위트와 명세를 작성할 것이다. 스위트는 기본적으로 시나리오를 표현하는 반면 명세는 이 시나리오에서 행해질 수 있는 것을 표현한다.

각 명세는 자바스크립트 함수인데, 설명 구문과 함수를 사용해서 ```it()```에 대한 호출로 표현된다. 설명은 특정 코드 조각이 BDD를 표현하고 명심하는 동장을 묘사해야만 한다. 그것은 이상적으로 의미있어야만 한다. 특정 코드 단위의 동작을 묘사하는 설명은 표시되기 기억되어야만 한다. 기본 명세의 예제가 여기있다:

```javascript
it('should be incrementing in value', function(){
    var counter = 0;
    counter++;
});
```

코드 동작에 대한 예상이 지정되기 전까지, 명세 그 자체로는 특별히 유용하지 않다. 예상은 ```expect()``` 함수와 [예상 일치기](https://github.com/pivotal/jasmine/wiki/Matchers) ( 예를들어 ```toEqual()```, ```toBeTruthy()```, ```toContain()```)을 사용해서 정의된다. 예상 일치기를 사용한 새로운 예제는 다음과 같다:

```javascript
it('should be incrementing in value', function(){
    var counter = 0;
    counter++;
    expect(counter).toEqual(1);
});
```

위의 코드는 동작 예상에 ```counter```는 1으로 전달한다. 마지막 줄의 예상을 읽기가 얼마나 쉬운지 보라( 당신은 어떤 설명이 없어도 공감할 것이다 ).

명세는 Jasmine의 ```describe()``` 함수를 사용해서 다시 설명 문자열과 함수를 전달해서 표현하는 대로 스위트로 묶인다. 스위트에 대한 이름이나 설명은 보통 테스트하는 컴포넌트나 모듈에 대한 것이다.

Jasmine은 실행하도록 요청하면 그 명세들의 결과를 보고할 때, 그것을 묶음의 이름으로 사용할 것이다. 예제에 포함된 단순한 스위트는 다음과 같을 것이다:

```javascript
describe('Stats', function(){
    it('can increment a number', function(){
        ...
    });

    it('can subtract a number', function(){
        ...
    });
});
```

스위트도 함수 범위를 공유하기 때문에 명세에서 접근 가능한 describe 블럿 내에서 변수와 함수를 정의하는 것이 가능하다:

```javascript
describe('Stats', function(){
    var counter = 1;

    it('can increment a number', function(){
        // counter는 1이다
        counter = counter + 1;
        expect(counter).toEqual(2);
    });

    it('can subtract a number', function(){
        // counter는 2이다
        counter = counter - 1;
        expect(counter).toEqual(1);
    });
});
```

***주의:*** 스위트는 묘사된 순서로 실행된다. 그것은 어플리케이션의 특정 부분이 먼저 표시되도록 테스트 결과를 보고 싶을 때 알아두면 유용하다.

Jasmine은 **spies**도 지원한다. - 단위 테스트에서 동작을 가상화하고, 가로채고, 흉내내는 방법. 스파이는 우리가 가상화한 행동을 흉내내는 함수로 바꾸는 것이다( 즉, 실제 구현에 독립적으로 테스트한다 ).

아래 예제에서, 우리는 인자가 예상대로 전달되도록 테스트하기 위해 가짜 Todo 함수의 ```setComplete``` 메쏘드를 스파이한다.

```javascript
var Todo = function(){
};

Todo.prototype.setComplete = function (arg){
    return arg;
}

describe('a simple spy', function(){
    it('should spy on an instance method of a Todo', function(){
        var myTodo = new Todo();
        spyOn(myTodo, 'setComplete');
        myTodo.setComplete('foo bar');

        expect(myTodo.setComplete).toHaveBeenCalledWith('foo bar');

        var myTodo2 = new Todo();
        spyOn(myTodo2, 'setComplete');

        expect(myTodo2.setComplete).not.toHaveBeenCalled();

    });
});
```

당신이 스파이를 사용하고 싶은 것이 AJAX 요청같은 어플리케이션의 [비동기적](http://en.wikipedia.org/wiki/Asynchronous_communication) 동작을 테스트하는 것이다. Jasmine은 다음을 지원한다:

* 스파이를 사용해서 AJAX 요청을 가상화하는 테스트를 작성한다. 이것은 우리가 AJAX 요청 전후로 동작하는 코드를 테스트하게 해준다. 반환되는 서버의 응답을 가상화 혹은 속이는 것도 가능하고 이런 종류의 테스트의 장점은 서버로 실제 호출이 없기 때문에 더 빠르다는 것이다.
* 스파이에 의존하지 않고 비동기적으로 테스트한다.

첫번째 형태의 테스트에서, AJAX 요청을 속이는 것과 올바른 URL을 호출하고 제공된 콜백을 실행하는지를 확인하는 것 모두가 가능하다.

```javascript
it('the callback should be executed on success', function () {
    spyOn($, 'ajax').andCallFake(function(options) {
        options.success();
    });

    var callback = jasmine.createSpy();
    getTodo(15, callback);

    expect($.ajax.mostRecentCall.args[0]['url']).toEqual('/todos/15');
    expect(callback).toHaveBeenCalled();
});

function getTodo(id, callback) {
    $.ajax({
        type: 'GET',
        url: '/todos/'' + id,
        dataType: 'json',
        success: callback
    });
}
```

당신이 ```andCallFake()```와 ```toHaveBeenCalled()``` 같은 일치기를 보기 어렵다면, 걱정하지 마라. 이 모든 것은 스파이 특화된 일치기이고, Jasmine[위키](https://github.com/pivotal/jasmine/wiki/Spies)에 문서화되어 있다.

두번째류의 테스트( 비동기 테스트 )에서, 우리는 위의 장점에 더해 Jasmine이 지원하는 세개의 다른 메쏘드 장점을 가질 수 있다:

* runs(function) - 마치 호출되는 것처럼 실행되는 블럭
* waits(timeout) - 다음 블럭이 실행되기까지의 순수 시간
* waitsFor(function, optional message, optional timeout) - 다른 작업이 완료될 때까지 명세를 정지시키는 방법. Jasmine은 제공된 함수가 true를 반환할 때까지 다음 블럭으로 가기 전에서 기다린다.


```javascript
it('should make an actual AJAX request to a server', function () {

    var callback = jasmine.createSpy();
    getTodo(16, callback);

    waitsFor(function() {
        return callback.callCount > 0;
    });

    runs(function() {
        expect(callback).toHaveBeenCalled();
    });
});

function getTodo(id, callback) {
    $.ajax({
        type: 'GET',
        url: 'todos.json',
        dataType: 'json',
        success: callback
    });
}
```

***주의:*** 단위 테스트에서 웹서버로 진짜 요청을 날릴때, 이것은 테스트를 실행할 때의 ( 서버 반응성을 포함해서 많은 요인에 기인해서 ) 큰 속도 저하 가능성이 있다는 것을 기억해 두는 것이 유용하다. 이것이 단위 테스트시 최소화하는 외부 의존성도 도입하기 때문에, 여기에서 사용되는 웹서버가 필요하지 않은 스파이를 선택하길 매우 추천하는 바이다.

## beforeEach과 afterEach()

Jasmine은 또한 각 테스트 전( ```beforeEach()``` )과 후( ```afterEach``` )에 실행될 수 있는 코드를 지정할 수 있도록도 해준다. 이것은 ( 명세에서 필요로 하는 변수들을 초기화하는 것같은 ) 무결한 조건을 유지하는 유용하다. 다음 예제에서, ```beforeEach()```는 명세가 속성을 테스트하는데 사용할 수 있는 새로운 예제 Todo 모델을 생성하는데 사용한다.

```javascript
beforeEach(function(){
   this.todo = new Backbone.Model({
      text: 'Buy some more groceries',
      done: false
   });
});

it('should contain a text value if not the default value', function(){
   expect(this.todo.get('text')).toEqual('Buy some more groceries');
});
```

테스트내의 각 중첩된 ```describe()```는 특정 스위트와 관련된 setup과 teardown 메쏘드를 포함하도록 하는 ```beforeEach()```와 ```afterEach()``` 메쏘드를 가질 수 있다. 우리는 조금 후에 연습에서 ```beforeEach()```를 사용할 것이다.

## 공유 범위

이전 섹션에서 당신은 ```beforeEach()``` 호출에서 ```this.todo``` 변수를 먼저 선언하고 나서 계속해서 ```afterEach()```에서 이것을 사용할 수 있는 것을 알았다. 이것은 공유된 함수 범위로 알려진 Jasmine의 강력한 기능 덕이다. 공유 범위는 선언된 변수( 즉 ```var``` )들은 아니지만 ```this``` 특성이 ( ```runs()```를 포함한 ) 모든 블럭에 공통적이게 해준다.


## 설정

이제 우리는 기본을 살펴보았으니 Jasmine을 다운로드해서 테스트를 작성하기 위한 설정을 해보자.

 Jasmine의 전체 배포판은 정규 배포 페이지에서 [다운로드](http://pivotal.github.com/jasmine/download.html)할 수 있다.

당신은 배포에 추가적으로 SpecRunner.html이라고 불리는 파일이 필요할 것이다. 그것은 https://github.com/pivotal/jasmine/tree/master/lib/jasmine-core/example에서 다운로드하거나 전체 Jasmine [저장소](https://github.com/pivotal/jasmine/zipball/master) 다운로드의 일부에서 받을 수 있다. 또 다른 방법으로 당신은 https://github.com/pivotal/jasmine.git에서 Jasmine 저장소를 ```git clone``` 할 수 있다.

[SpecRunner.html](https://github.com/pivotal/jasmine/blob/master/lib/jasmine-core/example/SpecRunner.html)를 살펴보자:

우선 Jasmine과 결과 보고서를 위해 필요한 CSS를 포함한다:


	<link rel="stylesheet" type="text/css" href="lib/jasmine-1.1.0.rc1/jasmine.css"/>
	<script type="text/javascript" src="lib/jasmine-1.1.0.rc1/jasmine.js"></script>
	<script type="text/javascript" src="lib/jasmine-1.1.0.rc1/jasmine-html.js"></script>


그 다음으로, 예제 테스트 몇개가 포함된다:


	<script type="text/javascript" src="spec/SpecHelper.js"></script>
	<script type="text/javascript" src="spec/PlayerSpec.js"></script>


마지막으로 테스트되는 소스가 있다:


	<script type="text/javascript" src="src/Player.js"></script>
	<script type="text/javascript" src="src/Song.js"></script>


***주의:*** SpecRunner의 이부분 아래는 실제 테스트를 실행하는 것을 담당하는 코드이다. 우리가 이 코드를 수정하는 것을 다루지 않는다고 가정하고, 살펴보는 것은 건너뛸 것이다. 하지만 나는 당신이 [PlayerSpec.js](https://github.com/pivotal/jasmine/blob/master/lib/jasmine-core/example/spec/PlayerSpec.js)와 [SpecHelper.js](https://github.com/pivotal/jasmine/blob/master/lib/jasmine-core/example/spec/SpecHelper.js)를 살펴보길 바란다. 그것들은 최소한의 테스트가 동작하는 방법을 경험하게 해주는 유용한 예제이다.

## Backbone에서의 TDD

Backbone으로 어플리케이션을 개발할 때, 각 코드 모듈 뿐만 아니라 모듈, 뷰, 컬렉션, 라우터 모두를 테스트하는 것이 필요할 수도 있다. 테스트에 TDD 접근법을 가지고 유명한 Backbone [Todo](https://github.com/addyosmani/todomvc/tree/master/todo-example/backbone)을 사용해서 이들 Backbone 컴포넌트를 테스트하는 명세 몇개를 살펴보자. 이 섹션을 위해서 우리는 Larry Myers Backbone Koans 프로젝트의 수정된 버젼을 사용할 것인데, 그것은 `practicals\jasmine-koans` 폴더에 있다.

## 모델

Backboine 모델의 복잡도는 당신 어플리케이션이 무슨일을 하는지에 따라 크게 달라진다. 다음 예제에서 우리는 기본값, 속성, 상태 변경 그리고 검증 규칙을 테스트할 것이다.

우선, ```describe()```을 사용해서 테스트할 모델의 스위트부터 시작하자:

```javascript
describe('Tests for Todo', function() {
```

모델은 이상적으로 속성을 위한 기본값을 가져야만 한다. 이것은 특정 속성값들이 없이도 객체를 생성할 때, 대신 기본값( 예를들어 '' )이 사용되게 해준다. 여기에서 아이디어는 어플리케이션이 예상치 못한 동작없이 모델과 상호동작하도록 하는 것이다.

다음 명세에서, 우리는 전달된 어떤 속성없이 새로운 Todo를 생성하고 나서 ```text```의 값이 무엇인지 한번 알아보는 것이다. 어떤 값도 지정하지 않았기 때문에 기본값 ```''```가 반환될 것을 기대한다.

```javascript
it('Can be created with default values for its attributes.', function() {
    var todo = new Todo();
    expect(todo.get('text')).toBe('');
});
```

모델이 작성되기 전에 이 명세를 테스트한다면, 예상한대로 테스트 실패를 초래할 것이다. 명세가 통과하기 위해 필요한 것은 ```text``` 속성에 대한 기본값이다. 우리는 다음과 같이 Todo 모델안에서 ( 간단히 사용할 ) default로 기본값을 구현할 수 있다:

```javascript

window.Todo = Backbone.Model.extend({

    defaults: {
      text: '',
      done:  false,
      order: 0
    }

```

다음으로, 초기화 후에 이들 속성값을 가져온 내용이 우리가 예상한 내용인 것과 같이 우리는 모델이 지정한 속성을 전달할지 테스트하고 싶다. 여기에서 ```text```에 대한 예상값에 대한 테스트에 추가해서 우리는 다른 기본값도 우리가 예상하던 값인지 테스트도 한다.

```javascript
it('Will set passed attributes on the model instance when created.', function() {
    var todo = new Todo({ text: 'Get oil change for car.' });

    // 우리 Todo에 각 속성에 대해 여기에서 
    // 예상되는 값이 무엇인가?

    expect(todo.get('text')).toBe('Get oil change for car.'');
    expect(todo.get('done')).toBe(false);
    expect(todo.get('order')).toBe(0);
});
```

Backbone 모델은 모델의 상태가 변할 때, 구동되는 model.change() 이벤트를 지원한다. 다음 예제에서 `state`에 의해서 Todo 모델의 속성값을 참조한다. 테스트하는데 상태를 변경이 중요한 이유는 어플리케이션에 상태 의존적인 이벤트가 있을지도 모르게 때문이다. 예를들어 Todo 모델이 갱신되면, 확인창을 보여주고 싶을 수도 있다.

```javascript
it('Fires a custom event when the state changes.', function() {

    var spy = jasmine.createSpy('-change event callback-');

    var todo = new Todo();

    // 상태 변경을 감시하기 위해 어떻게 해야하는가?
    todo.on('change', spy);

    // 강제로 상태를 변경하기 위해 무엇이 필요한가?
    todo.set({ text: 'Get oil change for car.' });

    expect(spy).toHaveBeenCalled();
});
```

어플리케이션에서 사용자( 그리고 다른 모듈 )가 전달한 입력이 '올바른지' 확인하기 위해 모델에 검증 로직을 포함하는 것이 일반적이다. Todo 앱은 무례한 단어가 포함된 경우인지 제공된 문자 입력을 검증하고 싶을지도 모른다. 유사하게 우리가 논리값을 사용해서 Todo 항목의 ```done``` 상태를 저장하면 우리는 임의의 문자열이 아닌 참/거짓 값이 전달되었는지 검증해야만 한다.

다음 명세에서, model.validate()를 실패한 검증이 "error" 이벤트를 구동한다는 사실에 장점이 있다. 이것은 올바르지 않은 입력이 들어왔을 때, 정상적으로 검증이 실패하는지를 테스트하게 해준다.

우리는 다음과 같이 Jasmine의 내장 함수 ```createSpy()```를 사용해서 error 이벤트를 흉내내게하는 errorCallback 스파이를 만든다:

```javascript
it('Can contain custom validation rules, and will trigger an error event on failed validation.', function() {

    var errorCallback = jasmine.createSpy('-error event callback-');

    var todo = new Todo();

    todo.on('error', errorCallback);

    // 검증을 실패하기 위해 할일 특성에 
    // 무엇을 설정해야만 하는가?

    todo.set({done:'a non-integer value'});

    var errorArgs = errorCallback.mostRecentCall.args;

    expect(errorArgs).toBeDefined();
    expect(errorArgs[0]).toBe(todo);
    expect(errorArgs[1]).toBe('Todo.done must be a boolean value.');
});

```

위에서 실패한 테스트가 검증을 지원하도록 하는 코드는 상대적으로 간단하다. 모델에 전달하기 전에 'done' 특성을 가지고 있고 올바른 논리값인지 확인하기 위해서, 우리는 ( Backbone 문서에서 추전한 대로 ) 모델의 validate() 메쏘드를 다시 쓴다.

```javascript
validate: function(attrs) {
    if (attrs.hasOwnProperty('done') && !_.isBoolean(attrs.done)) {
        return 'Todo.done must be a boolean value.';
    }
}
```

우리가 Todo 메쏘드의 최종 코드를 살펴보고 싶으면 아래에서 찾을 수 있다:

```javascript
var NAUGHTY_WORDS = /crap|poop|hell|frogs/gi;

function sanitize(str) {
    return str.replace(NAUGHTY_WORDS, 'rainbows');
}

window.Todo = Backbone.Model.extend({

    defaults: {
      text: '',
      done:  false,
      order: 0
    },

    initialize: function() {
        this.set({text: sanitize(this.get('text'))}, {silent: true});
    },

    validate: function(attrs) {
        if (attrs.hasOwnProperty('done') && !_.isBoolean(attrs.done)) {
            return 'Todo.done must be a boolean value.';
        }
    },

    toggle: function() {
        this.save({done: !this.get('done')});
    }

});
```


## 컬렉션

이제 우리는 Todo 모델에 대한 Backbone 컬렉션( TodoList )를 테스트하는 명세를 정의해야만 한다. 컬렉션은 순서와 필터링 관리를 포함한 일들을 처리하는 많은 목록에 관한 것이다.

컬렉션을 다룰 때 기억해야하는 몇가지 특별한 명세는 다음과 같다:

* 우리가 객체와 배열 모두로 새로운 Todo 모델을 추가할 수 있는지 여부
* 컬렉션의 기본 URL이 우리가 예상하는 값인지 같은 속성을 확인하는 속성 테스트
* ```done:true``` 상태의 항목을 의도적으로 추가하고 컬렉션에서 몇개의 항목이 완료되고 또 남아있는지 확인하기

이 섹션에서 우리는 첫 두개를 다루고 세번쩨는 한번 해 볼 심화 연습으로 남겨두겠다.

Todo 모델이 컬렉션에 객체나 배열로 추가되는 것을 테스트하는 것은 상대적으로 사소하다. 우선 우리는 새로운 TodoList 컬렉션을 초기화하고 그 길이( 즉 포함된 Todo 모델의 수 )가 0인지 확인한다. 그리고 나서 우리는 전체 갯수가 우리가 예상한대로 하기 위해 각 단계에서 컬렉션의 길이을 확인하면서 객체와 배열 모두 새로운 Todo들을 추가한다:

```javascript
describe('Tests for TodoList', function() {

    it('Can add Model instances as objects and arrays.', function() {
        var todos = new TodoList();

        expect(todos.length).toBe(0);

        todos.add({ text: 'Clean the kitchen' });

        // 여기에서 몇개의 할일이 추가되어야 하는가?
        expect(todos.length).toBe(1);

        todos.add([
            { text: 'Do the laundry', done: true },
            { text: 'Go to the gym'}
        ]);

        // 이제 전체 몇개가 있을까?
        expect(todos.length).toBe(3);
    });
...
```

모델의 속성과 유사하게 컬렉션의 속성을 테스트하는 것도 간단하다. 여기에서 우리는 collection.url( 즉, 서버상에서 컬렉션의 위치를 참조하는 url ) 이 우리가 예상하는 것인지 확인하는 명세를 가진다:

```javascript
it('Can have a url property to define the basic url structure for all contained models.', function() {
        var todos = new TodoList();

        // 모델에 기본 URL을 어떻게 지정되었는가?
        expect(todos.url).toBe('/todos/');
});

```

세번째 명세를 위해서, 컬렉션을 위한 구현이 얼마나 많은 Todo 항목들이 완료되었는지, 남아있는지를 필터링하는 메쏘드를 가지고 있는 것을 기억하는 것이 유용하다 - 우리는 이들 ```done()```과 ```remaining()```을 호출할 수 있다. 새로운 컬렉션을 생성하고 미리 ```done```을 상태를 ```true```로 가진 모델 하나와 기본 ```done``` 상태가 ```false```인 다른 두개를 추가하는 명세를 작성한다고 생각해라. ```done()```과 ```remainging()```을 사용해서 반환된 것의 길이를 테스트하는 것은 우리가 어플리케이션에서의 상태 관리가 잘 동작하는지 아니면 조금 고쳐야 하는지를 알게 해준다.

TodoList 컬렉션의 최종 구현은 아래와 같다:


```javascript
 window.TodoList = Backbone.Collection.extend({

        model: Todo,

        url: '/todos/',

        done: function() {
            return this.filter(function(todo) { return todo.get('done'); });
        },

        remaining: function() {
            return this.without.apply(this, this.done());
        },

        nextOrder: function() {
            if (!this.length) {
                return 1;
            }

            return this.last().get('order') + 1;
        },

        comparator: function(todo) {
            return todo.get('order');
        }

    });
```


## 뷰

Backbone 뷰를 테스트하는 것을 보기 전에, 그것들에 대한 Jasmine 명세를 작성하도록 도와주는 jQuery 플러그인을 간단히 살펴보자.

**Jasmine jQuery 플러그인**

Todo 어플리케이션이 DOM 조작에 jQuery를 사용하고 있다고 알고 있기 때문에, 뷰가 생성하는 렌러링 요소를 BDD 테스팅하는 것을 단순화하도록 도와주는 [jasmine-jquery](https://github.com/velesin/jasmine-jquery)라는 유용한 jQuery 플러그인이 있다.

플러그인은 다음과 같은 jQuery로 감싼 것들을 테스트하는데 도움이 되는 많은 추가적인Jasmine [일치기](https://github.com/pivotal/jasmine/wiki/Matchers)를 제공한다:

* ```toBe(jQuerySelector)``` 예제 ```expect($('<div id="some-id"></div>')).toBe('div#some-id')```
* ```toBeChecked()``` 예제 ```expect($('<input type="checkbox" checked="checked"/>')).toBeChecked()```
* ```toBeSelected()``` 예제 ```expect($('<option selected="selected"></option>')).toBeSelected()```

그리고 [다른 것](https://github.com/velesin/jasmine-jquery)도 많이 있다. 지원되는 일치기의 전체 목록은 프로젝트 홈페이지에서 찾을 수 있다. 표준 Jasmine 일치기와 유사하게 위의 사용자 정의 일치기는 .not 접두사를 사용해서 반전시킬 수 있는 것( 즉 ```expect(x).not.toBe(y)``` )을 알아두는 것도 유용하다:

```javascript
expect($('<div>I am an example</div>')).not.toHaveText(/other/)
```

jasmine-jquery도 우리가 테스트에서 사용하고 싶은 임의의 HTML 내용으로 로드하도록 하기위해 픽스쳐 모델을 포함한다. 픽스쳐는 다음과 같이 사용한다:

외부 픽스쳐 파일에 약간의 HTML을 포함한다:

some.fixture.html:
```<div id="sample-fixture">some HTML content</div>```

다음으로 실제 테스트안에서 다음과 갆이 그것을 로드한다:

```javascript
loadFixtures('some.fixture.html')
$('some-fixture').myTestedPlugin();
expect($('#some-fixture')).to<일치기의 나머지가 여기 들어간다>
```

jasmine-jquery 플러그인은 기본적으로 특정 디렉토리로부터 픽스쳐를 로드한다: spec/javascripts/fixtures. 만일 이 경로를 바꾸고 싶으면, 처음에 ```jasmine.getFixtures().fixturesPath = 'your custom path'```를 지정함으로써 가능하다.

마지막으로, jasmine-jquery는 다른 부수적인 작업을 할 필요없이 jQuery 이벤트를 가로채는 것을 지원한다. 이것은 ```spyOnEvent()```와 ```assert(eventName).toHaveBeenTriggered(selector)``` 함수를 사용해서 할 수 있다. 사용 예제는 다음과 같다:

```javascript
spyOnEvent($('#el'), 'click');
$('#el').click();
expect('click').toHaveBeenTriggeredOn($('#el'));
```

**뷰 테스트**

이번 섹션에서 우리는 Backbone 뷰에 대해 명세를 작성하는 세가지 방법을 볼 것이다: 초기 설정, 뷰 렌더링 그리고 마지막으로 템플릿팅. 후자의 두개는 가장 일반적으로 테스트되지만 왜 뷰 초기화에 대한 명세를 작성하는 것도 장점이 되는지 간단히 알아볼 것이다.

## 초기 설정

가장 기본적으로 Backbone 뷰에 대한 명세는 특정 DOM 요소와 올바르게 결합되었는지와 올바른 데이타 모델을 가졌는지를 검증해야만 한다. 이렇게 해야한다고 생각하는 이유는 그런 명세의 실패가 나중에 더 복잡한 테스트를 실패할 수 있고, 전체 값이 제공되면 작성하는 것도 쉽기 때문이다.

명세를 위해서 일관된 테스트 설정을 하기 위해, 우리는 DOM에 빈 ```UL```( #todoList )을 추가하고 빈 Todo 모델을 사용해서 새로운  TovoView 객체를 초기화하는 ```beforeEach()```를 사용한다. ```afterEach()```는 이전의 #todoList ```UL``` 뿐만 아니라 이전의 뷰도 제거하는데 사용된다.

```javascript
describe('Tests for TodoView', function() {

    beforeEach(function() {
        $('body').append('<ul id="todoList"></ul>');
        this.todoView = new TodoView({ model: new Todo() });
    });


    afterEach(function() {
        this.todoView.remove();
        $('#todoList').remove();
    });

...
```

작성하는 유용한 첫번째 명세는 생성한 TodoView가 올바른 ```tagName```( 요소 또는 className )을 사용하고 있는지 확인하는 것이다. 이 테스트의 목적은 생성되었을 때, DOM 요소에 올바르게 결합되었는지 확인하는 것이다.

Backbone 뷰는 일반적으로 초기화되면 빈 DOM 요소를 생성하지만 렌더링 성능에 문제없이 생성되기 위효 이 요소들을 가시적인 DOM에 결합되어 있지 않다.

```javascript
it('Should be tied to a DOM element when created, based off the property provided.', function() {
    //what html element tag name represents this view?
    expect(todoView.el.tagName.toLowerCase()).toBe('li');
});
```

또다시, TodoView가 이미 작성되어 있지 않다면 명세를 실패하는 것을 볼 것이다. 감사하게도, 이것을 해결하는 것은 단순히 특정 ```tagName```을 가진 Backbone 뷰를 생성하는 것이다.

```javascript
var todoView = Backbone.View.extend({
    tagName:  'li'
});
```

```tagName```에 대한 테스트 대신에 className을 사용하고 싶으면, 이것을 제공하는 jasmin-jquery의 ```toHaveClass()``` 일치기를 이용할 수 있다.

```
it('Should have a class of "todos"'), function(){
   expect(this.view.$el).toHaveClass('todos');
});
```

```toHaveClass()``` 일치기는 jQuery 객체에 대해 동작하고 플러그인이 사용되지 않으면 예외가 발생할 것이다.( 물론 jasmine-jquery를 사용하고 싶지 않으면 el.className에 접근해서 className을 테스트할 수도 있다 ).

당신은 ```beforeEach()```에서 우리가 초기( 아무것도 없지만 ) Todo 모델에 뷰를 전달하는 것을 볼 것이다. 뷰는 데이타를 제공하는 모델 객체의 지원을 받는다. 이것은 동작하는 뷰에게 매우 중요하기 때문에, 우리는 모델이 ( ```toBeDefined()``` 일치기를 사용해서 ) 모두 정의되었는지 확인하고 모델의 속성이 기본값이 있고 예상대로인지 확인하는 명세를 작성할ㄹ 수 있다.

```javascript
it('Is backed by a model instance, which provides the data.', function() {

    expect(todoView.model).toBeDefined();

    // 여기에서 Todo.get('done') 의 값은 무엇인가?
    expect(todoView.model.get('done')).toBe(false); // 혹은 toBeFalsy()
});
```

## 뷰 렌더링


다음으로 우리는 뷰 렌더링에 대한 명세를 작성하는 것을 볼 것이다. 특히, 우리는 TodoView 요소가 실제로 예상하는 대로 렌더링되는지 테스트하고 싶다.

작은 어플리케이션에서, BDD가 처음인 사람들은 뷰 렌더링을 눈으로 확인하는 것이 뷰의 단위 테스트를 대체할 수 있다고 말한다. 현실은 여러 개 뷰로 커진 어플리케이션을 다룰 때, 종종 최초부터 가능한 이과정을 자동화하는 것이 상식적이다. 화면에 가시적으로 존재하는 것 이상으로 확인이 필요한 렌더링 관점도 있다( 간단히 알아볼 것이다 ).

우리는 두개의 명세를 작성함으로써 뷰 테스트를 시작할 것이다. 천번째 명세는 뷰의 ```render()``` 메쏘드가 뷰 객체를 올바르게 반환하는지를 확인할 것인데, 그것은 체이닝을 위해 필요하다. 두번째 명세는 생성된 HTML이 정확히 TodoView와 연결된 모델 객체의 특성에 따라 우리가 생각한 대로 인지 확인할 것이다.

우리가 다룬 이전 명세와 달리, 이 섹션은 중첩 스위트를 사용하는 방법을 보여주고, 명세에 대한 조건들을 일관성있게 하기 위해 ```beforeEach()```를 더 많이 사용할 것이다. TodoView에 대한 첫번째 뷰 명세에서 우리는 단순히 ( Todo에 기반한 ) 예제 모델을 생성하고 그 모델과 연결된 TodoView를 객체화할 것이다.

```javascript
describe('TodoView', function() {

  beforeEach(function() {
    this.model = new Backbone.Model({
      text: 'My Todo',
      order: 1,
      done: false
    });
    this.view = new TodoView({model:this.model});
  });

  describe('Rendering', function() {

    it('returns the view object', function() {
      expect(this.view.render()).toEqual(this.view);
    });

    it('produces the correct HTML', function() {
      this.view.render();

      // 할일의 마크업의 전체 내용을 테스트하지 않기 위해서
      // jasmine-jquery의 toContain()을 사용하자
      expect(this.view.el.innerHTML)
        .toContain('<label class="todo-content">My Todo</label>');
    });

  });

});
```


이 명세를 실행하면, 두번째 것('produces the correct HTML')만 실패한다. 첫번째 명세('returns the view object')는 Backbone의 기본 동작으로 통과한다, 그것은 TodoView 객체가 ```render```에서 반환되는지 테스트한다. 우리는 아직 직접 ```render()``` 메쏘드를 덮어쓰지 않았다.

**주의:** 가독성을 유지하기 위한 목적으로 이 섹션의 모든 템플릿 예제는 다음 Todo 뷰 템플릿의 최소 버젼을 사용할 것이다. 이것을 확장하는 것은 사소한 것이기 때문에, 필요하면 이 예제를 편하게 참고해라:



	<div class="todo <%= done ? 'done' : '' %>">
	        <div class="display">
	          <input class="check" type="checkbox" <%= done ? 'checked="checked"' : '' %> />
	          <label class="todo-content"><%= text %></label>
	          <span class="todo-destroy"></span>
	        </div>
	        <div class="edit">
	          <input class="todo-input" type="text" value="<%= content %>" />
	        </div>
	</div>



두번째 명세는 다음 문장과 함께 실패한다:

```Expected '' to contain '<label class="todo-content">My Todo</label>'.```

이 이유는 render()의 기본 동작이 마크업을 생성하지 않기 때문이다. 이것을 고치는 render()를 바꿔 작성하자:

```javascript
render: function() {
  var template = '<label class="todo-content"><%= text %></label>';
  var output = template
    .replace('<%= text %>', this.model.get('text'));
  this.$el.html(output);
  return this;
}
```

위의 코드는 내장된 문자열 템플릿을 지정하고 템플릿내에 있는 "<% %>" 블럭을 가진 항목을 관련 모델의 대응되는 값으로 대체한다. 우리는 그 메쏘드에서 TodoView 객체를 반환도 하기 때문에 첫번째 명세도 통과할 것이다. 이런 테스트 명세에는 HTML 문자열을 사용하는 중요한 결함이 있다는 것을 알아둘 필요가 있다. 템플릿의 작은 변화( 단순한 탭이나 공백 )가 렌더링된 결과가 같을 지라도 명세를 실패하게 한다. 실제 어플리케이션의 대부분의 템플릿은 훨씬 복잡하기 때문에 유지하는데 더 많은 시간이 든다. 렌더링된 결과를 테스트하는 더 좋은 선택은 값을 얻어오고 살펴보는데 jQuery를 사용하는 것이다.

이것을 마음에 두고 이번에는 jasmine-jquery가 제공하는 사용자 정의 일치기를 사용해서 명세를 다시 작성하자:


```javascript
describe('Template', function() {

  beforeEach(function() {
    this.view.render();
  });

  it('has the correct text content', function() {
    expect(this.view.$('.todo-content'))
      .toHaveText('My Todo');
  });

});
```


픽스쳐를 언급하지 않고 단위 테스트를 논의하는 것은 불가능하다. 픽스쳐는 일반적으로 단위 테스트에 필요할 때( 안에 있든 외부 파일에 있든 ) 로드되는 ( HTML같은 ) 테스트 데이타를 포함하고 있다. 지금까지 우리는 뷰의 el특성에 기반해서 jQuery 예상을 만들었다. 이것은 많은 경우에 잘 돌아가지만, 마크업을 문서로 렌더링할야만 하는 객체들이 있다. 명세에서 이것을 다루는 가장 최상의 방법은 ( jasmine-jquery 플러그인이 우리에게 주는 또 하나의 기능인 )픽스쳐를 사용하는 것이다.

픽스쳐를 사용하는 최종 명세를 다시 만든다:


```javascript
describe('TodoView', function() {

  beforeEach(function() {
    ...
    setFixtures('<ul class="todos"></ul>');
  });

  ...

  describe('Template', function() {

    beforeEach(function() {
      $('.todos').append(this.view.render().el);
    });

    it('has the correct text content', function() {
      expect($('.todos').find('.todo-content'))
        .toHaveText('My Todo');
    });

  });

});
```

위의 명세에서 우리가 한 것은 렌더링된 할일 항목을 픽스쳐에 추가하는 것이다. 그리고나서 우리는 픽스쳐에 대한 예상을 설정했는데, 픽스쳐는 DOM에 이미 존재하는 요소에 뷰를 설정할 때 원하는 어떤 것이다. 픽스쳐를 제공하고 뷰가 객체화될 때 예상되는 요소를 정확히 가져간 ```el``` 특성을 확인하는 것이 필요하다.


## 템플릿팅 시스템으로 렌더링하기


(Handlebars, Mustache, 그리고 Underscore 자체 마이크로 템플릿팅같은 ) 자바스크립트 템플릿팅 시스템은 템플릿 문자열 안에서 조건 로직을 지원한다. 우리가 필요에 따라 계산할 수 있는 if / else / ternery 표현식을 추가할 수 있다는 것이 의미하는 것은 효과적으로 더 강력한 템플릿을 만들 수 있다는 것이다.

우리의 경우, 사용자가 Todo 항목이 완료( 다했음 )되었다고 지정했을 때, 우리는 진행중인 항목들과 달라졌다고 ( 문자 중간에 줄긋는 것같은 ) 가시적인 피드백을 주고 싶다. 이것은 아이템에 새로운 클래스를 붙이면 된다. 잘 동작하는 테스트 작성을 시작해보자:


```javascript
describe('When a todo is done', function() {

  beforeEach(function() {
    this.model.set({done: true}, {silent: true});
    $('.todos').append(this.view.render().el);
  });

  it('has a done class', function() {
    expect($('.todos .todo-content:first-child'))
      .toHaveClass('done');
  });

});
```

다음과 같은 문장과 함께 실패할 것이다:

```Expected '<label class="todo-content">My Todo</label>'
to have class 'done'.
```

그것은 다음과 같이 존재하는 render() 메쏘드를 고쳐서 해결할 수 있다:


```javascript
render: function() {
  var template = '<label class="todo-content">' +
    '<%= text %></label>';
  var output = template
    .replace('<%= text %>', this.model.get('text'));
  this.$el.html(output);
  if (this.model.get('done')) {
    this.$('.todo-content').addClass('done');
  }
  return this;
}
```


그러나 이건을 이상하리만큼 너무 쉽다. 템플릿에 로직이 증가함에 따라, 관련된 복잡도도 그러하다. 이것이 템플릿 라이브러리가 할 수 있는 것이다. 이전에 언급했듯이 사용할만한 많은 선택이 있지만 이 챕터의 목적에 맞게 Underscore의 내장 마이크로 템플릿팅을 사용할 것이다. 자유롭게 살펴볼만하 더 진보적인 선택들이 있는 반면, 이것의 장점은 추가적인 파일이 필요가 없고 많은 수정없이 Jasmine 명세를 쉽게 변경할 수 있다는 것이다.

수정된 TodoView 객체는 다음과 같이 Underscore 템플릿팅을 사용한다:

```javascript
var TodoView = Backbone.View.extend({

  tagName: 'li',

  initialize: function(options) {
    this.template = _.template(options.template || '');
  },

  render: function() {
    this.$el.html(this.template(this.model.toJSON()));
    return this;
  },

  ...

});
```


위에서 initialize() 메쏘드는 제공된 Undersocre 템플릿을 객체화라 ( _.template() 함수를 사용해서 ) 컴파일한다. 템플릿을 참조하는 더 일반적인 방법은 템플릿을 사용자 정의 script 타입( 예를들어 type="text/template" )을 사용해서 script 태그에 넣는 것이다. 이것은 어떤 브라우져가 이해하는 스크립트 타입이 아니기 때문에, 단순히 무시되지만, 아이디 속성으로 스크립트를 참조하는 것은 사용하고 싶은 템플릿이 페이지의 다른 부분으로 분리하게 해준다. 실제 어플리케이션에서 이렇게 하거나 테스트를 위해서 외부에 저장한 템플릿을 로드하는 것이 선호된다.

테스트 목적으로 우리는 문제를 단순화하기 위해서 문자열 삽입 방법을 계속 사용할 것이다. 그러나, 각 테스트의 Jasmine 범위에서 템플릿을 자동으로 생성하고 확장하는데 적용하는 유용하 방식이 있다. 'spec'폴더내에 새로운 디렉토리( 말하자면 'templates' )를 만들고 jasmine.yml이나 SpecRunner.html에 다음 내용의 새로운 스크립트를 추가하면, 우리는 우리가 사용하고 싶은 Underscore 템플릿을 포함하고 있는 todo 특성을 추가할 수 있다:

```javascript
beforeEach(function() {
  this.templates = _.extend(this.templates || {}, {
    todo: '<label class="todo-content">' +
            '<%= text %>' +
          '</label>'
  });
});
```

마지막으로, 우리는 TodoView 객체를 객체화할 때 템플릿을 참조하는 명세를 단지 갱신한다:


```javascript
describe('TodoView', function() {

  beforeEach(function() {
    ...
    this.view = new TodoView({
      model: this.model,
      template: this.templates.todo
    });
  });

  ...

});
```


우리가 본 원래 명세는 'done' 상태를 가진 Todo를 위한 추가적인 조건 로직을 가진 템플릿을 자유로이 수정하기 위해서 이 방법을 사용해서 전달된다:

```javascript
beforeEach(function() {
  this.templates = _.extend(this.templates || {}, {
    todo: '<label class="todo-content <%= done ? 'done' : '' %>"' +
            '<%= text %>' +
          '</label>'
  });
});
```

이것은 이젠 어떤 문제도 없이 통과할 것이다. jasmine-jquery가 ```loadFixtures()```와 ```readFixtures()``` 메쏘드를 만들어진 것을 사용해서 외부 픽스쳐를 명세로 로딩하는 것다 지원한다. 더 많은 정보를 위해서 jasmine-jquery 정규 [문서](https://github.com/velesin/jasmine-jquery)를 읽을 것을 고려해 봐라.


## 결론

우리는 이제 어떻게 Backbone.js의 모델, 뷰, 컬렉션에 대한 Jasmine 테스트를 작성하는 법을 배웠다. 라우팅을 테스트하는 것도 바람직하지만, 어떤 개발자는 Selenium같은 다른 툴에게 남겨두는 것이 더 낫다고 생각하기 때문에 기억만 하고 있어라.

James Newbery는 친절하게도 내가 위의 뷰 센션을 쓰도록 도와주었고 [Testing Backbone Apps With SinonJS](http://tinnedfruit.com/2011/04/26/testing-backbone-apps-with-jasmine-sinon-3.html) 에서의 그의 글은 큰 영감이 되었다( 당신은 그의 글 세번째 파트에서 뷰 명세에의 Handlebars 예제를 찾을 수 있을 것이다 ). 당신이 [SinonJS](http://sinonjs.org)을 사용한 Backbone의 스파이나 목 작성 뿐만 아니라 Backbone 라우터를 테스트하는 법을 배우고 싶다면 그의 시리즈를 읽어보라.

## 연습

연습으로 `practicals\jasmine-joans`에 있는 Jasmine Koans을 해보고 제공된 실패하는 테스트를 수정해 볼 것을 추천한다. 이것은 단순히 Jasmine 명세와 스위트가 어떻게 동작하는지를 배우는 것이 아니다. 예제를 통한 작업이 Backbone 기술을 테스트에도 적용될 것이다..


## 더 읽어볼 것
* [Jasmine + Backbone Revisited](http://japhr.blogspot.com/2011/11/jasmine-backbonejs-revisited.html)
* [Backbone, PhantomJS and Jasmine](http://japhr.blogspot.com/2011/12/phantomjs-and-backbonejs-and-requirejs.html)


## QUnit과 SinonJS를 사용한 Backbone 어플리케이션의 단위 테스트

## 소개

QUnit은 jQuery 팀원 [Jörn Zaefferer](http://bassistance.de/)이 만든 강력한 자바스크립트 테스트 스위트이며 자신들의 코드를 테스트하기 위해 ( jQuery과 Backbone.js와 같은 ) 큰 오픈 소스 프로젝트들에 의해 사용된다. 브라우져에서 뿐만 이리나 서버( Rhino, V8, 그리고 SpiderMonkey를 포함해서 지원되는 곳 )에서도 표준 자바스크립트 코드를 테스트할 수 있다. 이것은 많은 활용 예제에 대한 견고한 해결책이 되게 한다.

몇몇 Backbone.js 기여자들은 당신이 당장 Jasmine과 BDD로 시작하고 싶지않다면, QUnit이 테스트에 더 좋은 인문자용 프레임워크라고 생각한다. 이번 챕터에서 보듯이, 스파이와 목을 지원하는 더 강력한 테스트 솔루션을 만들기 위해 QUnit은 SinonJS와 같은 다른 솔루션과 결합할 수도 있다. 혹자는 Jasmine보다 낫다고 한다.

내 개인적인 추전은 두 프레임워크를 비교하고 가장 편리한 것을 선택할 가치가 있다.


# QUnit

## 설정하기

운좋게도, QUnit을 설정하는 것은 5분도 안 걸리는 간단한 작업이다.

우리는 먼저 세개의 파일로 구성된 테스트 환경을 설정한다:

* 테스트 결과를 보여주는 HTML **구조**,
* 테스트 프레임워크를 구성하는 **qunit.js** 파일,
* 테스트 결과를 스타일링하는 **qunit.css** 파일.

이들중에 뒤의 두개는 [QUnit website](http://qunitjs.com)에서 다운로드할 수 있다.

원한다면, 당신은 테스트 목적으로 QUnit 소스의 호스팅 버젼을 사용할 수도 있다. 호스팅 URL은 [http://github.com/jquery/qunit/raw/master/qunit/]에서 찾을 수 있다.

#### QUnit과 호환되는 마크업을 가진 예제 HTML:

```html
<!DOCTYPE html>
<html>
<head>
    <title>QUnit Test Suite</title>

     <link rel="stylesheet" href="qunit.css">
     <script src="qunit.js"></script>

     <!-- Your application -->
     <script src="app.js"></script>

     <!-- Your tests -->
     <script src="tests.js"></script>
</head>
<body>
    <h1 id="qunit-header">QUnit Test Suite</h1>
    <h2 id="qunit-banner"></h2>
    <div id="qunit-testrunner-toolbar"></div>
    <h2 id="qunit-userAgent"></h2>
    <ol id="qunit-tests">test markup, hidden.</ol>
</body>
</html>
```

위에서 아이디로 언급된 요소들을 경험해보자. QUnit이 실행될 때:

* **qunit-header**는 테스트 스위트의 이름을 보여준다
* **qunit-banner**는 테스트가 실패하면 빨강을 모든 테스트가 통과하면 녹색을 보여준다
* **qunit-testrunner-toolbar**는 테스트를 보여주는데 관련된 추가 설정을 포함한다
* **qunit-userAgent**는 navigator.userAgent 특성을 보여준다
* **qunit-tests**는 테스트 결과를 위한 컨테이너이다

잘 실행되면 위의 테스트 실행기는 다음과 같이 보이다:

![screenshot 1](img/7d4de12.png)

각 테스트 이름 뒤의 폼(a, b, c)의 수는 a) 실패한 단언, b) 통과한 단언, c) 전체 단언에 대응한다. 테스트 이름을 클릭하면 테스트케이스에 대한 모든 검증이 펴쳐져서 보여진다. 녹색인 단언은 성공적으로 통과된 것이다.

![screenshot 2](img/9df4.png)

그러나 어떤 테스트라도 실패하면, 테스트는 눈에 띈다( 그리고 가장 위쪽의 qunit-banner가 빨간색으로 바뀐다 ):

![screenshot 3](img/3e5545.png)


## 단언

QUnit은 많은 기본 **단언**을 지원한다. 단언은 코드가 반환한 결과가 예상한 것과 같은지 확인하기 위해서 테스트에서 사된된다. 단언이 실패하면, 우리는 버그가 있다는 것을 알게 된다. Jasmine과 비슷하게 QUnit은 회귀 테스트를 쉽게 할 수 있다. 특히 버그가 발견되었을 때, 버그의 존제를 테스트하는 단언을 작성하고 수정과 반영을 할 수 있다. 코드의 세부 변경이 테스트를 깬다면, 어떻게 대응하고 어디로 접근할 수 있는지 쉽게 알 수 있다.

우선 살펴볼 QUnit 단언은 :

*   `ok ( state, message )` - 첫번째 인자가 true인지를 전달한다
*   `equal ( actual, expected, message )` - 타입 변경까지 포함한 단순 비교 단언
*   `notEqual ( actual, expected, message )` - 위의 반대
*   `expect( amount )` - 각 테스트에서 실행이 예상되는 단언의 수
*   `strictEqual( actual, expected, message)` - `equal()`보다 더 엄격한 비교. 사소한 타입 변경 버그를 비하기 때문에 동일성 확인에 더 선호되는 방법으로 간주된다
*   `deepEqual( actual, expected, message )` - `strictEqual`와 유사하다. ( `===` 를 사용해서 ) 주어진 객체, 배열, 원시 타입의 내용을 비교한다.

QUnit으로 새로운 테스트 케이스를 만드는 것은 상대적으로 간단하고 ```test()```를 사용하는데, 이 메쏘드는 첫인자가 결과에 보여지는 테스트의 ```이름```이고 두번째는 단언들을 포함하고 있는 함수 ```콜백```인 테스트를 만든다. 이것은 QUnit이 실행되자마자 호출된다.

#### test( name, callback )를 사용한 기본 테스트케이스:

```javascript
var myString = 'Hello Backbone.js';

test( 'Our first QUnit test - asserting results', function(){

    // ok( boolean, message )
    ok( true, 'the test succeeds');
    ok( false, 'the test fails');

    // equal( actualValue, expectedValue, message )
    equal( myString, 'Hello Backbone.js', 'The value expected is Hello Backbone.js!');
});
```

위에서 우리가 한 것은 특정 값으로 변수를 정의하고나서 값이 예상한 것과 같은지 테스트하는 것이다. 이것은 비교 단언 ```equal()```을 사용해서 한다. 그것은 첫번째 인자로 테스트할 값이 들어오고 두번째 인자로 예상되는 값이 들어올 거라 예상한다. 우리는 또한 ```ok()```도 사용한다. 그것은 우리가 논리값으로 계산되는 함수나 변수를 통해 쉽게 테스트하게 해준다.

주의: 우리 테스트케이스에서 우리는 '예상되는' 값을 실행할 단언의 수를 정의한 ```test()```에 전달할 수 있다. 다음의 형태를 취한다: `test( name, [expected], test );` 혹은 다음과 같이 직접 test 함수의 가장 위에 예상을 지정한다: `expect( 1 )`. 나는 예상되는 단언의 수를 항상 정의하는 습관을 들이라고 권한다. 나중에 더 설명하겠다.

간단한 정적 변수를 테스트하는 것은 너무 사소하기 때문에, 우리는 실제 함수를 더 테스트할 수 있다. 다음 예제에서 우리는 문자열의 순서를 바꾸는 함수의 결과를 ```equal()```과 ```notEqual()```을 사용해서 결과가 올바른지 테스트한다:

#### 함수의 실제 결과를 예상되는 결과와 비교하기:

```javascript
function reverseString( str ){
    return str.split('').reverse().join('');
}

test( 'reverseString()', function() {
    expect( 5 );
    equal( reverseString('hello'), 'olleh', 'The value expected was olleh' );
    equal( reverseString('foobar'), 'raboof', 'The value expected was raboof' );
    equal( reverseString('world'), 'dlrow', 'The value expected was dlrow' );
    notEqual( reverseString('world'), 'dlroo', 'The value was expected to not be dlroo' );
    equal( reverseString('bubble'), 'double', 'The value expected was elbbub' );
})
```

( HTML 테스트 페이지가 로드될 때 보게되는 ) QUnit 테스트 실행기에서 이 테스트들을 실행하면, 네개의 단언은 통과했지만 마지막 것은 통과하지 못하는 것을 발견한다. `'double'`에 대한 테스트가 실패하는 이유는 본질적으로 잘못 작성되었기 때문이다. 우리 프로젝트에서 테스트가 통과하지 못하고 단언이 옳다면, 당신은 버그를 찾은 것이다!


## 단언에 구조 추가하기

테스트 케이스의 모든 단언을 묶는 것을 유지하기 어려워질 가능성이 높지만, 운좋게도 QUnit은 단언의 구조 블럭을 깔끔하게 지원한다. 이것은 ```module()```를 사용해서 한다 - 그 메쏘드는 우리가 쉽게 테스트를 묶게 해준다. 그룹핑의 일반적인 접근법은 특정 메쏘드를 테스트하는 여러 테스트를 같은 그룹( 모듈 )의 일부로 하는 것이다.

#### 기본 QUnit 모듈:
```javascript
module( 'Module One' );
test( 'first test', function() {} );
test( 'another test', function() {} );

module( 'Module Two' );
test( 'second test', function() {} );
test( 'another test', function() {} );

module( 'Module Three' );
test( 'third test', function() {} );
test( 'another test', function() {} );
```

우리는 이것을 ```setup()```과 ```teardown()``` 콜백을 우리 모듈에 넣어서 할 수 있다. ```setup()```은 각 테스트 전에 실행되는 반면 ```teardown()```은 테스트 후에 실행된다.

#### setup()과 teardown()을 사용하기:
```javascript
module( 'Module One', {
    setup: function() {
        // 이전에 실행
    },
    teardown: function() {
        // 이후에 실행
    }
});

test('first test', function() {
    // 첫 테스트를 실행
});
```

이 콜백은 하나 이상의 테스트를 사용하기 위해 객체화하고 싶은 컴포넌트를 정의하는데 ( 혹은 삭제하는데 ) 사용될 수 있다. 간단히 보았다시피, 이것은 프로젝트에서 우리가 여러 테스트로 참조하는 뷰, 컬렌션, 모델 혹은 라우터의 새 객체를 정의하는데 이상적이다.

#### 객체화하고 다시 정리하기 위해 setup()과 teardown()을 사용하기:
```javascript
// 상점과 상점 목록을 모델링하는
// 모델과 컬렉션을 정의한다

var Store = Backbone.Model.extend({});

var StoreList = Backbone.Collection.extend({
    model: store,
    comparator: function( store ) { return store.get('name') }
});

// 테스트를 위한 그룹을 정의한다
module( 'StoreList sanity check', {
    setup: function() {
        this.list = new StoreList;
        this.list.add(new Store({ name: 'Costcutter' }));
        this.list.add(new Store({ name: 'Target' }));
        this.list.add(new Store({ name: 'Walmart' }));
        this.list.add(new Store({ name: 'Barnes & Noble' });
    },
    teardown: function() {
        window.errors = null;
    }
});

// 추가된 항목의 순서를 테스트한다
test( 'test ordering', function() {
    expect( 1 );
    var expected = ['Barnes & Noble', 'Costcutter', 'Target', 'Walmart'];
    var actual = this.list.pluck('name');
    deepEqual( actual, expected, 'is maintained by comparator' );
});

```

여기에서, 상점 목록은 ```setup()```에서 생성되고 저장된다. ```teardown()``` 콜백은 단순히 window 범위에 저장되어 있지만 전혀 필요없는 에러 목록들을 지운다.


## 단언 예제

더 진행하기 전에, 테스트를 작성할 때 다양한 QUnit 단언이 어떻게 올바르게 사용되는지의 예제를 살펴보자:

### equal - 비교 단언. 실제값 == 예상값 이면 통과한다

```javascript
test( 'equal', 2, function() {
  var actual = 6 - 5;
  equal( actual, true,  'passes as 1 == true' );
  equal( actual, 1,     'passes as 1 == 1' );
});
```


### notEqual - 비교 단언. 실제값 != 예상값 이면 통과한다

```javascript
test( 'notEqual', 2, function() {
  var actual = 6 - 5;
  notEqual( actual, false, 'passes as 1 != false' );
  notEqual( actual, 0,     'passes as 1 != 0' );
});
```

### strictEqual - 비교 단언. 실제값 === 예상값 이면 통과한다.

```javascript
test( 'strictEqual', 2, function() {
  var actual = 6 - 5;
  strictEqual( actual, true,  'fails as 1 !== true' );
  strictEqual( actual, 1,     'passes as 1 === 1' );
});
```

### notStrictEqual - 비교 단언. 실제값 !== 예상값 이면 통과한다.

```javascript
test('notStrictEqual', 2, function() {
  var actual = 6 - 5;
  notStrictEqual( actual, true,  'passes as 1 !== true' );
  notStrictEqual( actual, 1,     'fails as 1 === 1' );
});
```

### deepEqual - 재귀 비교 단언. strictEqual()과 달리, 객체, 배열, 원시 타입에 동작한다.

```javascript
test('deepEqual', 4, function() {
  var actual = {q: 'foo', t: 'bar'};
  var el =  $('div');
  var children = $('div').children();

  equal( actual, {q: 'foo', t: 'bar'},   'fails - objects are not equal using equal()' );
  deepEqual( actual, {q: 'foo', t: 'bar'},   'passes - objects are equal' );
  equal( el, children, 'fails - jQuery objects are not the same' );
  deepEqual(el, children, 'fails - objects not equivalent' );

});
```

### notDeepEqual - 재귀 비교 단언. 이것은 deepEqual과 반대값을 반환한다.

```javascript
test('notDeepEqual', 2, function() {
  var actual = {q: 'foo', t: 'bar'};
  notEqual( actual, {q: 'foo', t: 'bar'},   'passes - objects are not equal' );
  notDeepEqual( actual, {q: 'foo', t: 'bar'},   'fails - objects are equivalent' );
});
```

### raises - 콜백이 어떤 예외를 던지는지 테스트하는 단언

```javascript
test('raises', 1, function() {
  raises(function() {
    throw new Error( 'Oh no! It`s an error!' );
  }, 'passes - an error was thrown inside our callback');
});
```

## 픽스쳐


때때로 우리는 DOM을 수정하는 테스트를 작성해야만 한다. 테스트들 사이에 그런 동작을 정리하는 것을 관리하는 것은 진짜 고통이 될 수도 있지만, 고맙게도 QUnit은 아래에서 보듯이 `#qunit-fixture` 요소의 형태로 이 문제에 대한 해결책을 가지고 있다.

#### Fixture markup:
```html
<!DOCTYPE html>
<html>
<head>
    <title>QUnit Test</title>
    <link rel="stylesheet" href="qunit.css">
    <script src="qunit.js"></script>
    <script src="app.js"></script>
    <script src="tests.js"></script>
</head>
<body>
    <h1 id="qunit-header">QUnit Test</h1>
    <h2 id="qunit-banner"></h2>
    <div id="qunit-testrunner-toolbar"></div>
    <h2 id="qunit-userAgent"></h2>
    <ol id="qunit-tests"></ol>
    <div id="qunit-fixture"></div>
</body>
</html>
```

우리는 픽스쳐에 정적인 마크업을 놓거나 단지 필요한 DOM 요소를 삽입/추가할 수 있다. QUnit은 자동적으로 각 테스트 후에 픽스쳐의 `innerHTML`을 원래 값으로 복원한다. 우리가 jQuery를 사용한 경우에 QUnit이 사용가능성을 확인하고 대신 ```$(el).html()```을 사용하는 것을 알아두면 유용하다. 그것은 어떤 jQuery 이벤트 처리자도 정리한다.


### 픽스쳐 예제:

이제 픽스쳐를 사용하는 전체 예제를 경험해보자. 우리 대부분이 jQuery로 하는데 사용하는 것은 리스트로 하는 것이다 - 그것들은 종종 메뉴, 그리드, 그리고 많은 다른 컴포넌트를 위한 마크업을 정의하는데 사용된다. 당신은 주어진 리스트를 특정 방식으로 다루기 전에 jQuery 플러그인을 사용해서 플러그인의 최종 ( 처리된 ) 결과가 예상한 대로인지 테스트하는 것이 유용할 수 있다.

다음 예제의 목적으로, 우리는 Ben Alman의 `$.enumerate()` 플러그인을 사용할 것이다. 그것은 리스트의 각 항목을 선택적으로 리스트의 첫번째 번호를 지정한 인덱스를 붙여준다. 플러그인에 대한 코드 조각은 아래에 있고 예제에서 만들어진 결과가 그다음에 있다:

```javascript
$.fn.enumerate = function( start ) {
      if ( typeof start !== 'undefined' ) {
        // `start` 값이 제공되었기 때문에 
	// 체이닝할 수 있는 초기 jQuery 객체가 반환된다.

        return this.each(function(i){
          $(this).prepend( '<b>' + ( i + start ) + '</b> ' );
        });

      } else {
        // `start` 값이 제공되지 않으면, 
	// 첫번째 선택된 요소에서 적당한 값을
	// 반환하는 getter같은 함수

        var val = this.eq( 0 ).children( 'b' ).eq( 0 ).text();
        return Number( val );
      }
    };

/*
    <ul>
      <li>1. hello</li>
      <li>2. world</li>
      <li>3. i</li>
      <li>4. am</li>
      <li>5. foo</li>
    </ul>
*/
```

이제 이 플러그인에 대한 명세를 작성하자. 우선 우리는 ```qunit-fixture``` 요소 안의 예제 항목들을 포함하는 목록을 위한 마크업을 정의한다:

```html
&lt;div id=&quot;qunit-fixture&quot;&gt;
    &lt;ul&gt;
      &lt;li&gt;hello&lt;/li&gt;
      &lt;li&gt;world&lt;/li&gt;
      &lt;li&gt;i&lt;/li&gt;
      &lt;li&gt;am&lt;/li&gt;
      &lt;li&gt;foo&lt;/li&gt;
    &lt;/ul&gt;
  &lt;/div&gt;
```

다음으로, 우리는 무엇을 테스트해야만 하는지에 대해 생각해야만 한다. `$.enumerate()`는 다음과 같은 몇가지 다른 사용례를 제공한다:

* **인자없이** - 즉 ```$(el).enumerate()```
* **0을 인자로** - 즉 ```$(el).enumerate(0)```
* **1을 인자로** - 즉 ```$(el).enumerate(1)```

각 목록 항목에 대한 문자열 값이 "n. item-text"과 같은 형태이고 우리가 예상되는 결과를 테스트하기 위해 이것을 필요로 하기 때문에, 우리는 ```$(el).eq(index).text()```을 사용해서 내용에 접근할 수 있다( .eq()에 대한 더 많은 정보는 [여기](http://api.jquery.com/eq/)에서 볼수 있다 ).

그리고 마지막으로 테스트 케이스는 여기있다:

```javascript
module('jQuery#enumerate');

test( 'No arguments passed', 5, function() {
  var items = $('#qunit-fixture li').enumerate();
  equal( items.eq(0).text(), '1. hello', 'first item should have index 1' );
  equal( items.eq(1).text(), '2. world', 'second item should have index 2' );
  equal( items.eq(2).text(), '3. i', 'third item should have index 3' );
  equal( items.eq(3).text(), '4. am', 'fourth item should have index 4' );
  equal( items.eq(4).text(), '5. foo', 'fifth item should have index 5' );
});

test( '0 passed as an argument', 5, function() {
  var items = $('#qunit-fixture li').enumerate( 0 );
  equal( items.eq(0).text(), '0. hello', 'first item should have index 0' );
  equal( items.eq(1).text(), '1. world', 'second item should have index 1' );
  equal( items.eq(2).text(), '2. i', 'third item should have index 2' );
  equal( items.eq(3).text(), '3. am', 'fourth item should have index 3' );
  equal( items.eq(4).text(), '4. foo', 'fifth item should have index 4' );
});

test( '1 passed as an argument', 3, function() {
  var items = $('#qunit-fixture li').enumerate( 1 );
  equal( items.eq(0).text(), '1. hello', 'first item should have index 1' );
  equal( items.eq(1).text(), '2. world', 'second item should have index 2' );
  equal( items.eq(2).text(), '3. i', 'third item should have index 3' );
  equal( items.eq(3).text(), '4. am', 'fourth item should have index 4' );
  equal( items.eq(4).text(), '5. foo', 'fifth item should have index 5' );
});

```

## 비동기 코드

Jasmine으로 할 때처럼, QUnit으로 테스트를 동기적으로 실행하는데 필요한 노련은 매우 간단하따. 즉, ( 프로세스 처리, Ajax 요청, 등등과 같은 ) 비동기적인 콜백을 필요로 하는 테스트는 어떤가? 다음 테스트가 실행될 때, QUnit이 제어하기 보다는 비동기적 코드로 다룰 때, 우리는 실행을 멈추고 다시 괜찮아질 때까지 기다려야만 하는 것을 알 수 있다.

기억하라: 특별한 고려없이 비동기적 코드를 실행하는 것은 다른 테스트에서 나타난 부정확한 단언이 호출될 수 있어서 그것이 옳은지 확인하고 싶다.

비동기 코드에 대한 QUnit 테스트를 작성하는 것은 ```start()```와 ```stop()``` 메쏘드를 사용해서 가능하다. 그것은 프로그램적으로 그 테스트동안 시작과 종료 지점을 지정한다. 여기 단순한 예제가 있다:

```javascript
test('An async test', function(){
   stop();
   expect( 1 );
   $.ajax({
        url: '/test',
        dataType: 'json',
        success: function( data ){
            deepEqual(data, {
               topic: 'hello',
               message: 'hi there!''
            });
            start();
        }
    });
});
```

jQuery ```$.ajax()``` 요청은 테스트 자원에 접속해서 반환된 데이타가 옳은지 단언하는데 사용된다. ```deepEqual()```은 ( 객체, 배열같은 ) 다른 데이타 타입을 비교하도록 해주고, 반환된 것이 예상한 것과 정확히 같은 것인지 확인해 주기 때문에 여기에서 사용된다. 우리는 Ajax 요청이 비동기전인 것을 알고 우선 ```stop()```을 호출하고 요청을 만드는 코드를 실행하고 마지막에 콜백의 맨 끝에서 QUnit에게 다른 테스트를 계속 실행해도 괜찮다고 알려준다.

주의: 만일 원한다면, ```stop()```을 포함하기 보다는 간단히 그것을 빼고 ```test()```를 ```asyncTest()```로 대체할 수 있다. 이것은 스위트에 비동기 테스트와 동기 테스트가 섞여있는 경우에 가독성을 개선한다. 이 설정이 많은 경우에 잘 동작하는 반면, ```$.ajax()``` 요정의 콜백이 실제로 호출될지에 대한 보장은 없다. 이것을 우리 테스트로 넣기 위해서 우리는 테스트 안에서 몇개의 단언을 만날지를 정의하는 ```expect()```를 또다시 사용할 수 있다. 이것은 테스트가 불충분한 단언으로 종료되면, 뭔가 잘못됐음을 알고 고치게 하는 안전 장치이다.



# SinonJS

Jasmine BDD 프레임워크로 Backbone.js 앱을 테스트하는 섹션과 비슷하게 우리는 거의 다 배웠고, 우리 Todo 어플리케이션에 대한 많은 QUnit 테스트를 작성했다.

우리가 시작하기 전에, 당신은 QUnit이 테스트 스파이를 지언하지 않는다는 것을 알아차릴 것이다. 테스트 스파이는 어떤 호출에 대한 인자, 예외, 반환값을 기록하는 함수이다. 그것들은 일반적으로 테스트 콜백과 테스트되는 어플리케이션 안에서 함수 사용법을 테스트한다.테스트 프레임워크에서 스파이는 보통 익명 함수이거나 이미 존재하는 래핑 함수이다.


## SinonJS는 무엇인가?

우리가 QUnit에서 스파이 지원을 대체하기 위해, 우리는 Christian Johansen이 만든 [SinonJS](http://sinonjs.org/)라는 목 프레임워크를 이용할 것이다. 우리는 또한 QUnit과 자연스럽운 통합( 설정이 최소화되었음을 뜻한다 )을 제공하는 [SinonJS-QUnit adapter](http://sinonjs.org/qunit/)도 사용할 것이다. Sinon.JS는 완전히 보이지 않는 테스트 프레임워크이고, 어떤 테스트 프레임워크와 같이 사용하는 것이 쉬워야만 한다. 그래서 그것은 우리의 요건에 딱 맞는다.

그 프레임워크는 어플리케이션을 단위 테스트하는데 이용할만한 세가지 기능을 지원한다:

* **익명 스파이**
* **존재하는 함수에 대한 스파이**
* **풍부한 관찰 인터페이스**

인자없인 ```this.spy()```를 사용하는 것이 익명 스파이를 생성한다. 이것은 ```jasmine.createSpy()```에 비유되고 다음 예제에서 SinonJS 스파이의 기본 사용을 볼 수 있다:

#### 기본 스파이:
```javascript
test('should call all subscribers for a message exactly once', function () {
    var message = getUniqueString();
    var spy = this.spy();

    PubSub.subscribe( message, spy );
    PubSub.publishSync( message, 'Hello World' );

    ok( spy1.calledOnce, 'the subscriber was called once' );
});
```

우리는 아래 예제와 같이 ( jQuery의 ```$.ajax``` 같은 ) 존재하는 함수를 스파이하기 위해 ```this.spy()```를 사용할 수도 있다. 이미 있는 함수를 스파이할 때, 함수는 보통과 같이 동작하지만 우리는 테스트 목적에 매우 유용할 수 있는 호출에 대한 데이타에 접근할 수 있다.

#### 존재하는 함수의 스파이:
```javascript
test( 'should inspect jQuery.getJSON's usage of jQuery.ajax', function () {
    this.spy( jQuery, 'ajax' );

    jQuery.getJSON( '/todos/completed' );

    ok( jQuery.ajax.calledOnce );
    equals( jQuery.ajax.getCall(0).args[0].url, '/todos/completed' );
    equals( jQuery.ajax.getCall(0).args[0].dataType, 'json' );
});
```

SinonJS는 만일 특정 수만큼 호출되었고 인자의 값에 대해 테스트한다면 c스파이가 특정 인자로 호출되었는지를 테스트하게 해주는 풍부한 스파이 인터페이스를 가지고 있다. 인터페이스에서 지원하는 기능 목록은 여기(http://sinonjs.org/docs/)에서 찾을 수 있지만, 매우 일반적으로 사용되는 몇 가지를 보여주는 예제를 한번 보자:


#### 인자 일치: 스파이가 특정 인자들로 호출되는지 테스트한다:

```javascript
test( 'Should call a subscriber with standard matching': function () {
    var spy = sinon.spy();

    PubSub.subscribe( 'message', spy );
    PubSub.publishSync( 'message', { id: 45 } );

    assertTrue( spy.calledWith( { id: 45 } ) );
});
```

#### 더 엄격한 인자 일치: 스파이가 적어도 한번 특정 인자들로만 호출되는지 테스트:

```javascript
test( 'Should call a subscriber with strict matching': function () {
    var spy = sinon.spy();

    PubSub.subscribe( 'message', spy );
    PubSub.publishSync( 'message', 'many', 'arguments' );
    PubSub.publishSync( 'message', 12, 34 );

    // This passes
    assertTrue( spy.calledWith('many') );

    // This however, fails
    assertTrue( spy.calledWithExactly( 'many' ) );
});
```

#### 호출 순서 테스트: 스파이가 다른 스파이 전후로 호출되었는지 테스트:

```javascript
test( 'Should call a subscriber and maintain call order': function () {
    var a = sinon.spy();
    var b = sinon.spy();

    PubSub.subscribe( 'message', a );
    PubSub.subscribe( 'event', b );

    PubSub.publishSync( 'message', { id: 45 } );
    PubSub.publishSync( 'event', [1, 2, 3] );

    assertTrue( a.calledBefore(b) );
    assertTrue( b.calledAfter(a) );
});
```

#### 실행 횟수 일치: 스파이가 특정 횟수만큼 호출되었는지 테스트:

```javascript
test( 'Should call a subscriber and check call counts', function () {
    var message = getUniqueString();
    var spy = this.spy();

    PubSub.subscribe( message, spy );
    PubSub.publishSync( message, 'some payload' );


    // 스파이가 단하번 호출되면 통과
    ok( spy.calledOnce ); // calledTwice와 calledThrice도 지원된다

    // 기록된 호출 횟수
    equal( spy.callCount, 1 );

    // 호출 인자 직접 확인
    equals( spy.getCall(0).args[0], message );
});
```


## 스텁과 목

SinonJS도 알려진 유용한 두가지 강력한 기능을 제공한다: 스텁과 목. 스텁과 목 모두 스파이 API 기능 모두를 구현하지만, 몇가지 추가 기능이 있다.

### 스텁

스텁은 우리가 특정 메쏘드에 존재하는 기능을 다른 것으로 바꾸게 해준다. 예외를 흉내내는데 매우 유용하고 코드의 의존성이 아직 없을 때 테스트 케이스를 작성하는데 자주 사용된다.

Backbone Todo 어플리케이션을 간단히 다시 살펴보자. 그것은 Todo 모델과 TodoList 컬렉션을 가지고 있다. 이것은 설명하기 위해, 우리는 새로운 모델을 추가하면 어떻게 동작하는 테스트하기 위해 TodoList 컬렉션을 분리해서 Todo 모델을 속이고 싶다.

우리는 스텁을 사용하는 것이 어떻게 하는 것인지 보여주기 위해서 모델을 아직 작성하지 않았다고 하자. 사용하는 모델을 참조하는 컬렉션은 다음과 같다:

```javascript
var TodoList = Backbone.Collection.extend({
    model: Todo
});

// 이 컬렉션의 객체를 다음으로 가정하자
this.todoList;
```

컬렉션이 새 모델을 객체화한다고 가정하고, 우리는 테스트를 위해서 모델 생성자를 서텁으로 만들어야 한다. 이것은 다음과 같이 단순한 스텁을 만듦으로써 할 수 있다:

```javascript
this.todoStub = sinon.stub( window, 'Todo' );
```

위의 코드는 window 객체 상에 Todo 메쏘드 스텁을 생성한다. 퍼시스턴트 객체의 스텁을 만들 때, 원래 상태를 복원해야만 한다. 이것은 다음과 같이 ```teardown()```에서 할 수 이다:

```javascript
this.todoStub.restore();
```

이다음에는, 우리는 생성자가 반환하는 것을 바꿔야만 한다. 그것은 원래의 ```Backbone.Model``` 생성자를 사용해서 효과적으로 할 수 있다. 이것은 Todo 모델은 아니지만, 실제 Backbone 모델을 제공한다.


```javascript
teardown: function() {
    this.model = new Backbone.Model({
      id: 2,
      title: 'Hello world'
    });
    this.todoStub.returns( this.model );
});
```

여기에서 예상은 이 코드가 TodoList 컬렉션이 스텁된 Todo 모델을 항상 객체화하도록 할 것이라는 것이다. 하지만 컬렉션의 모델에 대한 참조가 이미 있기 때문에, 우리는 다음과 같이 컬렉션의 모델 특성을 초기화해야만 한다:

```javascript
this.todoList.model = Todo;
```

그 결과 TodoList 컬렉션이 새로운 Todo 모델을 객체화할 때, 원하는 대로 Backbone 모델을 반환할 것이다. 이것은 다음과 같이 새로운 모델 상수를 추가하는 테스트에 대한 명세를 만들 수 있게 해준다:

```javascript
module( 'Should function when instantiated with model literals', {

  setup:function() {

    this.todoStub = sinon.stub(window, 'Todo');
    this.model = new Backbone.Model({
      id: 2,
      title: 'Hello world'
    });

    this.todoStub.returns(this.model);
    this.todos = new TodoList();

    // Let's reset the relationship to use a stub
    this.todos.model = Todo;
    this.todos.add({
      id: 2,
      title: 'Hello world'
    });
  },

  teardown: function() {
    this.todoStub.restore();
  }

});

test('should add a model', function() {
    equal( this.todos.length, 1 );
});

test('should find a model by id', function() {
    equal( this.todos.get(5).get('id'), 5 );
  });
});
```


### 목

목은 사실상 스텁과 같다. 하지만 그것은 전체 API를 가상화하고 사용방법에 대한 내장된 예상이 있다. 목과 스파이 사이의 차이는 사용에 대한 예상이 미리 정의되었기 때문에 예상에 맞지 않으면 사용할 수 없다.

여기 PubSubJS에 기초한 목을 간단히 사용하는 코드가 있다. 여기에서 콜백으로 `clearTodo()` 메쏘드가 있고, 동작을 보장하는 목을 사용한다.

```javascript
test('should call all subscribers when exceptions', function () {
    var myAPI = { clearTodo: function () {} };

    var spy = this.spy();
    var mock = this.mock( myAPI );
    mock.expects( 'clearTodo' ).once().throws();

    PubSub.subscribe( 'message', myAPI.clearTodo );
    PubSub.subscribe( 'message', spy );
    PubSub.publishSync( 'message', undefined );

    mock.verify();
    ok( spy.calledOnce );
});
```



## 연습

우리는 이제 Todo 어플리케이션을 위한 테스트 명세 작성을 시작할 수 있다. 그것은 컴포넌트( 예를들어 모델, 컬렉션 등 )에 따라 구분되고 목록이 작성된다. 테스트 이름과 테스트되는 로직, 그리고 만들려는 단언에 집중하는 것이 실용적이다. 이것은 우리가 배운 것이 전체 어플리케이션에 어떻게 적용되는지 통찰력을 주기 때문이다.

이번 섹션중 대부분을 이해하기 위해, 나는 `practicals\qunit-koans` 폴더의  QUnit Koans을 보길 바란다 - 이것은 Backbone.js Jasmine Koans의 일부를 차례로 QUnit으로 바꾼 것이다.

*당신이 아직 Koans중에 하나도 바꾼 것이 없다면, 그것들은 어떻게 어플리케이션을 위한 명세를 작성하는지를 보여주는 특정 테스트 프레임워크를 사용한 단운 테스트들이지만, 당신이 연습으로 채울 수 있게 하기 위해 몇몇 테스트는 빈채로 남아있다.*

### 모델

우리가 모델에 대해 하고 싶은 최소한의 테스트는:

* 새로운 객체가 예상되는 기본값으로 생성될 수 있다
* 속성이 올바르게 설정되고 가져올 수 있다
* 상태 변견이 필요에 따라 사용자 정의 이벤트를 구동한다
* 검증 규칙이 올바르게 적용된다

```javascript
module( 'About Backbone.Model');

test('Can be created with default values for its attributes.', function() {
    expect( 1 );

    var todo = new Todo();

    equal( todo.get('text'), '' );
});

test('Will set attributes on the model instance when created.', function() {
    expect( 3 );

    var todo = new Todo( { text: 'Get oil change for car.' } );

    equal( todo.get('text'), 'Get oil change for car.' );
    equal( todo.get('done'), false );
    equal( todo.get('order'), 0 );
});

test('Will call a custom initialize function on the model instance when created.', function() {
    expect( 1 );

    var toot = new Todo({ text: 'Stop monkeys from throwing their own crap!' });
    equal( toot.get('text'), 'Stop monkeys from throwing their own rainbows!' );
});

test('Fires a custom event when the state changes.', function() {
    expect( 1 );

    var spy = this.spy();
    var todo = new Todo();

    todo.on( 'change', spy );
    // 여기에서 todo 특성을 어떻게 갱신하는가?
    // 힌트: http://documentcloud.github.com/backbone/#Model-set
    todo.set( { text: 'new text' } );

    ok( spy.calledOnce, 'A change event callback was correctly triggered' );
});


test('Can contain custom validation rules, and will trigger an error event on failed validation.', function() {
    expect( 3 );

    var errorCallback = this.spy();
    var todo = new Todo();

    todo.on('error', errorCallback);
    // 검증이 실패하도록 todo 특성에 무엇을 설정해야만 하는가?
    todo.set( { done: 'not a boolean' } );

    ok( errorCallback.called, 'A failed validation correctly triggered an error' );
    notEqual( errorCallback.getCall(0), undefined );
    equal( errorCallback.getCall(0).args[1], 'Todo.done must be a boolean value.' );

});
```


### 컬렉션

컬렉션에 대해서 우리는 다음을 테스트하고 싶다:

* 새로운 모델 객체가 객체와 배열의 형태로 추가될 수 있다
* 모델의 변경이 필요한 사용자 이벤트를 구동시킨다
* 모델의 URL 구조를 정의하는 `url` 특성이 올바르게 정의되었다


```javascript
module( 'About Backbone.Collection');

test( 'Can add Model instances as objects and arrays.', function() {
    expect( 3 );

    var todos = new TodoList();
    equal( todos.length, 0 );

    todos.add( { text: 'Clean the kitchen' } );
    equal( todos.length, 1 );

    todos.add([
        { text: 'Do the laundry', done: true },
        { text: 'Go to the gym' }
    ]);

    equal( todos.length, 3 );
});

test( 'Can have a url property to define the basic url structure for all contained models.', function() {
    expect( 1 );
    var todos = new TodoList();
    equal( todos.url, '/todos/' );
});

test('Fires custom named events when the models change.', function() {
    expect(2);

    var todos = new TodoList();
    var addModelCallback = this.spy();
    var removeModelCallback = this.spy();

    todos.on( 'add', addModelCallback );
    todos.on( 'remove', removeModelCallback );

    // 어떻게 'add' 이벤트를 구동하는가?
    todos.add( {text:'New todo'} );

    ok( addModelCallback.called );

    // 어떻게 구동할 'remove' 콜백을 얻는가?
    todos.remove( todos.last() );

    ok( removeModelCallback.called );
});
```



### 뷰

뷰에 대하서 우리는 다음을 검증하고 싶다:

* 생성되었을 때, DOM 요소에 올바르게 묶인다
* 뷰의 DOM 표현이 보여야만 하는 경우, 렌더링될 수 있다
* 뷰 메쏘드를 DOM 요소에 묶이게 해준다

더 나아가서 뷰와 상호작용이 변경되어야만 하는 모델이 올바르게 갱신되었는지 테스트한다.


```javascript
module( 'About Backbone.View', {
    setup: function() {
        $('body').append('<ul id="todoList"></ul>');
        this.todoView = new TodoView({ model: new Todo() });
    },
    teardown: function() {
        this.todoView.remove();
        $('#todoList').remove();
    }
});

test('Should be tied to a DOM element when created, based off the property provided.', function() {
    expect( 1 );
    equal( this.todoView.el.tagName.toLowerCase(), 'li' );
});

test('Is backed by a model instance, which provides the data.', function() {
    expect( 2 );
    notEqual( this.todoView.model, undefined );
    equal( this.todoView.model.get('done'), false );
});

test('Can render, after which the DOM representation of the view will be visible.', function() {
   this.todoView.render();

    // 힌트: render()는 단지 뷰의 DOM 표현을 만들지만 DOM에 삽입하지는 않는다.
    //       그것을 어떻게 ul#todoList에 추가하는가?
    //       어떻게 뷰의 DOM 표현에 접근하는가?
    //
    // 힌트: http://documentcloud.github.com/backbone/#View-el

    $('ul#todoList').append(this.todoView.el);
    equal($('#todoList').find('li').length, 1);
});

asyncTest('Can wire up view methods to DOM elements.', function() {
    expect( 2 );
    var viewElt;

    $('#todoList').append( this.todoView.render().el );

    setTimeout(function() {
        viewElt = $('#todoList li input.check').filter(':first');

        equal(viewElt.length > 0, true);

        // 계속 진행한다는 것을 QUnit에게 알려준다
        start();
    }, 1000, 'Expected DOM Elt to exist');


    // 힌트: DOM 이벤트를 통해 'done' 상태를 전환하기 위해서 어떻게 뷰를 구동하는 방법.
    //       ( todos.js 70번째 줄을 보라. 거기에 이벤트 해쉬가 정의되어 있다. )
    //
    // 힌트: http://api.jquery.com/click

    $('#todoList li input.check').click();
    expect( this.todoView.model.get('done'), true );
});
```

### 이벤트

이벤트를 위해서, 우리는 몇가지 다른 경우를 테스트하고 싶다:

* 일반 객체가 사용자 이벤트를 지원하도록 확장한다
* 객체에 사용자 이벤트가 바인딩되고 구동된다
* 이벤트가 구동될 때 인자를 콜백에 전달한다
* 이벤트 콜백에 전달된 컨택스트를 바인딩한다
* 사용자 이벤트를 제거한다

그리고 아래에 모듈의 몇가지 다른 상세 내용이 있다:

```javascript
module( 'About Backbone.Events', {
    setup: function() {
        this.obj = {};
        _.extend( this.obj, Backbone.Events );
        this.obj.off(); // 각 명세가 실행하기 전에 모든 사용자 이벤트를 제거한다.
    }
});

test('Can extend JavaScript objects to support custom events.', function() {
    expect(3);

    var basicObject = {};

    // 어떻게 basicObject에 이 함수들을 넣는가?
    // 힌트: http://documentcloud.github.com/backbone/#Events
    _.extend( basicObject, Backbone.Events );

    equal( typeof basicObject.on, 'function' );
    equal( typeof basicObject.off, 'function' );
    equal( typeof basicObject.trigger, 'function' );
});

test('Allows us to bind and trigger custom named events on an object.', function() {
    expect( 1 );

    var callback = this.spy();

    this.obj.on( 'basic event', callback );
    this.obj.trigger( 'basic event' );

    // 어떻게 이 사용자 이벤트의 콜백인 후출되게 하는가?
    ok( callback.called );
});

test('Also passes along any arguments to the callback when an event is triggered.', function() {
    expect( 1 );

    var passedArgs = [];

    this.obj.on('some event', function() {
        for (var i = 0; i < arguments.length; i++) {
            passedArgs.push( arguments[i] );
        }
    });

    this.obj.trigger( 'some event', 'arg1', 'arg2' );

    deepEqual( passedArgs, ['arg1', 'arg2'] );
});


test('Can also bind the passed context to the event callback.', function() {
    expect( 1 );

    var foo = { color: 'blue' };
    var changeColor = function() {
        this.color = 'red';
    };

    // 어떻게 changeColor 함수의 'foo'를 참조하는 'this.color'를 얻는가?
    this.obj.on( 'an event', changeColor, foo );
    this.obj.trigger( 'an event' );

    equal( foo.color, 'red' );
});

test( 'Uses `all` as a special event name to capture all events bound to the object.', function() {
    expect( 2 );

    var callback = this.spy();

    this.obj.on( 'all', callback );
    this.obj.trigger( 'custom event 1' );
    this.obj.trigger( 'custom event 2' );

    equal( callback.callCount, 2 );
    equal( callback.getCall(0).args[0], 'custom event 1' );
});

test('Also can remove custom events from objects.', function() {
    expect( 5 );

    var spy1 = this.spy();
    var spy2 = this.spy();
    var spy3 = this.spy();

    this.obj.on( 'foo', spy1 );
    this.obj.on( 'bar', spy1 );
    this.obj.on( 'foo', spy2 );
    this.obj.on( 'foo', spy3 );

    // How do you unbind just a single callback for the event?
    this.obj.off( 'foo', spy1 );
    this.obj.trigger( 'foo' );

    ok( spy2.called );

    // 이벤트와 묶인 모든 콜백을 어떻게 한번의 메쏘드로 푸는가?
    this.obj.off( 'foo' );
    this.obj.trigger( 'foo' );

    ok( spy2.callCount, 1 );
    ok( spy2.calledOnce, 'Spy 2 called once' );
    ok( spy3.calledOnce, 'Spy 3 called once' );

    // 오브젝트와 묵인 모든 콜백과 이벤트를 어떻게 한번의 메쏘드로 푸는가?
    this.obj.off( 'bar' );
    this.obj.trigger( 'bar' );

    equal( spy1.callCount, 0 );
});
```

### 앱

적당한 어플리케이션 부트스트랩을 위한 명세를 작성하는 것도 유용할 수 있다. 다음 모듈을 위해서 설정이 TodoApp 뷰를 초기화해서 추가하고, 우리는 어플리케이션 상호작용에 올바르게 정의된  뷰의 지역 객체의 어떤 것이 지역 컬렉션 객체에 정상적으로 변경하는지  테스트할 수 있다.

```javascript
module( 'About Backbone Applications' , {
    setup: function() {
        Backbone.localStorageDB = new Store('testTodos');
        $('#qunit-fixture').append('<div id="app"></div>');
        this.App = new TodoApp({ appendTo: $('# <app') });
    },

    teardown: function() {
        this.App.todos.reset();
        $('# <app').remove();
    }
});

test('Should bootstrap the application by initializing the Collection.', function() {
    expect( 2 );

    notEqual( this.App.todos, undefined );
    equal( this.App.todos.length, 0 );
});

test( 'Should bind Collection events to View creation.' , function() {
      $('#new-todo').val( 'Foo' );
      $('#new-todo').trigger(new $.Event( 'keypress', { keyCode: 13 } ));

      equal( this.App.todos.length, 1 );
 });
```

## 더 읽어볼 것 & 자원

QUnit과 SinonJS로 어플리케이션을 테스트하는 이 센션의 것은 끝이다. 나는 당신이 [QUnit Backbone.js Koans](https://github.com/addyosmani/backbone-koans-qunit)을 한번 보고 그 예제를 확장할 수 있는지 알아보기 바란다. 더 읽고 싶으면 아래의 추가 자원들을 볼 것을 고려해라:

* **[Test-driven JavaScript Development (book)](http://tddjs.com/)**
* **[SinonJS/QUnit Adapter](http://sinonjs.org/qunit/)**
* **[SinonJS and QUnit](http://cjohansen.no/en/javascript/using_sinon_js_with_qunit)**
* **[Automating JavaScript Testing With QUnit](http://msdn.microsoft.com/en-us/scriptjunkie/gg749824)**
* **[Ben Alman's Unit Testing With QUnit](http://benalman.com/talks/unit-testing-qunit.html)**
* **[Another QUnit/Backbone.js demo project](https://github.com/jc00ke/qunit-backbone)**
* **[SinonJS helpers for Backbone](http://devblog.supportbee.com/2012/02/10/helpers-for-testing-backbone-js-apps-using-jasmine-and-sinon-js/)**




# 자원

## 책 &amp; 수업

* [PeepCode: Backbone.js Basics](https://peepcode.com/products/backbone-js)
* [CodeSchool: Anatomy Of Backbone](http://www.codeschool.com/courses/anatomy-of-backbonejs)
* [Recipies With Backbone](http://recipeswithbackbone.com/)
* [Backbone Patterns](http://ricostacruz.com/backbone-patterns/)
* [Backbone On Rails](https://learn.thoughtbot.com/products/1-backbone-js-on-rails)
* [MVC In JavaScript With Backbone](https://github.com/Integralist/Blog-Posts/blob/master/MVC%20in%20JavaScript%20with%20Backbone.md)
* [Backbone Tutorials](http://backbonetutorials.com/)
* [Derick Baileys Resources For Learning Backbone](http://lostechies.com/derickbailey/2011/09/13/resources-for-and-how-i-learned-backbone-js/)

## 확장 / 라이브러리

* [Backbone Marionette](https://github.com/derickbailey/backbone.marionette)
* [Thorax](http://walmartlabs.github.com/thorax)
* [Lumbar](http://walmartlabs.github.com/lumbar)
* [Backbone Layout Manager](https://github.com/tbranyen/backbone.layoutmanager)
* [Backbone Boilerplate](https://github.com/backbone-boilerplate/backbone-boilerplate)
* [Backbone Model Binding](https://github.com/derickbailey/backbone.modelbinding)
* [Backbone Relational - for model relationships](https://github.com/PaulUithol/Backbone-relational)
* [Backbone CouchDB](https://github.com/janmonschke/backbone-couchdb)
* [Backbone Validations - HTML5 inspired validations](https://github.com/n-time/backbone.validations)


# 결론


'Backbone.js 어플리케이션 개발하기'에 대한 것이 끝났다. 나는 당신에게 이책이 Backbone.js를 살펴보는데 유용하고, 빛을 밝혀주고 좋은 출발점이 되었길 바란다.

당신이 이 책의 영역중 더 확장할 수 있다고 생각하는 다른 주제가 있다면, 자유롭게 알려주길 바라고 아니면, 아직 좋지는 않지만 상위로 반영해주길 바란다. 나는 항상 제목을 가능한 포괄적으로 하고 싶다.

다음 번까지, 당신의 여정에 행운이 있기를!

## 주의

나는 이 책에  도움과 참고, 기여를 해준 Backbone.js, Stack Overflow, DailyJS( Alex YOun ) 그리고 JavaScript 위원회에 감사드리고 싶다. 이 프로젝트는 당신이 없었다면 불가능했기 때문에 당신에게 감사한다! :)


---
문의 bylee, 2013-
Where relevant, copyright Addy Osmani, 2012-2013.
