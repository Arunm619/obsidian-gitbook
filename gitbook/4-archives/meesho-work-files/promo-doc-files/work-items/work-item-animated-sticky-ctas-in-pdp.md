##### Situation
To enhance the user experience, we implemented dynamic smooth animations for the crucial "Add to Cart" and "Buy Now" buttons in the Meesho supply-android app's Payment Page. These buttons, utilised millions of times daily, reside in a complex Product Display Page (PDP) source code.

##### Task
To simplify the logic and improve code readability, we decided to create a library component within the mesh-android package, incorporating a finite state machine model. This would facilitate managing various states and transitions, focusing on animation and view rendering in the Animated Sticky Button Views.

##### Action
We meticulously studied states and events, introducing a finite state machine to handle the complexity. Defined states include Initial View, Potential Add to Cart Product View, Added To Cart View, Potential Immediate Buy Views, each with corresponding events to ensure smooth transitions.

##### Result
The Animated Sticky Button Views now seamlessly guide users through different states—enhancing user interaction, reducing complexity in code maintenance, and providing a structured foundation for future changes and improvements.