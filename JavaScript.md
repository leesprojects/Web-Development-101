#JavaScript 
![[JavaScript Cheatsheet.pdf]]

## Event Loop
#EventLoop
<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop">Event Loop by Mozilla</a>
Javascript has a runtime model based on an event loop responsible for executing the code, collecting and processing events and executing queued sub-tasks. 

![[JS Event Loop.png]]

### Stacks
When a function is called, a frame is created with the associated arguments and local variables and is added to a (First In, Last Out) stack. Any nested function calls will then create additional frames pushed into the stack meaning that nested functions are executed first, and work their way up to the parent function.

```js
function foo(b) {
  const a = 10;
  return a + b + 11;
}

function bar(x) {
  const y = 3;
  return foo(x * y);
}

const baz = bar(7); // assigns 42 to baz

//Push Frame 1: Call bar(7)
//Push Frame 2: bar(7) calls foo(21)
//Pop Frame 2 : foo() returns 42 to bar()
//Pop Frame 1 : bar() returns 42 to property baz as an assignment
```

### Heaps
A heap is where Objects are allocated a mostly unstructured region of memory.

### Queues
JavaScript runtime uses a message queue, each message has an associated function which is called ot handle the message. The queue one started, will continue until there are no more messages.
When the queue is ready to process, it starts from the oldest message (First In, First Out) creating a stack frame for each message calling a function using the message as a parameter.

```js
//Typical event loop implementation
while (queue.waitForMessage()) { //Queue is processed synchronously
  queue.processNextMessage();
}
```

#### "Run-to-completion"
The queue must fully process and complete a message before continuing. This is different from other languages like C where if a function runs within a thread, it can be paused so another piece of code can be run before it finishes.
The downside to it being a synchronous queue system is that if a message takes too long to complete it can severely reduce performance.

setTimeout takes in two parameters, (message, duration) where duration is actually the minimum amount of time needed for completion. Any delays indicate the minimum time for completion, and is never a guarantee. It still needs to process the item in the queue first.

```js
(() => {

  console.log('this is the start');

  setTimeout(() => {
    console.log('Callback 1: this is a msg from call back');
  }); // has a default time value of 0

  console.log('this is just a message');

  setTimeout(() => {
    console.log('Callback 2: this is a msg from call back');
  }, 0);

  console.log('this is the end');

})();

// "this is the start"
// "this is just a message"
// "this is the end"
// "Callback 1: this is a msg from call back"
// "Callback 2: this is a msg from call back"
```

### 'Never blocking'
The event loop has a property where the application is waiting for an IndexedDB query or XHR to return, it can still process other things such as I/O

## Syntax

```javascript
//Strings
const str = "Hello, World!";

str.toUpperCase();                //"HELLO, WORLD!"
str.toLowerCase();                //"hello, world!"
[str.length - 1];                 //"!"
str(0);                           //"H"
str(-1);                          //"!"
`Sample text: ${str}`             //"Sample text: "Hello, World!"

str.trim() ;                      //Removes leading and trailing spaces
str.endsWith("!");                //Returns true
str.replace(" ", "-");            //Replace the leftmost space with a dash
str.replaceAll(" ", "-");         //Replace all spaces with dashes
str.split(" ");                   //Split a string into an array with the " " delimiter

//Numbers
let num = "12345";
num.toString();                   //"12345"
Number.parseInt(num, 10);         //12345, parse 10 as the Radix
11 % 2                            //1

//Variables
let number = 123                  //Reassignable
const string = "Hello, World!"    //Cannot be reassigned

//Arrays
let animals = ["Jaguar", "Cat", "Dog"];

animals.push("Fish");
animals.pop();
animals.length = 0                //Most efficient way to empty an array
lastAnimal = animals.at(-1)       //Get's the Nth element
animals.includes("Jaguar");       //Returns a bool
animnals.splice(1, 2);            //Gets the first 2 elements starting from [1]
animals.forEach(animal {
  console.log(animal);            //Iterates through each element
});
animals.filter(animal => {
  return animal.substring(2);     //Returns an array of results
});
animals.find(animal {
  return animal === "Jaguar"      //Returns an index if present
});
animals.map(animal {
  return animal.toUpperCase();
});
animals.every(animal {
  animal => animal === "Jaguar"   //Returns false
});
animals.some(animal {
  animal => animal === "Jaguar"   //Returns yes
});

//Arrow Functions
const grades = [10, 20, 15];
const didPass = (grade) => {
  return grade >= 15
};

function sum(a = 0, b = 0) {      //Returns the product, or 0
  return a + b;
};

const double = x => x * 2;        //No returns on implicit return

//String cases
function StringTo(string){
    //return string.toUpperCase();
    return string.toLowerCase();
}

//String Indexing
function IndexAt(string, index){
    //return string[0]; //Returns the nth character (use index = string.length -1 for the last character)
    //return string.at(1); //Returns the first character (Start to End)
    return string.at(-1); //Returns the last character (End to Start)
}

//Substrings
function Substring(string, indexStart, indexEnd = 0){ //indexStart is Inclusive, indexEnd is Exclusive
    //return string.substring(1); //Returns character 1 to end
    return string.Substring(1, 10); //Returns characters 1 through 9
}

function AddStrings(stringA, stringB){

    return stringA += stringB;
}

function TemplateString(){ //Use ``, it gives access to more
    return `This is a
            multi-line Template String
            which is perfect for
            html code and formatting`
}

function StringInterpolation(value){
    return `Here's a dynamic string with a value of ${value}`;
}

