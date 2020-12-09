# Working With Strings

## Learning Goals

* Recognize how to declare a `String`
* Define _interpolation_
* Explain how different quote characters allow flexibility
* Join `String`s using `+`

## Introduction

Thus far in programming as conversation, we've used numbers as data most of the
time. Numbers are great because they reach across languages and cultures. But
there are times when we need our programs to return information in the form of
text. In this lesson, we'll learn more about using text (i.e. `String`s) in our
JavaScript expressions.

## Recognize How to Declare a `String`

We declare `String`s most often by enclosing our text in double quotes:

```js
let greeting = "Hello, folks";
```

The letters inside of a `String` are often called "characters."

The pair of matching `"`s are called "`String` delimiters" because they form a
boundary or _limit_ around the characters that make up the `String`.

We can also declare `String`s by putting the characters in single quotes:

```js
let greeting = 'Hello, folks';
```

or backticks:

```js
let greeting = `Hello, folks`;
```

Single quotes and double quotes can be used interchangeably in JavaScript &mdash; they are treated the same. Using backticks to enclose a string, however, brings some additional capabilities. A string enclosed in backticks forms a [template literal](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals), which allows you to _interpolate_ data into the `String`.

## Define _interpolation_

String _interpolation_ is the process of injecting the value of an expression (often, but not necessarily, the _variable lookup expression_) into a `String`. You wrap the expression inside the _interpolation operator_ which lets JavaScript know that it should interpret the value of the expression, convert it to a `String` if necessary, and insert it into the containing `String` where the _interpolation operator_ appeared.

The _interpolation operator_ looks like this: `${}`. When it appears in a backtick-delimited `String`, the return value of the expression inside the operator is "plugged in" to the containing `String`.

In a single or double-quoted `String` there is no interpolation possible. JavaScript would not interpret the value inside the `${}`; instead, it would create a literal string containing the operator and whatever expression is inside it.

```js
const barkCount = 3
const backtick = `Byron barks ${barkCount} times` //=> "Byron barks 3 times"
const singleQuote = 'Byron barks ${barkCount} times' //=> "Byron barks ${barkCount} times"
const doubleQuote = "Byron barks ${barkCount} times" //=> "Byron barks ${barkCount} times"
```

The expression inside the `${}` does not need to be a variable lookup. Any expression, i.e., any statement that returns a value, can be used:

```js
const byron = `Byron is ${2+3} years old` //=> "Byron is 5 years old"
```

Here JavaScript knows to interpret the value inside the interpolation operator because the string is enclosed in backticks. It evaluates the expression (`2 + 3` yields the value `5`), turns the result into a string and inserts it in place.

## Explain How Different Quote Characters Allow Flexibility

What if you needed to store some _dialog_ as a `String`:

In the book it would look like:

> "Wait," said Jo, "Do not go without me!"

If we want to create a string containing this text, we might try wrapping the whole thing in quotes, like this:

> ""Wait," said Jo, "Do not go without me!""

However, because `"` is the `String` delimiter, JavaScript would get confused. It would attempt to end the `String` right before the `W` as the two `"`s "delimit" the `String`.  Not what we wanted.

To fix this, we can use single quotes as our delimiter instead:

```js
const littleWomanEsque = '"Wait," said Jo, "Do not go without me!"'
```

Because the opening delimiter of the `String` was `'`, JavaScript will "close" the
`String` at the next `'` &mdash; at the very end. Inside of the single quotes, the
`"` loses its meaning of "here's a `String`" and, instead, is just a plain
literal,  letter-like character `"`.

But oh my goodness, what if the speaker said `Don't` instead of `Do not`.  That would break our `String` _again_ as JavaScript attempted to use the `'` inside `Don't` as the closing delimiter.

Sometimes we need to tell JavaScript, "Don't use this `'` or `"` as a `String` delimiter. To do this we need _escaping_.

We can "escape" the power of `"` or `'` to close a `String` by putting a `\` in front of it:

```js
const littleWomanEsque = '"Wait," said Jo, "Don\'t go without me!"'
```

Without the backslash, JavaScript would interpret the apostrophe inside `"Don't"` as the end of the string, and we'd end up with a mess. ***BUT*** since there is a `\` immediately before the second `'` (the apostrophe), thus _escaping_ it, JavaScript says "Oh you mean to use this as a character, not as a `String` delimiter. I'll find the next unescaped `'`."

It doesn't find an unescaped `'` until the very end, just like we want.

## Join `String`s using `+`

We already know that we can use `+` as an arithmetical operator to add two `Number`s together. But we can also use it as a `String` operator: when placed between two `String`s, it joins them and returns a ***new*** `String`.

You can use the REPL below to code along with this example and experiment.

<iframe height="400px" width="100%" src="https://repl.it/@LizBurton/JuvenileWorldlyJava?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

```js
const firstName = "Byronius";
const clanName = "Karbitus";
const commonName = "Maris";
let fullName;

// With +
fullName = firstName + " " + clanName + " " + commonName; //=> "Byronius Karbitus Maris"

// Or, with interpolation
fullName = `${firstName} ${clanName} ${commonName}`; //=> "Byronius Karbitus Maris"

// Keep in mind it returns a _new_ String; therefore:
firstName;  //=> "Byronius"
clanName;   //=> "Karbitus"
commonName; //=> "Maris"
fullName;   //=> "Byronius Karbitus Maris"
```

### A Warning About Mixing Data Types

Recall from the lesson on data types that JavaScript, unlike some other programming languages, will bend over backwards to return a value instead of throwing a type error. This means that the following will work in JavaScript:

```js
const fact = "Byron is "; // fact is of type `String`
const tail = " years old"; // tail is of type `String`
const age = 5; // age is of type `Number`

fact + age + tail; //=> "Byron is 5 years old"
```

If we were to try this in Ruby or Python, we would get an error, but JavaScript returns what it *thinks* we meant to do. While in this case this seems pretty reasonable, there are times when JavaScript's behavior will yield unexpected results. For this reason, best practice is **not** to depend on JavaScript to handle mixed data types in this way. A better way to handle this situation is by using interpolation instead:

```js
const fact = "Byron is"; 
const tail = "years old"; 
const age = 5; 

`${fact} ${age} ${tail}`; //=> "Byron is 5 years old"
```

Here, by using backticks and the interpolation operator, we are explicitly telling JavaScript to _interpret_ the expression inside the `${}`, convert it to a string (if necessary), and insert it into our String.

Another alternative is to use JavaScript's `toString()` method:

```js
const fact = "Byron is "; // fact is of type `String`
const tail = " years old"; // tail is of type `String`
const age = 5; // age is of type `Number`

fact + age.toString() + tail; //=> "Byron is 5 years old"
```

## When to Use `+` vs. `${}`

The choice of whether to use `+` or interpolation is, to a certain extent, a matter of personal preference &mdash; you can accomplish what you need to using either method. That said, however, JavaScript programmers tend to use interpolation more often than `+`. As you gain experience working with strings, you may find that using interpolation results in cleaner code that's easier to read. As a general rule, if the string you're constructing is simple and short, using `+` may be cleaner but you may want to consider using interpolation with more complex strings.

## Conclusion

In this lesson, we learned how to declare `String`s, how to interpolate the value of expressions into `String`s, how to use different quote delimiters and escaping to create more complicated `String`s, and a couple different methods for joining `String`s.
