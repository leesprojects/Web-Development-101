```toc
```

<a href="https://www.udemy.com/course/the-complete-guide-to-angular-2/learn/lecture/6655598#overview">Udemy course by Max</a> 
A reactive single-page application, all changes are rendered in the browser. It utilises Javascript to render changes much faster than reaching out to a server for each change. Since Angular is a JS framework, it changes the DOM during runtime.

## Typescript
#Typescript
A strict syntactical superset of Javascript which is a strongly typed language which is compiled to JavaScript.

## How Angular loads and displays components
#Bundles
The single-page aspect comes from only index.html being served, however, it contains an `<app-root>` component generated by the CLI. 
On compilation, the index.html file injects a set of bundle scripts such as `inline.bundle.js`, `polyfills.bundle.js` etc... One of the injections is `main.ts` which is responsible for bootstrapping the Angular application (`app.module.ts`)
Within `app.module.ts`, theres a bootstrapper for launching the AppComponent, this is only for the root component

| Bundle name | Purpose |
| - | - |
| inline | WebPack |
| polyfills | Browser compatability |
| main | Angular files |
| styles | Styles |
| vendor | 3rd party libraries |

`ng-serve` will compiles and runs the application from memory purely for development
`ng-build` will compile the application producing build files used for deployment

<i>Ahead of Time Compilation (AOT)</i> compilation is done during the build
<i>Just In Time Compilation (JIT)</i> compilation is done during runtime


## Components
#Components
Each component has it's own template and business logic
The `@Component` class decorator is needed for Angular to identify a .ts file as a component
`ng g c componentname`

```TS
import { component } from '@angular/core'

@Component({
	selector: 'app-home', 
	templateUrl: './home.component.html'
})
```

| Selector Option | Html Reference | Type |
| - | - | - |
| `app-home` | `<app-home></app-home>` | Element |
| `[app-home]`| `<div app-home></div>` | Attribute |
| `.app-home` | `<div class="app-home"></div>` | Class |


## App Module
#Modules
```TS
import { BroswerModule } from '@angular/platform-browser'
import { NgModule } from '@angular/core'
import { HttpModule } from '@angular/http'

import { AppComponent } from './app.component'
import { HomeComponent } from './home/home.component'

@NgModule({
	declarations: [ //Declares components within this module
		AppComponent,
		HomeComponent
	],
	imports: [ //Declares the packages needed for this module
		BrowserModule,
		HttpModule
	],
	providers: [
	],
	bootstrap: [
		AppComponent
	]
})
```

## Databinding
#Databinding
A link between Typescript and HTML

### One-Way Binding
One-Way: TypeScript interacting with HTML
```TS
{{ data }}          //String interpolation with a string property's value 
{{ data ? "Data exists" : "Data missing" }}
{{ getData() }}     //String interpolation with a function call returning a string

[property]="data" //Property Binding
```

One-Way: HTML interacting with TypeScript
```html
<input (event="expression")></input>

<button 
	class="btn btn-primary" disabled>                 <!--disabled is hardcoded-->
	Press Me
</button>

<!--Using [] allows Angular to interact with the DOM-->
<button
	class="btn btn-primary" [disabled]="isDisabled"> <!--bind disabled to isDisabled-->
	Press Me
</button>

<p>{{ title }}</p>          <!--String interpolation--> 
<p [innerText]="title"></p> <!--Property binding-->
```

Use String Interpolation Binding for displaying a property
Use Property binding for changing a property

Two-Way Binding
```TS
[(ngModel)]="data"
```

### Event Binding
#EventBinding
<a href="https://angular.io/guide/event-binding">Angular.io/event-binding</a>

Two-way binding (BAD method)
```html
<!-- Input updates the name using event listeners -->
<input 
	type="text"
	class="form-control"
	(input)="onUpdateName($event)"> //$event is a reserved variable for the data

<!-- (click) calls a function -->
<button 
	(click)="onCreateHome()"> <!--(eventName)="functionCall()"-->
</button>
```
```ts
pageName = "";
homePageCreatedStatus: boolean = false;

onUpdateName(event: Event) {
	this.pageName = (<HTMLInputElement>event.target).value //Cast it as an input element
}
onCreateHome() {
	this.homePageCreatedStatus = true
}
```

