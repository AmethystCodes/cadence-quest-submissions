# Chapter 4.0 Day 2 Quests

**1. What does .link() do?**
`.link()` creates a capability that can be accessed  

**2. In your own words (no code), explain how we can use resource interfaces to only expose certain things to the /public/ path.**

Using resource interfaces, the developer can determine what is publically accessible. If there are certain functions or variables that should not be accessed, the developer can use a resource interface and only include the fields they want accessed. 

**3. Deploy a contract that contains a resource that implements a resource interface.**

```cadence
pub contract Country {

    pub resource interface IState {
        pub var name: String
        pub var capital: String
        pub var population: Int
    }

    pub resource State: IState {
        pub var name: String
        pub var capital: String
        pub var stateBird: String
        pub var population: Int

        pub fun updatePopulation(newPopulation: Int): Int {
            self.population = newPopulation
            return self.population
        }

        init() {
            self.name = "New York"
            self.capital = "Albany"
            self.stateBird = "Eastern Bluebird"
            self.population = 19_510_000 
        }
    }

    pub fun createState(): @State {
        return <- create State()
    }

    init() {
    
    }

}
```


**Then, do the following:**

  * In a transaction, save the resource to storage and link it to the public with the restrictive interface.
 
```cadence
import Country from 0x01

transaction() {

  prepare(signer: AuthAccount) {
    signer.save(<- Country.createState(), to: /storage/MyStateResource)

    signer.link<&Country.State{Country.IState}>(/public/MyStateResource, target: /storage/MyStateResource)
  }

  execute {
  
  }

}
```

  * Run a script that tries to access a non-exposed field in the resource interface, and see the error pop up.

  * Run the script and access something you CAN read from. Return it from the script.
