## Chapter 4.0 Day 1 Quests

**1. Explain what lives inside of an account.**

Contract code and account storage live inside an account. Contract code is a contract that gets deployed to an account and account storage holds all of your data.

**2. What is the difference between the /storage/, /public/, and /private/ paths?**

The difference between the three paths is who can access it. Only the account owner can access the `/storage/` path. The `/public/` path is avaliable to everyone and the `/private/` is only avaliable to the account owner and anyone who the account owner gives access to.

**3. What does .save() do? What does .load() do? What does .borrow() do?**
  * `.save()` - stores data in account storage
  * `.load()` - takes data out of the account storage
  * `.borrow()` - creates references to objects in account storage

**4. Explain why we couldn't save something to our account storage inside of a script.**

Account storage should only be accessed through a transaction specifically in the prepare phrase.

**5. Explain why I couldn't save something to your account.**

It's not possible to save something to account storage without having the account owner sign a transcation authorizing access to their account storage

**6. Define a contract that returns a resource that has at least 1 field in it. Then, write 2 transactions:**

```cadence
pub contract Country {

    pub resource State {
        pub let name: String
        pub let capital: String

        init() {
            self.name = "New York"
            self.capital = "Albany"
        }
    }

    pub fun createState(): @State {
        return <- create State()
    }

}
```

  * A transaction that first saves the resource to account storage, then loads it out of account storage, logs a field inside the resource, and destroys it.
  
```cadence
import Country from 0x01

transaction() {

  prepare(signer: AuthAccount) {
    let newState <- Country.createState()
    signer.save(<- newState, to: /storage/MyStates)
    
    let loadState <- signer.load<@Country.State>(from: /storage/MyStates)
                     ?? panic("No State Resource Found.")
    
    log(loadState.name)
    destroy loadState
  }

  execute {
  
  }

}
```

  * A transaction that first saves the resource to account storage, then borrows a reference to it, and logs a field inside the resource.
```cadence
import Country from 0x01

transaction() {

   prepare(signer: AuthAccount) {
      let newState <- Country.createState()
      signer.save(<- newState, to: /storage/MyStates)
        
      let borrowState = signer.borrow<&Country.State>(from: /storage/MyStates)
          ?? panic("No State Resource Found.")

      log(borrowState.capital)
  }

}
```
