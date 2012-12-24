#Clean out your Sass junk drawer
__*CSS has had a long and sorted past. With every project, it's creator never sets out with the goal of making a complete and total mess of things. Their intention is not to build something that is practically illegible, impracticable to maintain and is limited in scale. But somehow, someway this is where many inevitably end up. What's sad is that even with tools like Sass at our disposal we still end up in the same place, just via a different path. Luckily, all is not lost. With some simple strategies, organizational methods and out of the box tools can really help get that junk drawer inline.*__ 

The *'Sass Junk Drawer.'* All of us using Sass at one time or another have done this. For most, this was a rookie mistake, but for others, this is a continuing issue with proper file management. Sass is unique as it doesn't come with any real rules for file management, developers are pretty much left to their own devices.

##Before we can heal, we need to confront our demons
Many early adaptors of Sass didn't stray far from old habits. We still created large documents, put all the `mixins` and `variables` at the top of the doc and just started hashing out a bunch of CSS rules. It was over time that we began to see ways we could break these files into smaller documents based on some common principles. Variables and mixins are the easy ones. Then `typography`, `forms` and some basic `chrome` concepts began to split off. These ideas were still in their infancy and developers were still creating extremely large files that encompassed layers of unnecessary complexity between common elements, layout and chrome.

Name-spacing was one of our early transgressions. The [nesting rules](http://goo.gl/yTlYb) feature in Sass made it seem so right, so awesome, so natural to [build CSS that mimicked our markup](http://goo.gl/Jw84O). But we were so wrong. We succumb to the pressures of specificity to dominate the cascade and found ourselves in a [CSS Selector Nightmare](http://goo.gl/Wr8Tp). Our code was hard to reuse and extremely fragile. But then again, reuse to us back then meant to use `mixins` and simply duplicate code throughout. 

Some began segmenting the code. Breaking it into even smaller and smaller chunks. Features like `@import` started to take hold and we began daisy-chaining our documents together. This worked, but without a real strategy this process was doomed. Files were created on the fly without any real hierarchy or architecture. By creating files and randomly importing them into others, simple mistakes like importing files that had classes thus creating duplicate classes in the output with each import, began to happen. Then when the `sass` folder started to get out of control, we started putting things in sub-folders, quickly giving way to 'junk drawers' of files. 

##Action based organization
Developers in the community tried early attempts at better organization from an action based point of view. After all, much of their application was organized this was as well and this made some sense. All of the elements in the view were part of an action, so making directories based on these actions created a 1:1 relationship between the application and the UI. Makes sense, right? 

This quickly falls apart as not all UI elements are based on actions. This is a perfect perspective for features and functionality, but not for design. This would be like doing all your development in the `V` of `MVC`, and that is just plane crazy talk. 