### Two-Way Binding
#ngModel #Input #ngForm
Two-way binding (GOOD method) 
```html
<input 
	type="text"
	class="form-control"
	[(ngModel)]="pageName"> <!-- Two-way bound to pageName property-->
	<!-- Input will have a default value of 'Initial Page Name' -->
```
```ts
pageName = "Initial Page Name" //This variable will automatically update from input's value
```

## Directives
#Directive
Directives are DOM instructions
Components are directives but with a template
Structural directives can add or remove elements from the DOM
Attribute directives can only change the element within the DOM

#NgIf #StructuralDirective
```HTML
<p *ngIf="showParagraph; else dontShow">
This code only shows if the property showParagraph is true
</p>
<!-- *ngIf uses an '*' because it's a structural directive -->
<!-- If false then that element is removed from the DOM entirely -->

<ng-template #dontShow>
	<p>Name isn't showing</p>
</ng-template> 
<!-- '#' represents a local -->
```

### `[ngStyle]`
#ngStyle #AtttributeDirective 
Allows dynamic CSS styling
```HTML
<p [ngStyle]="{backgroundColor: getColour()}"> 
	<!-- ngStyle is wrapped within [] because it's using data binding-->
</p>
```
```ts
	getColour(){
		return this.homePageEnabled === true ? 'green' : 'red'; //Show green if enabled
	}
```

### `[ngClass]`
#ngClass #AtttributeDirective
Allows dynamic CSS classes
```ts
<p [ngStyle]="{backgroundColor: getColour()}"
   [ngClass]="{enabled: homePageEnabled === true}" //if true then add class 'enabled'
> 	
	<!-- ngStyle is wrapped within [] because it's using data binding-->
</p>
```
```scss
.enabled {
	color: green;
}
```

### `*ngFor`
#ngFor #StructuralDirective
```HTML
<p *ngFor="let page of pages"></p> <!-- Creates a <p> for each page -->
<ui-card *ngFor="let card of cards"></ui-card> <!-- Creates several components -->
```

Finding the indexes for each element of an #ngFor
```HTML
<ui-card *ngFor="let card of cards: let i = index"
	[ngStyle]="backgroundColor: i <= 3 ? 'lightblue : 'transparent'">		

</ui-card>
<!-- index is a reserved property for *ngFor -->
```

## Decorators

### `@Input()`
#Input #Alias
```TS
@Input() elementStructure: { name: string, type: string }; //[elementStructure]=""
@Input('element') elementStructure: { name: string, type: string }; //[element]=""
//Instead of using [elementStructure] to provide a value, you now use an Alias instead 
```


##  RxJS
#RxJS is a library for asynchronous and event-based programs using observable sequences.

```JS
//Default JavaScript
document.addEventListener('click', () => console.log('Clicked!'));

//RxJS
fromEvent(document, 'click') //Takes a DOM element and an event listener
.subscribe(() => console.log('Clicked!'));
```

### Purity
```JS
//Default JavaScript - Impure
let count = 0;
document.addEventListener('click', () => console.log(`Clicked ${++count} times`));

//RxJS - Pure
fromEvent(document, 'click')
  .pipe(scan((count) => count + 1, 0))
  .subscribe((count) => console.log(`Clicked ${count} times`));

//scan() is the RxJS equivilent of JS's reduce()
```

### Flow
```JS
//This function limits the users input of clicks to be limited to once per second

//Default JavaScript
let count = 0;
let rate = 1000;
let lastClick = Date.now() - rate;
document.addEventListener('click', () => {
  if (Date.now() - lastClick >= rate) {
    console.log(`Clicked ${++count} times`);
    lastClick = Date.now();
  }
});

//RxJS FLOW
fromEvent(document, 'click')
  .pipe(
    throttleTime(1000),
    scan((count) => count + 1, 0)
  )
  .subscribe((count) => console.log(`Clicked ${count} times`));
```

### Flow Control Operators
```JS
filter
delay
debounceTime
take
takeUntil
distinct
distinctUntilCharged
```

