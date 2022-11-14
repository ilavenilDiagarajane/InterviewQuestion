##### What is the difference between Promise.all() vs Promise.allSettled()? Explain with an example.

promise.all()
- Take mutiple promise in array.
- wait for all fulfilled promise or first rejection.
- Return promise

```js
//example1 - all is resolve
const promise1 = Promise.resolve(3);
const promise2 = 42;
const promise3 = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, 'hello');
});
Promise.all([promise1, promise2, promise3]).then(
  (values) => {
  console.log(values);
},(values) => {
  console.log(values);
} )
// expected output: Array [3, 42, "hello"]

//example2 - any reject
const promise1 = Promise.reject(3);
const promise2 = 42;
const promise3 = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, 'foo');
});
Promise.all([promise1, promise2, promise3]).then(
  (values) => {
  console.log(values);
},(values) => {
  console.log(values);
} )
// expected output: 3
```


##### What is the difference between Promise.any() vs Promise.race()? Explain with an example.
Promise.any()
- Take mutiple promise in array.
- Wait for resolved promise.
- returns a single Promise.

```js
const promise1 = Promise.reject(0);
const promise2 = new Promise((resolve) => setTimeout(resolve, 100, 'first resolve promise'));
const promise3 = new Promise((resolve) => setTimeout(resolve, 500, 'second  resolve promise'));

const promises = [promise1, promise2, promise3];

Promise.any(promises).then((value) => console.log(value));
//// expected output: "first resolve promise"
```
Promise.race()
- Take mutiple promise in array.
- Wait for first resolved promise or rejected promise.
- returns a single Promise.

```js
//example1 - first reject promise
const promise1 = Promise.reject(0);
const promise2 = new Promise((resolve) => setTimeout(resolve, 100, 'first resolve promise'));
const promise3 = new Promise((resolve) => setTimeout(resolve, 500, 'second  resolve promise'));

const promises = [promise1, promise2, promise3];

Promise.race(promises).then((value) => console.log(value),(value)=>console.log(value));
//// expected output: 0

//example1 - first resolve promise
const promise1 = Promise.resolve(100);
const promise2 = new Promise((resolve) => setTimeout(resolve, 100, 'first resolve promise'));
const promise3 = new Promise((resolve) => setTimeout(resolve, 500, 'second  resolve promise'));

const promises = [promise1, promise2, promise3];

Promise.race(promises).then((value) => console.log(value),(value)=>console.log(value));
//// expected output: 100
```
#### List all lifecycle methods and their equivalent hook 
// componentWillmount
useEffect(() => {}, []);

// componentDidMount
// componentWillUpdate
// componentDidUpdate
useEffect(() => {}) || useEffect(() => {}, [dependencyArray]);

//componentWillUnmount
useEffect(() => {
  return () => {};
}, []);

#### What is higher order function? Explain with an example 
A higher order function is a function that takes a function as an argument, or returns a function.

```js

var array=[10,20,30,40]

var result=array.map((e)=>e*2);
console.log(result);
```

#### What is the difference between event stoppropagation vs stopimmediatepropagation.  Explain with an example

event stoppropagation
 - Prevents propagation of the current event.
 - capturing/bubbling phase .

  example1 - stoppropagation
 ```html

 <div class="parent" (onClick)="console.log('parent')">
    <button class="child" (onClick)="buttonClick(event)"></button>
</div>
<script>
    function buttonClick(event) {
        event.stopPropagation();
        console.log('child');
    }
</script>


 ```
 event stoppropagation
 - prevent the propagation of an event.
 - capturing/bubbling phase .
 - Prevent the execution of any other event listener attached to the element.
 
example1 - stopimmediatepropagation
```html
<script>
    $("div").click(function(event) {
      event.stopImmediatePropagation();
      alert('First click triggered');
    });

    $("div").click(function(event) {
      alert('Second click triggered');
    });
</script>
<div>Click me</div>
```
#### What is "key" prop and what is the benefit of using it in arrays of elements?
A key is a special string attribute you should include when creating arrays of elements. Key prop helps React identify which items have changed, are added, or are removed.
```js
const todoItems = todos.map((todo, index) =>
  <li key={index}>
    {todo.text}
  </li>
)
```
#### What is Lifting State Up in React? Explain with example
two child components share the same data from its parent, then move the state to parent instead of maintaining local state in both of the child components.

#### Explain the difference between Object.freeze() vs const

const 
- applies to variables. 
- It creates an immutable binding(i.e. you cannot assign a new value to the binding.)

Object.freeze 
- works on values, and more specifically, object values. 
- It makes an object immutable, (i.e. you cannot change its properties.)

```js
//example1- const value
const person = {
        name: "anu"
    };
         
person.name = "priya";
console.log(person.name);

// priya

const person = Object.freeze({name: "anu"});
 person.name = "priya";
 //anu
```
#### What strict mode in javascript?
strict mode is introduced as ES6 feature, where the code syntax and the variables cannot be used without declaration.

```js
'use strict';
str = "Hello World"; 
console.log(str);
 // => Throw a reference error

//without strict mode
 str = "Hello World"; 
console.log(str);
// hello world
```
#### What will be the output of the following JavaScript code? Why?

```js
var grades='S';  
var answer;  
switch(grades)
{  
    case 'S':  
        answer+="10";  
    case 'A':  
        answer+=" 8";  
    case 'B':  
        answer+=" 6";  
    default:  
        answer+=" 0";  
}  
document.write(result);
//"undefined1080"
```
#### What is the output of this code snippet? and Why?
```js
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}

//333
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}
//012
```
#### What's the output? Why?
```js
const person = {
name: 'Lydia',
age: 21,
};

const changeAge = (x = { ...person }) => (x.age += 1);
const changeAgeAndName = (x = { ...person }) => {
x.age += 1;
x.name = 'Sarah';
};

changeAge(person);
changeAgeAndName();

console.log(person);
```