# 5.2 Angular JS 2.0 Output

## whether App

날씨 정보를 간략하게 보여주고 지역별 날씨를 찾아주는 App
(추가로 날씨 Talk을 Open Chat으로 열어서 제공 예정)

아래 주소로 소스 확인 

https://github.com/seungshins/jsf-angular2-sample



### App 구조 설명

node express에 간단한 typescript 기반의 AngularJS 2.0 App으로 사용한 Package는 아래와 같다.

```
{
  "name": "jsf-angular2-sample",
  "version": "0.0.1",
  "private": true,
  "scripts": {
    "tsc": "tsc",
    "tsc:w": "tsc -w",
    "start": "concurrent \"npm run tsc:w\" \"npm run express\" ",
    "express": "node ./bin/www"
  },
  "dependencies": {
    "typescript": "^1.5.0-beta",
    "body-parser": "~1.15.1",
    "cookie-parser": "~1.4.3",
    "debug": "~2.2.0",
    "ejs": "~2.3.3",
    "express": "~4.13.4",
    "morgan": "~1.7.0",
    "serve-favicon": "~2.3.0",
    "node-sass-middleware": "0.8.0",
    "serve-favicon": "~2.3.0",
    "socket.io": "^1.4.3",
    "angular2": "2.0.0-beta.17",
    "systemjs": "0.19.6",
    "es6-promise": "^3.0.2",
    "es6-shim": "^0.33.3",
    "reflect-metadata": "0.1.2",
    "rxjs": "5.0.0-beta.0",
    "zone.js": "0.5.10"
  },
  "devDependencies": {
    "connect": "^3.4.0"
  }
}

```

> route/index.js

아래와 같이 /angular2라고 들어오는 Path에 대해서 response에 angular2 ejs 파일을 render하고

```
var express = require('express');
var router = express.Router();

/* GET home page. */
router.get('/', function(req, res, next) {
  // res.render('index', { title: 'Express' });
  res.render('angular2');
  // res.render('view.html');
});

router.get('/angular2', function(req, res, next) {
  res.render('angular2');
});

module.exports = router;
```

> public/app/app.component.ts

typescript로 기본적인 Wether 정보를 Wether API를 호출하여 보여주고 view로 보여주게 된다.

```
import {Component} from 'angular2/core';
import {Http, HTTP_PROVIDERS, BaseRequestOptions, RequestOptions} from 'angular2/http';
import {WeatherData} from './weatherdata';
import {ChatComponent} from './chat.component';
 
@Component({
  selector: 'my-app',
  viewProviders: [HTTP_PROVIDERS],
  templateUrl:'/app/view.html',
  //styleUrls: [ 'stylesheets/style.css' ],
  directives: [ChatComponent]
})
 
export class AppComponent {
  public title = 'S2 Weather';
  public weatherdata;
  public selectedWeatherdata;
  public cityName;
  constructor(public http: Http) {
    this.cityName = 'Seoul';
    this.getWeather(this.cityName);
  }

  onSelect(weatherdata) { 
    this.selectedWeatherdata = weatherdata;
  }

  getWeatherFromForm() {
    this.getWeather(this.cityName);
  }

  getWeather(cityName) {
    var appId = '2da6c5cca312fef5fa8fdc26f5ca8180';
    var param = 'q=' + cityName + '&mode=json&units=metric&APPID=' + appId;
    var query = 'http://api.openweathermap.org/data/2.5/weather?' 
                + param;
    this.http.get(query)
      .subscribe(
        data => this.parseWeatherData(data),
        err => this.logError(err.text()),
        () => console.log(this.weather)
      );
  }

  logError(err) {
    console.error('There was an error: ' + err);
  }

  parseWeatherData(data) {
    this.weatherdata = JSON.parse(data.text());
    this.weatherdata.main.temp = parseInt(this.weatherdata.main.temp);
    this.weatherdata.weather[0].icon = "http://openweathermap.org/img/w/" + this.weatherdata.weather[0].icon + ".png";
    console.log(this.weatherdata);
  }
}
```

> view.html

보여주는 view는 이 html과 같다.

```
<nav class="navbar navbar-inverse navbar-fixed-top">
      <div class="container">
        <div class="navbar-header">
          <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#navbar" aria-expanded="false" aria-controls="navbar">
            <span class="sr-only">Toggle navigation</span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
          </button>
          <a class="navbar-brand" href="#">{{title}}</a>
        </div>
        <div id="navbar" class="navbar-collapse collapse">
          <form class="navbar-form">
          	<div class="form-group">
              <input type="text" [(ngModel)]="cityName" placeholder="name"  class="form-control">
            </div>
			<button class="btn btn-success" type="submit" (click)="getWeatherFromForm()">
			Search</button>
          </form>
        </div><!--/.navbar-collapse -->
      </div>
    </nav>

<div class="jumbotron">
      <div class="container">
		<div *ngIf="weatherdata">
			<div class="panel panel-default">
			    <div class="panel-heading">
			      <h4 class="panel-title">{{weatherdata.name}}({{weatherdata.sys.country}})</h4>
			    </div>
			    <div>
			      <div class="panel-body">
					 <ul class="weather">
						 <li style="margin-top:3px;">
						  <!-- <h1><span><img src="http://openweathermap.org/img/w/03d.png" /></span> -->
						  <h1><span><img src="{{weatherdata.weather[0].icon}}" /></span>
						  {{weatherdata.main.temp}} °C
						  </h1>
						  <h3>{{weatherdata.weather[0].description}}</h3>
						  <!-- <h2>{{weatherdata.weather[0].main}}</h2>   -->
						 </li>
						 <!-- <button class="btn btn-primary" type="button" style="width: 200px" (click)="getWeather()">
						 Refresh</button>
						 </li> -->
						 <li style="margin-top:3px;">
						 <button class="btn btn-primary" type="button" style="width: 200px" [class.selected]="weatherdata === selectedWeatherdata" (click)="onSelect(weatherdata)">
						 Open Weather Chat</button>
						 </li>
						 <chat-detail [weatherdata]="selectedWeatherdata"></chat-detail>
					 </ul>
			      </div>
			    </div>
			  </div>
		 </div>
	</div>
</div>
```
기타 detail 내용도 위와 같은 방식으로 구현함.

이상의 내용은 Github의 소스를 참고