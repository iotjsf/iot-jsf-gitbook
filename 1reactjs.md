# 1.ReactJS

React 학습 추천: https://velopert.com/reactjs-tutorials

(하기 내용은 위 학습 사이트의 첫 내용을 학습하는 과정에서 직접가져온 것이므로, 저작권은 상기 사이트에 있음.)

**React 정의**

React는 페이스북에서 개발한 유저인터페이스 라이브러리로서 개발자로 하여금 재사용 가능한 UI를 생성 할 수 있게 해줍니다. 이 라이브러리는 현재 페이스북, 인스타그램, 야후, 넷플릭스를 포함한 많은 큰 서비스에서 사용되고 있습니다.
(위 서비스는 모바일이 아닐 것으로 판단됩니다. 모바일의 경우 아직 native app을 사용중이고, PC 환경에서의 서비스일 것입니다. )

이 라이브러리는 Virtual DOM 이라는 개념을 사용하여 상태의 변함에 따라 선택적으로 유저인터페이스를 렌더링합니다.
따라서, 최소한의 DOM 처리로 컴포넌트들을 업데이트 할 수 있게 해줍니다.

**Virtual Dom**

뜻 그대로 가상의 Dom이라고, 생각하면 됩니다. 즉, dom을 js의 object로 추상화하여 직접 dom을 handling하지않고, UI가 변경된 것만 diff하여 변경시키고, mapping된 dom을 update하는 방식.

**특징**

Virtual DOM 을 사용합니다
JSX: JSX 는 JavaScript 의 확장 문법으로, xml스타일을 javascript내에서 사용할 수 있도록 하여, 직관적으로 UI 구성을 확인할 수 있습니다.

**장점**

Virtual DOM 을 사용한 어플리케이션의 성능 향상
클라이언트에서도 렌더링 될 수 있고, 서버측에서도 렌더링 될 수 있음 (이를 통해 브라우저측의 초기 렌더링 딜레이를 줄이고, SEO 호환도 가능해집니다)
Component 의 가독성이 매우 높고 간단하여 쉬운 유지보수가 가능해집니다.
프레임워크가 아닌 라이브러리서 다른 프레임워크들과 사용이 가능합니다. React 에선 UI만 신경쓰고, 빠져있는 부분은 본인이 좋아하는 라이브러리를 사용하여 stack 을 본인의 입맛대로 설정 할 수 있음
제한

