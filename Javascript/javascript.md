<div align="center">
  <img height="60" src="https://img.icons8.com/color/344/javascript.png">
<h1>Javascript</h1>
</div>

<h2>Table of contents<h2>

  - [Introduction](#introduction)
  - [JavaScript Language Basics](#javascript-language-basics)
  - [JS functions](#js-functions)
  - [JS built-in objects](#js-built-in-objects)
  - [error Object](#error-object)
  - [function Object](#function-object)
  - [Browser Object Model (BOM)](#browser-object-model-bom)
  - [Document Object Model (DOM](#document-object-model-dom)
  - [Events](#events)
  - [AJAX & JSON](#ajax--json)
  - [OOP](#oop)

<br>

## Introduction:

```javascript
console.dir() // is the way to see all the properties of a specified JavaScript object
```
You can change the style of the output in the console using <mark>%c</mark>

```javascript
console.log("%c HELLO WORLD","color:blue; background:green"); //blue text with green background
```
___
<br>

## JavaScript Language Basics:
<br>
JavaScript is a loosely typed and dynamic language. Variables in JavaScript are not directly associated with any particular value type, and any variable can be assigned (and re-assigned) values of all types:
<br><br>

```javascript
let foo = 42;    // foo is now a number
foo     = 'bar'; // foo is now a string
foo     = true;  // foo is now a boolean
```
<br>

### Data Types in JS:
<br>

#### Primitive data types::
1. string
2. number
3. boolean
4. undefined
5. bigint
6. symbol
#### Structural Root Primitive::
7. null
#### Non Primitive data types::
8. object
9. function

<br>

##### NB: undefined is the initial value assigned to your variables unless you assign a value yourself
<br>

##### NB:
```javascript
var x;
console.log(typeof x); //undefined

x = null;
console.log(typeof x); //object

x = function () {
    console.log(typeof x);
}
console.log(typeof x); //function

x = {
    b:3,
    a: 5,
}
console.log(typeof x); //object
```
<br>

### Falsy values:
1. zero
2. false
3. null
4. undefined
5. empty string
<br>

<mark>any other value is truthy</mark>

##### NB:
the return statement from && is the value that resulted / not resulted the return value to be <u>false</u> while in case of || is the value that resulted / not resulted the return value to be <u>true</u>


```javascript

console.log(5 && 0); // return 0 ... false
console.log(5 && 2); // return 2 ... true

console.log(5 || 0); // return 5 ... true
console.log(5 || 2); // return 5 ... true

```

##### NB:
since one not(!) returns the opposite boolean value of the variable, double not(!!) or !(!) will return the equivalent boolean value of the variable

```javascript
console.log(!9); //false

console.log(!!9);//true
```
### Coercion
coercion happens when js parser / engine convert a data type from one type to another

```javascript
console.log(5=="5")// returns true as JS converts the numerical 5 to string, it's solved by using strict equality

console.log(3<2<1) //returns true!!.. the parser her converted 3<2 to false and the equation became false < 1 then false is changed into zero so the final equation became 0<1 which returns FALSE ... to solve this problem we use brackets => 3<(2<1) this will returns false
```

#### unary operators
![unary](assets/imgs/unary.png)
<br>

[Operator_Precedence#Associativity](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence#Associativity)
### communicating with user:

```javascript
alert("END IS NEAR!!");
var x=4;
alert("value of x: "+x);

var name= prompt("enter your name","Mr.J"); // in case the prompt showed up and I clicked cancel instead of ok the value of name will be null... the default value

var action= confirm("are you sure?") // action value is either true or false
```
___

## JS functions
<br>

### Built-in functions

```javascript
var x = "abc1001"

var x = 'abc1001';
console.log( parseInt(x)); //Nan

x = '1001abc1001';
console.log(parseInt(x)); //1001

x = '10.01abc1001';
console.log(parseInt(x)); //10

x = '10.01abc1001';
console.log(parseFloat(x)); //10.01

x = '01000';
console.log(parseInt(x, "2")); //8

// we add radix (the second parameter for the parseInt) to the to convert from binary to decimal base

//you can convert from octal to decimal by changing the radix to 8

//you can convert from Hexadecimal to decimal by changing the radix to 16


function div(x) {
  if (isFinite(1000 / x)) {
    return 'Number is NOT Infinity.';
  }
  return 'Number is Infinity!';
}

console.log(div(0));
// expected output: "Number is Infinity!""

console.log(div(1));
// expected output: "Number is NOT Infinity."
```


```javascript
//tricky examples using isFinite() & isNan()


console.log(typeof '4abc');
console.log(typeof 4);

console.log(isFinite('4abc')); //false

console.log(isNaN('4abc')); //true

console.log(isNaN('abc4')); //true

console.log(isFinite('0.4')); //true

console.log(isFinite('4')); //true

console.log(isFinite(4)); //true


console.log(isNaN("125")); //false

console.log(isNaN(125)); //false

//isFinite() returns true only if the input is a number without characters

//isNan() returns true only if the input is included in quotation marks
```

##### NB:

prompt output is always a string value so if you're getting a numerical value you need to covert it use parseInt() or parseFloat()

[octal number system](https://www.tutorialspoint.com/octal-number-system)
<br>

[hexadecimal number system](https://www.tutorialspoint.com/hexadecimal-number-system)


```javascript
//encodeURIComponent() is a used to escape special characters in javascript, while decodeURIComponent() is a return the main string back before encoding

// encodes characters such as ?,=,/,&,:
console.log(`?x=${encodeURIComponent('test?')}`);
// expected output: "?x=test%3F"

console.log(`?x=${decodeURIComponent('?x=test%3F')}`);
// expected output: "?x=?x=test?"
```
### functions:

##### NB: if you didn't specify a return statement the function returns undefined

```javascript
var x = 5;
function(){
   var x=8; //overriding a preexisted global variable  is called  shadowing
 //... the rest of your code here
}
```
##### NB: You can define variables <u>without the var keyword</u> inside a function but that results in making your variable <u>Global</u> instead of being local to the function

```javascript
var x = 4;
function dragon() {
    y = 5;
    console.log(x + y);
}
console.log(y); //undefined
dragon(); //9
console.log(y); //5
```
___
<br>

## JS built-in objects
<br>

![JS built-in objects](assets/imgs/builtinObj.png)

### String methods
<br>

```javascript
var myStr = "Welcome To Javascript World!!!!!!!!";

console.log(myStr.charAt(myStr.length - 1)); //!

console.log(myStr.indexOf("j")); //-1
console.log(myStr.indexOf('J')); //11
//NB : indexOf() is case sensitive

console.log(myStr.indexOf('script')); //15

console.log(myStr.indexOf('!')); //27
console.log(myStr.lastIndexOf('!')); //34

console.log(myStr.substr(4,11)); //ome To Java ... return 11 characters starting from character of index 4
console.log(myStr.substring(4,11)); //ome To ... returns from character of index 4 to character of index 10

console.log(myStr.split(' ')); //[ 'Welcome', 'To', 'Javascript', 'World!!!!!!!!' ] 
console.log(myStr.split('')); //[ 'W', 'e', 'l', 'c', 'o', 'm', 'e', ' ', 'T', 'o', ' ', 'J', 'a', 'v', 'a', 's', 'c', 'r', 'i', 'p', 't', ' ', 'W', 'o', 'r', 'l', 'd', '!', '!', '!', '!', '!', '!', '!', '!' ]

console.log(myStr.replace("c", "#")); //Wel#ome To Javascript World!!!!!!!! 

console.log(myStr); //Welcome To Javascript World!!!!!!!! 
```
##### NB:

all these string method don't manipulate the string
<br>ie. these methods return a new output not affecting the value of myStr is the same

<br>

### [Regexp pattern](assets/files/regExp%20pattern.pdf) :

How to write a regular expression?
<br> /pattern/flag

<br>

what are the available flags in JS:
+ i => ignore case sensitive .. search is case-insensitive: no difference between A and a

- m => multiple lines

- g=> global match .. looks for all matches, without it – only the first match is returned.

- s =>
Enables “dotall” mode, that allows a dot . to match newline character \n

- u => Enables full unicode support. The flag enables correct processing of surrogate pairs.

- y => “Sticky” mode: searching at the exact position in the text

![Regex cheat sheet](assets/imgs/cheatsheetRegex.jpeg)
<br>

### Array
<br>


#### Array Functions
<br>

```javascript
var myArr = [1, 2,3,5,10,11,7,26];

//converts an array to string
console.log(myArr.join(''));//12351011726

console.log(myArr.join());//1,2,3,5,10,11,7,26

console.log(myArr.join('*')); //1*2*3*5*10*11*7*26

console.log(myArr); //[ 1, 2, 3, 5, 10, 11, 7, 26 ] 


console.log(myArr.reverse()); //[ 26, 7, 11, 10, 5, 3, 2, 1 ] 

console.log(myArr); //[ 26, 7, 11, 10, 5, 3, 2, 1 ] 


console.log(myArr.sort()); //[ 1, 10, 11, 2, 26, 3, 5, 7 ] 

console.log(myArr.sort(function (a, b) {
	return a - b; //[ 1, 2, 3, 5, 7, 10, 11, 26 ]
}));

console.log(myArr); //[ 1, 2, 3, 5, 7, 10, 11, 26 ]


```
##### NB:
- join() didn't affect my main array's value!
- reverse() & sort affected my main array's value!

<br>

#### Associative Array
<br>

- Arrays with named indexes / user defined keys (where the keys is string) are called associative arrays (or hashes).

- JavaScript does not support arrays with named indexes / user defined keys.

- In JavaScript, arrays always use numbered indexes.

<br>

##### NB
you can't use array properties/methods or the regular for loop with associative arrays as they are basically objects in JavaScript, not a real array.

<br>

```javascript

var associativeArr = new Array();

var x = "first value";
associativeArr[x] = 1000;
associativeArr['new elem'] = 'abc';
associativeArr['username'] = 'ali';
associativeArr['user age'] = 22;
associativeArr['user skill'] = ['swim', 'dance', 'read', 'play'];

console.log(associativeArr.length);//0
console.log(associativeArr.join()); //empty string

for (let i = 0; i < associativeArr.length; i++) { //not working as there's no array to iterate through
	console.log(associativeArr[i]);
}

//the methods above would have worked if the values were stored by the index (0,1,2 ...) not the key value pair like we did

for (const key in associativeArr) {
    console.log(key + ' : ' + associativeArr[key]);
}
//first value : 1000 ​​​​​at ​​​key + ' : ' + associativeArr[key]​

//new elem : abc ​​​​​at ​​​key + ' : ' + associativeArr[key]​​​

//username : ali ​​​​​at ​​​key + ' : ' + associativeArr[key]​​​

//user age : 22 ​​​​​at ​​​key + ' : ' + associativeArr[key]​​​
 
//user skill : swim,dance,read,play 
```

### Date
![date](assets/imgs/date.png)

```javascript
var today = new Date();

console.log(today);//Mon Sep 21 2020 06:58:19 GMT+0200 (Eastern European Standard Time) 

console.log(today.getDate()); //21

console.log(today.getDay()); //1

console.log(today.getMonth()); //8

console.log(today.getYear()); //120

console.log(today.getFullYear()); //2020

console.log(today.setDate(15)); //output is the equivalent in milliseconds ...1600145930957

console.log(today);//Tue Sep 15 2020 06:59:51 GMT+0200 (Eastern European Standard Time) 

console.log(today.setMonth(1)); //output is the equivalent in milliseconds ... 1581742830840

console.log(today); //Sat Feb 15 2020 07:00:45 GMT+0200 (Eastern European Standard Time) 

console.log(today.toDateString()); //Sat Feb 15 2020

console.log(today.toLocaleString()); //2/15/2020, 7:01:15 AM 

//toDateString() & toLocaleString() don't affect the format of my today object
console.log(today); //Sat Feb 15 2020 07:01:32 GMT+0200 (Eastern European Standard Time) 

```
___
<br>

## error Object
<br>

```javascript

```

___
<br>

## function Object
<br>

```javascript

```
___
<br>

## Browser Object Model (BOM)
<br>

```javascript

```

___
<br>

## Document Object Model (DOM)
<br>

```javascript

```

___
<br>

## Events
<br>

```javascript

```

___
<br>

## AJAX & JSON
<br>

```javascript

```

___
<br>

## OOP
<br>

```javascript

```
