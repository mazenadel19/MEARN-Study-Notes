<div align="center">
  <img height="60" src="https://img.icons8.com/color/344/javascript.png">
<h1>Javascript</h1>
</div>

<h2>Table of contents<h2>

- [Introduction:](#introduction)




<br>

## Introduction:

Primitive Data types: string,number,boolean,null,undefined

What does it mean for a variable to be primitive?

Anything in JS is being dealt with as an object, these data types are assigned to the window object directly as they don't have a parent object that they are created from

```js
var x="123";
console.log(x); //123
console.log(window.x); //123
```

```js
//trivia

var y=null;
typeof y//object;

var z;
typeof z//undefined
y==z //true ==>both has absent of value meaning
y===z // false .. case is different with strict equality as it checks for the vakue and the datatype

```

```js
var str=new String("madia");//memory (size of object)
var str="madia";
```

difference between the first case where I used the constructor way and the literal way of creating a string like the second example is the memory allocated to both.
in case of using a constructor more memory is being consumed as it's creating an identical instance with all the properties it find in the parent it's created from

the literal way depends in it's creation on th built in function in js, it doesn't inherit the properties from string object.

NB: primitive variable can be converted to an object from the same type IN RUN TIME ONLY by simply adding a dot after it's name, it's being wrapped into an object but not a real object

```js
str._____
```

to remove a property in runtime
```js
var book = {
    Name: "JS",
    "Version": 2,
    Edition: 1.2,
    published: false,
    publishedDate: new Date(),
}

delete publishedDate

//outpout

/**
*   var book = {
*    Name: "JS",
*    "Version": 2,
*    Edition: 1.2,
*    published: false,
**/
```
to check if a property exists in object

```js
published in book //true
```

to return all the keys from an object
```js
Object.keys(book) //return array of the properties in book object

// or

for (key in book){
    console.log(key)
    console.log(book[key])// if i wanted to retrieve the values for the keys
    console.log(book.key)// returns 7 undefined as it looks up for a property called key
}

for(key in book){
    if(typeof book[key] !=="function")
    console.log(book[key]); //get all props values
}
```