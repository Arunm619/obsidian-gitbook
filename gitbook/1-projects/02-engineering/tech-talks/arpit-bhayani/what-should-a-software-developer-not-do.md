

### 1. Thinking working code is task done. 

This is the least the employer is expecting out of our work. 
Working code is not work done. Happy path alone is not work done. 

- Bare minimum = working code. 
- Code should be extensible to meet future product requirements. 
	Product will evolve. We are paid to solve business problems. create products. products will always evolve. 
	If tomorrow product asks for a new feature, it should be easily buildable. We shouldn't say we need to scrap off existing code and create afresh as we earlier the requirements were different. 

- Accomodate future product requirements.
- Well documented code. 
- Standards of the code base 
	- Every code base is unique. 
	- Practice is followed within each code base. 
	- Defining classes, constants, project structure, naming conventions,  etc. 
	- Your code should be indistinguishable from other lines of code within the code base. That is truly a good codebase. 
- Code should cover all edge cases. 
- No conditions apply. 
- New changes from new developers should not break the code. Sufficient test cases are mandatory for this to be true. 
- Unit tests, integration tests, etc.
- Code should run fast at scale. Write algorithmically best possible solution. 
These are bare minimums expectations from the employer. 


### 2. Avoid reinventing the wheel. 

We like to build stuff from scratch. 
Refrain from building libraries from scratch. 
Project delivery timeline would shoot. 
Thats not good. 
We can have bugs with new libraries compared to open-source publicly available alternative libraries.


Existing solutions doesn't fit your problem. Then you can create one. Its okay then. 

Very thoroughly discussed and get buy-ins from others. 



### 3. Don't Over-engineer

Dont think about handling billion of users on day0.
Most projects don't last more than 2 years. 

Be realistic. Know your customers. Speak with data. 
Build for your org. Unless of course if your org. is Google. then build for it. 

World is highly competitive. Get to the market fast. 
Make quick iterations. Identify PMF - product market fit and then decide to scale if it goes well. 
Don't eat up time unnecessarily on things that don't matter. 

### 4. Don't have a strong bias

YOU ARE NOT PART OF A CULT!

Dont be adamant about the tech stack. Dont get attached to it. 
They are meant to solve different problems. 

You cant write high performant application with python. You can't build LLM with Kotlin. 

Use the right tools. Learn the new tools if needed. 
Your toy is not the only best thing out there. Explore other toys as well. 


You can't use redis everywhere. It is memory-bound only. 
What happens if you want to store large amounts of data, then you have to move to dynamo db its disk bound. 


Domain of Software engineering is not prescriptive at all. There's no one size fit all solutions. 

Everything is a trade-off. There is no decision tree for everything out there in the field. 


### 5. Design patterns are not everything. 

Over abstraction, over extensibility kills productivity, developer experience. 
Makes it harder to understand the code base. 
5 layers of abstractions. so many interfaces and implementations. This is overkill.

Extensibility is good. But over-extensibility is not. 

Know your limits. Dont over do it.

Try to derive outputs and outcomes. Dont super-impose design patterns. 
Draw the line properly. 

There's no hard and bound rule to everything.










