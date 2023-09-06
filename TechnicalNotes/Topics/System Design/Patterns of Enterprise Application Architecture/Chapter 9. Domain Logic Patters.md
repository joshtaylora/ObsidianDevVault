## Transaction Script
- Organizes business logic by procedures where each procedure handles a single request form the presentation
- The majority of business applications can be thought of as a series of transactions
	- A `transaction` may view some information as organized in a particular way, another will make changes to it
- Each interaction between a client system and a server system contains a certain amount of logic
- A `Transaction Script` organizes all this logic primarily as a single procedure, making calls directly to the database or through a thin database wrapper
	- Each transaction will have its own Transaction Script, although common subtasks can be broken into subprocedures
### How It Works
- The domain logic is primarily organized by the transactions that you carry out with the system
- Structure the code into modules in a way that makes sense
- You don't need to worry about what other transactions are doing, your task is to get the input, interrogate the database, munge, and save your results to the database
- 