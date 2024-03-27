
Composable functions have @composable annotations

- Composable functions are the fundamental building blocks of an application built with Compose.

- Composable can be applied to a function or lambda to indicate that the function/lambda can be used as part of a composition to describe a transformation from application data into a tree or hierarchy.
- Annotating a function or expression with Composable changes the type of that function or expression. 
- For example, Composable functions can only ever be called from within another Composable function. 
- A useful mental model for Composable functions is that an implicit "composable context" is passed into a Composable function, and is done so implicitly when it is called from within another Composable function. 
- This "context" can be used to store information from previous executions of the function that happened at the same logical point of the tree.


**Modifiers**
Modifiers are a key technique in Jetpack Compose to influence both the look and behavior of composable functions