function StringParsing(number){
    //return number.toString();
    //return Number.parseInt("The ladder is 2 metres long", 10); //Returns NaN
    return Number.parseInt("The ladder is 2 metres long", 10); //Returns 2
}

function MathRounding(number){
    return Math.floor(number);
    return Math.ceil(number);
    return Math.round(number);
}

function LetAndConst(){
    let variableA = 1; //let is a re-assignable declarator
    variableA = 2; //Use 'let' for things like incrementers
    variableA = 505;
    const variableB = 1; //const is a non re-assignable declarator
    //variableB = 2; //Returns an error
}

function Modulo(wholeNumber){
    if(wholeNumber % 2 === 0){
        //It's even
    }else{
        //It's odd
    }
}

function Arrays1(){
    const animals = []; //Making an array a const, gives us access to array-specific methods
    animals.push("Dog"); //We can add to a const array because it's not immutable!
    animals.push("Cat");
    animals.at(0); //Returns "Dog"
}

function ForEach(){
    console.log("hello");
    const animals = ["Dog", "Cat", "Fish"];
    const animalsUpperCase = [];
    animals.forEach(function(animal){
        animalsUpperCase.push(animal.toUpperCase());
        console.log(animal);
        return animal; //This returns from the loop callback, but is only useful if it's assigned a variable
    });
    return animalsUpperCase;
}

function ArrayFilter(){
    const numbers = [1, 2, 30, 177, 17, 22, 8];
    let numbersFiltered = numbers.filter(function(number){
        return number <= 30;
    })
    console.log(numbersFiltered);
}

function ArrayFind(){
    const animals = ["Dog", "Cat", "Fish"];
    findResult = animals.find(function(animal){ //Returns the string if found or undefined if not found
        return animal === "Cat";
    })
    console.log(findResult);
}

function ArrayMap(){
    const numbers = [1, 2, 30, 177, 17, 22, 8];
    let numbersMapped = numbers.map(function(number){
        return number * 2;
    })
    console.log(numbersMapped);
    
    const animals = ["Dog", "Cat", "Fish"];
    let animalsUpper = animals.map(function(animal){
        return animal.toUpperCase();
    })
    console.log(animalsUpper);
}

function ArrayIncludes(){
    const numbers = [1, 2, 30, 177, 17, 22, 8];
    const target = 30

    includesNum = numbers.includes(target);
    console.log(includesNum);
}

function ArrayJoin(){
    const animals = ["Dog", "Cat", "Fish"];
    joinedAnimals = animals.join(" | "); //The first parameter is the "glue"
    console.log(joinedAnimals);
}

function ArraySort(){
    const numbers = [1, 2, 30, 177, 17, 22, 8];
    const numbersSorted = numbers.sort((a, b) => {return a-b})
    const numbersSorted2 = numbers.sort((a, b) => {return b-a})
    console.log(numbers);
    console.log(numbersSorted);
    console.log(numbersSorted2);
}

ArraySort();

function UsingMaps(){
    const numbers = [1, 2, 30, 177, 17, 22, 8];
    const mapNums = new Map([
        ['name', 'Panther'],
        ['name', 'Chameleon'],
        ['name', 'Duck']
    ]);

    //Populating a map
    for(var i = 0; i < numbers.length; i++){
        mapNums.set(numbers[i], i); //Add the current number to the map using it's index as the key
    }
    
    //Map iterators
    const mapNumsIterator = mapNums[Symbol.iterator]();
    for(const item of mapNumsIterator){
        console.log(item);
    }
}

function ArraySets(){
    const numbers = [1, 2, 30, 177, 17, 22, 8, 8];
    const numbersSet = new Set(numbers); //Sets are good for removing duplicates
    const numbersSetSpread = [...numbersSet];
    const numbersSpread = [...numbers];
    console.log(numbersSetSpread);
    console.log(numbersSpread);
}
```