# Chapter 3.0 Day 1 Quests

**1. In words, list 3 reasons why structs are different from resources.**
  * Can be copied
  * Can be lost or overwritten
  * Can be created whenever you want

**2. Describe a situation where a resource might be better to use than a struct.**

When creating an NFT using a resource is better than using a struct because it's really difficult to lose a resource, they're extremely secure and impossible to copy. 

**3. What is the keyword to make a new resource?**

```javascript
create
```

**4. Can a resource be created in a script or transaction (assuming there isn't a public function to create one)?**

No, a resource cannot be created in a script or transaction. A resource can *ONLY* be created inside of a contract.

**5. What is the type of the resource below?**

```javascript
pub resource Jacob {

}
```

The type of the resource is `Jacob`

**6. Let's play the "I Spy" game from when we were kids. I Spy 4 things wrong with this code. Please fix them.**

```javascript
pub contract Test {

    // Hint: There's nothing wrong here ;)
    pub resource Jacob {
        pub let rocks: Bool
        init() {
            self.rocks = true
        }
    }

    pub fun createJacob(): @Jacob { // there is 1 here - Added @
        let myJacob <- create Jacob() // there are 2 here - Changed = to <-; added create keyword
        return <- myJacob // there is 1 here - Added <- 
    }
}
```
