#Clean out your CSS junk-drawer
__*CSS has had a long and sorted past. With every project, it's creator never sets out with the goal of making a complete and total mess of things. Their intention is not to build something that is practically illegible, impractical to maintain and is limited in scale. But somehow, someway this is where many inevitably end up. Even with tools like CSS pre-processors at our disposal we still end up in the same place, just via a different path. Luckily, all is not lost. With some simple strategies, organizational methods and out-of-the box tools, we can really help get that junk-drawer inline.*__ 

For many of us getting started with Sass, at one time or another have created a *junk-drawer* of files. For most, this was a rookie mistake, but for others, this is a continuing issue with our architecture and file management techniques. Sass doesn't come with any real rules for file management so developers are pretty much left to their own devices.

##Large files and increased complexity
For many, our CSS started out very simple. As [tableless web design](http://goo.gl/Td8uZ) began to really take foothold, our stylesheets quickly began to grow in size. We tried to break our stylesheets into smaller documents, but these strategies proved to have serious performance issues. Linking to multiple stylesheets meant [multiple server hits](http://goo.gl/vSdp3) and [CSS' @import feature](http://goo.gl/8Yvtn) had such a negative impact on [web page performance](http://goo.gl/ZkP2w) it's practice was quickly abandoned.   

Developers recently turned to [CSS pre-processors](http://goo.gl/SdnOh) for new solutions but sadly didn't stray from old habits. We still created large documents, placing all our [mixins](http://goo.gl/a8TUR) and [variables](http://goo.gl/ce27v) at the head of the doc and just started hashing out a bunch of CSS rules.

Looking for better management techniques, we began breaking these large stylesheets into smaller documents based on common principles. *Variables* and *mixins* were the easy ones. Then *typography*, *forms* and basic *design* concepts began to split off. This reduced our individual file size, but without a real strategy this process was doomed. As the files grew in number, sub-directories quickly gave way to *junk-drawers* of files haphazardly daisy-chained together. 

##Controller/action based CSS
With increased popularity in [Model-View-Controller(MVC) frameworks](http://goo.gl/STqQ), developers began to look at these file structure solutions to solve their issues. Organizing your [CSS based on controllers](http://goo.gl/rGecm) was a popular approach. While there is some merit to this in regards to template/layout styles, this practice inevitably lends itself to creating styles that are too specific to the view and not easily reused throughout the rest of the application.

Abuse of the [nesting rule](http://goo.gl/yTlYb) was our most egregious transgression. A feature that made it seem so right, so awesome and so natural to [build CSS that mimicked our markup](http://goo.gl/Jw84O). But we were so wrong. We succumb to the pressures of specificity to dominate the cascade and found ourselves in a [CSS Selector Nightmare](http://goo.gl/Wr8Tp). Our CSS was hard to reuse and extremely fragile.

Between views, duplicated code begins to reveal itself and developers made valid attempts to abstract the code. A [/partials](http://goo.gl/iRHu0) directory, another MVC pattern was quickly adopted. A repository for custom built mixins, variables and other reusable codes. In essence, a *junk-drawer*.

In other attempts to abstract away from the view, some thought to organize their files from the action perspective. If the visual elements are part of an action, making directories based on these actions makes sense, right? Sadly, this quickly falls apart as well. Not all UI elements can be easily categorized this way. Random files again populate the directory. Universal widgets, plug-ins, and custom mixins begin to collect. Again we are suffering from the *junk-drawer* effect. 

##Learn from our mistakes
I speak from experience as I have made all of these mistakes. It was during my journey of *doing it wrong* that I began to see the error of my ways. Ironically, for a long time I had the right solution, but didn't realize it. Years ago I worked on a team developing an enterprise CMS. By default we had to decompose a site's UI to it's lowest common elements. From those elements we could then build up to modules and then finally assemble the view in the CMS populated with content. While my stylesheet management techniques weren't perfected, by conceptualization of UI abstraction was. 

After sitting down and analyzing the code I had written for a recent project I began to realize that we were engineering our CSS from entirely the wrong perspective. From legacy CSS down to Action Based methods, we were building our code from the outside in. There was more focus on the end view then there was on the elements that built the view. 

