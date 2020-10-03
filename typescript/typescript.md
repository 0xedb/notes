# TypeScript Note


## Basic Types

*`boolean`, `number`, `undefined`, `null`, `string`, `bigint`, `symbol`
```ts
let married : boolean = false;
let age : number = 3
let name : string = "bruno"
let fee : bigint = 5300n


let why : undefined = undefined  
let address : null = null 

// by default null & undefined are subtypes of other types
```

<br /> 

* array
```ts
let items : string[] = ["pin", "pencil", "pen"]

// or

let items : Array<string> = ["pin", "pencil", "pen"]  
```

<br />

* tuple : fixed number of elements with known types
```ts
let set : [string, number] = ["pen", 39]
```

<br />

* enum 
```ts
enum Level {
	Beginner		// numbering starts @ 0
	Pro = 12
	Legendary	// number 14
}

let myLevel : Level = Level.Pro
let myLevel : Level = Level[1]
```


<br />

* unknown
```ts
let year : unknown 
year = 2020
year = "twenty-twenty"
```


<br />

* any
```ts
let prefer : any = 3
prefer = false
```

> differs from `unknown` in that it has access to arbitrary properties, even ones that don't exist

<br />

* void
```ts
// absense of type (eg. function return values)

function sayHi() : void {
	return "Hi!"
}

// only known and undefined can be assigned by default
``` 

<br />

* never 
```ts
// represent type value that can never occur
// Eg. function throwing exception

function BadBadBad(): never {
	throw new Error("BadBadBad")
}
```

<br />

* object
```
// representing non-primitive type

function obj(o: object | null): void {
	
}

obj({})
```


* type assertions
```ts
let len : number = (someValue as string).length

// or

let len : number (<string> someValue).length
```

<br />

* Note on `Number`, `Object`, `String`, `Boolean` etc
> Don't use these as types. Use the lower case versions
```ts
let v : String 		// Terrible Idea
let v : string		// Recommended Usage
```


<br />

## Interfaces
#### Describe shape of value
```ts 
interface Human {
	name: string;
	age: number;
	parent: Human;
}
```

* optional properties
```ts
interface Human {
	name: string;
	age: number;
	PIN?: number	;	// doesn't have a PIN
} 
```

* readonly properties
```ts
// unmodifiable after creation

interface Point {
	readonly x: number;
	readonly y: number;
}

// TypeScript provides a Readonly array 
// with all mutation methods removed via ReadonlyArray<T>

let arr : number[] = [1, 2, 200]
let roArr : ReadonlyArray<number> = arr

// Readonly vs const
// Readonly is for properties whereas const is for variables
```

* function types
```ts
// interfaces can define functions too

interface SearchFunc {
	(name: string, age : int) : Human;
}

let search : SearchFunc

search = function(name: string, age: int) : Human {
	return new Human(name, age)
}
```

* indexable types
```ts
interface StringArray {
	[index: number] : string;
}

interface MoreArray {
	[index: string] : number
}
```

* extending interfaces
```ts
interface NewOne extends SearchFunc {
	length: number
}
```


<br />


## Functions
```ts
function ab(s: string): string {
	return s
}

// with optional parameter
fucntion ab(s?: string) : string {
	return s || "hello"
}

// handling rest pararmeters
function ab(s: string, ...restOfNames: string[]) {
	// do something useful
}

// function overloads are allowed
```

<br />


## Literal Types
```ts
// string
type Easing = "ease" | "ease-in" | "ease-out"

// number
function diceRoll() : 1 | 2 | 3 | 4 | 5 | 6 {
	return 4;	 // or one of those values
}
```

<br />


## Unions & Intersection Types
```ts
// describes value that can assume several types

function getPet(): Fish | Cat | Bird {
	// do something useful
}

// intersection type
function getExpensivePet(): Expensive & Pet {
	return the_expensive_pet; 
}
```

<br />


## Classes
```ts
class Greeter {
  greeting: string;				// default public

  constructor(message: string) {
    this.greeting = message;
  }

  greet() {
    return "Hello, " + this.greeting;
  }
}

let greeter = new Greeter("world");


// readonly modifier(once set, it's locked)
// must initialize @ declaration
class Opt {
	readonly name: string

	constructor(n: string) {
		this.name = n;
	}
}

let mine = new Opt("jeep")


// parameter properties
// shortens normal format

class Opt {
	constructor(readonly name: string) {}
}

// public, private, and protected modifiers can be used


// abstract classes

// classes from which others may be derived 
// but not instantiated directly
// can contain implementation details
// abstract needs to be added before abstract methods

abstract Opt {
	abstract makeSound(): void;
	
	move(): void {
		console.log("Moving...")
	}
}

// interface can extend classes
class Point {x: number; y: number}

interface Point3d extends Point {
	z: number
}

let point: Point3d = {x: 2, y: 2, z: 1};
```

<br />

## Enums
* as above

<br />

## Generics
```ts
function doSomething<T>(thing: T) {}

interface Generically<T> {
	<T>(arg: T): T;
}

class GenericName<T> {
	zeroValue: T
	add(x:T, y: T) => T;
}

// generic constraints

function loggingIdentity<T extends Lengthwise>(arg: T) : T {}
```

<br />

> `keyof` operator
```ts
// ensure only allowed keys are used 

interface Person {
	name: string; age: number; address: string;
}

function logger(k: keyof Person) {}	
// only Person keys allowed
// strings : name, age, address
```




