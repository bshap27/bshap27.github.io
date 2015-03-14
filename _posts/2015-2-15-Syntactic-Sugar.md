---
layout: post
title: Addicted to Syntactic Sugar
---

Similar to the way avocados have ‘good fat’ so they aren’t bad for your health, Syntactic Sugar, in Ruby, is 'good sugar,' in that it makes Ruby delicious to write without compromising the integrity or specificity of your code (code health, if you will).

Yukihiro “Matz” Matsumoto created the Ruby language with beauty, art, and nature in mind, intending to equip the programmer with a linguistically intuitive language with which to build powerful, complex code. By abstracting frequently-occurring complex expressions to simpler commands, and offering built-in syntactic shortcuts, Ruby reads more like English than most other programming languages. “Syntactic sugar” refers to the linguistic flexibility deliberately built into the Ruby language that allows us to read and write functional code that’s easier on the eyes, requires fewer lines of code, and consequently induces fewer headaches. As a result, I imagine syntactic sugar is primarily what makes Ruby the most approachable language for programming newbies, not to mention the one most frequently taught in web development bootcamps.

Allow me to explain.


##Syntactic Sugar Helps Code Read More Naturally

In Ruby, a method is always called on an object using dot notation. In the example below, the string "i am yelling" is my object and "upcase" is my method. Observe.

{% highlight ruby %}
"i am yelling".upcase
=> "I AM YELLING"
{% endhighlight %}

You may be thinking, "But wait, what about methods like 'puts'? I don't use a dot there." And you'd be right. Because when you call the method puts, which prints a string to the screen, what you're really doing is calling the method on an implicit receiver, which is the object you are in - usually the default object, 'main'. Technically, when you write:

{% highlight ruby %}
puts 'Becca is brilliant!'
{% endhighlight %}

what you're really telling the computer to do is

{% highlight ruby %}
self.puts 'Becca is brilliant!'
{% endhighlight %}

If you're confused, you're in good company, and that's ok. I'll talk more about scope another time. Just take my word for it that writing 'self.puts' is the same as just writing 'puts,' and that syntactic sugar allows you to take this shortcut and eliminate the need for the dot.

