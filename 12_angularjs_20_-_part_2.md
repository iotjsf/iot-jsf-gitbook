### 1.2 AngularJS 2.0 - Part 2

AngularJS 2.0의 특징 중 Expressive HTML : For eg:- ngIF, ngFor 등 부분을 보면<br>
프로그래밍의 개념이 조금 더 들어간 부분이 있다.

> ngFor


*ngFor의 예제를 보면

```
import {Component, View} from 'angular2/core';
import {NgFor} from 'angular2/common';
@Component({
  selector: 'if-for',
  
})
@View({
	directives:[NgFor]
	template: `
	    <h2>NgFor Example</h2>
	    <ul>
	    	<li *ngFor="#name of names">{{name}}</li>
	    </ul>
	    `
})
export class ForAndIf {
	names = ["Paul", "David", "Jack"];
}
```

*ngFor="#name of names"에서 For라는 많이 보던 문법의 뜻과 같이 ""에서 나오는 값이<br>
여러개가 있으면 있는 만큼 반복해서 해당 <li>태그를 생성하겠다는 뜻이며<br>
이 예제에서는 "Paul", "David", "Jack"과 같이 세개의 이름이 있어서 세개의 <li>태그가 생성된다.<br>


> ngIf

*ngIf의 예제를 보면

```
import {Component, View} from 'angular2/core';
import {NgIf} from 'angular2/common';

@Component({
  selector: 'if-for',
  
})
@View({
	directives:[NgIf]
	template: `
	    <h2>NgIf Example</h2>
	    <p *ngIf="amITrue">Yes I am true</p>
	    <p *ngIf="!amIFalse">I made the false true</p>
	    `
})
export class ForAndIf {
	amITrue=true;
	amIFalse=false;
}
```

*ngIf="amITrue"에서 amITrue라는 값이 True이냐를 보고 해당 라인의 태그를 생성할지 결정하며<br>
False일 경우에는 해당 태그가 생성되지 않는다.


> ngSwitch

[ngSwitch]의 예제를 보면

```
import {Component, View} from 'angular2/core';
import {NgSwitch, NgSwitchWhen, NgSwitchDefault} from 'angular2/common'

@Component({
	selector: 'eg-switch',
  
})
@View({
	directives: [NgSwitch, NgSwitchWhen, NgSwitchDefault]
	template: `
	    <h2>NgSwitch Example</h2>
	    <span (click)="increase()" [style.cursor]="'pointer'">
	    	Click to Change The number :: 
	    </span>
	    <span [ngSwitch]="myVal">
	    	<template [ngSwitchWhen]="1">One</template>
	    	<template [ngSwitchWhen]="2">Two</template>
	    	<template [ngSwitchWhen]="3">Three</template>
	    	<template [ngSwitchWhen]="4">Four</template>
	    	<template [ngSwitchWhen]="5">Five</template>
	    	<template ngSwitchDefault>Zero</template>
	    </span>
		
	    `
})
export class SwitchTemplates {
	myVal = 0;
	increase: function () {
		if (this.myVal === 5)
			this.myVal = 0;
		else
			this.myVal++;
	}
}
```

[ngSwitch]="myVal"에서 myVal 변수 값을 보고 값이 "1"이면 첫번째 templete 태그<br>
"2"이면 두번째 templete 태그를 출력하고 (Click) 이벤트 처리부에서 increase 함수를<br>
호출하여 값이 1,2,3,4,5,0,1,2,3,4,5,... 와 같이 변화되어 보여지는 templete이 변경된다<br>

> PIPE

Angular 1.0에서 2.0로 버전업이 되면서 지원되는 Feature중에 하나로<br>
원하는 형식으로 Data를 표현하려는 개념의 PIPE가 있다.<br>

```
import {Component, View} from 'angular2/core';
@Component({
  selector: 'eg-pipe',
  
})
@View({
	template: `
	    <h2>Pipe Example</h2>
	    <h4>1. Today is {{today}}</h4>
	    <h4>2. Today is {{today | date}}</h4>
	    <h4>3. Today is {{today | date:"dd/MM/yyyy"}}</h4>
	    `
})
export class PipeExample {
	today = new Date();

}
```

해당 소스에서 보듯이 today라는 변수가 Date()의 생성된 값이지만 다양하게 표현하고 싶을때는<br>
계속 새로운 변수를 만들거나 함수를 만들어야 하지만 PIPE를 활용해서 간편하게 쓸 수 있다<br>

> Customized PIPE

Date처럼 Built in type 외에도 내가 필요한 형식으로 PIPE를 사용하고 싶을 때는<br>
Customized해서 사용한다<br>

PIPE를 Design 해보면

```
//file name: remove-spaces.ts
import {Pipe} from "angular2/core";

@Pipe({
	name : "removeSpaces"
})

export class RemoveSpaces{
	transform(value){
		return value.replace(/ /g, "");
	}
}
```

@Pipe를 선언하고 Class 안에 / 를 빈값으로 바꾸는 transform() 함수를 만들면<br>

```
import {Component, View} from 'angular2/core';
import {RemoveSpaces} from './remove-spaces.ts';


@Component({
  selector: 'remove-spaces-impl',
  
})
@View({
	pipes: [RemoveSpaces],
	template: `
	    <h2>Custom pipe : removeSpaces</h2>
	    <h4> {{sampleString}} => {{sampleString | removeSpaces}}</h4>
	    `
})
export class RemoveSpacesImpl {
	sampleString = "I love angular 2";
}
```

View 부분에서 pipes 속성을 앞에 선언한 파일을 Import한 이름으로 넣어주고<br>
h4 부분에서 PIPE를 통해 앞의 Customize된 값을 사용할 수 있다.<br>
여러개 변환이 있으면 .transform()을 지정한다.<br>

> Elvis operator

PIPE와 같이 새로 등장한 Feature로 JAvascript에서 자주 발생하는 하위 레벨의 값을 접근할 떄<br>
해당 속성이 없어 Undefined로 리턴하는 부분을 방지할 수 있다.


```
import {Component, View} from 'angular2/core';
@Component({
  selector: 'eg-elvis',
  
})
@View({
	template: `
	    <h2>Elvis operator Example</h2>
	    <h4>This is working fine {{obj.temp}}</h4>
	    <h4>This line will break the application {{obj.temp.me.she.he}}. Please uncomment and check</h4>
		<h4>This line will be printed but nothing on right side {{obj?.temp?.me?.she?.he}}</h4>
	    `
})
export class ElvisExample {
	obj = {
		temp:"I am temp"
	}

}
```

{{obj?.temp?.me?.she?.he}}와 같이 ?. ?. ?로 표현하면 해당 값이 있는 범위까지 찾고<br>
값을 리턴해준다.<br>

[pipe 관련 자료](http://voidcanvas.com/angular-2-pipes-filters/)
