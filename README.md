# Selection with Conditionals: the if Statement

## Learning Goals

* Learn to use the `if` statement

## Introduction

We've covered the default sequence the JavaScript engine follows when reading
and executing JavaScript code. We've also learned that there are two types of
statements that will enable us to change the default sequence: **selection**
statements and **repetition** statements. In this lesson and the next one, we'll
learn more about **selection** statements, i.e., conditionals.

![Selection Image](https://curriculum-content.s3.amazonaws.com/phase-0/pac-2-intro/Selection_thick.png)

**Conditional** statements enable us to execute code if a certain condition is
true (or false). Some real-life examples might look like:

* `if` hungry → make a meal.
  * `else` → don't make a meal.
* `if` light is green → press gas pedal.
  * `else` → press brake pedal.
* `if` it's the first of the month → pay the bill.
  * `else` → don't pay the bill.

You might also hear this referred to as **control flow** because it helps
control the flow (i.e., sequence) of an application.

JavaScript includes three structures for implementing code conditionally: _if
statements_, _switch statements_, and _ternary expressions_. In this lesson, we
will learn how to construct `if` statements.

### Note about the Embedded REPL's in this Lesson

You'll notice that the embedded REPL's in this lesson look a little different
from the ones you've seen in previous lessons. They include both a code window
on the top, and the console window on the bottom. Code is pre-written in the
code window so you just need to click the "Run" button to see what it does.

Note, however, that if you want to experiment with any of the code (which we
strongly recommend), you'll need to open [replit][] in the browser and
copy/paste the code there.

## Learn to Use the `if` Statement

To write a basic `if` statement, we use the following structure:

```js
if (condition) {
  // Block of code
}
```

It consists of the `if` keyword followed by the condition to be checked in
parentheses.  After that comes a _block statement_ (more commonly called a _code
block_): one or more JavaScript expressions or statements enclosed in `{}`. The
_code block_ contains the code we want to execute _if_ the condition returns a
truthy value:

<iframe height="400px" width="100%" src="https://replit.com/@lizbur10/FixedUnacceptableCable?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

In the code above, age is initialized to 30, so the condition (`age >= 18`)
resolves to `true`. The code in the code block executes, setting the `isAdult`
variable to `true`. Copy/paste the code above into [replit][] and try making
some changes (e.g., assigning different values to `age`; changing the
conditional statement) to see what happens.

### `else`

Often we want to run one block of code when the condition returns a `truthy`
value and a _different_ block of code when it returns a `falsey` value. To do
this, we use an `else` clause:

<iframe height="400px" width="100%" src="https://replit.com/@lizbur10/CourteousEquatorialTree?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

Note that the `else` clause **does not take a condition** — if the condition for
the `if` returns a falsey value, we want the `else` code block to run **no
matter what**. This means that exactly one of the code blocks will _always_ run.

### The Ternary Expression

Recall that this is the exact situation where we can use a ternary expression.
Here's what the code above would look like using a ternary:

<iframe height="400px" width="100%" src="https://replit.com/@lizbur10/EnchantedAchingProcedurallanguage?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

Here, we assign `isAdult` as `true` if the condition returns a truthy value and
as `false` otherwise, exactly like the version using `if`.

Remember that a ternary is an _expression_ — it returns a _value_. What
this means is that we can simplify the code above a bit and assign the _result_ of
the ternary directly to a variable:

```js
const age = 26;
const isAdult = age >= 18 ? true : false;

isAdult;
//=> true
```

The ternary expression is evaluated and resolved to `true`, and that value is
assigned to the variable `isAdult`. Try this version out in [replit][] to verify
that it works.

**Advanced:** What is the ternary above doing? Basically, it's saying: "when the
conditional code returns `true`, return `true`, and when the conditional code
returns `false`, return `false`." Sounds a bit redundant, doesn't it? When the
return values are `true` and `false` as in the example above, you actually don't
need to use a ternary — or an `if...else` — at all! This is because
***the conditional is an expression as well***. The return value of `age >= 18`
is a _Boolean value_ (`true` or `false`), so it can be assigned directly to our
`isAdult` variable:

```js
const age = 6;
const isAdult = age >= 18;

isAdult;
//=> false
```

The ternary (or `if...else`) is only necessary if the desired return value is
something other than a Boolean:

```js
const age = 20;
const ageMessage = age >= 18 ? "Congratulations! You're an adult!" : "Enjoy your childhood while it lasts!";

ageMessage;
//=> "Congratulations! You're an adult!"
```

> **Top Tip:** Be careful not to overuse the ternary expression. It's fine for
> slimming down a simple `if...else`, but be conscious of how easy your code is
> to understand for an outsider. Remember, you generally write code once, but it
> gets read (by yourself and others) **far** more than once. The ternary is
> often more difficult to quickly interpret than a regular old `if...else`, so
> make sure the reduction in code is worth any potential reduction in
> readability.

### `else if`

We've discussed the case where our condition is _binary_ (one code block
executes if the conditional returns true and a second executes otherwise), but
sometimes we need to check multiple conditions. We can handle this situation by
using one or more `else if` clauses.

Let's say that instead of just deciding whether the passed-in `age` meets the
criterion for `isAdult`, we want to add in some other examples of adulthood (in
American society, at least): `canWork`, `canEnlist`, and `canDrink`.
16-year-olds can legally work; 18-year-olds can do what 16-year-olds can do
**plus** they can enlist and they are legal adults; 21-year-olds can do what 16-
and 18-year-olds can do **plus** they can drink (at the federally set minimum
age).

Here's how we can handle that using `else if` clauses:

<iframe height="400px" width="100%" src="https://replit.com/@lizbur10/SuburbanScentedAccounting?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

Any time you use an `if...else if` construction, **at most one code block will
be executed**. As soon as one of the conditions returns a truthy value, the
attached code block runs and the conditional statement ends. In the example
above, we have not included an `else` statement so, if none of the conditions is
truthy, no code blocks will be run. If we had included an `else` clause, exactly
one code block would be run.

Try different values for `age` in [replit][] and check the resulting values of
the four variables.

### Nested `if` Statements

You may have noticed that there is some redundancy in the example above: three
of the four variables appear in more than one of the conditions. In this
circumstance, we can streamline our code a bit by using nested conditional
statements:

<iframe height="400px" width="100%" src="https://replit.com/@lizbur10/MutedUntrueAdware?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

The first `if` condition checks for the "base level" of adulthood (`age >= 16`),
and each subsequent nested `if` "adds on." Note that each inner `if` statement
is nested **inside** the code block of the one before. This means that the inner
`if` statements will only execute if the outer ones are truthy. This makes
sense: if age is less than 16, we're done — there's no need to check the
remaining conditions because we know they have to be false as well. Otherwise
JavaScript will keep checking each subsequent condition until it either comes to
one that is false or finishes running all the code blocks.

While nested `if`s are more efficient than `if...else if`s for handling
overlapping categories, they are also more difficult to read. An `if...else if`
construction will always work. You should consider the tradeoff of readability
vs. efficiency in deciding which construction to use.

## Conclusion

In this lesson, we've learned about one of the _selection statements_ that
enable us to modify the _default sequence_: the `if` statement. In the simplest
case, the `if` statement consists of the `if` clause, a condition, and a code
block to run if the condition returns `true`. In more complex situations, we can
add one or more `else if` clauses or an `else` clause.

In the next lesson, we'll learn about another selection statement we can use to
create conditional code: the `switch` statement.

## Resources

* MDN
  * [Conditional statements](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Control_flow_and_error_handling#Conditional_statements)
  * [`if...else` statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else)

[replit]: https://replit.com/languages/javascript
