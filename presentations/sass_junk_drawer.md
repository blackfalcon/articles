#Clean out your Sass junk drawer
__*CSS has had a long and sorted past. With every project, it's creator never sets out with the goal of making a complete and total mess of things. Their intention is not to build something that is practically illegible, impracticable to maintain and is limited in scale. But somehow, someway this is where many inevitably end up. What's sad is that even with tools like Sass at our disposal we still end up in the same place, just via a different path. Luckily, all is not lost. With some simple strategies, organizational methods and out of the box tools can really help get that junk drawer inline.*__ 

The *'Sass Junk Drawer.'* All of us using Sass at one time or another have done this. For most, this was a rookie mistake, but for others, this is a continuing issue with our code architecture and file management techniques. Sass doesn't come with any real rules for file management, developers are pretty much left to their own devices. Reminds me of the old days of Javascript.

##Before we can heal, we need to confront our demons
For many of us, CSS started out as very simple documents. Primarily due to lack of browser support and other less technical reasons, most of our presentation code was in the markup. In the early 2000's as [tableless web design](http://goo.gl/Td8uZ) began to really take foothold, our stylesheets quickly began to grow in size and CSS didn't offer us much support. We tried to break our stylesheets into smaller documents, but these strategies proved to have serious performance issues. Linking to multiple stylesheets meant multiple server hits and CSS's `@import` feature had such a negative impact on [web page performance](http://goo.gl/ZkP2w) it's practice was quickly abandoned.   

Looking for better tools to do our job developers turned to CSS processors, Sass for example, but sadly didn't stray from old habits. We still created large documents, put all the [mixins](http://goo.gl/a8TUR) and [variables](http://goo.gl/ce27v) at the top of the doc and just started hashing out a bunch of CSS rules. 

Over time that we began to see ways we could break these files into smaller documents based on common principles. Variables and mixins were the easy ones. Then *typography*, *forms* and some basic *chrome* concepts began to split off. This worked, but without a real strategy this process was doomed. As the `sass` files grew in number we started putting things in sub-folders, quickly giving way to *junk drawers* of files haphazardly daisy-chained together. 

Abuse of the [nesting rule](http://goo.gl/yTlYb) was our next transgression. A feature that made it seem so right, so awesome, so natural to [build CSS that mimicked our markup](http://goo.gl/Jw84O). But we were so wrong. We succumb to the pressures of specificity to dominate the cascade and found ourselves in a [CSS Selector Nightmare](http://goo.gl/Wr8Tp). Our CSS was hard to reuse and extremely fragile.   

##Controller based CSS
With introduction of the Asset Pipeline, Rails shipped with a function to generate controllers from the command line. Running this command will generate new files in the `app/assets/javascripts/` and `app/assets/stylesheets/` locations. While this may be a good solution for Javascript, this has lead some to think that organizing your [CSS based on controllers](http://goo.gl/rGecm) is a good idea as well. 

While there is some merit to this in regards to template layout styles, this practice inevitably lends itself to creating styles that are too specific to the view and not easily reused throughout the rest of the application. Not to mention, in order to specify modular styles between templates we need to again dominate the cascade by deeply nesting our selectors. File size and performance no-nos. 

Between views, duplicated code will begin to reveal itself we will attempt to abstract the code. Another organizational technique is to create a `/partials` directory. This will be a repository for custom built mixins, variables and other reusable codes. In essence, we are creating another *junk-drawer*.

##Action based organization
In attempts to abstract away from the view process we discussed, some developers have thought to organize from an action perspective. If the visual elements are part of an action, making directories based on these actions makes sense, right? Sadly, his quickly falls apart as well as not all UI elements can be easily categorized this way. 

As visual elements grow, random files begin to populate the Sass directory again. Universal widgets, plug-in styles, custom mixins and minor interactive elements begin to collect. Without a strategy other then *action* based categorization, we are back again filling our new *junk-drawer*. 

##Learn from our mistakes
I speak from experience as I have made all of these mistakes. It was recently in my journey of *doing it wrong* that I began to see the error in my ways. The irony was that for a long time I had the right solution, but didn't realize it. 

For a few years I worked on a team developing an enterprise CMS. By default we had to deconstruct the UI of a site down to it's elements and reusable modules. While my stylesheet management techniques weren't perfected, by conceptualization of UI abstraction was. 

After sitting down and analyzing the code I had written for a recent project I began to realize that we were engineering our CSS from entirely the wrong perspective. From legacy CSS down to Action Based methods, we were building our code from the outside in. There was more focus on the end view then there was on the elements that built the view. 

