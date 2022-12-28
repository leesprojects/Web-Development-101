<b>Idempotent</b>: When an operation always produces the same result. E.g. Adding an item to a set multiple times doesn't result in multiple of the same item in that set, it will always be just one therefore, idempotent.

```js
`1 * 1 * 1 * = 1`
```

  
<b>Ephemeral</b>: An item that lasts a very short amount of time

<b>Anonymous</b>: A function without a name, e.g.
```js
nums.map(x => x * 2)
```

<b>Predicate</b>: A function that returns a single boolean value, e.g. IsOnHomePage()
```js
function isOnHomepage(x: string){
  return x === "yes";
}
```

<b>Abstract</b>: An abstract object, in JS it means that class cannot be instantiated by itself and must be inherited.
```js
abstract class Fish {
  swim() { return '>>>>' }
}
class Shark extends Fish {
  face: "shark;
}
```

<b>Serialisation</b>: A collection of items in a fixed order.
```js
const data = {
  hello: 'world'
}
JSON.stringify(data); //Serialising a JS object into JSON to be imported into a Python script
```

```python
import json

dataFromJs = "{hello: 'world'}"

x = json.loads(dataFromJs) #Deserialise the JSON object into Python
```