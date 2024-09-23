# How actually terraform works?

Terraform lets you define your infrastructure as code and lets you reuse that same blueprint for all of your infrastructure provisioning. 

> ***It works in few simple steps***
> 
> *Step 1:*
> 	It reads the code and decides what is the user is going to do
> *Step 2:*
> 	Therefore is goes and searches for the existing state of that infrastructure which is represented by a **Graph (Directed Acyclic Graph, where each node is a Resource)** and compares it to the code. Refer - [[002_states]]
> *Step 3:*
> 	Therefore it decides what is actaually different between those two, and it will only create or delete the only difference between the code and the state
> *Step 4:*
> 	It will give you a plan on what it is going to do and if you agree with that it will only gonna make that change