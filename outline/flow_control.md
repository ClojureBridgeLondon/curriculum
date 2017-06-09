---
layout: default
title: Flow Control
permalink: /outline/flow_control.html
---

{::options parse_block_html="true" /}

{% comment %}

http://clojurebridge.github.io/curriculum/outline/flow_control.html

{% endcomment %}

<section>
Flow Control
-------------------------
{: .slide-title .chapter}

* `if`
* `cond`
* Boolean logic
</section>

<section ng-controller="NarrativeController">
### What is flow control?
{: .slide_title .slide}

#### Decisions how to react <button class="link" ng-bind-html="details" ng-model="block11" ng-click="block11=!block11"></button>

> "Flow control" is the programming term for deciding how to react to
> a given circumstance. We make decisions like this all the time. *If*
> it's a nice day out, *then* we should visit the park; *otherwise* we
> should stay inside and play board games. *If* your car's tank is
> empty, *then* you should visit a gas station; *otherwise* you should
> continue to your destination.
{: ng-show="block11" .description}

#### Testing conditions to react <button class="link" ng-bind-html="details" ng-model="block12" ng-click="block12=!block12"></button>

> Software is also full of these decisions. *If* the user's input is
> valid, *then* we should save their data; *otherwise* we show an error
> message. The common pattern here is that you test some condition and
> react differently based on whether the condition is *true* or *false*.
{: ng-show="block12" .description}
</section>

<section ng-controller="NarrativeController">
### `if`
{: .slide_title .slide}

<button class="link" ng-bind-html="details" ng-model="block21" ng-click="block21=!block21"></button>

> In Clojure, the most basic tool we have for the flow control is the `if`
> operator. It allows you to choose between two options depending upon a condition.
{: ng-show="block21" .description}

