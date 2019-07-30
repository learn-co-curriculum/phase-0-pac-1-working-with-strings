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

Thus far in programming as conversation, we've really used numbers a lot. We
use numbers because they reach across language, culture, and time itself.
Occasionally we've tossed a `String` or a `Symbol` in for variety, but not
often.

As we start writing more advanced programs, we want to say fun things like
`"Byron the poodle barks 10 times"`. These, occasionally silly, programs help
us get the grasp of programming. As a result, we need to learn a bit more about
the `String` type.

It's just like when we learned to talk: We learned to ask questions, make
statements, and communicate usefully, but at some point we were expected to
give our responses in full, proper sentences. So, let's learn how to format
Ruby's responses into meaningful `String`s.

## Recognize How to Declare a `String` with Double-quotes

We declare `String`s most often by putting them in double-quotes:

```ruby
greeting = "Hello, folks"
```

The pair of matching `"` are called "`String`-delimiters because they form a
boundary or _limit_ around a bunch of characters that make up the `String`.

## Recognize How to Declare a `String` with Single-quotes

We can also declare `String`s by putting them in single-quotes:

```ruby
greeting = 'Hello, folks'
```

## State the Difference Between Single- and Double-quoted `String`s

The difference between single- and double-quoted `String`s is best seen when
using a special power of the `String`: _interpolating_ data.
 
### Define _interpolation_

When you use the _interpolation operator_ you take data from the programming
language, convert it to a `String`, and then place it inside the `String`.  A
double-quoted `String` permits `#{}` to be used as a special box to Ruby.
Inside that "box," Ruby "plugs in" the value of the expression _after_
converting it to a `String`. We call `#{}` the "interpolation operator."

A single-quoted string means, "Nope, don't _interpolate_. Treat everything
literally even `#{}`."

```ruby
bark_count = 3
dq = "Byron barks #{bark_count} times" #=> "Byron barks 3 times"
sq = 'Byron barks #{bark_count} times' #=> "Byron barks #{bark_count} times"
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
literal, letter-like `"`.

But oh my goodness, what if the speaker said `Don't` instead of `Do not`.  That
would break our `String` again as Ruby attempted to use `Don't`'s `'` as the closing delimiter.

What a mess.  Sometimes we need to say "Don't use this `'` or `"` as a `String`
delimiter. To do this we need _escaping_.

## Demonstrate Escaping Double-quotes in a `String`

But what if you needed interpolation _but also_ had embedded double-quotes? You
can "escape" the power of `"` to close a `String` by putting a `\` in front of
it:

```ruby
character = "Amy"
little_woman_esque = "\"Wait,\" said #{character}, \"Do not go without me!\""
```

Since the delimiting character is `"`, we could change the word to `Don't` as
well.

## Join `String`s using `+`

Now here's an interesting use of the `+` operator! When placed between
`String`s, it joins them and returns a ***new*** `String`.

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

Be careful, `+` only joins `Strings` with both sides are `String`

```ruby
fact = "Byron is "
tail = " years old"
age = 5

fact + age + tail #=> TypeError (no implicit conversion of Integer into String)
```

Ruby is not sure whether you want to add like an `Integer` (stored in `age`) or
add like `String`s contained in `fact` and `tail`! If you need to do this, you
should use the `to_s` method on data **OR** use the interpolation operator
`#{}` which does the calculation and converts the result to a `String`
automatically.

```ruby
fact = "Byron is "
tail = " years old"
age = 5

fact + age.to_s + tail #=> "Byron is 5 years old"
```

Most types feature a _method_ called `.to_s` ("to `String`") which turns them
into a `String`.  Once a non-`String` is converted to a `String`, it can be
joined with `+` to another `String`.

You might still be unclear on what a "method" is. You might remember the
`.class` method we introduced when we were talking about type, earlier. For
now, think of methods as "commands" you can ask values to do in Ruby.

## Conclusion

With mastery of `String`, we can use the expressions we've learned thus far to
make interesting programs using only expressions. We're going to provide an
example in the next lesson.
