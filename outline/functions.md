---
layout: default
title: Functions
permalink: /outline/functions.html
---

{::options parse_block_html="true" /}

{% comment %}

http://clojurebridge.github.io/curriculum/outline/functions.html

{% endcomment %}

<section ng-controller="NarrativeController">
Functions
-------------------------------
{: .slide-title .chapter}

* What are functions?
* Functions that take other functions
* Predicate functions
* Anonymous functions
* Pure functions
</section>

<section ng-controller="NarrativeController">
### What are functions?
{: .slide_title .slide}

* You already know some: `count`, `conj`, `first`
* Maths operators are functions too: `+`, `-`, `*`, `/`
* A piece of code that takes values and returns a value
* Reference: [Basics of Function](http://clojurebridge.github.io/community-docs/docs/clojure/function-creation/)
</section>

<section ng-controller="NarrativeController">
#### Defining functions <button class="link" ng-model="block21" ng-click="block21=!block21">Details</button>

> * We use `defn` to define a function.
> * We give it a *name* so we may call it later i.e. `add`
> * A Vector is used to specify the function's *arguments* i.e. `[x y]`
> * A String can be provided for a description e.g. `"Adds together..."`
> * The *body* is the form (thing in parentheses) that follows i.e. `(+ x y)` 
> * We call the function by creating a form with it's name and arguments i.e. `(add 1 2)`
{: ng-show="block21" .description}

```clojure
(defn add                        ; name
  "Adds together two numbers"    ; documentation
  [x y]                          ; arguments
  (+ x y))                       ; body

(add 1 2)         ;=> 3 
(add (add 1 2) 4) ;=> 7
```
</section>


<section ng-controller="NarrativeController">
### EXERCISE: Find per-person share of bill among a group
{: .slide_title .slide}

* Create a new function, `add-one`, that takes a single argument
  and adds one to it.

* It should call our `add` function.
</section>

<section ng-controller="NarrativeController">
### Functions that take other functions
{: .slide_title .slide}

#### <button class="link" ng-model="block71" ng-click="block71=!block71">Intro</button>

> Some of the most powerful functions you can use with collections can
> take other functions as arguments.
> This is one of the most magical things about Clojure and many other programming languages.
> It's a complicated idea that may not make sense at first.
> Let's look at an example to learn more about it.
{: ng-show="block71" .description}

> Reference: [Higher-order Function](http://clojurebridge.github.io/community-docs/docs/clojure/higher-order-function/)
{: ng-show="block71" .description}
</section>

<section ng-controller="NarrativeController">
#### `map` function

#### <button class="link" ng-bind-html="details" ng-model="block101" ng-click="block101=!block101"></button>

> `map` is a function that takes another function, along with a
> collection. It calls the function provided to it on each member of
> the collection, then returns a new collection with the results of
> those function calls. This is a weird concept, but it is at the core
> of Clojure and functional programming in general.
{: ng-show="block101" .description}

```clojure
(map count ["a" "abc" "abcdefg"]) ;=> (1 3 7)
(map even? [0 1 2 3 4])           ;=> (true false true false true)
```

> References:
> [count](http://clojuredocs.org/clojure.core/count),
> [even?](http://clojuredocs.org/clojure.core/even_q)
</section>

<section ng-controller="NarrativeController">
#### `reduce` function

#### <button class="link" ng-bind-html="details" ng-model="block111" ng-click="block111=!block111"></button>

> Let's look at another function that takes a function. This one is
> `reduce`, and it is used to turn collections into a single value.
{: ng-show="block111" .description}

> `reduce` takes the first two members of the provided collection and
> calls the provided function with those members. Next, it calls the
> provided function again--this time, using the result of the previous
> function call, along with the next member of the collection.
> `reduce` does this over and over again until it finally reaches the
> end of the collection.
{: ng-show="block111" .description}

```clojure
(reduce + [30 60 90])              ;=> 180
(reduce str ["h" "e" "l" "l" "o"]) ;=> "hello"
```
</section>

<section ng-controller="NarrativeController">
### Bonus section
* Those are the main things you need to know about functions
* You can stop here and move on to the next stage in the curriculum
* But if you're thirsty for more, take a look at the bonus sections that follows
* You don't have to do all of these, go as far as you like
</section>


<section>
#### EXERCISE: Find the average
{: .slide_title .slide}
* Create a function called `average`
* It should take a vector of bill amounts
* It should return the average of those amounts.
* Hint: You will need to use the functions `reduce` and `count`.
</section>

<section ng-controller="NarrativeController">
### Assignment: `let`
{: .slide_title .slide}

#### <button class="link" ng-model="block301" ng-click="block301=!block301">Intro</button>

> When you are creating functions, you may want to assign names to
> values in order to reuse those values or make your code more
> readable. Inside of a function, however, you should _not_ use `def`,
> like you would outside of a function. Instead, you should use a
> special form called `let`.
{: ng-show="block301" .description}

> Reference: [Assignment let](http://clojurebridge.github.io/community-docs/docs/clojure/let/)
{: ng-show="block301" .description}
```clojure
(defn average [values]
  (let [c (count values)
        s (reduce + values)]
    (/ s c)))
(average [1.0 1.0 2.0 3.0 5.0]) ;=> 2.4
```
</section>


<section ng-controller="NarrativeController">
### Predicate functions

* Higher-order functions often just want to work with a yes/ no function
* Functions that return a boolean (true/ false) are often called *predicate functions*
* Predicate functions often end with a question mark
* You've already seen `even?`

```clojure
(remove even? [1 2 3 4 5 6]) ;=> (1 3 5)

(defn less-than-10? [x] (< x 10))
(filter less-than-10? [8 9 10 11]) ;=> (8 9)
```
</section>

<section ng-controller="NarrativeController">
### Anonymous functions

#### Functions without names <button class="link" ng-bind-html="details" ng-model="block201" ng-click="block201=!block201"></button>

> So far, all the functions we've seen have had names, like `+` and
> `str` and `reduce`. However, functions don't need to have names, just
> like values don't need to have names. We call functions without names
> *anonymous functions*.
> An anonymous function is created with `fn`, like so:
{: ng-show="block201" .description}

> Reference: [Anonymous Function](http://clojurebridge.github.io/community-docs/docs/clojure/anonymous-function/)
{: ng-show="block201" .description}


```clojure
(fn [s1 s2] (str s1 " " s2))
```

#### vs. not anonymous functions <button class="link" ng-bind-html="details" ng-model="block202" ng-click="block202=!block202"></button>

> Before we go forward, you should understand that you can _always_
> feel free to name your functions. There is nothing wrong at all with
> doing that. However, you _will_ see Clojure code with anonymous
> functions, so you should be able to understand it.
{: ng-show="block202" .description}

```clojure
(defn join-with-space
  [s1 s2]
  (str s1 " " s2))
```
</section>

<section ng-controller="NarrativeController">
#### Anonymous function example <button class="link" ng-bind-html="details" ng-model="block203" ng-click="block203=!block203"></button>

> Why would you ever need anonymous functions?
> Anonymous functions can be very useful
> when we have functions that take other functions.
> Such as `map` or `reduce`, which we learned in Functions section.
> Let's look at usage examples of anonymous functions:
{: ng-show="block203" .description}

```clojure
(filter (fn [x] (< x 10)) [8 9 10 11]) ;=> (8 9)
```
</section>

<section ng-controller="NarrativeController">
### Pure functions (inputs)

* Where possible you should try to write *pure* functions
* To be pure a function must only depend upon it's inputs
* A pure function always returns the same output for a given input

```clojure
(def one 1)
(defn add-one [x] (+ x one))   ; depends on `one` having been declared
(add-one 5)                    ;=> 6
(def one 2)
(add-one 5)                    ;=> 7    oh dear :(
```
</section>

<section ng-controller="NarrativeController">
#### Pure functions (side-effects)

* It must also cause no observable side-effects
* A side effect is any result 

```clojure
(println "I'm impure")         ; writing to the console is a side-effect
(rand)                         ; reading (from a random number generator) is too
```
</section>

<section ng-controller="NarrativeController">
#### Side-effects

* Side-effects are vital if you want to interact with the real world!
* But they do make you functions less predictable (you can't rely on the real world)...
* ... and harder to reason about (so much to hold in your head)!

</section>


{% comment %}

:star2: A link below is for a slide only. Go to [README.md](../README.md)
instead. :star2:

{% endcomment %}

<section>
Return to the <a href="javascript:;" onClick="Reveal.slide(1);">first slide</a>,
or go to the [curriculum outline](/curriculum/#/1).
</section>
