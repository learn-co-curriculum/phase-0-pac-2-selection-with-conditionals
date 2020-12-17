# Selection with Conditionals: the 'if' Statement

## Learning Goals

* Learn to use the `if` statement

## Introduction

We've covered the default sequence the JavaScript engine follows when reading
and executing JavaScript code. We've also learned that there are two types of
statements that will enable us to change the default sequence: **selection**
statements and **repetition** statements. In this lesson and the next one, we'll
learn more about **selection** statements, i.e., conditionals.

![Seelection Image](https://curriculum-content.s3.amazonaws.com/programming-univbasics-2/sequence-and-comments/Selection_thick.png)

**Conditional** statements enable us to execute code if a certain condition is
true (or false). Some real-life examples might look like:

* `if` hungry :arrow_right: make a meal.
  * `else` :arrow_right: don't make a meal.
* `if` light is green :arrow_right: press gas pedal.
  * `else` :arrow_right: press brake pedal.
* `if` it's the first of the month :arrow_right: pay the bill.
  * `else` :arrow_right: don't pay the bill.

You might also hear this referred to as **control flow** because it helps
control the flow (i.e., sequence) of an application.

JavaScript includes three structures for implementing code conditionally: _if
statements_, _switch statements_, and _ternary expressions_. In this lesson, we
will learn how to contruct `if` statements.

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

```js
const age = 30;

let isAdult;

if (age >= 18) {
  isAdult = true;
}
//=> true

isAdult;
//=> true
```

If the condition returns a **falsey** value, we do nothing:

```js
const age = 14;

let isAdult;

if (age >= 18) {
  isAdult = true;
}

isAdult;
//=> undefined
```

### `else`

Often we want to run one block of code when the condition returns a `truthy`
value and a _different_ block of code when it returns a `falsey` value. To do
this, we use an `else` clause:

```js
const age = 14;

let isAdult;

if (age >= 18) {
  isAdult = true;
} else {
  isAdult = false;
}
//=> false

isAdult;
//=> false
```

Note that the `else` clause **does not take a condition** &mdash; we want its
code block to run any time the condition for the `if` returns a falsey value.

### The Ternary Expression

Recall that, in this situation, we can also use a ternary expression.
Here's what the code above would look like using a ternary:

```js
const age = 45;
let isAdult;

age >= 18 ? (isAdult = true) : (isAdult = false);
//=> true

isAdult;
//=> true
```

In the above example, we assign `isAdult` as `true` if the condition returns a
truthy value and as `false` otherwise, exactly like the version using `if`.

Remember that a ternary is an _expression_ &mdash; it returns a _value_. What
this means is that we can simplify the code above a bit and assign the result of
the ternary directly to a variable:

```js
const age = 6;
const isAdult = age >= 18 ? true : false;

isAdult;
//=> false
```

The ternary expression is evaluated and resolved to `false`, and that value is
assigned to the variable `isAdult`.

**Advanced:** When the return values are `true` and `false` as in the example
above, you actually don't need to use a ternary &mdash; or an `if...else` &mdash;
at all! This is because ***the conditional is an expression as well***. The
return value of `age >= 18` is a _Boolean value_ (`true` or `false`), so it can
be assigned directly to our `isAdult` variable:

```js
const age = 6;
const isAdult = age >= 18;

isAdult;
//=> false
```

The ternary (or `if...else`) is necessary if the desired return value is something
other than a Boolean:

```js
const age = 20;
const ageMessage = age >= 18 ? "Congratulations! You're an adult!" : "Enjoy your childhood while it lasts!";

ageMessage;
//=> "Congratulations! You're an adult!"
```

**Top Tip:** Be careful to not overuse the ternary expression. It's fine for
slimming down a simple `if...else`, but be conscious of how easy your code is
to understand for an outsider. Remember, you generally write code once, but it
gets read (by yourself and others) **far** more than once. The ternary is often
more difficult to quickly interpret than a regular old `if...else`, so make
sure the reduction in code is worth any potential reduction in readability.

### Nested Conditionals

What if, instead of just deciding whether the passed-in `age` meets the criteria
for `isAdult`, we want to add in some other examples of adulthood (in American
society, at least): `canWork`, `canEnlist`, and `canDrink`. 16-year-olds can
legally work; 18-year-olds can do what 16-year-olds can do **plus** they can
enlist and they are legal adults; 21-year-olds can do what 16- and 18-year-olds
can do **plus** they can drink (at the federally set minimum age). To handle
this situation, we can employ nested conditional statements:

```js
const age = 17;

let isAdult, canWork, canEnlist, canDrink;

if (age >= 16) {
  canWork = true;

  if (age >= 18) {
    isAdult = true;
    canEnlist = true;

    if (age >= 21) {
      canDrink = true;
    }
  }
}

canWork;
//=> true

isAdult;
//=> undefined

canEnlist;
//=> undefined

canDrink;
//=> undefined
```

The first `if` condition checks for the "base level" of adulthood, and each
subsequent nested `if` "adds on." Note that each inner `if` statement is nested
**inside** the code block of the one before. This means that the inner `if`
statements will only execute if the outer ones are truthy. This makes sense: if
age is less than 16, we're done &mdash; there's no need to check the remaining
conditions because we know they have to be false as well. Otherwise JavaScript
will keep checking each subsequent condition until it either comes to one that
is false or finishes running all the code blocks.

### `else if`

Another way to represent multiple possible conditions is with one or more `else
if` clauses. Here the overlap is handled explicitly, by repeating the setting of
the variables under each of the conditions in which they apply:

```js
const age = 20;

let isAdult, canWork, canEnlist, canDrink;

if (age >= 21) {
  isAdult = true;
  canWork = true;
  canEnlist = true;
  canDrink = true;
} else if (age >= 18) {
  isAdult = true;
  canWork = true;
  canEnlist = true;
} else if (age >= 16) {
  canWork = true;
}
//=> true

isAdult;
//=> true

canWork;
//=> true

canEnlist;
//=> true

canDrink;
//=> undefined
```

With this construction, unlike the nested construction, **at most one code block
will be executed**. As soon as one of the conditions returns a truthy value, the
attached code block runs and the conditional statement ends. In the example
above, we have not included an `else` statement so, if none of the conditions is
truthy, no code blocks will be run. If we had included an `else` clause, exactly
one code block would be run.

As a general rule, you should stick to using the `if...else if` construction under
most circumstances. Nested `if`s are a bit more efficient when you have
overlapping categories as in the example above, but they are harder to read.
Most of the time an `if...else if` construction will work just as well.

## Conclusion

In this lesson, we've learned about one of the _selection statements_ that
enable us to modify the _default sequence_: the `if` statement. In the next
lesson, we'll learn about the second: the `switch` statement.

## Resources

* MDN
  * [Conditional statements](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Control_flow_and_error_handling#Conditional_statements)
  * [`if...else` statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else)
