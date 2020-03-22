# A calculation system for the future

## Goals

* **Keep domain behaviour separate from implementation** 
Should need to change if we switch Http servers, or logging or auth frameworks, or databases

* **Should allow for automatic transformation by the "engine" into efficient compute** 
For example - can be calculated one by one per row, or using matrix transformation or batch compute

* **Keep pure functional and stateless as much as possible**

* **Data interactions should be milestoned**

* **Specifications should be precise and typed**
Use enum's and numerical identifiers, not strings, 

* **Concise** Goal is to express business logic in a way that is devoid of runtime concerns and is as precise and clear as possible.

* **Calculation Changes Tracked** Definitions should be milestoned 

* **No duplicate definitions** A pure function should be define once and only once.

* **Language agnostic** Stretch goal - an we express in something like Haskell, but generate into Java and other languages

* **Debugging** Need to be able to understand 


## What if

* No strings allowed for calc specs - all filtering has to be on ID's - we provide an integrated IDE or code gen approach that adds the ability to see the value.
Issues - what about NLP - language stuff. Why - performance, and enables typical data science related optimizations, matrix and GPU. 

* Code vs data - really the same thing, lets not choose, have both. A lot of the config we have is that. 

* Local mode with ability to debug end to end? Or remote debugging to allow full debug ? vs perhaps a trace mode?

* Testing - developers are bad at writing tests, for this we would leverage auto gen property based testing

* Reliability - directly proportional to the number of variations in the inputs - dependencies. Narrow those by setting bounds

* Staged calculations - often we need to do a bunch of calculations and then calculate on the results (tiered calculations)

* Everything available live ? what if it could all tick

* Everything with some capability to diddle or stub ? 

* Pre-cached results - save big pieces

* Avoid fp precision issues - what if we stored the fractions

* If branches in code - that is where the complexity is. Similar to compiler speculation, what changes cause us to take a different branch.

* Use only the primitives in the language and the standard library to implement. Reduce dependency hell

* Only humans - fully authorized end to end - no p2 or batch to batch

* Storing intermediate results - do it

* Ownership - teams own balances - calculation outputs

* Provide full set of math/stats libs

* The problem with rules engines & drived reference data - like SCRP. Teams can own derived ref data

## Selling points

* Need to be able to operate from many code bases



## Prior solutions

* Haxe

## Challenges

* Language differences
  * Testing implementations for each language
  * Lack of functional collections in Java and others
  * Mismatches in primitive types







