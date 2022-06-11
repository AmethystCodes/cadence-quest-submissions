# Chapter 2.0 Day 4 Quests

**1. Deploy a new contract that has a Struct of your choosing inside of it (must be different than Profile).**

```javascript
pub contract Information {

    pub struct History {
      pub let diabetes: Bool
      pub let highHDL: Bool
      pub let highBloodPressure: Bool
      pub let account: Address

      init(_diabetes: Bool, _highHDL: Bool, _highBloodPressure: Bool, _account: Address) {
        self.diabetes = _diabetes
        self.highHDL = _highHDL
        self.highBloodPressure = _highBloodPressure
        self.account = _account
      }
    }
    
    init() {}
}
```

**2. Create a dictionary or array that contains the Struct you defined.**

```javascript
pub contract Information {

    pub var patientHistory: {Address: History}
  
    pub struct History {
      pub let diabetes: Bool
      pub let highHDL: Bool
      pub let highBloodPressure: Bool
      pub let account: Address

      init(_diabetes: Bool, _highHDL: Bool, _highBloodPressure: Bool, _account: Address) {
        self.diabetes = _diabetes
        self.highHDL = _highHDL
        self.highBloodPressure = _highBloodPressure
        self.account = _account
      }
    }
    
    init() {
      self.patientHistory = {}
    }
}
```


**3. Create a function to add to that array/dictionary.**

```javascript
pub contract Information {

    pub var patientHistory: {Address: History}
  
    pub struct History {
      pub let diabetes: Bool
      pub let highHDL: Bool
      pub let highBloodPressure: Bool
      pub let account: Address

      init(_diabetes: Bool, _highHDL: Bool, _highBloodPressure: Bool, _account: Address) {
        self.diabetes = _diabetes
        self.highHDL = _highHDL
        self.highBloodPressure = _highBloodPressure
        self.account = _account
      }
    }
    
    pub fun addHistory(diabetes: Bool, highHDL: Bool, highBloodPressure: Bool, account: Address) {
      let newHistory = History(_diabetes: diabetes, _highHDL: highHDL, _highBloodPressure: highBloodPressure, _account: account)
      self.patientHistory[account] = newHistory
    }
    
    init() {
      self.patientHistory = {}
    }
}
```

**4. Add a transaction to call that function in step 3.**

```javascript
import Information from 0x01

transaction(diabetes: Bool, highHDL: Bool, highBloodPressure: Bool, account: Address) {

  prepare(signer: AuthAccount) {}

  execute {
    Information.addHistory(
    diabetes: diabetes, 
    highHDL: highHDL, 
    highBloodPressure: highBloodPressure, 
    account: account)
    log("Patient History Added!")
  }

}
```

**5. Add a script to read the Struct you defined.**

```javascript
import Information from 0x01

pub fun main(account: Address): Information.History? {
  return Information.patientHistory[account]
}

// or use panic 

import Information from 0x01

pub fun main(account: Address): Information.History {
  return Information.patientHistory[account] ?? panic("Account Not Found")
}
```
