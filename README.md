## Install
Basic-promise is a module promise with a simple syntax
```shell
npm install basic-promise
```

**Basic**
```js
var promise = require('basic-promise');
var p = promise(); // => Declare the promise

p.then(function(a){ // => The promise is resolved
	console.log(a); // => Resolve param
	console.log('DONE');
}, function(a){ // => The promise is rejected
	console.log(a); // => Reject param
	console.log('ERROR')
}, function(){ // => The promise is complete (after resolve or reject)
	console.log('COMPLETE');
});

//or

p.on('resolve', function(a){ // => The promise is resolved
	console.log(a); // => Resolve param
	console.log('DONE');
})
.on('reject', function(a){ // => The promise is rejected
	console.log(a); // => Reject param
	console.log('ERROR')
})
.on('complete', function(){ // => The promise is complete (after resolve or reject)
	console.log('COMPLETE');
});

p.resolve('a'); // => Execute the function for resolve with the param "a"
p.reject('a'); // => Execute the function for reject with the param "a"
```

**Multiple**
```js
var ps = [promise(), promise()]; // => Array of promises
// or
var ps = [promise().then(function(){ // => Array of promises with listener events
    console.log('resolve');
},function(){
    console.log('reject');
}, function(){
    console.log('complete');
}),
promise().then(function(){
    console.log('resolve');
},function(){
    console.log('reject');
}, function(){
    console.log('complete');
})];
// or
var ps = 2; // => Number of promises

var p = promise(ps);
p.then(function(){
	console.log('All the promises is resolve');
}, function(){
	console.log('Minimum one was rejected');
}, function(){
	console.log('All the promises were completed');
});

//Only with multiple promises
p.promises; //Return an array of promises
p.eq(2); //Returns the promise to fix the position 2 (the position is 0 to infinite)

//trigger all
p.promises.forEach(function(promise, position){
	promise.resolve('This promise is: '+position);
});
//Here execute the resolve event in the multiple promise => console.log('All the promises is resolve');

```