<div align="center">
  <img height="60" src="https://telerikhelper.files.wordpress.com/2015/08/es6.png">
    <h1>ES6</h1>
</div>

<h2>Table of contents<h2>

- [var scope vs let scope](#scope)
- [Callback & Promises:](#callback--promises)
  - [The Callback Hell:](#the-callback-hell)
  - [Promises](#promises)
  - [Async & Await](#async--await)
- [XHR & AJAX:](#xhr--ajax)
  - [Fetch](#fetch)
  - [Axios](#axios)
- [Prototypes, Classes, OOP & The New Operator](#prototypes-classes-oop--the-new-operator)
- [Module:](#module)

## Scope

what is the difference between `var` scope and `let` scope?

<details><summary><b>Answer</b></summary>

`var` is function scoped while `let` is block scoped

```js
for (let i = 0; i < 5; i++) {
	let msg = 'zzzzzzzzz';
	console.log(msg); //prints out zzzzzzzzzzz 5 times
}

console.log(msg); //Error
```

```js
for (var i = 0; i < 5; i++) {
	var msg = 'zzzzzzzzz';
	console.log(msg); //prints out zzzzzzzzzzz 5 times
}

console.log(msg); //prints out zzzzzzzzzzz
console.log(i); //5
```

</details>

## Callback & Promises

Javascript is **a single threaded language** yet it can handle doing asynchronous stuff like

```js
console.log('I happen First!');
setTimeOut(() => {
	console.log('I happen Third!');
}, 3000);
console.log('I happen Second!');

///// OUTPUT:
//I happen First!
//I happen Second!
//I happen Third!
```

haven't you ever wonder HOW??
![Javascript](images/1.png)

### The Callback Hell

<br>

let's have an example where we have only a button on the screen and we're moving it horizontally

![image](images/2.png)

this is what a callback hell looks like, a function calling back a function, calling back a function,calling back a function ...etc

if we wanted to write this to look a little nicer it shall look like this

![image](images/3.png)

let's trigger an action to stop the button if it's about to get outside the screen

![image](images/4.png)

```js
//NB:
.clientWidth //returns the width of the screen

.getBoundingclientRect // returns dimension and position related information about selected element
```

Now let's change this a little so instead of having just a straight forward callback, we'll have 2 callbacks, one for if we can go further to the right and one if we reached the edge

![image](images/5.png)

<br>

<h4>NB:</h4>
- there's a minor issue in our code here because of the timeout, the dimensions being sent to our function are not sync with our button move , one way around this is like this

<br><br>

![image](images/6.png)
![image](images/7.png)
![image](images/8.png)
![image](images/9.png)

Can't you sense it yet? when you had one call back it was barely bearable but with two call backs it gets ugly and super looooooong, enter promises

### Promises

![image](images/10.png)

promise is a pattern for writing async code

![image](images/12.png)

this is how our long code would look like with promises

![image](images/11.png)

ok so now we understand why promises are useful, but how do we write a promise?

```js
let willGetYouADog = new Promise((resolve, reject) => {
	//promise always takes a callback function with two param resolve and reject
	let rand = Math.random();
	if (rand > 0.5) {
		resolve();
	} else {
		reject();
	}
});
console.log('willGetYouADog', willGetYouADog);

//returns either one of two objects
// Promise {<fulfilled>: undefined}
// Promise {<rejected>: undefined}
```

<h5>NB:</h5>
by default promise status is pending

```js
let willGetYouADog = new Promise((resolve, reject) => {
	//promise always takes a callback function with two param resolve and reject
	let rand = Math.random();
	if (rand > 0.5) {
		resolve();
	} else {
		reject();
	}
});

//to define what to do incase of resolve or rejection

willGetYouADog.then(() => {
	console.log("ok we're buying a dog");
});

willGetYouADog.catch(() => {
	console.log("nope we're getting a bird");
});

//this can also be written like this , which is more typical

/*

willGetYouADog.then(() => {
    console.log("ok we're buying a dog");
}).catch(() => {
    console.log("nope we're getting a bird");
});

*/
```

```js
let willGetYouADog = new Promise((resolve, reject) => {
	setTimeout(() => {
		//we added a setTimeout to simulate sending a request and waiting for it to come back or waiting for an animation to finish

		let rand = Math.random();
		if (rand > 0.5) {
			resolve();
		} else {
			reject();
		}
	}, 5000);
});
willGetYouADog
	.then(() => {
		console.log("ok we're buying a dog");
	})
	.catch(() => {
		console.log("nope we're getting a bird");
	});
```

one thing that is usually done is returning a promise from a function

```js
const makeDogPromise = () => {
	return new Promise((resolve, reject) => {
		setTimeout(() => {
			let rand = Math.random();
			if (rand > 0.5) {
				resolve();
			} else {
				reject();
			}
		}, 5000);
	});
};
makeDogPromise()
	.then(() => {
		console.log("ok we're buying a dog");
	})
	.catch(() => {
		console.log("nope we're getting a bird");
	});
```

---

<h3>
You can send and receive data inside your resolve and reject, this is useful when dealing with a real project as you'd want to know the reason if your promise was rejected
</h3>

```js
//Fake request Example:

const fakeRequest = (url) => {
	return new Promise((resolve, reject) => {
		setTimeout(() => {
			let rand = Math.random();

			if (rand < 0.3) {
				reject({ status: 404 });
			} else {
				let pages = {
					'/users': [
						{ id: 1, username: 'nene' },
						{ id: 2, username: 'bebo' },
					],
					'/about': 'this is the about page data',
				};

				let data = pages[url];

				resolve({ status: 200, data });
			}
		}, 1000);
	});
};
fakeRequest('/about')
	.then((res) => {
		console.log(
			`ABOUT REQUEST : RESOLVED REQUEST',status code: ${res.status}, data:${res.data}`, //'RESOLVED REQUEST',status code: 200, data:this is the about page data
		);
	})
	.catch((res) => {
		console.log(`ABOUT REQUEST : REJECTED REQUEST,status : ${res.status}`);
	});
```

<h4>NB: res is the data passed by the resolve or reject, then gets data from resolve and catch from reject</h4>

```js
const fakeRequest = (url) => {
	return new Promise((resolve, reject) => {
		setTimeout(() => {
			const pages = {
				'/users': [
					{ id: 1, username: 'nene' },
					{ id: 2, username: 'bebo' },
				],
				'/about': 'this is the about page data',
			};

			const data = pages[url];
			// console.log("fakeRequest -> data", data);
			// console.log("fakeRequest -> pages[url]", pages[url]);
			if (data) {
				resolve({ status: 200, data });
			} else {
				reject({ status: 404 });
			}
		}, 1000);
	});
};
fakeRequest('/goaafs')
	.then((res) => {
		//REJECTED REQUEST,status : 404

		console.log(
			`RESOLVED REQUEST',status code: ${res.status}, data:${res.data}`, //'RESOLVED REQUEST',status code: 200, data:this is the about page data
		);
	})
	.catch((res) => {
		console.log(`REJECTED REQUEST,status : ${res.status}`);
	});
```

```js
const fakeRequest = (url) => {
	return new Promise((resolve, reject) => {
		setTimeout(() => {
			const pages = {
				'/users': [
					{ id: 1, username: 'nene' },
					{ id: 2, username: 'bebo' },
				],
				'/about': 'this is the about page data',
			};

			const data = pages[url];
			// console.log("fakeRequest -> data", data);
			// console.log("fakeRequest -> pages[url]", pages[url]);
			if (data) {
				resolve({ status: 200, data });
			} else {
				reject({ status: 404 });
			}
		}, 1000);
	});
};

fakeRequest('/users')
	.then((res) => {
		console.log('data:', res.data); //data: [ { id: 1, username: 'nene' }, { id: 2, username: 'bebo' } ]
		console.log('status:', res.status); //status: 200
		console.log('request worked!'); //request worked!
	})
	.catch((res) => {
		console.log(`USER REQUEST : REJECTED REQUEST,status : ${res.status}`);
	});

// got object object when i used template literals, dkw :(
```

```js
const fakeRequest = (url) => {
	return new Promise((resolve, reject) => {
		setTimeout(() => {
			const pages = {
				'/users': [
					{ id: 1, username: 'nene' },
					{ id: 2, username: 'bebo' },
				],
				'/users/1': {
					id: 1,
					username: 'nene',
					upvotes: 360,
					city: 'Lisbon',
					topPostId: 454321,
				},
				'/users/2': {
					id: 2,
					username: 'bebo',
					upvotes: 5560,
					city: 'Cyber City',
				},
				'/posts/454321': {
					id: 454321,
					title: 'ladies and gents, may i introduce my pet pig, Hamlet',
				},
				'/about': 'this is the about page data',
			};

			const data = pages[url];
			if (data) {
				resolve({ status: 200, data });
			} else {
				reject({ status: 404 });
			}
		}, 1000);
	});
};

fakeRequest('/users').then((res) => {
	console.log('res', res); //{ status: 200, data: [ { id: 1, username: 'nene' }, { id: 2, username: 'bebo' } ] }

	console.log('data:', res.data[0].id); // 1
	const firId = res.data[0].id;

	fakeRequest(`/users/${firId}`).then((res2) => {
		console.log('res2 : ', res2); //res2 :  { status: 200, data:  { id: 1, username: 'nene',upvotes: 360, city: 'Lisbon',topPostId: 454321 } }
		console.log(res2.data.topPostId); //454321
		const topPost = res2.data.topPostId;

		fakeRequest(`/posts/${topPost}`).then((res3) => {
			console.log(res3); //{ status: 200, data:  { id: 454321, title: 'ladies and gents, may i introduce my pet pig, Hamlet' } }
		});
	});
});
```

THIS IS THE SAME AS CALLBACK HELL, there gotta be a better way

```javascript
//this is our code without all the comments and notice that we can only catch error for the first promise only

fakeRequest('/users')
	.then((res) => {
		const firId = res.data[0].id;

		fakeRequest(`/users/${firId}`).then((res2) => {
			const topPost = res2.data.topPostId;

			fakeRequest(`/posts/${topPost}`).then((res3) => {
				console.log(res3);
			});
		});
	})
	.catch((err) => {
		console.log('oh nooo', err);
	});
```

if we are returning a promise from .then() we can immediately call .then() again this is called promise chaining

```javascript
const fakeRequest = (url) => {
	return new Promise((resolve, reject) => {
		setTimeout(() => {
			const pages = {
				'/users': [
					{ id: 1, username: 'nene' },
					{ id: 2, username: 'bebo' },
				],
				'/users/1': {
					id: 1,
					username: 'nene',
					upvotes: 360,
					city: 'Lisbon',
					topPostId: 454321,
				},
				'/users/2': {
					id: 2,
					username: 'bebo',
					upvotes: 5560,
					city: 'Cyber City',
				},
				'/posts/454321': {
					id: 454321,
					title: 'ladies and gents, may i introduce my pet pig, Hamlet',
				},
				'/about': 'this is the about page data',
			};

			const data = pages[url];
			if (data) {
				resolve({ status: 200, data });
			} else {
				reject({ status: 404 });
			}
		}, 1000);
	});
};

fakeRequest('/users')
	.then((res) => {
		console.log(res);
		//{ status: 200, data: [ { id: 1, username: 'nene' }, { id: 2, username: 'bebo' } ] }

		const firId = res.data[0].id;
		return fakeRequest(`/users/${firId}`);
	})
	.then((res2) => {
		console.log(res2);
		//{ status: 200, data:  { id: 1,  username: 'nene', upvotes: 360, city: 'Lisbon',topPostId: 454321 } }

		const topPost = res2.data.topPostId;
		return fakeRequest(`/posts/${topPost}`);
	})
	.then((res3) => {
		console.log(res3);
		//{ status: 200, data:  { id: 454321, title: 'ladies and gents, may i introduce my pet pig, Hamlet' } }
	})
	.catch((err) => {
		console.log('oh nooo', err);
	});
```

each promise will work right after the promise before it if it finished successfully if not this .catch at the end will catch error for all of them

---

### promises recap

```js
let myProm = new Promise((resolve, reject) => {
	let x = 1 + 1;

	if (x == 2) {
		resolve('this is sent in the resolve');
	} else {
		reject('this is sent in the reject');
	}
});

myProm
	.then((dataFromResolve) => {
		console.log('this is in the then ::::', dataFromResolve);
	})
	.catch((dataFromReject) => {
		console.log('this is in the catch ::::', dataFromReject);
	});

//output: this is in the then :::: this is sent in the resolve
```

```js
userleft = false;
userwatchcatmemes = true;

function studyingPromise() {
	return new Promise((resolve, reject) => {
		if (userleft) {
			reject({
				name: 'userleft',
				message: ':(',
			});
		} else if (userwatchcatmemes) {
			reject({
				name: 'userleft',
				message: 'cats > ppl',
			});
		} else {
			resolve("great job, keep working hard and you'll reach your dreams");
		}
	});
}

studyingPromise()
	.then((res) => {
		console.log(res);
	})
	.catch((err) => {
		console.log(err.name + '  ' + err.message);
	});

//output: userleft  cats > ppl
```

```js
//promise.all runs all the promises and after they are all done it calls then()
const goforawalk1 = new Promise((resolve, reject) => {
	resolve('resolve of walking1');
});

const goforawalk2 = new Promise((resolve, reject) => {
	resolve('resolve of walking2');
});

const goforawalk3 = new Promise((resolve, reject) => {
	resolve('resolve of walking3');
});

//Promise.all they all run at the same time
Promise.all([goforawalk1, goforawalk2, goforawalk3]).then((data) => {
	console.log(data); //["resolve of walking1", "resolve of walking2", "resolve of walking3"]
});
//returns as soon as any promise is done
Promise.race([goforawalk1, goforawalk2, goforawalk3]).then((data) => {
	console.log(data); //resolve of walking1
});
```

```js

let prom1 =  Promise.resolve('hello');
let prom2 = '77';
let prom3 = new Promise((resolve, reject) => {
    setTimeout(resolve,2000,'goodbye')
});
let prom4 = fetch('https://jsonplaceholder.typicode.com/todos').then((res) => {
    return res.json();
});

Promise.all([prom1, prom2, prom3, prom4]).then((data) => {
    console.log(data
```

---

## Async & Await

### async

```javascript
async function greet() {
	return 'hi';
}
console.log(greet()); // Promise {<fulfilled>: "hi"}
//function preceded with async return a 'resolved' promise with the value returned

greet().then((data) => console.log(`promise resolved with value ${data}`)); //promise resolved with value hi
```

to create a promise with a rejected value throw an error!!

```javascript
async function add(x, y) {
	if (typeof x !== 'number' || typeof y !== 'number') {
		throw 'X & Y Must be numbers';
	} else {
		return x + y;
	}
}

add('a', 'x')
	.then((val) => {
		console.log(`resolved with ${val}`);
	})
	.catch((err) => {
		console.log(`rejected with ${err}`);
	});
```

```javascript
// same function without async
function add(x, y) {
	return new Promise((resolve, reject) => {
		if (typeof x !== 'number' || typeof y !== 'number') {
			reject('X & Y Must be numbers');
		} else {
			resolve(x + y);
		}
	});
}

add('a', 'x')
	.then((val) => {
		console.log(`resolved with ${val}`);
	})
	.catch((err) => {
		console.log(`rejected with ${err}`);
	});
```

### await

![await](images/await.png)

```javascript
// unfortunately not good enough example
function makeRequest(location) {
	return new Promise((resolve, reject) => {
		console.log(`making request to ${location}`);
		if (location == 'google') {
			resolve('google says hi');
		} else {
			reject('we only talk to google');
		}
	});
}

// makeRequest().then((datafromresolve) => {
//     console.log('it worked cuz I'm returning a promise', datafromresolve);
// }).catch((datafromreject) => {
//     console.log('it worked cuz I'm ret urning a promise', datafromreject);
// })

function processRequest(response) {
	return new Promise((resolve, reject) => {
		console.log(`processing response`);
		resolve(`extra information ${response}`);
	});
}

// makeRequest('google').then((res) => {
//     return processRequest(res)
// }).then((response) => {
//     console.log(response)
// })

async function dowork() {
	//with async functions you handle errors with try & cat
	try {
		const response = await makeRequest('goooaagle'); //this tells compiler to hold on and don't do anything else before this finish executing
		console.log(response);
		const processReq = await processRequest(response);
		console.log(processReq);
	} catch (err) {
		console.log('error!!', err);
	}
}
dowork();
```

```javascript
//good example
let posts = [
	{ title: 'post1', body: 'this is post1' },
	{ title: 'post2', body: 'this is post2' },
];

function getPosts() {
	setTimeout(() => {
		let outPut = '';
		posts.forEach((post, i) => {
			outPut += `<li>${post.title}</li>`;
		});
		document.body.innerHTML = outPut;
	}, 1000);
}

getPosts();

function createPost(post) {
	setTimeout(() => {
		posts.push(post);
	}, 2000);
}

createPost({ title: 'post3', body: 'this is post3' });
//the problem here is that once our body is created we can't add more elements into it, notice that adding elements to body takes one second while creating a new element takes two seconds
```

```javascript
//solution 1 using callbacks
let posts = [
	{ title: 'post1', body: 'this is post1' },
	{ title: 'post2', body: 'this is post2' },
];

function getPosts() {
	setTimeout(() => {
		outPut = '';
		posts.forEach((post, i) => {
			outPut += `<li>${post.title}</li>`;
		});
		document.body.innerHTML = outPut;
	}, 1000);
}

function createPost(post, callback) {
	setTimeout(() => {
		posts.push(post);
		callback();
	}, 2000);
}

createPost({ title: 'post3', body: 'this is post3' }, getPosts);
```

```javascript
//same functionality but with promises

let posts = [
	{ title: 'post1', body: 'this is post1' },
	{ title: 'post2', body: 'this is post2' },
];

function getPosts() {
	setTimeout(() => {
		outPut = '';
		posts.forEach((post, i) => {
			outPut += `<li>${post.title}</li>`;
		});
		document.body.innerHTML = outPut;
	}, 1000);
}

function createPost(post) {
	return new Promise((resolve, reject) => {
		setTimeout(() => {
			posts.push(post);
			const err = false;

			if (!err) {
				resolve();
			} else {
				reject('sth went wrong');
			}
		}, 2000);
	});
}

createPost({ title: 'post3', body: 'this is post3' })
	.then(getPosts)
	.catch((err) => console.log(err));
```

```javascript
//same example with async/await
let posts = [
	{ title: 'post1', body: 'this is post1' },
	{ title: 'post2', body: 'this is post2' },
];

function getPosts() {
	setTimeout(() => {
		outPut = '';
		posts.forEach((post, i) => {
			outPut += `<li>${post.title}</li>`;
		});
		document.body.innerHTML = outPut;
	}, 1000);
}

function createPost(post) {
	return new Promise((resolve, reject) => {
		setTimeout(() => {
			posts.push(post);
			const err = false;

			if (!err) {
				resolve();
			} else {
				reject('sth went wrong');
			}
		}, 2000);
	});
}

async function init() {
	await createPost({ title: 'post3', body: 'this is post3' });
	getPosts();
}

init();

//this way we solved the problem with our first example, if we removed async and await we'll get post1 and post2 only!!
```

---

## XHR & AJAX

XHR stands for XMLHttpRequests

<h4>NB: </h4> XHR doesn't support promises or arrow functions

![XHR](images/xml1.png)

```javascript
//error not working :\ xmlhttprequest is not defined .. will ignore it for now since this is not the way I will usually use

const firstReq = new XMLHttpRequest();

// you can use either onload and onerror or addeventlistner

firstReq.addEventListener('load', function () {
	console.log('it worked');
	const data = JSON.parse(this.responseText); // convert json to javascript
	console.log(data);
});
firstReq.addEventListener('error', function () {
	console.log('ERROR!!!');
});

firstReq.open('GET', 'https://swapi.co/api/planets/'); //set request method and request url
firstReq.send(); //nb: this happen async
console.log('Request Sent!!');

// Access to XMLHttpRequest at 'https://swapi.co/api/planets/' from origin 'null' has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource.
```

[Solved using this](https://chrome.google.com/webstore/detail/moesif-origin-cors-change/digfbfaphojjndkpccljibejjbppifbc)

<h4>VERY IMPORTANT NOTE:</h4>
this with arrow functions usually refers to windows object as it refers to the parent of the parent, the parent get inherited through children

<br><br>

### ajax

Converting Json to Javascript

```javascript
let data = `{"ticker":{"base":"BTC","target":"USD","price":"46738.12773829","volume":"76039.39437002","change":"20.94220054"},"timestamp":1614301922,"success":true,"error":""}`;

let parsedData = JSON.parse(data); //converting Json to Javascript

console.log(parsedData);

/*
error: ""
success: true
ticker:
base: "BTC"
change: "20.94220054"
price: "46738.12773829"
target: "USD"
volume: "76039.39437002"
__proto__: Object
timestamp: 1614301922
__proto__: Object
*/
```

Converting Javascript to Json

```javascript
const dog = {
	breed: 'lab',
	color: 'black',
	isAlive: true,
	age: 5,
	owner: undefined,
};

const stringfiedData = JSON.stringify(dog); //converting Javascript to Json

console.log(stringfiedData);
/*
{"breed":"lab","color":"black","isAlive":true,"age":5}
*/
```

---

### Fetch

![fetch](images/fetch1.png)

fetch/ promise /xhr return an <mark>object</mark>, you catch this object by setting a parameter in then() and catch()

```javascript
let prom = fetch('https://swapi.dev/api/planets/')
	.then((response) => {
		console.log(
			response.json().then((myObj) => {
				for (const iterator of myObj.results) {
					console.log(iterator.name);
				}
			}),
		);
	})
	.catch((err) => {
		console.log('EEEEERRRRRROOOOOORRRRR');
		console.log('err');
	});

prom;
```

<h5>NB</h5>
The Promise returned from fetch() won’t reject on HTTP error status even if the response is an HTTP 404 or 500. Instead, it will resolve normally (with ok status set to false), and it will only reject on network failure or if anything prevented the request from completing.

```javascript
// in order to solve this we check for the status first
let prom = fetch('https://swapi.dev/api/pzlanets/').then((response) => {
	//this triggers the error change pzlanets in the url to planets
	console.log('received object :', response);
	if (!response.ok) {
		console.log('not status 200', response.status);
		console.log('EEEEERRRRRROOOOOORRRRR');
	} else {
		console.log(
			response.json().then((myObj) => {
				for (const iterator of myObj.results) {
					console.log(iterator.name);
				}
			}),
		);
	}
});
prom;
```

OR

```javascript
let prom = fetch('https://swapi.dev/api/pzlanets/')
	.then((response) => {
		console.log('received object :', response);
		if (!response.ok) {
			throw new Error(`status code: ${response.status}`);
		} else {
			console.log(
				response.json().then((myObj) => {
					for (const iterator of myObj.results) {
						console.log(iterator.name);
					}
				}),
			);
		}
	})
	.catch((err) => {
		console.log('EEEEERRRRRROOOOOORRRRR');
		console.log(err);
	});

prom;

//NB : if you want to trigger the error change the url (/api/planets) not the domain itself (https://swapi.dev)
```

---

```javascript
let prom = fetch('https://swapi.dev/api/planets/')
	.then((response) => {
		console.log('received object :', response);
		if (!response.ok) {
			throw new Error(`status code: ${response.status}`);
		} else {
			return response.json(); //response.json() is a promise
		}
	})
	.then((myObj) => {
		console.log('Fetching all Planets (first 10)');
		console.log(myObj);
		console.log(myObj.results[0].films[0]);
		let movie = myObj.results[0].films[0];
		return fetch(movie);
	})
	.then((response) => {
		console.log('received object :', response);
		if (!response.ok) {
			throw new Error(`status code: ${response.status}`);
		} else {
			return response.json(); //response.json() is a promise
		}
	})
	.then((result) => {
		console.log('Fetching opening crawler from first movie');
		console.log(result.opening_crawl);
	})
	.catch((err) => {
		console.log('EEEEERRRRRROOOOOORRRRR');
		console.log(err);
	});

prom;
```

```javascript
// Refactoring

const checkStatusAndParse = (response) => {
	console.log('received object :', response);
	if (!response.ok) {
		throw new Error(`status code: ${response.status}`);
	} else {
		return response.json();
	}
};
const fetchM = (myObj) => {
	// console.log(myObj.results);
	for (let planet of myObj.results) {
		console.log(planet.name);
	}
	let nextURL = myObj.next;
	return fetch(nextURL);
};

let prom = fetch('https://swapi.dev/api/planets/')
	.then(checkStatusAndParse)
	.then(fetchM)
	.then(checkStatusAndParse)
	.then(fetchM)
	.then(checkStatusAndParse)
	.then(fetchM)
	.then(checkStatusAndParse)
	.then(fetchM)
	.then(checkStatusAndParse)
	.then(fetchM)
	.catch((err) => {
		console.log('EEEEERRRRRROOOOOORRRRR');
		console.log(err);
	});
```

```javascript
// how to make a function retruns a promise
//1

function xyz() {
	// your code here

	const p = new Promise((resolve, reject) => {
		resolve(your - promise - object - here);
	});
	return p;
}

//2

function xyz() {
	// your code here

	return Promise.resolve(your - promise - object - here);
}
```

---

### fetch recap

```js
// fetch is async function which allows us to hit http point and have response returned as a promise

// const promise = fetch('https://jsonplaceholder.typicode.com/todos/1');

let myprom=  fetch('https://reqres.in/api/users')

myprom.then((res) => {
    return res.json(); //take care of this silly mistake cuz it broke the code multiple times before, we use return keyword with arrow function
   })
   .then((data) => console.log(data));
   .catch( e=>console.log('error!!!',e))

```

promises vs async await

```js
fetch('https://api.cryptonator.com/api/full/btc-usd')
	.then((res) => {
		console.log('response, waiting to parse', res);
		return res.json();
	})
	.then((data) => {
		console.log('parsed response', data);
		console.log(data.ticker.price);
	})
	.catch((e) => console.log('error!!!', e));

/**
 * fetch resolve the promise as soon as it receives the header so it doesn't wait till response body is back completely (response come backin the form of seprated streams and not a single chunk)
 *! to solve this drawback we use `.json()` method and it returns another promise with the whole data
 */
```

```js
const getBitcoinPrice = async () => {
	try {
		let res = await fetch('https://api.cryptonator.com/api/full/btc-usd');
		// let data1 = res.json();
		// console.log(data1); //returns a promise!!

		let data = await res.json();
		console.log(data);
		/*
   error: ""
   success: true
   ticker:
   base: "BTC"
   change: "-145.68770750"
   markets: (9) [{…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}]
   price: "46262.72972434"
   target: "USD"
   volume: "95861.89435499"
   __proto__: Object
   timestamp: 1614346922
   */
		console.log('price', data.ticker.price);
	} catch (e) {
		console.log('error', e);
	}
};

document.addEventListener('load', getBitcoinPrice());
```

```js
// to insert data to api
let myprom = fetch('https://reqres.in/api/users', {
	method: 'POST',
	headers: {
		'Content-Type': 'application/json',
	},
	body: JSON.stringify({
		name: 'xexo',
	}),
});

myprom
	.then((res) => {
		return res.json();
	})
	.then((data) => console.log(data));
//{name: "xexo", id: "204", createdAt: "2020-10-21T12:04:45.630Z"} createdAt: "2020-10-21T12:04:45.630Z" id: "204" name: "xexo"
```

### Axios

axios resolve the promise when all the data comes back unlike fetch

```javascript
axios
	.get('https://api.cryptonator.com/api/full/btc-usd')
	.then((res) => {
		console.log(
			'old price is ' + Math.round(46559.35130774) + '... newer price is',
			Math.round(res.data.ticker.price),
		);
		let currentBitPrice = res.data.ticker.price;
		if (currentBitPrice < 46559.35130774) {
			console.log('price is down, go buy some bitcoin');
		} else {
			console.log("Price is on the rise!! you're gaining money");
		}
	})
	.catch((e) => {
		console.log('error!!!!!!!!!!!!!!!!!!!!!!!!!!', e);
	});
```

```javascript
let fetchBPrice = async () => {
	try {
		let res = await axios.get('https://api.cryptonator.com/api/full/btc-usd');
		console.log(res.data.ticker.price);
	} catch (e) {
		console.log(e);
	}
};

fetchBPrice();
```

## Prototypes, Classes, OOP & The New Operator

what is a prototype and what is `__proto__`?

<details><summary><b>Answer</b></summary>

the idea of prtotype is to make a big object which is the prototype for other objects, ie make an Array object and all the custom made arrays will inherit from the array object

`__proto__` is a property made on our "big" prototypes to collect all the shared functions that would be inherited to any smaller prototype

```javascript
Array.prototype

concat: ƒ concat()
constructor: ƒ Array()
copyWithin: ƒ copyWithin()
entries: ƒ entries()
every: ƒ every()
fill: ƒ fill()
filter: ƒ filter()
find: ƒ find()
findIndex: ƒ findIndex()
flat: ƒ flat()
flatMap: ƒ flatMap()
forEach: ƒ forEach()
includes: ƒ includes()
indexOf: ƒ indexOf()
join: ƒ join()
keys: ƒ keys()
lastIndexOf: ƒ lastIndexOf()
length: 0
map: ƒ map()
pop: ƒ pop()
push: ƒ push()
reduce: ƒ reduce()
reduceRight: ƒ reduceRight()
reverse: ƒ reverse()
shift: ƒ shift()
slice: ƒ slice()
some: ƒ some()
sort: ƒ sort()
splice: ƒ splice()
toLocaleString: ƒ toLocaleString()
toString: ƒ toString()
unshift: ƒ unshift()
values: ƒ values()
Symbol(Symbol.iterator): ƒ values()
Symbol(Symbol.unscopables): {copyWithin: true, entries: true, fill: true, find: true, findIndex: true, …}
__proto__: Object
```

all these properties will be inherited to any array we make

---

the difference between `__proto__` and `.prototype` is that `.prototype` is the original object prototype, the one you see in the example above while `__proto__` is a reference for `.prototype`, you see it on defined custom objects, they're the same thing in the end of the day

```js
let arr = [1, 2, 3];
arr.__proto__; //returns the functions above but it's a reference, they are defined on Array object, similar to defining any function on an object

/*
Array.protoype.megaman=()=>{
    console.log('megaman saved us!')
}

now Array should have a function called megaman.
*/
```

NB: it's not recommended to add your own variables and functions on the prototype

</details>

<br>

What is the deal with the `New` Keyword?


<details><summary><b>Answer</b></summary>

let's make a factory function to make colors

```javascript

function makeColor(r, g, b) {
	const color = {};
	color.r = r; //<- this is called  property
	color.g = g;
	color.b = b;
	color.rgb = function() {
		const { r, g, b } = this; //in regular function this refers to the caller which is what is on the left of the dot (.)
		return `rgb(${r}, ${g}, ${b})`;
	};
	color.hex = function() {
		const { r, g, b } = this;
		return (
			'#' + ((1 << 24) + (r << 16) + (g << 8) + b).toString(16).slice(1)
		);
	};
	return color;
}

const color1 = new Color(40, 255, 60);
color1.hex();
const color2 = new Color(0, 0, 0);
color2.hex();

color1.hex === color2.hex //false

```
the word new makes it much easier as it implicitly create us the color object and implicitly returns it

// *****************
// THE NEW OPERATOR!
// *****************

// 1. Creates a blank, plain JavaScript object;
// 2. Links (sets the constructor of) this object to another object;
// 3. Passes the newly created object from Step 1 as the this context;
// 4. Returns this if the function doesn't return its own object.


```js
function Color(r, g, b) { //function with capitalized name is called construnctor function
	this.r = r;
	this.g = g;
	this.b = b;
}
```
now with the help from the word `new` we will have the same result as the one from the factory function

PS: in constructor function the word `this` refers to the implicite object we didn't create

<br>

and in order to add function on the prototype instead of adding them as properties we use

```js
Color.prototype.rgb = function() {
	const { r, g, b } = this;
	return `rgb(${r}, ${g}, ${b})`;
};

Color.prototype.hex = function() {
	const { r, g, b } = this;
	return '#' + ((1 << 24) + (r << 16) + (g << 8) + b).toString(16).slice(1);
};

Color.prototype.rgba = function(a = 1.0) {
	const { r, g, b } = this;
	return `rgba(${r}, ${g}, ${b}, ${a})`;
};

```

this way we have the same function on each color instead of creating a new function instance on each color like in the factory code

and you call those functions the same you'd with regular function property

```js
const color1 = new Color(40, 255, 60);
color1.hex();
const color2 = new Color(0, 0, 0);
color2.hex();

color1.hex === color2.hex //true

```

</details>

<br>

what is a `class`?

<details><summary><b>Answer</b></summary>

`class` is a syntactic sugar to do factory Constructor functions, you'll achieve the same result but with a much cleaner code

```javascript

class Color {
	constructor(r, g, b, name) { //a function that executs immediately whenever a new color is created , constructor is a must in classes!!
		this.r = r;
		this.g = g;
		this.b = b;
		this.name = name;
	}
	innerRGB() { //no Color.prototype.innerRGB 🥳
		const { r, g, b } = this;
		return `${r}, ${g}, ${b}`;
	}
	rgb() {
		return `rgb(${this.innerRGB()})`;
	}
	rgba(a = 1.0) {
		return `rgba(${this.innerRGB()}, ${a})`;
	}
	hex() {
		const { r, g, b } = this;
		return (
			'#' + ((1 << 24) + (r << 16) + (g << 8) + b).toString(16).slice(1)
		);
	}
}
const red = new Color(255, 67, 89, 'tomato');
const white = new Color(255, 255, 255, 'white');

```
- the classes create a new empty object and set the value of `this` to the new object

</details>


what is `extends`?

<br>
<details><summary><b>Answer</b></summary>

```javascript
class Pet {
  constructor(name, age) {
    console.log('IN PET CONSTRUCTOR!');
    this.name = name;
    this.age = age;
  }

  eat() {
    return `${this.name} is eating!`;
  }
}

class Cat extends Pet {
  constructor(name, age, livesLeft = 9) {
    console.log('IN CAT CONSTRUCTOR!');
    super(name, age);
    this.livesLeft = livesLeft;
  }

  meow() {
    return 'MEOWWWW!!';
  }
}

class Dog extends Pet {
  bark() {
    return 'WOOOF!!';
  }

  eat() {
    return `${this.name} scarfs his food!`;
  }
}

```

`extends` keyword is used to make a class inherits the same properties from a parent class

 what is the deal with `super`?

say when you create a cat, you want it to have a property called livesleft

```javascript
class Cat extends Pet {
  constructor(name, age, livesLeft = 9) {
    this.name = name;
    this.age = age;
    this.livesLeft = livesLeft;
  }

  meow() {
    return 'MEOWWWW!!';
  }
}

```
now there's no need for name and age as each cat is already a pet and cats have properties like name and age from pet but inorder to add a property to cat you need this `constructor` keyword and thus the word `super` which will reference our pet's name and age constructor

```javascript
class Cat extends Pet {
  constructor(name, age, livesLeft = 9) {
    console.log('IN CAT CONSTRUCTOR!');
    super(name, age);
    this.livesLeft = livesLeft;
  }

  meow() {
    return 'MEOWWWW!!';
  }
}

```


</details>

<br>
<details><summary><b>Answer</b></summary>


</details>

<br>
<details><summary><b>Answer</b></summary>

```javascript


```

</details>

<br>

---

## Module

import and export statements allows you to break you code in different files and modules

- export : export classes, functions, objects or variables from a file or a module
- import : import classes, functions, objects or variables to your file

<h5>Named Exports</h5>

![alt](images/mod1.png)

**you import with the same name you exported with!!!, you can give aliases non the less after importing with that very same name**

to import a whole file you use the \* and you call the function by the alias

![alt](images/mod2.png)

as is used for giving aliases for your file names

![alt](images/mod3.png)

you can only have one default export in your file, when importing the name doesn't need curly braces

![alt](images/mod4.png)

```js
    // you will need this basic structure in your html file
    <script src="es6-module-loader-dev.js"></script>
    <script src="traceur.js"></script>
    <script type="module">
        System.import("./base.js")
    </script>
```

[es6-module-loader-dev.js](es6-module-loader-dev.js)

[traceur.js](traceur.js)

example for multiple export statment
![alt](images/mod5.png)
exporting as, same to import as
![alt](images/mod6.png)
exporting the whole file
![alt](images/mod7.png)
