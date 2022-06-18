# Chapter 3.0 Day 3 Quests

**1. Define your own contract that stores a dictionary of resources. Add a function to get a reference to one of the resources in the dictionary.**

```cadence

pub contract Traveler {

  pub var countryInformation: @{String: Country}
  
  pub resource Country {
    pub let population: Int
    pub let language: String
    pub let currency: String
    
    init(_population: Int, _language: String, _currency: String) {
      self.population = _population
      self.language = _language
      self.currency = _currency
    }
  }
  
  pub fun getCurrency(key: String): &Country {
    return (&self.countryInformation[key] as &Country?)!
  }
  
  init() {
    self.countryInformation <- {
      "United States": <- create Country(_population: 331_501_080, _language: "English", _currency: "US Dollar" ),
      "Serbia": <- create Country(_population: 6_899_126, _language: "Serbian", _currency: "Serbian Dinar" ),
      "Mexico": <- create Country(_population: 128_932_753, _language: "Spanish", _currency: "Mexican Pesos" )
    }
   }

}

```

**2. Create a script that reads information from that resource using the reference from the function you defined in part 1.**

```cadence

import Traveler from 0x01

pub fun main(): String {
  let countryCurrency = Traveler.getCurrency(key: "Serbia")
  return countryCurrency.currency
}

```

**3. Explain, in your own words, why references can be useful in Cadence.** 

References can be useful in Cadence because they allow you to interact with resources without needing to move the resource. 
