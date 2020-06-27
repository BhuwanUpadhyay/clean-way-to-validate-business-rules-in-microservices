# Clean way to validate business rules in Microservices

Blog: <https://bhuwanupadhyay/blog/clean-way-to-validate-business-rules-in-microservices/>

## Walkthrough

Validating business rules in software system needs to proper consideration to acheive notable advantages: easy to change in the future, easy to test, maintain data consistency and easy to diagnose. By structuring and checking business rules appropriately reduces the possibility of error and makes the maintenance easier.

This article will cover how practically implement the best way to validate and structure business rules in microservices. Let's say we have to develop a microservice for an Order Management Process. It has various business rules that needs to check during different order state. 

![](https://raw.githubusercontent.com/BhuwanUpadhyay/clean-way-to-validate-business-rules-in-microservices/master/assets/bpm.png)
