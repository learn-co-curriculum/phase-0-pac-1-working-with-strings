# Working With Strings

## Learning Goals

* Recognize how to declare a `String` with double quotes
* Recognize how to declare a `String` with single quotes
* State the difference between single- and double-quoted `String`s
* Define _interpolation_
* Explain how different quote characters allow flexibility
* Demonstrate escaping double quotes in a `String`
* Join `String`s using `+`
* Identify why `TypeError` happens when + `String` with `Integer`

## Introduction

Thus far in programming as conversation, we've used numbers as data most of the
time. Numbers are great because they reach across languages and cultures. But
there are times when we need our programs to return information in the form of
text. In this lesson we'll learn more about using text (i.e. `String`s) in our
Ruby expressions.

## Recognize How to Declare a `String` with Double Quotes

We declare `String`s most often by putting letters in double quotes:

![String Declaration](https://curriculum-content.s3.amazonaws.com/programming-univbasics/working-with-string/Image_91_SyntaxDeclaration.png)

Or, in Ruby:

```ruby
greeting = "Hello, folks"
```

The letters inside of a `String` are often called "characters."

The pair of matching `"`s are called "`String` delimiters" because they form a
boundary or _limit_ around the characters that make up the `String`.

## Recognize How to Declare a `String` with Single Quotes

We can also declare `String`s by putting the characters in single quotes:

![Single Quote String](https://curriculum-content.s3.amazonaws.com/programming-univbasics/working-with-string/Image_91B_SyntaxDeclaration.png)

Or, in Ruby:

```ruby
greeting = 'Hello, folks'
```

## State the Difference Between Single- and Double-quoted `String`s

For the most part, single and double quotes can be used interchangeably in Ruby. However, there is one instance where you need to use double quotes: when you are _interpolating_ data into a `String`.

### Define _interpolation_

When you use the _interpolation operator_ you take data from the programming
language, convert it to a `String` and then place that `String` _inside_ of
the `String` where the _interpolation operator_ appeared.

The _interpolation operator_ looks like this: `#{}`. When it appears in a
double-quote-delimited `String`, the return value of the expression inside the
operator is "plugged in" to the containing `String`.

In a single-quoted `String` there is no interpolation possible. Ruby simply
sees `#{}` as "hash-mark, left-curly brace, right-curly brace."

```ruby
bark_count = 3
double_q = "Byron barks #{bark_count} times" #=> "Byron barks 3 times"
single_q = 'Byron barks #{bark_count} times' #=> "Byron barks #{bark_count} times"
```

Here's a slightly more complex example to help you remember:

![Interpolation with arithmetic](https://curriculum-content.s3.amazonaws.com/programming-univbasics/working-with-string/Image_91C_SyntaxDeclaration.png)

## Explain How Different Quote Characters Allow Flexibility

What if you needed to store some dialog as a `String`:

In the book...

> "Wait," said Jo, "Do not go without me!"

As a `String` for Ruby...

> ""Wait," said Jo, "Do not go without me!""

Since `"` is the `String` delimiter, Ruby would get confused if we gave it this
`String`. It would attempt to end the `String` right before the `W` as the two
`"`s "delimit" the `String`.  Not what we wanted.

It might be a wise choice to use single quotes here.

```ruby
little_woman_esque = '"Wait," said Jo, "Do not go without me!"'
```

Because the opening delimiter of the `String` was `'`, Ruby will "close" the
`String` at the next `'` &mdash; at the very end. Inside of the single quotes, the
`"` loses its meaning of "here's a `String`" and, instead, is just a plain
literal,  letter-like character `"`.

But oh my goodness, what if the speaker said `Don't` instead of `Do not`.  That
would break our `String` _again_ as Ruby attempted to use the `'` inside `Don't` as the
closing delimiter.

What a mess. Sometimes we need to say "Don't use this `'` or `"` as a `String`
delimiter. To do this we need _escaping_.

## Demonstrate Escaping Double Quotes in a `String`

So, what are we to do when we need interpolation _but also_ have embedded
double quotes? We can "escape" the power of `"` to close a `String` by putting
a `\` in front of it:

```ruby
character = "Amy"
little_woman_esque = "\"Wait,\" said #{character}, \"Do not go without me!\""
```

Since the delimiting character is `"`, we _should_ close the `String`
immediately before the `W`. ***BUT*** since there is a `\` immediately before
the second `"`, thus _escaping_ it, Ruby says "Oh you mean to try this as a character,
not as a `String` delimiter. I'll find the next unescaped `"`."

It doesn't find an unescaped `"` until the very end, just like we want.

By the way, we could also change the word to `"Do not"` to `"Don't"` as well
since `'` is not being used as a delimiter.

## Join `String`s using `+`

Now here's an interesting use of the `+` operator! When placed between
`String`s, it joins them and returns a ***new*** `String`.

Try this out in IRB (or make up your own variation):

```ruby
first_name = "Byronius"
clan_name = "Karbitus"
common_name = "Maris"

# With +
full_name = first_name + " " + clan_name + " " + common_name #=> "Byronius Karbitus Maris"

# Or, with interpolation
full_name = "#{first_name} #{clan_name} #{common_name}" #=> "Byronius Karbitus Maris"

# Keep in mind it returns a _new_ String; therefore:
first_name  #=> "Byronius"
clan_name   #=> "Karbitus"
common_name #=> "Maris"
full_name   #=> "Byronius Karbitus Maris"
```

## Identify Why TypeError Happens When `+` String with Integer

Be careful, ***`+` only joins `Strings`! To work, both sides must be of type `String`***:

```ruby
fact = "Byron is "
tail = " years old"
age = 5

fact + age + tail #=> TypeError (no implicit conversion of Integer into String)
```

Ruby is not sure whether you want to add like an `Integer` (stored in `age`) or
add like `String`s contained in `fact` and `tail`! If you need to do this, you
should use the `to_s` method on data (like `5`) **OR** use the interpolation
operator `#{}` which, as we said earlier, does the calculation and converts the
result to a `String` automatically.

```ruby
fact = "Byron is "
tail = " years old"
age = 5

fact + age.to_s + tail  #=> "Byron is 5 years old"
"#{fact} #{age} #{tail}" #=> "Byron is 5 years old"
```

Most data types feature a _method_ called `.to_s` ("to `String`") which turns
them into a `String`. Once a non-`String` is converted to a `String`, it can
be joined with `+` to another `String`.

You might still be unclear on what a "method" is. You might remember the
`.class` method we introduced when we were talking about type in an earlier lesson. For
now, think of methods as "commands" you can ask values to do in Ruby.

## Conclusion

With mastery of `String`, we can use the expressions we've learned thus far to
make interesting programs using only expressions. We're going to provide an
example in the next lesson.