This isn’t really any different than the way we approach the English language. We use syntactic sugar in everyday speech! Take contractions (won't, isn't, I'll, etc), for example. They make written and verbal speech sound more natural, or colloquial, to us.

For example, let's dissect this conversation which I may or may not have been subject to this weekend:

_Best friend:_ “Why _don’t_ you come to the party with me? _Let’s_ just check it out for an hour. What do you mean you _aren’t_ leaving the house? _You’re_ never _gonna_ find your sexy smart sensitive doctor prince charming on your couch! _It’s_ you I’m looking out for!”

Now remove the contractions.

_Best friend:_ “Why _do not_ you come to the party with me? _Let us_ just check it out for an hour. What do you mean you _are not_ leaving the house? _You are_ never _going to_ find your sexy smart sensitive doctor prince charming on your couch! _It is_ you I’m looking out for!”

Say it out loud. Aside from sounding snottier, it also just doesn’t roll off the tongue. Also, I know “gonna” isn’t a contraction, but you get my point.


##Syntactic Sugar Helps Reduce Unnecessary Effort

Here's an array:
{% highlight ruby %}
things_i_love = ['dark_chocolate', 'knitting', 'skydiving']
{% endhighlight %}

Let's say we wanted to see what the first item in my `things_i_love` array is. We refer to items in arrays by their index, which are numbered starting at 0. So, to see what the first item is in this array, I could generally write:

{% highlight ruby %}
things_i_love[0]
=> "dark_chocolate"
{% endhighlight %}

and that would return me the string "dark_chocolate." But I told you before that all methods call on an object using a dot. Where's the dot?

Well, the notation above is actually an abbreviated version of this:

{% highlight ruby %}
things_i_love.[](0)
=> "dark_chocolate"
{% endhighlight %}

It looks gross without the sugar coat, right? What is this, even? Well, we're calling the method `[]` (which, out loud, would be "bracket") on the object `things_i_love`, and passing the index of 0 to it as an argument. But that's so much more confusing than the first way. And because our friend Matz was concerned with elegance, he's constructed the language such that we can break syntactic rules in the interest of ease and clarity.

Now for an English comparison. I don’t know about you, but I hate typing on an iPhone. Now, this is kind of a bad example because sometimes autocomplete does exactly the opposite of what you want it to do.

<a href="http://www.damnyouautocorrect.com/" target="_blank"><center><img src="/images/autocorrect.jpg" width=40%></center></a>

But it also allows me to type the letter ‘u’ and it will automatically convert it to the word ‘you’ so that I don’t sound like a pre-teen. This eliminates 2 letter-taps of effort and yields the same end result (a text message that most likely contains the dancing cat girls emoji).

Another thing humans do along these lines: we say "YOLO!" instead of always having to say “you only live once,” which of course you have to say all the time.

This is no different than taking advantage of syntactic sugar in Ruby to skirt the rules of conventional syntax.

##Syntactic Sugar Helps Reduce Unnecessary Complexity

Let's say we have an array and we want to 'puts' out each item in the array.

{% highlight ruby %}
things_i_love = ['dark_chocolate', 'knitting', 'skydiving']
{% endhighlight %}

To iterate over this array, I'd need to set up a loop that puts out each item, and in each cycle of the loop, increases the index by 1.

{% highlight ruby %}
def puts_each_item array
  index = 0 				   # starts my index at 0, sets up a counter
  while index < array.length # sets up a loop that ends the program
  							   # once the index matches the number of 
  							   # items in my array
  	puts array[index] 		 # puts out the item for the current index
  	index += 1 			   # increments the index by 1
  end 					    # ends the loop
end 							# ends the program.
{% endhighlight %}

This is so annoying! I have to do that EVERY TIME I want to do something to each item in an array?

Nope, no I don't. In programming, we iterate over an array all the time. Ruby has iterator methods built in to make this easier for us. I could have taken this up a level of abstraction and simply written:

{% highlight ruby %}
def puts_each_item array
  array.each do |item| # calls the 'each' method, a built-in iterator,
  					     # on my array object and specifies the
  					     # variable name, in |bars|, to represent
  					     # each item in the array.
  	puts item 		  # compare this line to puts array[index], above
  end 				  # end loop
end 					  # end program.
{% endhighlight %}

So much cleaner.

Now for an English example. I like to conjure an image of a micro-managing mom:

_Mom:_ “Sweetie, could you help me prepare for dinner by putting 5 plates out? Make sure to fold a napkin and put it on the lefthand side of each plate. Then put a fork on top of the napkin and a knife to the right of the plate, and don’t forget 5 glasses!”

Mom could have just said, “Sweetie, could you set the table?” I know where everything goes. I’m 26. Thanks, Mom.

And so does Ruby. Although computers don’t have the power to make any assumptions on our behalf, in many cases we don’t need to take the computer through every step one by one, thanks to syntactic sugar. We can add a level or two of abstraction and save ourselves the time of dictating lengthy instructions.

......

So, do you see what I’m saying? We can consolidate words and syntax in our code, just like in written and spoken language, to remove clutter and thereby make our code easier to write and understand.

##Syntactic Vinegar

I’d be remiss not to mention the antithesis to syntactic sugar: syntactic vinegar.

Syntactic vinegar is the exact opposite of syntactic sugar in that certain expressions in Ruby are deliberately ugly and/or complicated so as to discourage their use.

It amuses me to liken syntactic vinegar to the use of business jargon. Jargon exists in order for you to express yourself clearly within a certain context, but it tends to be exceptionally annoying outside of that context. For example, in an office setting you might need to say to your boss, “I’m sorry, I just don’t have the bandwidth to do that right now.” It’s probably the most professional way to express that you’re overwhelmed by your workload. However, if you were say that to your friends as an excuse not to go to a party, you’d just sound like an ass.

In Ruby, there’s a method called `instance_variable_get` that allows you to find an instance variable given an instance of a class. To do this in a manner considered acceptable by most Rubyists, you'd make an attribute reader method at the time that the variable is defined, so that you can access the variable outside of the class. The `instance_variable_get` method is a comparatively ‘dirty’ way to access that same information. A wise instructor at Flatiron School wrote:
>I believe that `instance_variable_get` is an unruby-esque method name in that in contains a verb and additionally puts the verb dangling at the end, if anything, it should read `get_instance_variable.` Its weird name should remind us, DON'T DO THIS.

Similarly, in front end development, it is considered bad practice to use tags like `<strong>` and `<em>` in your HTML file; it's more proper to separate styling into a dedicated CSS file. It’s cleaner that way. Although `<strong>` and `<em>` aren’t technically deprecated, <a href="http://www.w3schools.com/tags/tag_strong.asp" target="_blank">w3 schools</a> put it this way:
“Tip: [The `<strong>`] tag is not deprecated, but it is possible to achieve richer effect with CSS.”

In other words, these tags are HTML syntactic vinegar. 

In conclusion, be appreciative of syntactic sugar in Ruby and in English. Here’s a life tip: You don’t need to spell out “et cetera.” None of us really know how to spell it without looking it up. Just say etc. and be grateful that it’s socially acceptable. Love, syntactic sugar.

<!--tags: abstraction, syntactic sugar, syntactic vinegar, ruby, matz-->