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

## 