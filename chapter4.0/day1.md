## Chapter 4.0 Day 1 Quests

**1. Explain what lives inside of an account.**

Contract code and account storage live inside an account. Contract code is a contract that gets deployed to an account and account storage holds all of your data.

**2. What is the difference between the /storage/, /public/, and /private/ paths?**

The difference between the three paths is who can access it. Only the account owner can access the `/storage/` path. The `/public/` path is avaliable to everyone and the `/private/` is only avaliable to the account owner and anyone who the account owner gives access to.

**3. What does .save() do? What does .load() do? What does .borrow() do?**
  * `.save()` - stores data in account storage
  * `.load()` - takes data out of the account storage
  * `.borrow()` - 

**4. Explain why we couldn't save something to our account storage inside of a script.**

**5. Explain why I couldn't save something to your account.**

**6. Define a contract that returns a resource that has at least 1 field in it. Then, write 2 transactions:**

  * A transaction that first saves the resource to account storage, then loads it out of account storage, logs a field inside the resource, and destroys it.

  * A transaction that first saves the resource to account storage, then borrows a reference to it, and logs a field inside the resource.
