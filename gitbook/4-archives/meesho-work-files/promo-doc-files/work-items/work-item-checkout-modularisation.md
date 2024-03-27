##### Situation
Situation is basically like 80% of the checkout code is modularised and moved out of app module. We wanted to modularise the remaining 20% too, which were basically the core and base classes for the entirety of the checkout flow from app module to checkout module.
##### Task
Identify the usage and dependency of the core classes across the packages. Move them to core checkout module. And ensure the functionality is intact. And the dependency is resolvable by other dependent packages.
##### Action 
Do tasks in a successful manner. You can eloborate on this.
Thereby achieving 100% of the modularisation, successfully moving out of app module resulting in decreased build time and improved developer productivity.
##### Result
Achieved 100% of the modularisation, successfully moving out of app module resulting in decreased build time and improved developer productivity.

Jira: [Modularise the checkout package from app module](https://meesho.atlassian.net/browse/DNC-5691)
PR: [Modularise Checkout Package](https://github.com/Meesho/supply_android/pull/7114)
