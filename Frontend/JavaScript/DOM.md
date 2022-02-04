# Document Object Model - DOM

### How can we control a web page?

- a web page is made of HTML & CSS.
- HTML can be manipulated by JS.
- JS controls HTML, what we see on the screen, through **DOM**.

### What is DOM?

- JavaScript creates a tree-like representation of the HTML documentation called DOM, Document Object Model.
- DOM is a programmatic representation of HTML document which is sent by the browser.
- it is the real view of what we are seeing through the screen.
- synchronization of DOM and the screen is done by the browser.
- we can control DOM to indirectly change the screen.
- Chrome exposes another set of APIs, an object, for the JS in order to for it to interact with the HTML
- that object is called `document`

### document.querySelector()

- we can select an element of a HTML code with `document.querySelector()`
- between the parenthesis, we put `tag`, `class`, or `id`.
- in `const heading = document.querySelector('h1')` , `heading` holds the **reference** of the h1 element.
- it returns the **first** matching element.

### document.querySelectorAll()

- unlike `document.querySelector`, it returns **all** matching elements **as an array**.
- what it returns is an array of HTML nodes.
- the type of what `document.querySelectorAll()` returns is `NodeList`.

### EventListener

- we can add an EventListener to HTML elements and make it work like a button.
- it looks like something like this;

```jsx
const button = document.querySelector('#btn')

function func() {
	// some commands
}

button.addEventListener('click', func)
```

- the first parameter of `addEventListener` is `'click'` and the second parameter is name of a function that we want to execute.

### getElementById

- it is a little bit faster than `querySelector`
- it only works with `ids` , where `querySelector` works with all kinds of selectors
- `getElementById` creates a hash map of all the `ids` on the page with their corresponding references.

**Difference with `querySelector`**

`querySelector` can be nested but `getElementById` can not.

```jsx
// querySelector returns a node
// A node is a subtree of a DOM
// JS exposes querySelector methods on a node

const ul = document.querySelector('ul')
const li = ul.querySelectorAll('li') // this is possible

// getElementById does not exist on a node
// getElementById uses hash maps and indices
// getElementById can only be use with document

```

`querySelector` can be run on any node but `getElementById` only can be run on `document`

### Create elements dynamically

we use `createElement` and `appendChild` to dynamically create element to the DOM

Method 1. using `createTextNode`

```jsx
// explicit way of creating elements with tags

const ul = document.querySelector('list-item')

const li = document.createElement('li')
const b = document.createElement('b')

const textNode = document.createTextNode('Sentence ')
b.appendChild(textNode)

const textNode2 = document.createTextNode(counter)
li.appendChild(b)
li.appendChild(textNode2)

ul.appendChild(li)
```

Method 2. using `createElement` and `innerHTML`

```jsx
// implicit way of creating elements with tags

const ul = document.querySelector('list-item')

const li = document.createElement('li')
li.innerHTML = '<b>Sentence</b> ' + counter

ul.appendChild(li)
```

### Attributes

`getAttribute()` and `setAttribute()` 

```jsx
// parseInt(variable, base)
// -> base: the base of the variable like 2, 10. 16

const number = parseInt(li.getAttribute('data-counter'), 10)

const li = ul.querySelector('[data-counter="' + counter + '"]')

// setAttribute(nameOfTheAttribute, value)
li.setAttribute('data-counter', counter)
```

**Custom Attribute**

we can create a Custom Attribute using `data-` and we can use it with `querySelector()`

### CSS manipulation