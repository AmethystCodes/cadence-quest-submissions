# Chapter 3.0 Day 5 Quests

For today's quest, you will be looking at a contract and a script. You will be looking at 4 variables (a, b, c, d) and 3 functions (publicFunc, contractFunc, privateFunc) defined in SomeContract. In each AREA (1, 2, 3, and 4), I want you to do the following: for each variable (a, b, c, and d), tell me in which areas they can be read (read scope) and which areas they can be modified (write scope). For each function (publicFunc, contractFunc, and privateFunc), simply tell me where they can be called.

| variable/function | Read (Area) | Write (Area) | Called (Area) |
| :--- | :---: | :---: | :---: |
| pub(set) var a | 1, 2, 3, 4 | 1, 2, 3, 4 | |
| pub var b | 1, 2, 3, 4 | 1, 2 | |
| access(contract) var c | 1, 2, 3 | 1, 2 |
| access(self) var d | 1, 2 | 1, 2 |
| pub fun publicFunc |  |  | 1, 2, 3, 4 |
| access(contract) fun contractFunc | | | 1, 2, 3 | 
| access(self) fun privateFunc | | |  1, 2  |
