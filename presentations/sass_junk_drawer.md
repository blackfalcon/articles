#Clean out your Sass junk drawer
__*CSS has had a long and sorted past. With every project, it's creator never sets out with the goal of making a complete and total mess of things. Their intention is not to build something that is practically illegible, impracticable to maintain and is limited in scale. But somehow, someway this is where many inevitably end up. What's sad is that even with tools like Sass at our disposal we still end up in the same place, just via a different path. Luckily, all is not lost. With some simple strategies, organizational methods and out of the box tools can really help get that junk drawer inline.*__ 

The 'Sass Junk Drawer.' All of us using Sass at one time or another have done this. For most, this was a rookie mistake, but for others, this is a continuing issue with proper file management. Sass is unique as it doesn't come with any real rules for file management, developers are pretty much left to their own devices. The Rails community has tried to help in cleaning things up. Back before the Asset Pipeline we used to keep the Sass files in the `public` folder. Then came Rails 3.1, but I would argue that the concept of having controller specific Sass is not such a good idea. So, what do we do?

##Before we can heal, we need to confront our demons
Many early adaptors of Sass didn't stray far from our old habits. We still created large documents, put all the `mixins` and `variables` at the top of the doc and just started hashing out a bunch of CSS rules. It was then over time that we began to see ways we could break these files into smaller documents based on some common principles. Variables and mixins are the easy ones. Then maybe `typography`, then forms and some basic `chrome` concepts. These ideas were still in their infancy and we were still creating extremely large files that encompassed layers of unnecessary complexity between common elements, layout and chrome.  

Name-spacing was one of our early transgressions. The 'white-space selector inheritance' feature in Sass made it seem so natural, so right, so awesome. But we were so wrong. This broke every good CSS rule in the book and made our code hard to reuse and very fragile. But then 'OOCSS` came along and showed us another way. 

So we began segmenting our code. Breaking it into even smaller and smaller chunks. Features like `@import` started to take hold and we began daisy-chaining our documents together. This worked, but without a real strategy this process was doomed. Files were created on the fly and without any real hierarchy or architecture, we simply created more files and imported them into others. Sure we put things into 'folders', but this process quickly gave way to 'junk drawers' of files. 

##Action based orginization
Developers in the community tried early attempts at better organization from an action based point of view. After all, much of their application was organized this was as well and this made some sense. All of the elements in the view were part of an action, so making directories based on these actions created a 1:1 relationship between the application and the UI. Makes sense, right? 

This quickly falls apart as not all UI elements are based on actions. This is a perfect perspective for features and functionality, but not for design. This would be like doing all your development in the `V` of `MVC`, and that is just plane crazy talk. 











