# Chapter 4.0 Day 3

**1. Why did we add a Collection to this contract? List the two main reasons.** 

We added a Collection to the contract so that we are able to store multiple resources in the same path and to allow others to deposit into the Collection.

**2. What do you have to do if you have resources "nested" inside of another resource? ("Nested resources")**

If you have resources "nested" inside of another resource, you need to declare a `destory` function that manually destroys the nested resources. 

**3. Brainstorm some extra things we may want to add to this contract. Think about what might be problematic with this contract and how we could fix it.**

  * **Idea #1: Do we really want everyone to be able to mint an NFT? 🤔.**

    No, you can create an admin minter resource. This makes it so that only the owner of the resource can use the minting function

  * **Idea #2: If we want to read information about our NFTs inside our Collection, right now we have to take it out of the Collection to do so. Is this good?**
  
    No, this is not good. Instead, creating a resource interface for the Collection and then linking the collection to a `/public/` path is a better option. 

  * **NFT Metadata**
