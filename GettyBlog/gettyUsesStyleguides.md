#Style guides: Documenting the design
by Dale Sande

Small and enterprise alike, companies deal with issues of UI inconsistency, scaleability and maintainability. Developers will agree that in the lifecycle of a site, HTML and CSS have a tendency to quickly get out of sync. But why? Many will point the finger at the technologies, HTML and CSS are in a family of technologies that have seen little in the way of advancements. While languages have come and gone and some have seen major overhauls to meet the needs of modern developers, HTML and CSS seem to just sit there. It wasn't unitl the new mobile evolution that HTML and CSS have really started to get some attention again. 

Blaming the technologies to me is the easy way out, I think that the issue runs deeper. Presentational layer technologies historically have fallen under the domain of designers. If developers are doing the work, it is usually something that they are assigned to do, not something that the feel passionate about. Communication is typically one-way and rarely have I seen a fruitful collobration between designers and developers. There is the hand-off after the designer completes the comp and the review after developer has done the work, but this is not collobrative communication, this is a one-way radio signal. 

##If communication is broken, find another way to communicate
At Getty Images we faced many of these same challenges. While we have very tallented designers and amazingly skilled developers, communiation was one sided, knowledge was in an information silo and as a result feature development was slow, resource consuming and fraught with issues. Both design and development teams were looking for solutions to reduce design and development cycles and the solution arrived at style guides.

A few years back the idea of style guides for websites was not a widely known concept. Searching the Internet was often meet with few results on the topic. Not to say that this was a new concept all together, there have been style guides, or what some have called a 'brand-bible', have been around for years. But a useful application to the web was still in it's infiancy. Like many other concepts, when it comes to the web we need to reinvent the wheel. 

##What is a style guide?
A style guide is a documented design and brand standard. Historically a style guide will consist of all the 'design' standards and illustrate examples of typography, color, elemental patterns, etc. This will provide a framework to inform new design work and clients the same. The styleguide is also intended to provide a resource for designers and developers to create a taxonomy as to how things should look and work. 

A key component of a modern style guide is not to simply document these visual artifacts, but it needs to be presented in a format from which it is intended. Simply put, a web based styleguide needs to live as code. Be presented in the browser and of course be responsive and adaptive. A style guide needs to embody all the characteristics that the final producion application will. 

##Reuse is free, unique flowers are expensive
I have found over my career as a UI Engineer/Developer and Designer that presentation layer code suffers from two distinct but coupled issues; underestimation and devalued importance. As Product Owners continue to devalue the importance of this work (after all anyone can do HTML and CSS, right?!) the developers continue to reduce the estimation of work. But the work is still there, it didn't go away. Now we suffer from one of the greatest injustices there are, the passionate developer who works off the clock to do a good job, but hides the real effort that went into the work. 

The style guide is the great equalizer of truths. When design elements are created and the only documented on the page itself, it is trapped in that singulare experience. It is this encasement of ideas where designers and developers alike gloss over the opportunities for reuse and instead default to redeveloping the experience. When these same design elements are created in the styleguide they are autonomous. They are easily identifiable and infinatelly resuable. As new feature development continues, we should all be asking, "What is in the style guide that we get for free and what will cost new development time?" 

##Documenting is nice, but abstract development?
At Getty Images we have embraced this concept to a point where we see that we can push it even further. Not only does a style guide provide a documented resoruce of the bits and pieces of the UI, but it also serves as a development environment for new artifacts. 

We have discovered that abstraction from the application yields powerful results. Consistency, enterprise scaleability and easily maintainable code. Using the framework of the style guide, our design process is moving towards a more collobrative model between designers and developers, building assets inside the style guide first and then applying them to the actual application. As well, prototyping the experience on multiple formats in real time.

##QA made easy
Another tangable artifact of the style guide and the process of abstract development before application integration is the QA process. Developing UIs in this style lends itself to instant quality reviewes between browers, plarforms and devces. Design styles are not exclusive to individual pages or experience of the site. QA is no longer reqired to review the same astethics repeatedly because of poor attempts at reuse. 

At Getty Images we have found this to be a huge win for company resources. 

##Is this really time well spent?
Some may argue that this is wasted effort and time is best spent on developing application functionality. My experience has shown me otherwise. Regardless where the effort is focused, the work never goes away. Once that we acknowledge that it is worth a little investment up-front, then we will profit in the end. 

In fact is has been my experience that if you do not make this investment in the UI up front, you will lose time, money, and resources in the end. Comments like, "Why did this take 10 days to update?" begin to come up in conversation and no one really like saying, "The HTML and CSS was all messed up and it was hard to get working in IE7."








