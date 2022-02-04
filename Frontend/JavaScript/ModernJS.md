# Modern JS - ES6+

ES6 (== ES2015) is a version of JS where a lot of new features were added to the language

## Destructured Syntax

```jsx
// ES6 == ES2015

// Destructured Syntax
// putting three dots (...) infront of an array destructures it

const arr1 = [1, 2, 3]
const arr2 = [4, 5, 6]

const arr3 = [...arr1, ...arr2]

console.log(arr3) // => [1, 2, 3, 4, 5, 6]

const arr4 = [arr1, arr2]

console.log(arr4) // => [ [1, 2, 3], [4, 5, 6] ]

// object destructuring

const obj1 = {
	name: 'mehul'
}

const obj2 = {
	// if destructured properties overlap,
	// latest property gets assigned to the value
	name: 'john', 
	age: 22
}

const obj3 = {
	...obj1,
	...obj2
}

console.log(obj3) // => { "name": "john", "age": 22 }
```

### Property Shorthand

```jsx
var name = 'bar';

var foo = {
  name: name
};

// shorthand
var foo = {
  name
};
```

## Arrow Function

**No hoisting**

unlike normal function with `function` declaration, using a ‘arrowed’ function before its declaration throws an error

→ normal function with `function` declaration gets hoisted to the top. Therefore, where the function is called doesn’t matter when it comes to `function` declared functions.

```jsx
const arrowFunction = (arg) => {
	return arg * 2
}

// if there is no function body, return can be omitted
const arrowFunction = (arg) => arg * 2

// if there is one argument, brackets also can be omitted
// zero or more than two argument needs brackets
const arrowFunction = arg => arg * 2
```

## Array Methods

### Map

```jsx
// iterated the entire array and
// returns a value according to the input callback function
****
const arr = [1, 2, 3, 4, 5, 6, 7, 8]
const forloop = []

for (let i = 0; i < arr.length; i++) {
	const el = arr[i]
	forloop.push(el ** 2)
}

const newMappedArray = arr.map(element => element ** 2)

console.log(arr, newMappedArray) // => [1, 2, 3, 4, 5, 6, 7, 8] [1, 4, 9, 16, 25, 36, 49, 64]
// map does not mutate the original array
```

### Filter

```jsx
// takes a boolean return function and
// includes the element if the function is true, excludes the vice versa

const arr = [1, 2, 3, 4, 5, 6, 7, 8]

const filteredArray = arr.filter(element => element < 5)

console.log(filteredArray) // => [1, 2, 3, 4]

const friends = {
	{
		name: 'x',
		age: 17
	},
	{
		name: 'y',
		age: 21
	},
	{
		name: 'z',
		age: 22
	}
}

const filteredFriends = friends.filter(friend => friend.age > 18)

console.log(filteredFriends) // => 'y', 'z'
```

### Find

```jsx
const friends = {
	{
		name: 'x',
		age: 17
	},
	{
		name: 'y',
		age: 21
	},
	{
		name: 'z',
		age: 22
	}
}

const findX = friends.find(friend => friend.name === 'x')

console.log(findX) // => 'x'
```

### ForEach

```jsx
const friends = {
	{
		name: 'x',
		age: 17
	},
	{
		name: 'y',
		age: 21
	},
	{
		name: 'z',
		age: 22
	}
}

friends.forEach(friend => {
	// similar to normal for-loop
})
```

## Template Literals

```jsx
// we need \ at the end of line to make multiple line string literals

const aboutMe = 'This is me.\
\
\
This will break'

// another way of making multiple line string literals is to use backticks(`)
// this is called template literals

const aboutMeLatest = `This is me.

dsfdsdfsdf

This will not break`
```

```jsx
const person = {
	name: 'chaejun',
	age: 22
}

const aboutMe = 'My name is' + person.name + 'and I am ' + person.age + 'years old'

// we can use ${} to inject variables in the template literals
const aboutMeLatest = `My name is ${person.name} and I am ${person.age} years old`
```

## Promise and Fetch

```jsx
// fetch() returns a 'Promise' object
const promiseObject = fetch('/data.json')

promiseObject.then(response => {
	const promiseObject2 = response.json()
	promiseObject2.then(data => {
		console.log(data) // => {'record': 'value'}
	})
})
```

### Promise

Promise is an object which promises, it does not say that it will definitely, to resolve a value in near future

How do we know that the promise object got the value?

We do that by adding `.then()` after the promise object.

`.then()` accepts a function which has `data` as a first parameter.

That `data` is the resolved value.

### Summary

`fetch` is an API from the browser which returns a `promise` object.

`promise` is an object which promises to deliver a value sometime in the near future.

As soon as the object has the data, `.then()` runs.

To read the data in json format, use `.json()` , which returns another promise object.