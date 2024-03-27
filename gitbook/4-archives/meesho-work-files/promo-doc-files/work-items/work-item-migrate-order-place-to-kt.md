##### Situation
The Order Place Page within the Transact flow is currently implemented in Java and is responsible for executing the order placement logic, including preorders API calls and place order API calls. As part of the modularization process for Transact checkout flows, there is a need to migrate the relevant files to Kotlin.

##### Task
Migrate the following Java files to Kotlin:

- com.meesho.supply.order.OrderPlaceVm
- com.meesho.supply.order.OrderPlaceActivity

This migration is a crucial initial step in the modularization of Transact checkout flows.

##### Action 

Commence the migration of com.meesho.supply.order.OrderPlaceVm and com.meesho.supply.order.OrderPlaceActivity from Java to Kotlin, preserving the current logic. After meticulous testing to ensure functionality remains unchanged, update documentation and communicate the successful completion of the migration. This initiative aims to enhance code consistency and maintainability within the Transact checkout flows.


##### Result
The migration of Order Place Page files from Java to Kotlin lays the foundation for the modularization of Transact checkout flows, contributing to code consistency and enhancing maintainability.