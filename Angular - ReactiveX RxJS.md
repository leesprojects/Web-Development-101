ReactiveX is An API for asynchronous programming with observable streams.

A stream is an abstract collection of value emitted over time, e.g. messages in a chatroom, values being entered on a form.
An observable allows you to both emit and respond to subscriptions

**Cold Observables** is when values are emitted outside of the observable producer

## Observables
```TS
//Observable (Producer of events)
var messageObservable = Observable.create((res) => {
	try{
		res.next(`It's currently ${new Date()}`);
		res.complete(`Observable was finished at ${new Date()}`);
		res.next(`I won't ever be created`) //This will never be called
	} catch(err) {
		o.error(err);
	}
});

//Observer
firstMessageObservable.subscribe(
	(x)   => console.log(x),
	(err) => console.log("There was an error")
	()    => console.log("Completed")
})

secondMessageObservable.subscribe(
	(x)   => console.log(x),
})

firstMessageObservable.add(secondMessageObservable); //The second observable is now a child element of the first meaning second follows all rules applied to first i.e. 6001ms

setTimeout(() => {
	messageObservable.ubsubscribe()
}, 6001)
```

## Subjects
```JS
var messageSubject = new Subject();
var messageReplaySubject = new ReplaySubject(30, 200); //200 is the ms of messages it will backtrace to call

messageSubject.subscribe(
	data => addItem("Observer1: " + data),
	err  => addItem(err)
	()   => addItem("Final item added")
)

messageReplaySubject.subscribe(
	data => addItem("Observer1: " + data),
	err  => addItem(err)
	()   => addItem("Final item added")
)

var messageSubject2 = messageSubject.subscribe(
	data => addItem("Subject Observer 2: " + data)
)

var messageReplaySubject = messageSubject.subcribe(
	data => addItem("Replay Observer 2: " + data)
)
```

A Behaviour Subject only differs from a Subject in that it receives the previous message instead of the next one.

## Async Subject
```TS
import { AsyncSubject } from "rxjs/AsyncSubject"

var asyncMessage = new AsyncSubject(); //AsyncSubject only retrieves the last value which is provided from the complete() subject
```

## Operators
Methods that can be used on Observables and Subjects allowing you to change the existing observable as a new observable (It does not affect the original)
Static Operators 
Instance Operators work on most RxJS operators

Uses a marble diagram
![[Pasted image 20230123201400.png]]