### Values
```JS
//Default JavaScript
let count = 0;
const rate = 1000;
let lastClick = Date.now() - rate;
document.addEventListener('click', (event) => {
  if (Date.now() - lastClick >= rate) {
    count += event.clientX;
    console.log(count);
    lastClick = Date.now();
  }
});

//RxJS Value usage
fromEvent(document, 'click')
  .pipe(
    throttleTime(1000),
    map((event) => event.clientX),
    scan((count, clientX) => count + clientX, 0)
  )
  .subscribe((count) => console.log(count));
```

### Observables
[Observables](https://angular.io/guide/observables) are lazy-push collections of multiple values

|  | Single | Multiple |
| - | - | -| 
| Pull | Functions | Iterators |
| Push | Promises | Observables |

To invoke an observable, it needs to be subscribed to. Some types of observables are automatically stopped after execution such as a HTTP GET request, however, other types will need to be manuallly stopped or otherwise they will result in memory leaks.

### Subscriptions
[Subscriptions](https://angular.io/guide/observables#subscribing) are needed for initialising an instance of an Observable
```JS
const observable = new Observable((subscriber) => {
  subscriber.next(1);
  subscriber.next(2);
  subscriber.next(3);
  setTimeout(() => {
    subscriber.next(4);
    subscriber.complete();
  }, 1000);
});

console.log('just before subscribe');
observable.subscribe({
  next(x) {
    console.log('got value ' + x);
  },
  error(err) {
    console.error('something wrong occurred: ' + err);
  },
  complete() {
    console.log('done');
  },
});
console.log('just after subscribe');


//Console Logs
>>just before subscribe
>>got value 1
>>got value 2
>>got value 3
>>just after subscribe
>>got value 4
>>done
```

Subscription with an unsubscription preventing memory leaks.
```TS
//CORRECT USE OF OBSERVABLES
//Subscription which unsubscribes when the component is destroyed
private countToInfinitySubscription;

constructor() {}

ngOnInit() {
	this.countToInfinitySubscription = interval(1000).subscribe(count => {
	console.log(count);
	})
}

ngOnDestroy(): void {
	this.countToInfinitySubscription.unsubscribe(); //Prevents memory leaks
}

//INCORRECT USE OF OBSERVABLES
//Subscription without an unsubscriber allowing memory leaks
ngOnInit() { //Exiting from this component DOESN't stop this subscription
	interval(1000).subscribe(count => {
		console.log(count);
	})
}
```

```TS
//This HTTP GET observable is automatically unsubscribed from when completed
getAnimals(){
	this.http.get("https://localhost:5001/api/animals")
	.subscribe({
	  next: res => this.animals = res,
	  error: err => console.log(err)
});
```

```TS

```

### Pipes


## JavaScript - Asynchronous Programming

### Callbacks
A **Callback** function is a function which is passed into another function with the expectation that the callback will be called at the appropriate time. It is a form of asynchronous programming native to JavaScript. The drawback is that it can quickly descend into 'callback-hell'.

```JS
//This example uses JavaScripts native callbacks and event listeners
function doStep1(init, callback) {
  const result = init + 1;
  callback(result);
}

function doStep2(init, callback) {
  const result = init + 2;
  callback(result);
}

function doStep3(init, callback) {
  const result = init + 3;
  callback(result);
}

//This is known as 'Callback-hell' as it's difficult to debug as an error can be at any nested level within the function instead of only at the top level of doOperation()
function doOperation() {
  doStep1(0, (result1) => {
    doStep2(result1, (result2) => {
      doStep3(result2, (result3) => {
        console.log(`result: ${result3}`);
      });
    });
  });
}

doOperation();
```

### Promises
A [promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise#description) is a proxy for a value which may be unknown on creation of the promise. Handlers can be attached to either the 'fulfilled' or 'rejected' response. Promises can hold one of three states: 1. Pending, 2. Fulfilled, 3. Unfulfilled. When a promise is either fulfilled or unfulfilled, it's deemed 'resolved' and can no longer have any state changes.
![[Pasted image 20230114221352.png]]

## Debugging
#SourceMaps
Sourcemaps allow the browser to read in main.bundle.js which contains all components, modules etc... and then display it as the source formatting i.e. app.component.ts
The quickest way to use this is by opening F12/Sources/webpack://./src/app
Adding a breakpoint into that code will show the local properties and their values at the time of the breakpoint
