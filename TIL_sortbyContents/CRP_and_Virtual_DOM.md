웹 브라우저의 렌더링 과정을 CRP라고 한다. 대략적으로 서버로부터 전송받은 html파일을 파싱하고, js와 css를 읽어 DOM tree를 생성하고 레이아웃을 작성하여 View에 보여주는 과정이 큰 흐름이다.
### CRP 과정
1. HTML을 HTML 파서로 읽어 DOM Tree를 구성한다.
2. ```<link>```나 ```<style>``` 태그를 만나면 DOM Tree 구성을 멈추고 CSS 파싱을 시작하여 CSSOM Tree를 만든다.
3. 브라우저의 자바스크립트 엔진은 서버로부터 응답된 js를 파싱한다. 이때 js를 읽으며 DOM이나 CSSOM을 변경할 수 있다.
4. 완성된 렌더트리를 기반으로 레이아웃을 계산하고 페인팅한다.

여기서 DOM과 CSSOM이라는 용어가 등장한다.
### DOM(Document Object Model)
* 웹 문서를 구조화한 표현, 요소들을 객체화시킴
* 자바스크립트에서 웹페이지의 요소를 선택 및 각종 로직을 수행할 때 사용된다.
* HTML 태그 특성상 Tree 구조로 표현되며, 각 노드들은 웹 페이지의 다양한 부분(요소, 속성, 텍스트 등)을 나타낸다.

### CSSOM(CSS Object Model)
* CSS를 객체로 나타냄
* DOM과 마찬가지로 트리구조로 표현된다.

앞서 언급한 렌더링 과정의 경우 동적인 로직이 여러번 수행될 때마다 DOM이 객체의 변화를 반영하고 렌더링해야하는데 오래 걸리게 된다.<br>
이 고민에서 등장한 것이 Virtual DOM이다.

### Virtual DOM
* 실제 DOM을 추상홯하여 메모리 내에 가상으로 존재하게 한다. 
* 웹페이지의 DOM구조를 메모리에 로드하여 실제 DOM에 변화를 주기 전에 Virtual DOM에 변화를 처리하게 한다.
* 렌더링 과정이 필요없기 때문에 성능이 향상된다.
* Virtual DOM은 2개가 생성되는데, 각각 변화되기 전, 변화한 DOM이다. 
* 변화할 Virtual DOM과 변하기 전의 Virtual DOM을 비교하고 변경이 필요한 부분만 찾아내 실제 DOM에 적용한다
  * 이 과정을 **Diffing**과 **Reconciliation**이라고 한다.