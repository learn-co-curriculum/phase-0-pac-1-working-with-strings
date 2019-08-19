# Working With String

## Learning Goals

* Recognize how to declare a `String` with double-quotes
* Recognize how to declare a `String` with single-quotes
* State the difference between single- and double-quoted `String`s
* Define _interpolation_
* Explain how different quote characters allow flexibility
* Demonstrate escaping double-quotes in a `String`
* Join `String`s using `+`
* Identify why `TypeError` happens when + `String` with `Integer`

## Introduction

Thus far in programming as conversation, we've used numbers as data most of the
time. We used numbers because they reach across language, culture, and time
itself.  Occasionally we've tossed a `String` or a `Symbol` in for variety, but
not often. But it's really helpful to have our expression return funny
`String`s or things like that.

Let's learn how to format Ruby's _evaluations_ into `String`s that help ensure
our understanding of programming in Ruby.

## Recognize How to Declare a `String` with Double-quotes

We declare `String`s most often by putting letters in double-quotes:

```ruby
greeting = "Hello, folks"
```

The letters inside of a `String` are often called "characters."

The pair of matching `"` are called "`String`-delimiters because they form a
boundary or _limit_ around the that make up the `String`.

## Recognize How to Declare a `String` with Single-quotes

We can also declare `String`s by putting _characters_ in single-quotes:

```ruby
greeting = 'Hello, folks'
```

## State the Difference Between Single- and Double-quoted `String`s

The difference between single- and double-quoted `String`s is best seen when
using a special power of the `String`: _interpolating_ data.
 
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

## Explain How Different Quote Characters Allow Flexibility

What if you needed to store some dialog as a `String`:

In the book...

> "Wait," said Jo, "Do not go without me!"

As a `String` for Ruby...

> ""Wait," said Jo, "Do not go without me!""

Since `"` is the `String` delimiter, Ruby would get confused if we gave it this
`String`. It would attempt to end the `String` right before the `W` as the two
`"`s "delimit" the `String`.  Not what we wanted.

It might be a wise choice to use a single-quote here.

```ruby
little_woman_esque = '"Wait," said Jo, "Do not go without me!"'
```

Because the opening delimiter of the `String` was `'`, Ruby will "close" the
`String` at the next `'` &mdash; at the very end. Inside of the `'...'`, the
`"` loses its meaning of "here's a `String`" and, instead, is just a plain
literal,  letter-like character `"`.

But oh my goodness, what if the speaker said `Don't` instead of `Do not`.  That
would break our `String` _again_ as Ruby attempted to use `Don't`'s `'` as the
closing delimiter.

What a mess.  Sometimes we need to say "Don't use this `'` or `"` as a `String`
delimiter. To do this we need _escaping_.

## Demonstrate Escaping Double-quotes in a `String`

So, what are we to do when we need interpolation _but also_ have embedded
double-quotes? We can "escape" the power of `"` to close a `String` by putting
a `\` in front of it:

```ruby
character = "Amy"
little_woman_esque = "\"Wait,\" said #{character}, \"Do not go without me!\""
```

Since the delimiting character is `"`, we _should_ close the `String`
immediately before the `W`. ***BUT*** since there is a `\` immediately before
the `"`, thus _escaping_ it, Ruby says "Oh you mean to try this as a character,
not as a `String` delimiter, I'll find the next unescaped `"`."

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

Be careful, ***`+` only joins `Strings` with both sides are `String`***:

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
"#{fact} #{age} #{tail} #=> "Byron is 5 years old"
```

Most data types feature a _method_ called `.to_s` ("to `String`") which turns
them into a `String`.  Once a non-`String` is converted to a `String`, it can
be joined with `+` to another `String`.

You might still be unclear on what a "method" is. You might remember the
`.class` method we introduced when we were talking about type, earlier. For
now, think of methods as "commands" you can ask values to do in Ruby.

## Conclusion

With mastery of `String`, we can use the expressions we've learned thus far to
make interesting programs using only expressions. We're going to provide an
example in the next lesson.