> Reference: [Conditional `if`](http://clojurebridge.github.io/community-docs/docs/clojure/if/)
{: ng-show="block21" .description}

```clojure
(if (< age legal-drinking-age)
  ["water" "soda"]
  ["water" "soda" "beer" "wine"])
```

```clojure
(if conditional-expression
  expression-to-evaluate-when-true
  expression-to-evaluate-when-false)
```
</section>

<section ng-controller="NarrativeController">
#### Truthiness <button class="link" ng-bind-html="details" ng-model="block51" ng-click="block51=!block51"></button>

> When testing the truth of an expression, Clojure considers the
> values `nil` and `false` to be false and everything else to be true.
> Here are some examples:
{: ng-show="block51" .description}

> Reference: [Truthiness](http://clojurebridge.github.io/community-docs/docs/clojure/truthiness/)
{: ng-show="block51" .description}


```clojure
(if "anything other than nil or false is considered true"
  "A string is considered true"
  "A string is not considered true")
;=> "A string is considered true"
```

```clojure
(if nil
  "nil is considered true"
  "nil is not considered true")
;=> "nil is not considered true"
```

```clojure
(if (get {:a 1} :b)
  "expressions which evaluate to nil are considered true"
  "expressions which evaluate to nil are not considered true")
;=> "expressions which evaluate to nil are not considered true"
```
</section>

<section>
#### EXERCISE 1:
{: .slide_title .slide}

* write a function `ordinal` that takes a number `n` as an argument
* start from the template on this slide
* if `n` equals `1`, then the function should return `"1st"`, otherwise it should return the number + `"th"`
* you will have to use the [`str`](http://clojurebridge-berlin.github.io/community-docs/docs/clojure/str/) function
* don't worry yet about "2nd" or "3rd"

```clojure
(defn ordinal [n]
  (if ;; condition
      ;; then
      ;; else
  ))
```

```clojure
;; usage of ordinal function
(ordinal 1)    ;=> "1st"
(ordinal 5)    ;=> "5th"
```
</section>

<section>
#### EXERCISE 2:
{: .slide_title .slide}

* extend the `ordinal` function to correctly generate "2nd" and "3rd"
* hint: you can use an `if` inside another `if`

```clojure
;; usage of the new ordinal function
(ordinal 1)    ;=> "1st"
(ordinal 2)    ;=> "2nd"
(ordinal 3)    ;=> "3rd"
(ordinal 4)    ;=> "4th"
```
</section>


<section ng-controller="NarrativeController">
### `cond`
{: .slide_title .slide}

<button class="link" ng-bind-html="details1" ng-model="block61" ng-click="block61=!block61"></button>
<button class="link" ng-bind-html="details2" ng-model="block62" ng-click="block62=!block62"></button>

> The `if` operator takes only one predicate.
> When we want to use multiple predicates, `if` is not a good option.
> We have to write nested, nested, ... and nested `if` conditions.
> To branch to multiple situations, `cond` operator works well.
{: ng-show="block61" .description}

> Reference: [Conditional `cond`](http://clojurebridge.github.io/community-docs/docs/clojure/cond/)
{: ng-show="block62" .description}

```clojure
(if (= n 1)
  "1st"
  (if (= n 2)
    "2nd"
    (if (= n 3)
      "3rd"
      (str n "th"))))
```

In this case `cond` comes in handy.

```clojure
(cond
  (= n 1) "1st"
  (= n 2) "2nd"
  (= n 3) "3rd"
  :else   (str n "th"))
```
</section>

<section ng-controller="NarrativeController">
#### General form of `cond` operator

```clojure
(cond
  predicate1 expression-to-evaluate-when-predicate1-is-true
  predicate2 expression-to-evaluate-when-predicate2-is-true
  ...
  :else      expression-to-evaluate-when-all-above-are-false)
```
</section>

<section ng-controller="NarrativeController">
#### `cond` example

```clojure
(cond
  (< x 10)    "x is smaller than 10"
  (< 10 x 20) "x is between 10 and 20"
  (< 20 x 30) "x is between 20 and 30"
  (< 30 x 40) "x is between 30 and 40"
  :else       "x is bigger than 40")
```

</section>

<section>
#### EXERCISE 3 [BONUS]: Temperature conversion with `cond`
{: .slide_title .slide}

Write a function that can convert degrees Celcius, Fahrenheit, or Kelvin to Celcius

Here is how it should work

``` clojure
(to-celcius 32.0 :F)         ;=> 0.0
(to-celcius 300 :K)          ;=> 26.85
(to-celcius 22.5 :C)         ;=> 22.5
(to-celcius 22.5 :gibberish) ;=> "Unknown scale: :gibberish"
```

Starting point:

``` clojure
(defn to-celcius [degrees scale]
  (cond
    ;; ...
    ))
```

Formulas:

* (°F  -  32)  x  5/9 = °C
* °K + 273.15 = °C
</section>

<section>
#### EXERCISE 3: Solution
{: .slide_title .slide}

Write a function that can convert degrees Celcius, Fahrenheit, or Kelvin to Celcius

``` clojure
(defn to-celcius [degrees scale]
  (cond
    (= scale :C) degrees
    (= scale :F) (* (- degrees 32) 5/9)
    (= scale :K) (- degrees 273.15)
    :else        (str "Unknown scale: " scale)))
```

``` clojure
(to-celcius 32.0 :F)         ;=> 0.0
(to-celcius 300 :K)          ;=> 26.85
(to-celcius 22.5 :C)         ;=> 22.5
(to-celcius 22.5 :gibberish) ;=> "Unknown scale: :gibberish"
```
</section>

<section ng-controller="NarrativeController">
### Boolean logic with `and`, `or`, and `not`
{: .slide_title .slide}

#### <button class="link" ng-model="block81" ng-click="block81=!block81">Intro</button>

> `if` statements are not limited to testing only one thing. You can
> test multiple conditions using boolean logic. _Boolean logic_ refers
> to combining and changing the results of predicates using `and`,
> `or`, and `not`.
{: ng-show="block81" .description}

> If you've never seen this concept in programming before, remember
> that it follows the common sense way you look at things normally. Is
> this _and_ that true? Only if both are true. Is this _or_ that true?
> Yes, if either -- or both! -- are. Is this _not_ true? Yes, if it's
> false.
{: ng-show="block81" .description}
</section>

<section ng-controller="NarrativeController">
### Truthy and falsey table <button class="link" ng-bind-html="details" ng-model="block91" ng-click="block91=!block91"></button>

> `and`, `or`, and `not` work like other functions (they aren't
> exactly functions, but work like them), so they are in _prefix
> notation_, like we've seen with arithmetic.
{: ng-show="block91" .description}

| x     | y     | (`and` x y) | (`or` x y) | (`not` x) | (`not` y) |
| ----- | ----- | --------- | -------- | ------- | ------- |
| false | false | false | false | true  | true  |
| true  | false | false | true  | false | true  |
| true  | true  | true  | true  | false | false |
| false | true  | false | true  | true  | false |

</section>

<section ng-controller="NarrativeController">
#### `and`, `or`, and `not` combination <button class="link" ng-bind-html="details" ng-model="block101" ng-click="block101=!block101"></button>

> `and`, `or`, and `not` can be combined. This can be hard to read.
> Here's an example:
{: ng-show="block101" .description}

```clojure
(defn leap-year?
  "Every four years, except years divisible by 100, but yes for years divisible by 400."
  [year]
  (and (zero? (mod year 4))
       (or (zero? (mod year 400))
           (not (zero? (mod year 100))))))
```
</section>

{% comment %}

:star2: A link below is for a slide only. Go to [README.md](../README.md)
instead. :star2:

{% endcomment %}

<section>
Return to the <a href="javascript:;" onClick="Reveal.slide(1);">first slide</a>,
or go to the [curriculum outline](/curriculum/#/1).
</section>
