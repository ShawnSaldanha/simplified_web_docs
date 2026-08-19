# Advanced JavaScript Topics
- **NOTE :** *Some content with respect to node.js can be found at [nodejs](NodeJs.md)*
- **NOTE** : To get more in-depth about all these please refer to [mdn web docs](https://developer.mozilla.org/en-US/).

## Rest Operator
- It collects multiple values into an object or an Array
- It is passed as an argument to a function
- it should be based as a last parameter
```javascript
function Greeting(greet , ...names){
  names.forEach((name) => `${greet} , ${name}` )
}

Greeting("Good Day" , "John" , "Doe" , "Alice" , "Mary")

// Good Day , John
// Good Day , Doe
// Good Day , Alice
// Good Day , Mary
```

## Spread Operator
- It is an operator that expands/copies from an array or an object

```javascript
const numbers = [10 , 20 , 30 , 40 , 50]
const names = ["John" , "Alice" , "Mary" , "Doe" , "Jack"]

const combined = [ ...numbers , ...names]

console.log(combined)

// [ 10 , 20 , 30 , 40 , 50 , "John" , "Alice" , "Mary" , "Doe" , "Jack" ]

const maximum = Math.max(numbers)
console.log(maximum) // NaN

const max = Math.max(...numbers)
console.log(max) // 50

```
***Note:*** The Spread operator can be used in objects also .

## Destructuring

### Object Destructuring
The older way was using the **. (Dot)** operator

But , we now use the ***{ attribute1 , attribute2 } = object*** way to get the data 

```javascript
const user = {id : 1 , "name" : "John" }
const address = {"State" : "Karnataka" , "City" : "Bengaluru"}

const userDetails = {...user , ...address}

//Old Style

console.log("Hello " + userDetails.name) // Hello John

//New Style

const { name , State } = userDetails;

console.log("Hello " + name + " from " + State) // Hello John from Karnataka

```

### Array Destructuring


```javascript
const combined = [10 , 20 , 30 , 40 , 50 , "John" , "Alice" , "Mary" , "Doe" , "Jack"]
const [first , second , ...others] = combined

console.log(first)     // 10
console.log(second)    // 20
console.log(others)    // [ 30 , 40 , 50 , "John" , "Alice" , "Mary" , "Doe" , "Jack" ]
console.log(others[1]) // 40
```

### JavaScript single Threaded Model 
- JavaScript is a language that works in a single thread
- So the previous operation should finish to start the next one
#### Synchronous 
- Here the program waits for the current operations result and only then moves to the next operation .
- If a operation fails then it won't go to the next operation but instead fails

```
Time ──>

[ Step 1: run Function1() ] ──> Done
                                └──> [ Step 2: run Function2() (Takes 5 seconds) ] ═════════> Done
                                                                                             └──> [ Step 3: run Function3() ] ──> Done
```

#### Asynchronous
- Here the program uses event loop to switch between operations and does the other operations while waiting for the current one to complete
- Doesn't break the entire program
```
Time ──>

Main Code Thread:
[ run Function1() ] ──> [ run Function2() ] ──> [ run Function3() ] ───────────────────────────> [ Function2 Finish Callback ]
                             │                                                                       ^
                             │ (Starts background timer/fetch)                                       │
Background:                  v                                                                       │
                             [ Processing Function2 background work... ] ════════════════════════════╝
```
## Callback Functions
- These are the functions that are passed as an input to other functions and are executed when the main function finishes execution
```javascript

function sum(num1 , num2 , callback){
  setTimeout(()=> {
    const sum = num1 + num2;
    console.log("The sum is " + sum)
    callback(sum)  
  } , 5000)
}
function div(num1, callback){
  setTimeout(() => {
    const divRes = num1 / 2;
    console.log(divRes);
    callback()
  } , 3000)
}
function end(){
  console.log("Completed");
}
sum(100 , 200 , (total) => {
  div(total , end)
})

```
## Promises
- Is an object that generates an event that can result in either **resolve** or **reject**
- The states are **Pending** , **Resolve** and **Reject**
- So we need to use the keywords like **.then()** , **.catch()** and **.finally** to chain and call the promise for resolving it
- Note that promises are objects and are synchronous in nature , for the example we are using setTimeout to make it asynchronous
***The Approach 1 to Use Promises***
```javascript

function buyMovieTicket(accountBalance) {
  return new Promise((resolve, reject) => {
    console.log("Processing payment... Please wait.");
    
    // Simulate a 2-second network delay
    setTimeout(() => {
      if (accountBalance >= 15) {
        resolve("🎟️ Ticket purchased successfully!"); // Success path
      } else {
        reject("❌ Transaction Failed: Insufficient funds."); // Error path
      }
    }, 2000);
  });
}

// 🚀 Test Case 1: You have enough money ($50)
buyMovieTicket(50)
  .then((successMessage) => console.log(successMessage))
  .catch((errorMessage) => console.log(errorMessage));

// Output : 🎟️ Ticket purchased successfully!

// 🚀 Test Case 2: You have enough money ($5)
buyMovieTicket(5)
  .then((successMessage) => console.log(successMessage))
  .catch((errorMessage) => console.log(errorMessage));

// Output : ❌ Transaction Failed: Insufficient funds.
```

***The Approach 2 to Use Promises***
```javascript
const getData = new Promise((resolve, reject) => {
  console.log("Getting Data...");

  setTimeout(() => {
    const isServerOnline = true; 
    if (isServerOnline) {
      resolve({ id: 1, name: "John Doe", role: "Admin" }); // Success: Pass the data object
    } else {
      reject("Error: Could not connect to the database."); // Failure: Pass an error message
    }
  }, 2000);
});
getData
  .then((data) => {
    console.log("Success! Data received:", data);
  })
  .catch((error) => {
    console.log("Failed!", error);
  });


// Output if isServerOnline = true : Success! Data received: { id: 1, name: "John Doe", role: "Admin" }
// Output if isServerOnline = false : Error: Could not connect to the database.
```
## Fetch Promise
One of the 2 methods to get the API responses from the backend is **fetch** which is inbuilt in javascript
***Note:*** The fetch returns a promise that has to be handled
```javascript
	const getProductData = () => {
		const responsePromise = fetch("http://www.fakestoreapi.com/products")
		
		responsePromise.then(response => {
			if(response.ok){
				return response.json();
			} else {
				return Promise.reject("Some internal Error)
			}
		}).then(pipelinedData => {
			console.log(pipelinedData)
		}).catch(errorProneData => {
			console.log(errorProneData)
		})
	}
	
	getProductData()
```

## Async & Await
In-order to reduce the complexity of chaining caused by the Promises chaining we use Async and Await 
- await must only be used where the function is mentioned as async or say asynchronous else it will not work but instead give an error

***Approach 1 of writing the Async Await***

```javascript

const getProductData = async () => {
	const responseData = await fetch("https://fakestoreapi.com/products")
	const data = await responseData.json()
	console.log(data)
}

getProductData()

```

***Approach 2 of writing Async Await***

```javascript
async function getProductData(){
	const responseData = await fetch("https://www.fakestoreapi.com/products")
	const data = await responseData.json()
	console.log(data)
}

getProductData()
```
## Working of JavaScript and DOM
We have multiple Js Engines , google has V8 engine and mozilla has spiderMonkey and safari has Js Core . DOM means **Document Object Model** which the browser creates when an website loads .
- V8 engine cannot understand **DOM**'s , browser API bridges the gap
### Event Driven Architecture 
- It is a design pattern where the flow of the program is determined by events. An event can be a user click, a file upload, a timer finishing, or a message arriving from another server.
- **Event Listener** is the one listening to the events performed by the user to trigger an action 
- **Event Handlers** are the methods/functions which are performed when a particular event is triggered
- **Events** can be anything from loading to clicking to anything
- Passing control over to Event Handler is the job of **V8**
- 
## Extras
- **Diffing:** The process of **comparing** the old Virtual DOM with the new Virtual DOM to find out exactly what changed.
- **Reconciliation:** The entire **syncing** process where the library takes those changes and updates the real browser screen.
- Component lifecycle in react , JSX , route
