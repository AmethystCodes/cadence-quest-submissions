# Chapter 6 (Bonus Chapter) Day 2 Quests

**1. Figure out how to mint an NFT to yourself by sending a transaction using the Flow CLI, like we did today when we set up our collection. You will also likely have to pass an argument as well.**

```cadence
import NonFungibleToken from 0x01
import BalloonBuddies from 0x02

transaction(recipient: Address, name: String, favouriteColor: String, luckyNumber: Int) {
  
    prepare(signer: AuthAccount) {
        let minter = signer.borrow<&BalloonBuddies.Minter>(from: /storage/Minter)
                        ?? panic("This signer is not the one who deployed the contract.")
        
        let recipientsCollection = getAccount(recipient).getCapability(/public/BalloonBuddiesCollection)
                                        .borrow<&BalloonBuddies.Collection{NonFungibleToken.CollectionPublic}>()
                                        ?? panic("Recipient does not have a Collection.")

        let nft <- minter.createNFT(name: name, favouriteColor: favouriteColor, luckyNumber: luckyNumber)
    
        recipientsCollection.deposit(token: <- nft)
    }

    execute {
        log("NFT was minted 🎉")
    }
}
```

**2. Run a script to read the new totalSupply using the Flow CLI**
```cadence
import BalloonBuddies from 0x02
pub fun main(): UInt64 {
  let supply = BalloonBuddies.totalSupply

  return supply
}
```

**3. Run a script to read the ids of NFTs in someone's collection using the Flow CLI**
```cadence
import NonFungibleToken from 0x01
import BalloonBuddies from 0x02

pub fun main(address: Address): [UInt64] {
  let publicCollection = getAccount(address).getCapability(/public/BalloonBuddiesCollection)
                .borrow<&BalloonBuddies.Collection{NonFungibleToken.CollectionPublic}>()
                ?? panic("The address does not have a Collection.")

  return publicCollection.getIDs()
}
```

**4. Run a script to read a specific NFT's metadata from someone's collection using the Flow CLI**
```cadence
import NonFungibleToken from 0x01
import BalloonBuddies from 0x02

pub fun main(address: Address, id: UInt64): &BalloonBuddies.NFT {
    let publicCollection = getAccount(address).getCapability(/public/BalloonBuddiesCollection)
                            .borrow<&BalloonBuddies.Collection{BalloonBuddies.ICollection}>()
                            ?? panic("Collection cannot be accessed.")
    
    return publicCollection.borrowAuthNFT(id: id)
}
```

**5. Run a script to read the GoatedGoats totalSupply on Flow Mainnet. Their contract lives here: https://flow-view-source.com/mainnet/account/0x2068315349bdfce5/contract/GoatedGoats**
```cadence
import GoatedGoats from 0x2068315349bdfce5
pub fun main(): UInt64 {
  let supply = GoatedGoats.totalSupply

  return supply
}
```
**6. Figure out how to read someone's GoatedGoats NFTs from their collection and run a script using the Flow CLI to do it.**

Get GoatedGoats ID's from an address:
```cadence
import GoatedGoats from 0x2068315349bdfce5

pub fun main(address: Address): [UInt64] {
  let goatedGoatsCollection = getAccount(address).getCapability(GoatedGoats.CollectionPublicPath)
                                .borrow<&GoatedGoats.Collection{GoatedGoats.GoatCollectionPublic}>()
                                ?? panic("Address does not have a Goated Goats Collection")
  return goatedGoatsCollection.getIDs()
}
```
