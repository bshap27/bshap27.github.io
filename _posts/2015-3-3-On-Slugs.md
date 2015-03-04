---
layout: post
title: On Slugs
---

Q: What is a slug?

<p>A: This is a slug:</p>
<p class="img_caption"><img src="http://news.gardentoolbox.co.uk/wp-content/uploads/2013/06/slug.jpg" width=450><p>
<figcaption>source: http://news.gardentoolbox.co.uk/articles/slugs-removing-them-naturally-and-un-naturally</figcaption>

A: This is also a slug:
<p><img src="images/slug.png"></p>

Which did you think I meant? And why is this relevant?

Now that I'm building web apps, it's important for me to be conscious of creating RESTful URLs. REST, which stands for Representational State Transfer, refers to a set of conventions within web architecture that define best practices or standards for representing resources on the web (where a resource is any data requested by the user).

The REST philosophy has several components, but a fundamental tenet is that URLs on the web should be readable and somewhat intuitive. In order to comply with the RESTful pattern, it is generally preferable for URLs to represent what the page displays in a human-readable format. If I were to send you a link to my Twitter page, it's pretty awesome that I can direct you to twitter.com/bshap27, where bshap27 is my Twitter handle, and it's as simple as that. Easy to understand, easy to remember. It would be pretty annoying if the URL were something nonsensical like twitter.com/iowueyiuahsldkfjabdm, or even something like twitter.com/user/1/5/8/4/ . Neither of those paths are RESTful, because I can't intuit what they mean. Now, what if I wanted to send you a link to a new song I recorded called "I Love Sunshine"? Spaces can't be used in a URL. This is where slugs come in.

A slug, in this context, refers to a string of words that is stripped of spaces and filled instead with punctuation that is more compatible with a URL, usually a dash. When most browsers identify spaces in a URL, they automatatically render those spaces to a default string. A quick Google search of my own name shows me that Google changed the space in my search terms to the string "%20":

<em>https://www.google.com/webhp?sourceid=chrome-instant&ion=1&espv=2&ie=UTF-8#q=becca%20shapiro</em> => becca%20shapiro

But that's messy. So when we're creating URLs of our own, we follow REST conventions and use a slug. www.beccastunes.com/i-love-sunshine. (Disclaimer: not a real website or song).

Aesthetics and usability aren't the only reasons we use slugs. I mean, how often do people actually type out URLs that are more than like, 20 characters? Slugs don't just help PEOPLE find a website, they help SEARCH ENGINES find a website. Including search keywords in your site URL can increase your page rank. And when link contents are easily discernable from the URL, users are better able to gauge whether the content is relevant to them and are more likely to click. Hasn't a friend ever sent you an email with no subject and just a link? And has it ever happened to you that the link URL was jumbled, and you weren't sure if it was spam? Readable URLs prevent this conundrum. And therefore, slugs are important from an SEO perspective.

Now, at some point, really long URLs are excessive. And super long URLs can actually hurt SEO rather than bolster it because too many keywords can be perceived as junk. So from comments on StackOverflow and several other blogs and forums, I've done the work for you and deduced that a reasonable standard seems to be 5 words or less. A common practice is to remove terms like 'the', 'and', 'or', etc. in order to keep word/character count manageable.

Finally, you may be wondering about the etymology of the word slug. I was too. Enjoy.

<p class="img_caption2 becca_border"><a href="http://stackoverflow.com/questions/6750300/how-did-the-term-slug-as-in-urls-originate"><img src="images/slug_stack_overflow_2.png"></a></p>
<figcaption>http://stackoverflow.com/questions/6750300/how-did-the-term-slug-as-in-urls-originate</figcaption>

<p class="img_caption2 becca_border"><a href="http://stackoverflow.com/questions/4230846/what-is-the-etymology-of-slug"><img src="images/slug_stack_overflow.png"></a></p>
<figcaption>http://stackoverflow.com/questions/4230846/what-is-the-etymology-of-slug</figcaption>

Open Questions and Other Resources:
<li>How would <a href="http://en.wikipedia.org/wiki/Roy_Fielding">Roy Fielding</a>, the inventor of REST, feel about bit.ly?</li>
<li>Further reading: <a href="http://www.wpkube.com/seo-beginners-guide-to-permalinks-and-slugs/">SEO Beginners Guide to Permalinks and Slugs</a> (note: look at the URL for this article. Very RESTful).</li>
<li>Did you know that if you <a href="https://www.youtube.com/watch?v=PsVj3Hjr5vw">lick a banana slug</a>, your tongue goes numb? (Fun fact, I've done it). </li>