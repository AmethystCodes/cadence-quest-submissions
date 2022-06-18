# Chapter 3.0 Day 2 Quest

**1. Write your own smart contract that contains two state variables: an array of resources, and a dictionary of resources. Add functions to remove and add to each of them. They must be different from the examples above.**

```cadence

pub contract Day2 {

    pub var arrayOfNames: @[Name]
    pub var dictionaryOfNames: @{String: Name}

    pub resource Name {
        pub let username: String
        init() {
            self.username = "Amethyst"
        }
    }

    pub fun addArrayNames(arrayName: @Name) {
        self.arrayOfNames.append(<- arrayName)
    }

    pub fun removeArrayNames(index: Int): @Name {
        return <- self.arrayOfNames.remove(at: index)
    }

    pub fun addDictionaryName(dictionaryName: @Name) {
        let key = dictionaryName.username

        let oldDictionaryName <- self.dictionaryOfNames[key] <- dictionaryName
        destroy oldDictionaryName
    }

    pub fun removeDictionaryName(key: String): @Name {
        let dictionaryName <- self.dictionaryOfNames.remove(key: key) ?? panic("Could not find username!")
        return <- dictionaryName
    }

    init() {
        self.arrayOfNames <- []
        self.dictionaryOfNames <- {}
    }

}

```
