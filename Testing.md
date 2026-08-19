# Unit Testing
- The testing made from the smallest unit of an application usually functions
- Mainly to check the logic of the function or unit
# Jest
***Note : Refer [jest](https://jestjs.io)*** for docs
- It is a javascript testing framework
```javascript
// specs/Login.test.js

const AuthService = require('../src/Login')

const { describe , test , expect } = require('@jest/globals')

describe('Testing the Login Functionality of a Auth Service', () => { 
	// Positive Cases
	test('Given Valid Username and Password it should return true' , () => {
		// Arrange
		const authService = new AuthService()
		const username = 'admin'
		const password = 'pass@123'
		
		// Action
		
		const actualValue = authService.authenticate(username , password)
		
		// Assert
		
		expect(actualValue).toBe(true) 
	})
	
	// Negative Cases 
	test('Given invalid username and password , it should return false' , ()=>{
		const authService = new AuthService()
		const username = 'admin'
		const password = 'pass@123'
		
		// Action 
		
		const actualValue = authService.authenticate(username , password)
		
		// Assert
		
		expect(actualValue).toBe(false)
	})
})


// src/Login.js

class AuthService{
	
	constructor(){}

	authenticate(username , password){
		if(username === null || username === undefined || username.toString().trim() === ''){
			throw new Error("Username should not be null or empty")
		}
		if(password === null || password === undefined || password.toString().trim() === ''){
			throw new Error("password should not be null or empty")
		} else {
			return username === "admin" && password === "pass@123"
		}
	}
}

module.exports = AuthService
```

- ***Note : In the test package.json the scripts should be updated to select the relevant test tool***
- Run using `npm test`
# Extras
- Minimum requirements for the tests 
	- Positive cases
	- Negative cases
	- boundary / edge cases
- **TDD ( Test Driven Testing )** :  Test First Approach / Test Last Approach 
	- The better approach is Test First Approach
- **Shift Left Testing** : Approach of adding testing right from the requirements phase
- **BDD ( Behavioural Driven Development )**: Used for manual testing
- Pattern used for Testing - AAA : Arrange , Act , Assert 
