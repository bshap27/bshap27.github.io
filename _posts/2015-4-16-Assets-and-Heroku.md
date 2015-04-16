---
layout: post
title: My Assets and Heroku are In A Fight
---

<b>READ THIS POST IF: you are deploying an app to Heroku and the build fails while compiling assets.</b>

Scenario: I'm working on an app that is styled using a theme from a vendor. I've copied the CSS files I need into vendor/assets/stylesheets and the javascripts into vendor/assets/javascripts, without any nesting. All files seem to be properly required in my app; my manifests require the vendor/assets trees and the styling and behavior in my app are as I want them to be.

It comes time to push up to Heroku. <code>git push heroku master</code>. She starts writing temp files, ok good... she runs rake assets:precompile, it's looking normal... and then precompiling assets fails. What gives?


<b>All the things I tried:</b> <a href="#fix">(skip to the fix)</a>

<u>Precompiling Assets</u>

It seems reasonable to try to precompile assets before pushing up to Heroku and then running the build again. So I run rake assets:precompile locally and it passes without fail. I push up to Heroku, and the build works! But I notice that my javascripts are broken, both locally and remotely. There's a sidebar that should expand and collapse upon click of the menu icon, and it isn't working. Huh.

<u>Mixed Dependencies</u>

So I look into my javascripts manifest and I think jquery might be required twice. It feels wrong, but I remove //require jquery and //require jquery_ujs. And javascripts go back to normal! Ok, cool.

I continue business as usual. I decide to work on my login page. I click sign out and... what? Why am I served a rails error? It seems as though clicking the link that directs to users/sign\_out is trying to take me to the users#show route, users/:id, because it thinks "sign\_out" is a user_id. Devise was the first feature I implemented, over a week ago, and it's worked up til now. Weird. I troubleshoot this as best I know.

<u>Route configuration</u>

I change the order of the "devise_for" and "resources :users" in routes.rb. That doesn't do it. I remove "resources :users" completely. No dice.

The sign out route is inherited via Devise as sessions/users/sign\_out, so it's tucked away in the Devise gem within the sessions controller and isn't actually present in my project. But I can run <code>rails generate devise:controllers users</code> to generate this controller (and all devise controllers). I explicitly set <code>devise_for :users, controllers: { sessions: "users/sessions" }</code> hoping that by explicitly telling my routes.rb file where the sessions routes lives, it will no longer confuse the sign out and show routes.

This doesn't do anything at all. I revert.

<u>Asset loading</u>

There's an entypo icon inside of my Sign Out link. Maybe having an asset inside of that link is breaking the link action? I remove it. No change. Revert.

<u>Baseline compatibility: Does Devise play nice with Heroku?</u>

How are my assets, devise, and heroku even related? Well, I start researching Devise and Heroku. Many sources confirm that sometimes compiling assets during a heroku push will break as a result of using Devise, but upon further research, this issue is specific to rails 3 and produces an error message dissimilar to that I was getting. So I ruled out Devise as the cause of the Heroku compile issue, and deduced that //require jquery and //require jquery\_ujs had to be put back in.

<u>Application configuration</u>

I start vigorously searching stackoverflow.
I add <%= javascript_include_tag :defaults %> to application.html.erb. No change.

<u>Javascript Manifest File (mounting order)</u>

At this point, it seems like I need to diagnose why precompiling assets is break my javascripts in the first place. Are my scripts required in an incorrect order in the manifest file?

I use rake assets:clobber to remove the precompiled assets I had just generated (which deletes the public/assets folder).

I search the theme FAQs on the vendor site, but although the help topics are fairly thorough I find nothing referencing the mounting order of the javascript files.

I un-require the vendor tree and look back into my theme and decide to manually list out each vendor javascript that I need, in the exact same order as the theme's example files. Re-precompile. No change.

<u>CSS</u>

I need to look at this from a new angle. If precompiling is working locally, albeit breaking my javascript, why does compiling break in Heroku push? I look back at the error. 

<code>rake aborted!<br>
Invalid CSS after</code>.....

Wait, invalid CSS? What is that about? When I precompile, only the javascript is broken.

<a name="fix"></a><b>THE FIX!!!!</b>

I grab a brilliant Flatiron instuctor who suggests the issue might have something to do with my manifest file being a SASS document while the rest of my stylesheets are a combination of CSS and SASS. I deduce it might be a good idea to standardize to either all SASS or all CSS. I'm not even using any SASS, so I change all of the .scss file extentions to .css, including the manifest file, remove 'gem SASS-RAILS' from my Gemfile, bundle, commit, and push. It goes through. Heart racing. Open the heroku app. Styling is all in place. Sign in. Click the sidebar, it expands and collapses. Sign out.TA DA!!!

Oh my god. I can't believe I have spent 8 hours on this issue, and it was CSS the whole time - it had nothing to do with JQuery, or Devise, WHAT A RABBIT HOLE THAT WAS.

<b>Moral of the story: If you try to push up to Heroku and your build is aborted in the middle of compiling assets, and you see an "invalid CSS" error message, check your file extensions FIRST.</b>

Your issue is unlikely to be due to any of the following:<ul>
<li>Devise (specifically, the order of your routes in routes.rb probably doesn't matter, and whether your controllers are tucked into Devise or present in your app file tree shouldn't either.)</li>
<li>Icons included in the display value of links</li>
<li>The order of your files in the javascript manifest</li>
<li>The presence of //require jquery and //require jquery\_ujs in the javascript manifest. <b>READ: DO NOT REMOVE THESE.</b></li>
<li>Javascripts included manually in the head of application.html.erb</li>
<li>The presence of old compiled assets</li></ul>


By the way, I couldn't find this information anywhere on stackoverflow. Watch me spread the gospel of this fix all over the internet.

Needless to say I'll be making a sacrifice to the Heroku gods tonight. Godspeed, dear Heroku users.