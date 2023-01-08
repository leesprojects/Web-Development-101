[Angular Glossary](https://angular.io/guide/glossary)

Attribute Directive - A type of directive that can listen to and modify HTML elements, attributes, properties and components.

Bootstrap - To run a program

Binding - Assigning a value to a variable or property, usually a variable to a DOM object

Callback - When a function is passed as an argument into another function.

Class Decorators - Immediately before a class definition, declaring the class to be given a type and provides suitable metadata. E.g. `@Component(), @Directive(), @Pipe(), @Injectable() and @NgModule()``

Class Field Decorator - A decarator statement immediately before a  field in a class declaring it's type e.g. `@Input` and `@Output`

`@Component` - A class with the `@Component` decorator associates itself with a companion template creating a definition for a view. A component is special type of directive as it extends `@Directive()` 

Data Binding - A process for displaying data values and respond to user actions such as clicks, touches, keystrokes etc... 

Decorator - A function that modifieds a class or property definition, aka an *annotation* 

Dependency Injection - A mechanism for creating and deliering parts of an application (dependencies) to other parts of the same application. Typically they are services, values or functions.

Directive - A class which can modify the structure of the DOM or attributes within a DOM and data model. Defined by the `@Directive()` decorator. There are three types of directives 1. Components (which extends `@Directive`), 2. Attribute directive and 3. Structural directive.

A selector is used to refer to a directive e.g. `<ng-container>` or `<my-directive>`

Eagar Loading - NgModules that are loaded on launch, instead of those at run time which are referred to as 'lazy-loaded'

Element - A DOM element which is an instance of the `ElemantRef` class

Entry Point - A JS Module imported by npm. E.g. `@angular/core` can be entered with `@angular/core` or `@angular/core/testing`

Immutability - The inability to alter the state of a value after creation. E.g. Reactive forms recreate a new data model with each change, whereas template-driven forms perform mutable changes using `NgModel`'s two-way data bidning to modify in place.

Injectable - Generates a dependency defined with the `@Injectable()` decarator

`@Input()` - Makes the property available as a target of property binding. Data from the template can flow into the input property  

Interpolation - A form of data-binding in a template expression

Ivy - The current compilation and rendering pipeline engine.

Just-In-Time Compilation (JIT) - The Angular JIT compiler converts angular HTML and TS into JS code at run time as part of bootstrapping. `ng build` and `ng serve` both use JIT as opposed to AOT compilation.

Lazy Loading - A process speeding up loading time by splitting the application into bundles and only loading them when needed. Whereas, eager-loaded are always loaded on launch

[Lifecycle Hook](https://angular.io/guide/lifecycle-hooks) - An interace allowing access to the lifecycle directives and components.
| Hook Method | Functionality |
| - | - |
| ngOnChanges | When an input or output binding value changes |
| ngOnInit | After the first ngOnChanges | 
| ngDoCheck | Developers custom change detection |
| ngAfterContentInit | After content initialised |
| ngAfterViewInit | After the component views are initialised |
| ngAfterViewChecked | After every check a components view |
| ngOnDestroy | Just before a directive is destroyed |

`@NgModule()` - A class definition which declares and serves as a manifest for a block of code for a specific function 

ngc - The TypeScript to JavaScript transpiler that processes angular decorators, metadata and templates emitting JavaScript code

Observable - 

Template - HTML code which is to be rendered e.g. index.html

