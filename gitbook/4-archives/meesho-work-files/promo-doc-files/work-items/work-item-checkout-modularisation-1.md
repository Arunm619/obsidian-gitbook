### Checkout Modularization
##### Situation
The majority (80%) of the checkout code has been successfully modularized and moved out of the app module. However, the remaining 20%, consisting of core and base classes for the entire checkout flow, needs modularization. This step is crucial for achieving a fully modularized checkout system.
##### Task
Identify the usage and dependency of the core classes across the packages, move them to the core checkout module, and ensure functionality remains intact. Resolve dependencies to ensure other dependent packages can seamlessly utilize the modularized core classes.
##### Action 
The action involves a meticulous process of identifying dependencies, relocating core classes to the checkout module, and validating the functionality. Extensive testing and collaboration with development teams ensure a successful transition, resulting in improved developer productivity and reduced build times.
##### Result
Achieved 100% modularization by moving the remaining core classes out of the app module. This accomplishment not only decreases build times but also significantly improves developer productivity by providing a streamlined and modular codebase.
#### Competencies Achieved
- Coding & Problem Solving
- Architecture & Design
#### Reasoning
The task requires a deep understanding of the existing codebase, its dependencies, and the architectural considerations for successful modularization.
#### Links
PR Link: [Checkout Modularization PR](insert link here)  
Solutioning Doc Link: [Checkout Modularization Solutioning Doc](insert link here)