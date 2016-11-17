# 1.3 AngularJS 2.0 - Part 3

Angular 2.0에서 새로워 진 점을 공식 AngularJS 홈페이지에서 보면 아래와 같다. 일단 저장.


> **What’s new in AngularJs 2.0**

Though Angular 2.0 is enriched with hell lot of features, but here I will describe only those which is really extraordinary and forced the team to rewrite the framework.

**Change in ideology**<br>
When Angular was first created, the major focus was on data binding, templating etc. The primary target was to get rid of the traditional painful process of handling DOM using JavaScript / jQuery. But now the world has been changed, JavaScript has been evolved, definition of client side app has been modified. Thus there was a requirement for a complete different framework.

**A future ready framework**<br>
Angular 2.0 syntaxes are not very much vanilla JavaScript; I mean it’s preferred to use AtScript or TypeScript which is based on ES6. As we all know browsers have already started implementing ES6 and soon we all will start developing our apps in ES6 instead of ES5. Angular 2.0 is giving this opportunity to you, with 100% browser backward compatibility.

**Web components**<br>
Another futuristic thing is Web Components. Web component means small or integrated modules of HTML and JavaScript (css can also be added) which is made to look after a specific work. Many believes in future the web development will be based on web components only (frameworks like polymer are running on this path). Angular 2.0 is providing you a platform for web component based development.

**Router changes**<br>
As things have been moved to MVC to web components, routers are also redesigned. The child router will convert each component of the application into a smaller application by providing it with its own router. It will help encapsulate entire feature sets of an application.

**No require.js (in future)**<br>
Previously in case of large Angular apps, for modular code structure I had to use require.js; but as Angular 2.0 by default supports ES6, things are auto modular. No need for a third party library. However currently as browsers are not supporting ES6 properly, you will need system.js

**Much better DI**<br>
The DI in Angular has been improved a lot in 2.0, where they introduced child injectors, instance scope etc. More on this can be found in the upcoming tutorials of Void Canvas.

**Dynamic loading**<br>
Many of us may have faced the necessity where you wanted to provide the controller or directive at runtime. Don’t worry, you are all set to fall in love with 2.0.

**Async templating**<br>
As Angular 2.0 templates are using ES6 module spec, so template compiling will be asynchronous from now on.

**Logging**<br>
A service called diary.js has been introduced to Angular 2.0, which will help you to log the application’s performance. This can be very useful to find the flaws of your own code and make the app more performant.