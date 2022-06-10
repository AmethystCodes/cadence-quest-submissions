# Chapter 2.0 Day 3 Quests

1. **In a script, initialize an array (that has length == 3) of your favourite people, represented as Strings, and log it.**

![Cadence Script](/chapter2.0/images/array-script.png)

2. **In a script, initialize a dictionary that maps the Strings Facebook, Instagram, Twitter, YouTube, Reddit, and LinkedIn to a UInt64 that represents the order in which you use them from most to least. For example, YouTube --> 1, Reddit --> 2, etc. If you've never used one before, map it to 0!**
 
![Cadence Dictionary](/chapter2.0/images/dictionary-script.png)

3. **Explain what the force unwrap operator ! does, with an example different from the one I showed you (you can just change the type).**

    The force unwrap operator `!` returns the value that is inside an optional. If the optional contains a value, it is returned; however, if the optional has no value or `nil` then the unwrap operator panics and aborts the execution. In the first image below, the optional is removed when the result is returned. In the second image, an error is thrown because the value of `luckyNum` is `nil`.

<p align="center">
  <img src="/chapter2.0/images/unwrap-optional.png">
</p>

<p align="center">
  <img src="/chapter2.0/images/unwrap-nil.png">
</p>

4. **Using this picture provided, explain...**

<p align="center">
  <img src="https://github.com/emerald-dao/beginner-cadence-course/blob/main/chapter2.0/images/wrongcode.png">
</p>

   * **What the error message means**
       * The error message means that the value returned was an optional but the return type used was `String` 
   * **Why we're getting this error**
       * We're getting this error because the return value does not match the return type 
   * **How to fix it**
       * Fix this error by changing the return type to `String?` from `String` 