어플리케이션의 View 레이어만 다루므로 이 외의 부분은 다른 기술을 사용해야 합니다 (예를 들어 Ajax, Router 등의 기능은 직접 구현하거나 다른 모듈을 설치하여 사용합니다. 하지만 그 과정이 그렇게 복잡하지 않습니다.
React 버전 v15부터 IE8 이하 버전을 지원하지 않습니다. (IE8 이하 버전을 지원해야 할 경우 v0.14 버전을 사용 해야 합니다.
페이스북은 React 버전을 v0.14 에서 v15로 껑충  띄웠습니다. 그 이유는 production 에서 사용해도 된다고 안정성을 약속한다는것을 강조하기 위함이라고 합니다.

**맛보기**

React 프로젝트를 시작하려면 Node.js 와 NPM 을 설정하고 이것저것 설정을 많이 해야합니다. 그치만, 그 과정을 생략하고 먼저 React 맛보기를 해보기 위하여 유용하고 편한 웹서비스인 webpackbin 을 사용해보록 하겠습니다.

http://www.webpackbin.com/ 접속

webpackbin 은 NPM 설치 없이도 브라우저에서 webpack 을 사용하여 프로젝트를 생성 할 수 있게 해주는 도구입니다.

상단의 Boilerplates > React 클릭

Boilerplates 기능을 이용하면 미리 준비된 React 프로젝트를 바로 클론하여 React 프로젝트를 단숨에 시작 할 수 있습니다.
좌측 에디터에 index.html, main.js, HelloWorld.js 파일이 생성되었지요? HelloWorld.js 파일을 열어보세요.

```
import React from 'react';

function HelloWorld () {
  return (
    <h1>Hello World!</h1>
  );
}

export default HelloWorld;
```


코드의 상단에선 React 를 import 했습니다. 이 import 는 공식적으로 업데이트된 자바스크립트 문법인 ECMAScript2015(ES6) 의 문법이며, var React = require('react'); 와 동일한 의미 입니다.원래는 이렇게 모듈을 require 을 하는것은 Node.js 의것 입니다. 클라이언트사이드에선 보통 html 태그에서 script 르 통하여 여러 파일을 불러오지 이렇게 require 을 하지 않습니다. 지원하지도 않구요.

하지만, webpack 이라는 도구를 사용하여 마치 Node.js 에서 require 하는것과 같이 모듈을 불러올 수 있게 하는 것 입니다. webpack 은 이렇게 import(혹은 require) 한 모듈들을 불러와서 한 파일로 합칩니다. 이 작업을 번들링(bundling) 이라고 합니다.

import 하단에 있는 코드는 Stateless Functions 를 통하여 HelloWorld 라는 컴포넌트를 선언하는 코드입니다.

`return (<h1>HelloWorld</h1>)` 이런식으로 HTML 같은 코드가 ' 나 " 도 없이 그냥 적혀있죠? 이 코드는 JSX 코드입니다. 이 코드는 webpack 에서 번들링 과정을 거치면서 webpack 에서 사용하는 babel-loader 를 통하여 JavaScript 로 변환됩니다. 위 JSX 코드가 JavaScript 로 변환되면 다음과 같습니다.

  ```
  return React.createElement(
    "h1",
    null,
    "Hello World!"
  );
  ```

이번엔 main.js 파일을 열어보세요
```
import React from 'react';
import {render} from 'react-dom';
import HelloWorld from './HelloWorld.js';

render(<HelloWorld/>, document.querySelector('#app'));
```

HelloWorld.js 에서 만든 컴포넌트를 여기서 불러와서 페이지에 렌더링합니다.

이 파일은 webpack 의 entry 파일입니다. 여기서부터 import 하는 파일들을 재귀적으로 모두 불러와서 하나의 파일로 합치는거죠.
React 컴포넌트를 페이지에 렌더링 할 때에는 react-dom 모듈을 불러와서 render 함수를 통하여 처리합니다.

여기서 render 함수의 첫번째 파라미터는 렌더링 할 JSX 형태 코드입니다. 여기서는 HelloWorld 컴포넌트를 렌더링하도록 설정하였습니다. 이런식으로, 컴포넌트를 만들면 <컴포넌트이름/> 이런식으로 HTML 태그를 작성하듯이 쓸 수 있는겁니다.

두번째 파라미터는 렌더링 할 HTML 요소입니다. 여긴 id가 app 인 요소에 렌더링을 하게 설정했네요. 이 요소는 index.html 에서 찾아 볼 수 있습니다.
```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8"/>
  </head>
  <body>
    <div id="app"></div>
    <script src="main.js"></script>
  </body>
</html>
```

**컴포넌트에 속성을 줘보자**

HelloWorld 컴포넌트에 속성을 만들어봅시다. 코드를 다음과 같이 수정하세요.

```
import React from 'react';

function HelloWorld (props) {
  return (
    <h1>Hello {props.name}!</h1>
  );
}

export default HelloWorld;
```

함수에 props 파라미터를 추가하고, 이 props.name 값을 JSX 안에서 렌더링하도록 하였습니다.
JavaScript 값을 JSX에서 렌더링 할 때에는 { }안에 감싸면 됩니다.

코드를 저장하고, 이제 main.js 를 열어서 다음과 같이 수정하세요.

```
import React from 'react';
import {render} from 'react-dom';
import HelloWorld from './HelloWorld.js';

render(<HelloWorld name="iotjsf"/>, document.querySelector('#app'));
```
 
위와 같이 HelloWorld 컴포넌트에 name 값을 설정해주고저장을 하세요.

상단의 Live 버튼을 누르면 코드가 수정 될 때마다 바로 반영이 됩니다.