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
  - [object Object](#object-object)
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

1. syntax error
2. type error
3. range error
4. reference error
5. eval error
6. URI error


### SyntaxError : error when trying to interpret syntactically invalid code.

```javascript
alert("hello"; //syntaxError
```
<br>

### TypeError : represents an error when an operation could not be performed, typically (but not exclusively) when a value is not of the expected type. It may be thrown when:

<br>

- an operand or argument passed to a function is incompatible with the type expected by that operator or function; or
- when attempting to modify a value that cannot be changed; or
- when attempting to use a value in an inappropriate way.53


```javascript
console.logg("hello"); //type error, console.logg is not a function 
```

<br>

### RangeError : when a value is not in the set or range of allowed values.

```javascript
console.log(123.456.toFixed(2)); //123.46
console.log(123.456.toFixed(101)); //RangeError: toFixed() digits argument must be between 0 and 100 


/**
 * toFixed() method formats a number using fixed-point notation
 * 1 => to the nearest units digit
 * 2 => to the nearest tenth digit
 * 3 => to the nearest hundredth digit
**/
```
```javascript
var myError = new Error("custom err0r");


var result = parseInt(prompt('enter a value between 10 and 20', '15'));

if (result > 20) {
    throw myError;
} else if (result < 10) {
    throw new RangeError ("Out of range");
} else {
    alert("with in accepted range");
}
```
```javascript
//error properties

console.log(myError.name); //Error
console.log(myError.message); //custom err0r
```
<br>

#### error handling:

1. try ... catch

2. onerror event handler: the old standard solution, used to retrieve additional information about error and suppress error in the console

1- try and catch :

  if the try block <u>throws</u> an error will move directly to the catch block and ignore the rest of the code inside the try block... similarly if the catch block <u>throws</u> an error will ignore it and go to the finally block

  <br>

```javascript
var result = parseInt(prompt('enter a value between 10 and 20', '15'));

try{
    if (result > 20)
        throw "error!!!";
     else if (result < 10)
        throw new RangeError ("Out of range");
     else
        console.log("with in accepted range");

    console.log('logging form the try block');
}
catch(e){
console.log("logging from the catch block");
}
console.log("done");

/***
 * prompt<== 15
 * output:
 * with in accepted range
 * logging form the try block
 * done
 *
 ** prompt<== 55
 * output:
 ** logging from the catch block
 ** done
 ***/
```

```javascript
var result = parseInt(prompt('enter a value between 10 and 20', '15'));

try{
    if (result > 20)
        throw "error!!!";
     else if (result < 10)
        throw new RangeError ("Out of range");
     else
        console.log("with in accepted range");

    console.log('logging form the try block');
}
catch(e){
console.logg("catch error occurred"); //typeError here will prevent the execution of the catch block
console.log("logging from the catch block");
}
finally{
console.log("done");
}
/**
 *prompt<== 55
 * output:
 * done
 *
 * NB: if there's no finally block and the code was the same, the rest of the code wouldn't have been executed as the error in the catch would stop the execution of the rest of my code
*/

```
```javascript
var result = parseInt(prompt('enter a value between 10 and 20', '15'));

try{
    if (result > 20)
        throw "error!!!";
     else if (result < 10)
        throw new RangeError ("Out of range");
     else
        console.log("with in accepted range");

    console.log('logging form the try block');
}
catch(e){
        if (e instanceof RangeError) {
               console.log("this is a range error msg");
               console.log(e.name);
                console.log(e.message);
          } else if( e === "error!!!") {
            console.log("this is too much, man!")
          }

        console.log("logging from the catch block");
}

finally{
        console.log("done");
}

console.log("logging from after the finally block"); // will be displayed if there's no error in the catch block or the finally block

/**
 * prompt<== 55
 * this is too much, man!
 * logging from the catch block
 * done
 * logging from after the finally block
 */
```
2- onerror event :

```javascript
window.onerror = errorHandle;

function errorHandle(msg,url,l,col,err){

document.write("msg : "+msg);
document.write("<br>");
document.write("url : "+url);
document.write("<br>");
document.write("l : "+l);
document.write("<br>");
document.write("col : "+col);
document.write("<br>");
document.write("err : "+err);


return true; //will not show the error in the console
//return false will show the error in the console
}

var result = parseInt(prompt('enter a value between 10 and 20', '15'));


if (result > 20)
    throw "error!!!";
 else if (result < 10)
    throw new RangeError ("Out of range");
 else
    console.log("with in accepted range");


console.log('logging form the try block');

console.log("done");


/**
 * prompt<== 8
 * msg : Uncaught RangeError: Out of range
 * url : pen.js
 * l : 26
 * col : 7
 * err : RangeError: Out of range
 */
```

<br>

### ReferenceError :invalid reference used, raised when referring to a variable that doesn't exist in the scope


<br>

### EvalError : raised by eval when used incorrectly

<br>

### URIError : raised when encodeURI() or decodeURI() are used incorrectly

___
<br>

## object Object
<br>

### Custom Function

#### function statement vs function expression

```javascript
//function statement ... Hoisted (can be called before it's declaration)

function sum(a,b){
  return a+b;
}
//function expression  ... Not Hoisted (Has to be called after declaration)

//part after the equal sign is called anonymous function or literal function

var myFun = function (a,b){
  return a+b ;
}
```
#### Assign a function to array
```javascript
 var myArr = [1,2,3,function (a,b){
  return a+b ;
},5];

//call function
var summation = myArr[3]
summation(2,2) //4
//or
myArr[3](2,2) //4
```
#### return function from function

```javascript

function newAddingFunction (x, y, z) {
	return function () {
		return x + y + z;
	};
};

var result = newAddingFunction(1, 2, 3);
console.log(result());

```
### Custom Object
#### you can create an object using:
1. constructor
2. literal way
![object declaration](assets/imgs/customObj1.png)
#### adding properties to object with dot notation and subscript notation
![dot & subscript notations](assets/imgs/customObj2.png)


```javascript
var myCustObj = {
    name: "abbas el mehtas",
    age: 21,
    info: function () {
        return "my name is " + this.name + " I'm " + this.age + " years old." //this refers to the calling object
    }
}

console.log(myCustObj.info()) //my name is abbas el mehtas I'm 21 years old. 
```

Q: How can you create multiple object having the same properties
A: we can either use factory method or a constructor

```javascript
//factory method

function employee(nm, dept, sal) {
	return {
		name: nm,
		department: dept,
		salary: sal,
		info: function () {
			return this.name + '  works in the ' + this.department+" department";
		},
	};
}

var emp1 = employee('ahmed','mearn',2200);
console.log(emp1.info()); //ahmed  works in the mearn department 


//constructor method

function Employee(name, department, salary) {

//defining properties for the "caller object" ==> this

    this.empName = name;
    this.empDep = department;
    this.empSalary = salary;

}

var emp2 = new Employee("Aizen", "13", 13113);
console.log(emp2); //Employee { empName: 'Aizen', empDep: '13', empSalary: 13113 } 
console.log(emp2["empName"]);
```
### object methods
```javascript

//instant methods
console.log(emp2.hasOwnProperty('empName')); //true
console.log(emp2.hasOwnProperty('empname')); //false
console.log(emp2.toString()); //[object Object] .... this is the string representation of objects, its telling me it's an object from  the parent Object and It inherit from it all it's properties, hence toString()


//static functions (Class Methods)
console.log(Object.keys(emp2)); // [ 'empName', 'empDep', 'empSalary' ] 
console.log(Object.values(emp2)); // [ 'Aizen', '13', 13113 ] 

//delete property from object

delete emp2.empName

console.log(emp2); //Employee { empDep: '13', empSalary: 13113 } 

for (const key in emp2) {
        console.log(key + " : " +emp2[key])
}
//empDep : 13
//empSalary : 13113
```
Q: what is the difference between instance method and static method ?

A: Instance method are methods which require an object of its class to be created before it can be called. Static methods are the methods in Java that can be called without creating an object of class.

### data descriptor

data descriptor means :
- to prevent <u>loop</u> over the object and it properties
- to prevent <u>deleting</u> the object properties
- to prevent <u>changing the value</u> specified with a key once it's initiated ...ie property's value can't be changed

<br>

data descriptor default values:

  value: undefined;

  writable:false;

  configurable:false

  enumerable:false

##### NB : these values are added implicitly after I define my objName and PropName


```javascript
/*

//static method:

Object.defineProperty(objName,propName,{
    accessor descriptor or  data descriptor
}
})
*/

var name = "ali";
var age = 25;
var address="5 sesame st. "

var obj = {};

Object.defineProperty(obj, 'name', {
  value: name,

  writable: false, // cant change it's value once defined

  configurable: false, // cant delete the value specified to my propName

  enumerable : false // can't loop over properties in the object
});

console.log(obj.name);//ali

obj.name = "zidan";

console.log(obj.name); //ali ... even if i didn't write 'writable: false' the value would have still been ali as it's the default value, in order to change the value writable should be true

delete obj.name

console.log(obj.name);//ali

for (const key in obj) {
    console.log(i+":"+obj[key]) // NO OUTPUT, doesn't log anything as I've prevented looping over this object
}

//to define multiple properties

Object.defineProperties(obj, {
	age: {
        value: age,
		writable: true,
		configurable: false,
		enumerable: false,
	},
	addr: {
        value: address,
		writable: true,
		configurable: false,
		enumerable: false,
	},
});

obj.age = 23;
console.log(obj.age); //23
delete obj.addr
console.log(obj.addr) //5 sesame st.
```

### accessor descriptor

```javascript
var department = 'SD';


Object.defineProperties(obj, {
    department:{
        get: function () { //can remove it if I don't want the department value to be accessible  and know it's value
            return department
        },
        set: function (val) {//can remove it if I don't want the department value to be editable
            department = val;
        }
    },
    display: {
        // set: function (val) {
        //     display = val;
        // },
        get: function () {
            return 'this is a display method...' + ' my department is ' + this.department + ' my name is '+ this.name ;
        }
    }
}
)
console.log(obj.department) //SD
obj.department = "SA";
console.log(obj.department) //SA .. if there was no set property the value would have stayed the same

var displayOutput = obj.display;
console.log(displayOutput); //this is a display method... my department is SA my name is ali 
```

![](assets/imgs/DataAndAccessorDescriptor.png)
![](assets/imgs/DataAndAccessorDescriptor2.png)
___
<br>

## function Object
<br>

![function](assets/imgs/fun.png)

```javascript
//IIFE => Immediate invoke function expression
//ex:
(function (a,b){
  return a+b;
})()
```
### function object property

```javascript
function sum() {
    var total = 0;
    console.log(arguments.length)
   for (var index in arguments) {
       total += arguments[index];
   }
    return total
}


console.log(sum(1,2,3,4,5,6)) //21
```

### function object method

```javascript
//function borrow using apply .. this will make able to use .join() on the string!!

var arr = [];
var str = "Hello Javascript";

console.log(arr.join.apply(str, ['**'])); //H**e**l**l**o** **J**a**v**a**s**c**r**i**p**t 
console.log([].join.apply(str, [,]));//H,e,l,l,o, ,J,a,v,a,s,c,r,i,p,t 

//function borrow using call

console.log(arr.join.call(str, "-"));//H-e-l-l-o- -J-a-v-a-s-c-r-i-p-t .. could have been written [].join.call as well

//binding .. the pro of using binding method is that I can define how I'm joining my string in the return statement so I can return different forms for the same string

//NB if you defined how you're binding in the declaration it will ignore  what you're using to bind when using the  literal function

var res = [].join.bind(str,"-*")
console.log(res()) //H-*e-*l-*l-*o-* -*J-*a-*v-*a-*s-*c-*r-*i-*p-*t 

var res2 = [].join.bind(str,)
console.log(res2('-*-')); //H-*e-*l-*l-*o-* -*J-*a-*v-*a-*s-*c-*r-*i-*p-*t 

var res3 = [].join.bind(str,"-*")
console.log(res("--")) //H-*e-*l-*l-*o-* -*J-*a-*v-*a-*s-*c-*r-*i-*p-*t 
```

#### shadowing concept

```javascript
  var a = 7

  function foo(){
    var a = 45; // this is called shadowing as I created a variable with the same name inside the function as the global variable

  }
```

#### closure
closure means variable that are inherited in my local scope from the outer scope

![closure](assets/imgs/closure.png)
NB: I've a variable a sent already in my innerFun/result that why I ignored the value of a from the closure
![closure](assets/imgs/closure2.png)

#### IIFE Pattern
```javascript
function outerFun() {
    var arr = [];

    for (var i = 0; i < 3; i++) {

        arr.push(function () {
            console.log(i); //return 3 3 3
        })

    }

    return arr
}

var result = outerFun();
console.log(result[0]());
console.log(result[1]());
console.log(result[2]());
//explanation : the return is 3 each time as it doesn't have value for i so it get the value from the outer scope after the loop is done
--------------------------------------------
function outerFun() {
    var arr = [];

    for (var i = 0; i < 3; i++) {

        arr.push(
					(function (j) {
						return function () {
							console.log(j); //0,1,2
						};
					})(i),
				);

    }

    return arr
}

var result = outerFun();
console.log(result[0]());
console.log(result[1]());
console.log(result[2]());

//explanation the is a pattern for a well known problem, here I've made the variable i appear in my local scope by sending it each time using the immediate invoke, I sperated the scopes of the two function to avoid the problem from the previous solution where I was getting the value of i after the loop is already done

```

___
<br>
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
