### AngularJS 2.0 - Part 1

기본적으로 AngularJS2는 Javascript Framework이며 Client Side App 제작에 사용된다.

> AngularJS2의 이점은 뭘까?

```
Expressive HTML : For eg:- ngIF, ngFor 등
강력한 데이터 바인딩(Data Binding)
Support Modular By Design
백엔드(Back-end) 통합 서비스 내장
```

이중에서 체감되는 이점은 데이터 바인딩인것 같다.<br>
@Componet로 시작되는 구조로 App Component 에서 부터 필요한 부분을<br>
하위 단계에서 또 새로운 Menu Component, Content Component와 같이 하위 level로<br>
이어지는 구조로 프로그램의 모듈화가 장점이다.

아래는 One-way Component의 예시이다.

```
import {Component, View} from 'angular2/core';
import {FORM_DIRECTIVES} from 'angular2/common';
 
 
@Component({
	selector: 'oneway-binding-input',
 
})
@View({
	directives: [FORM_DIRECTIVES]
	template: `
	    <h2>Simple one way binding</h2>
	    <input type="text" #myInput [ngModel]="myValue" />
	    <p>Input value is : {{myValue}}</p>
	    <button (click)="changeToRandom()">Change to random</button>
	    `
})
export class OneWayDataBinding {
	myValue = 'Paul Shan';
	changeToRandom(){
		var aNum = Math.random();
		this.myValue = aNum;
	}
}

```

@Component의 브레슬릿 내용을 보면 oneway-binding-input라는 HTML이나 Ejs 등의 <br>
View에 선언된 <oneway-binding-input></oneway-binding-input> Tag에 해당 Data를<br>
Binding한다는 의미이다.

@View에 선언된 내용은 해당 Tag에 templete으로 선언된 내용으로 넣어주겠다는 의미이고<br>
여기서 볼 부분은 

첫번째, #myInput [ngModel]="myValue" 부분은 myValue로 선언된 값을 binding 하겠다는 의미이며<br>
{{myValue}}은 Class에 있는 값의 myValue를 계속 참조한다.<br>

두번째, export class ... 으로 된 부분은 View에서 참고할 값을 Class로 정의한 것이다.<br>
여기서 myValue라는 변수는 최초값을 View에 보여주고 button Click시 생성되는 myValue를<br>
저장하고 View에서 가져갈 수 있게 해준다.

Two Way Binding은 #myInput **[ngModel]**="myValue" 을 #myInput** [(ngModel)]**="myValue"<br>
와 같이 () 차이지만 Call-By-Reference Call-By-Value와 같다고 생각하면 될 듯하다.<br>

대부분 ()을 붙여서 실제 값을 가져오도록 사용한다.

[data-binding example](http://voidcanvas.com/data-binding-in-angular-js-2-0-with-examples/)

기타 더 다양한 Component 활동은 위 사이트를 참고하라

