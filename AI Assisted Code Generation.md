# AI Assisted Code Generation
# Prompt
A prompt must contain certain things mandatorily and they are
- Role
- Context
- Output
- Task
# Code Craftsmanship
- Treating software development as a professional craft , not just writing code that works
- Writing clean , maintainable , reusable code
- continuously improving technical skills
- following good engineering practices
- taking ownership of code quality
- learning from feedback and mistakes
- collaborating effectively with the team
## Standards
### Clean Code
- Keep functions small and single responsibility
- **D**ont **R**epeat **Y**ourself : Use Modular functions to reuse the code
- **K**eep **I**t **S**imple , **S**tupid 
- Readable : Make the code easier to read by giving better variable and function naming in the code
- Create consistency in the code : indentation , braces , naming , file structuring , comments , error handling , code formatting , max function size , import organization
- Some of the tools enforcing it are : ESLint , Prettier , SonarQube
### Naming Conventions
- Variables should be in camelCasing preferably in java (Meaningful nouns)
- Functions should follow camelCasing (verbs describing action)
- Classes should be in PascalCasing
- Constants should be in SCREAMING_SNAKE_CASING
## Definition of Done and Continuous
- A shared checklist that defines when a piece of work is considered completely finished 
- More like a checklist which is maintained to keep a log of things as and when completed
### Flow 
```
Code completed -> Unit test Completed -> Code Review Completed -> Acceptance Criteria completed -> Integration Testing done -> No critical defects -> Merged to main -> Done
```

### Acceptance Criteria
- The Specific conditions that must be satisfied for a user story to be accepted
### Technical Dept
- The future cost createed when we choose a quick or less-than-ideal technical solution today
- Types of Debts are : 
	- Poorly Designed Code
	- Missing tests
	- Temporary workarounds
	- Lack of Documentation
	- Duplicate code 
	- Outdated dependencies
	- Poor Architecture
### Refactoring 
- Improving the internal strucuture of the existing code without changing its behaviour
- Could include
	- rename variables
	- extract metjods
	- remove duplicate code
	- simplify conditions
	- break large classes
	- remove unused code
	- improve architecture
### Continuous  Improvement
```
Build -> Measure -> Learn -> Improve
```
### Professional Responsibility
- Code quality
- Security
- Testing
- Honestly
- Ownership
- Continuous learning

# Summary
- Craft : Professional Mindset
- Clean Code : simple and maintainable 
- Standards : consistent rules
- Naming : clear and meaningful
- AC : what to build
- DoD : when its finished
- Debt : cost of shortcuts
- Refactor : same behaviour , better structure
- Improve : keep getting better
