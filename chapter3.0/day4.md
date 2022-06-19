# Chapter 3.0 Day 4 Quests

**1. Explain, in your own words, the 2 things resource interfaces can be used for (we went over both in today's content)**

  * Used to set requirements that a resource must have; For example, if a resource interface contains `pub var greeting: String`, the resource that implements the         resource interface will need to have a `greeting` variable or Cadence will throw an error
  * Can be used to expose only specific varibales and functions, meaning resources can be created with 10 functions but by using an interface the developer can choose     to expose only 1 function.


**2. Define your own contract. Make your own resource interface and a resource that implements the interface. Create 2 functions. In the 1st function, show an example of not restricting the type of the resource and accessing its content. In the 2nd function, show an example of restricting the type of the resource and NOT being able to access its content.**

```cadence

pub contract Shopping {

  pub resource interface IList {
    pub var storeName: String
    pub var budget: Int
  }

  pub resource List {
    pub var storeName: String
    pub var budget: Int

    pub fun addNewStore(newStoreName: String): String {
      self.storeName = newStoreName
      return self.storeName
    }

    init() {
       self.storeName = "Target"
       self.budget = 20
    }
  }

  pub fun noInterface() {
    let newStore: @List <- create List()
    newStore.addNewStore(newStoreName: "Macys")
    log(newStore.storeName)

    destroy newStore
  }

  pub fun yesInterface() {
    let newStore: @List{IList} <- create List()
    newStore.addNewStore(newStoreName: "Macys")
    log(newStore.storeName)

    destroy newStore
  }
}

```

**3. How would we fix this code?**

```cadence

pub contract Stuff {

    pub struct interface ITest {
      pub var greeting: String
      pub var favouriteFruit: String
      pub fun changeGreeting(newGreeting: String): String //Add function to struct interface
    }

    // ERROR:
    // `structure Stuff.Test does not conform 
    // to structure interface Stuff.ITest`
    pub struct Test: ITest {
      pub var greeting: String
      pub var favouriteFruit: String // Add favouriteFruit variable to struct

      pub fun changeGreeting(newGreeting: String): String {
        self.greeting = newGreeting
        return self.greeting // returns the new greeting
      }

      init() {
        self.greeting = "Hello!"
        self.favouriteFruit = "Blueberries" // Initialize favouriteFruit
      }
    }

    pub fun fixThis() {
      let test: Test{ITest} = Test()
      let newGreeting = test.changeGreeting(newGreeting: "Bonjour!") // ERROR HERE: `member of restricted type is not accessible: changeGreeting`
      log(newGreeting)
    }
}

```
