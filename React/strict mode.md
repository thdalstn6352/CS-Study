StrictMode는 아래와 같은 부분에서 도움이 됩니다.

안전하지 않은 생명주기를 사용하는 컴포넌트 발견
레거시 문자열 ref 사용에 대한 경고
권장되지 않는 findDOMNode 사용에 대한 경고
예상치 못한 부작용 검사
레거시 context API 검사
React의 향후 릴리즈에서 더 많은 기능이 더해질 예정입니다.

안전하지 않은 생명주기를 사용하는 컴포넌트 발견
블로그 글에서 설명하였듯, 비동기 React 애플리케이션에서 특정 생명주기 메서드들은 안전하지 않습니다. 하지만 애플리케이션이 서드 파티 라이브러리를 사용한다면, 해당 생명주기 메서드가 사용되지 않는다고 장담하기 어렵습니다. Strict 모드는 이러한 경우에 도움이 됩니다!

Strict 모드가 활성화되면, React는 안전하지 않은 생명주기 메서드를 사용하는 모든 클래스 컴포넌트 목록을 정리해 다음과 같이 컴포넌트에 대한 정보가 담긴 경고 로그를 출력합니다.

strict mode unsafe lifecycles warning
Strict 모드에 의해 발견된 문제들을 해결한다면, 향후 릴리즈되는 React에서 concurrent 렌더링의 이점을 얻을 수 있을 것입니다.

레거시 문자열 ref 사용에 대한 경고
이전의 React에서 레거시 문자열 ref API와 콜백 API라는, ref를 관리하는 두 가지 방법을 제공하였습니다. 문자열 ref가 사용하기 더 편리했지만 몇몇 단점들이 있었습니다. 그래서 공식적으로는 콜백 형태를 사용하는 것을 권장하였습니다.

React 16.3에서는 여러 단점 없이 문자열 ref의 편리함을 제공하는 세 번째 방법을 추가하였습니다.

class MyComponent extends React.Component {
  constructor(props) {
    super(props);

    this.inputRef = React.createRef();
  }

  render() {
    return <input type="text" ref={this.inputRef} />;
  }

  componentDidMount() {
    this.inputRef.current.focus();
  }
}
이제는 객체 ref가 문자열 ref를 교체하는 용도로 널리 더해졌기 때문에, Strict 모드는 문자열 ref의 사용에 대해 경고합니다.

주의

콜백 ref는 새로운 createRef API와 별개로 지속해서 지원될 예정입니다.

컴포넌트의 콜백 ref를 교체할 필요는 없습니다. 콜백 ref는 조금 더 유연하기 때문에, 고급 기능으로서 계속 지원할 예정입니다.

createRef API에 대해서 알아보기

권장되지 않는 findDOMNode 사용에 대한 경고
이전의 React에서 주어진 클래스 인스턴스를 바탕으로 트리를 탐색해 DOM 노드를 찾을 수 있는 findDOMNode를 지원하였습니다. DOM 노드에 바로 ref를 지정할 수 있기 때문에 보통은 필요하지 않습니다.

findDOMNode는 클래스 컴포넌트에서도 사용할 수 있었지만, 부모가 특정 자식이 렌더링되는 것을 요구하는 상황이 허용되어, 추상화 레벨이 무너지게 되었습니다. 이로 인해 부모가 자식의 DOM 노드에까지 닿을 가능성이 있어 컴포넌트의 세세한 구현을 변경할 수 없게 되어 리팩토링이 어려워지는 상황을 만들고 말았습니다. findDOMNode는 항상 첫 번째 자식을 반환하지만, Fragment와 함께 사용할 경우 컴포넌트에서 여러 DOM 노드를 렌더링하게 됩니다. findDOMNode는 일회성, 읽기 전용 API입니다. 물어보았을 때만 값을 반환합니다. 자식 컴포넌트가 다른 노드를 렌더링할 경우, 변경 사항에 대응할 방법이 없습니다. 그러므로, findDOMNode는 항상 변하지 않는, 단일 DOM 노드를 반환하는 컴포넌트에서만 정상적으로 작동해왔습니다.

ref를 넘겨주는 방식을 사용해 커스텀 컴포넌트에 ref를 넘겨 DOM까지 닿게 하는 것으로, 이를 분명하게 만들 수 있습니다.

DOM 노드를 감싸는 래퍼를 만들어 ref를 바로 붙이는 것 역시 가능합니다.

class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.wrapper = React.createRef();
  }
  render() {
    return <div ref={this.wrapper}>{this.props.children}</div>;
  }
}
주의

노드가 레이아웃 바깥의 요소가 되는 것을 막고자 한다면, CSS에서 display: contents 속성을 사용할 수 있습니다.

예상치 못한 부작용 검사
개념적으로 React는 두 단계로 동작합니다.

렌더링 단계는 특정 환경(예를 들어, DOM과 같이)에 어떤 변화가 필요한 지 결정하는 단계입니다. 이 과정에서 React는 render를 호출하여 이전 렌더와 결과값을 비교합니다.
커밋 단계는 React가 변경 사항을 반영하는 단계입니다(React DOM의 경우 React가 DOM 노드를 추가, 변경 및 제거하는 단계를 말합니다). 이 단계에서 React는 componentDidMount 나 componentDidUpdate 와 같은 생명주기 메서드를 호출합니다.
커밋 단계는 일반적으로 매우 빠르지만, 렌더링 단계는 느릴 수 있습니다. 이로 인해, 곧 추가될 concurrent 모드(아직 기본적으로는 비활성화됨)는 렌더링 작업을 더 작은 단위로 나누고, 작업을 중지했다 재개하는 방식으로 브라우저가 멈추는 것을 피합니다. 즉, React는 커밋하기 전에 렌더링 단계의 생명주기 메서드를 여러 번 호출하거나 아예 커밋을 하지 않을 수도(에러 혹은 우선순위에 따른 작업 중단) 있습니다.

렌더링 단계 생명주기 메서드는 클래스 컴포넌트의 메서드를 포함해 다음과 같습니다.

constructor
componentWillMount (or UNSAFE_componentWillMount)
componentWillReceiveProps (or UNSAFE_componentWillReceiveProps)
componentWillUpdate (or UNSAFE_componentWillUpdate)
getDerivedStateFromProps
shouldComponentUpdate
render
setState 업데이트 함수 (첫 번째 인자)
위의 메서드들은 여러 번 호출될 수 있기 때문에, 부작용을 포함하지 않는 것이 중요합니다. 이 규칙을 무시할 경우, 메모리 누수 혹은 잘못된 애플리케이션 상태 등 다양한 문제를 일으킬 가능성이 있습니다. 불행히도, 보통 이러한 문제들은 예측한 대로 동작하지 않기 때문에 발견하는 것이 어려울 수 있습니다.

Strict 모드가 자동으로 부작용을 찾아주는 것은 불가능합니다. 하지만, 조금 더 예측할 수 있게끔 만들어서 문제가 되는 부분을 발견할 수 있게 도와줍니다. 이는 아래의 함수를 의도적으로 이중으로 호출하여 찾을 수 있습니다.

클래스 컴포넌트의 constructor, render 그리고 shouldComponentUpdate 메서드
클래스 컴포넌트의 getDerivedStateFromProps static 메서드
함수 컴포넌트 바디
State updater 함수 (setState의 첫 번째 인자)
useState, useMemo 그리고 useReducer에 전달되는 함수
주의

개발 모드에서만 적용됩니다. 생명주기 메서드들은 프로덕션 모드에서 이중으로 호출되지 않습니다.

예를 들어, 아래의 코드를 생각해봅시다.

class TopLevelRoute extends React.Component {
  constructor(props) {
    super(props);

    SharedApplicationState.recordEvent('ExampleComponent');
  }
}
얼핏 보면 이 코드에는 문제가 없어 보입니다. 하지만, SharedApplicationState.recordEvent의 연산 결과가 계속 달라진다면, 이 컴포넌트를 여러 번 인스턴스 화했을 때 애플리케이션의 상태를 잘못된 방향으로 이끌 수 있습니다. 이와 같은 이해하기 어려운 버그들은 개발 중에 나타나지 않을 수도 있고, 일관성이 없어 발견하지 못할 수도 있습니다.

컴포넌트의 constructor와 같은 메서드를 의도적으로 두 번 호출하면 strict mode가 이와 같은 패턴을 쉽게 찾을 수 있도록 합니다.

주의

React 17부터 React는 자동으로 console.log() 같은 콘솔 메서드를 수정해서 생명주기 함수의 두 번째 호출에서 로그를 찍지 않습니다. 그러나, 회피책을 사용할 수 있다면 의도하지 않은 동작이 발생할 수 있습니다.

레거시 context API 검사
레거시 context API는 오류가 발생하기 쉬워 이후 릴리즈에서 삭제될 예정입니다. 모든 16.x 버전에서 여전히 돌아가지만, Strict 모드에서는 아래와 같은 경고 메시지를 노출합니다.

warn legacy context in strict mode


