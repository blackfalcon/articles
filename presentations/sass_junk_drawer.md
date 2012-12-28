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
I speak from experience as I have made all of these mistakes. It was during my journey of *doing it wrong* that I began to see the error of my ways. Ironically, for a long time I had the right solution, but didn't realize it. Years ago I part of a team that developed an enterprise CMS(I know, who hasn't). By default we had to decompose a site's UI to it's lowest common elements. From those elements we could then build up to modules and then finally assemble the view populated with CMS content. While my stylesheet management techniques weren't perfected, but my conceptualization of UI abstraction was. 

After sitting down and analyzing the code I had written for a recent project I began to realize that we were engineering our CSS from entirely the wrong perspective. One of the first mistakes was that we were engineering from the full page comp. This was forcing us to think of the view as a whole for every feature and UI element. We were building all of our code from the *outside-in*. 

It was then that I started thinking back to the CMS. Due to the patterns already set in the framework, by default we always started from the elemental perspective. Type, colors, forms, elements, basic UI chrome (borders, shadows, icons, etc). Once we had those elements coded in the CSS, then it was a matter of applying the skin to the CMS modules. The modules then in-turn were used in the view and the content was applied via the CMS. It worked seamlessly. 

##Element, module, view
Not all sites and web apps are built in these types of frameworks. So how can we apply these principals into everyday projects? The first thing we need to do is be better at decomposing the designs we are tasked with building. It is this *inside-out* approach that is the real key to a good process, file structure and a scaleable architecture. Coding the element, creating the module and assembling the view. 

Here I propose the following file structure that embodies this point of view. In the root there are directories for more complex concepts, then individual Sass partials to address the elemental parts and last is a Sass manifest file to aggregate all the awesome.

```
sass/
	buttons/
	color/
	forms/
	layouts/
	modules/
	typography/
	ui_patterns/
	_buttons.scss
	_config.scss
	_design.scss
	_forms.scss
	_reset.scss
	_typography.scss
	style.scss
```

###Sass partials and the manifest
[Partials](http://goo.gl/iRHu0) are a simple and powerful weapon in the Sass arsenal. Simply put, any file that has an *underscore* before the name, `_partialName.scss`, will __not__ be processed into a `.css` file by itself. It is required to be imported into a file that __will__ be processed into CSS.  

###Manifest files
In this file structure example, the only file that is processed into CSS is the `style.scss` manifest.  It's here where all your custom add-ons, configs, elements, modules, views, mixins, extends, etc., are all imported and processed into a production stylesheet. It is important that this file be kept void of any CSS rules. Rules at this level is a poor organizational habit and speaks to unnecessary randomization of CSS rules.  

This is not to say that `style.scss` is the only Sass manifest file. Manifests can import other manifests. As seen in this [example manifest](http://goo.gl/4bO7j) from the Toadstool style guide framework, sub-directories can also contain manifest directories. This pattern helps to keep the `style.css` manifest from becoming overwhelming to manage as well to keep sub-directory files nicely organized.

Here I would especially follow *The Inception Rule: don’t go more than four levels deep.* That is if you want to keep your sanity. Going beyond this rule will increase unnecessary complexity in your app.

####Manual manifest files or glob-imports
*Manual* manifests are just that, manual management of imported Sass files from sub-directories. This is a good practice to follow when you need specific control over the inheritance of files. Example, rule A needs to come before rule B in the output cascade. 

*Glob-imports* on the other hand is a way for you to simply point to a directory in your manifest, `@import "directory/*";` and Sass will import all the files in alphabetical order. This is great for a directory of mixins or functions that simply need to be loaded in memory for Sass to process the CSS. If you want to use the *glob* function but require a specific order, a naming convention like `_01_mixin.scss` could work as well. 

While *glob-import* is a feature available to Rails projects, this is not a native feature of Sass. If you are not developing a Rails project, [Chris Eppstein](https://github.com/chriseppstein) wrote a [RubyGem](http://goo.gl/ww5Wo) that can be used with Sass or Compass projects. 

###Configurable options
An advanced concept of using a Sass structure like this is using a `_config.scss` file to manage the [smart defaults](http://goo.gl/BZOUE) for your UI. Nested in the module directories, `@mixin` and `@extend` rules can be engineered to take advantage of these configurable options. 

In the same way as manifest files, no CSS is ever processed from the `_config.scss` file. It should only be included in a processed *Sass manifest* file, such as `style.scss`. It is also important to import this file at the top of the `style.scss` file so that all imported code thereafter will be able to take advantage of these configurable values. 

###Element partials
It is in the elemental partials that we start to get to work. Writing Sass rules that will create your UI foundational layer of the site/app. `_buttons.scss`, `_design.scss`, `_forms.scss`, `_reset.scss` and `_typography.scss` all contain Sass rules that will process into CSS. While they will import other *partials*, `@mixin` and `@extend` rules, it is important to remember that these files are engineered __only to output__ CSS.  

It is important to understand that these *element partials* are logic-less layers. Mixins, placeholder selectors and custom functions should be abstracted out into a sub-directories for portability and scaleability.

Let's take __buttons__ for example. It's amazing that something as simple as buttons can be such an amazingly complex architecture. Between gradients, :hover and :active states, one could go a little mad. Thankfully, there are people out there that have tried to solve this problem for you and there are a number of really awesome [Compass Extensions](http://goo.gl/qN4IZ) you can install to help you get started. So it is in this partial that we only write our button styles. 

```scss
button, a.button {
  @inlcude button(#d22);
}
```

###Custom mixins, placeholder selectors and functions organization 
Using our button example again, let's say that you need to roll your own. In the file structure there is a corresponding `buttons/` directory where you will keep your `_mixin.scss` and `_extend.scss` and custom functions. 

Keeping these functional Sass files separate from the actual processed CSS rules is an important concept. This will improve readability and search-ability of your code. Patterns like placing mixing in the same file as the CSS rules leads to overly complex files to scan. Not to mention opportunities for accidental pollution of your processed CSS. For example, you have a mixin inside a document that contains CSS rules and you need that mixin available from another resource, importing partial will cause your CSS rules to be __duplicated__. And that's bad. 

##Modules and UI patterns
Now that we have established the architecture of our UI foundation, it is time to start assembling some modules. In essence, a module is an assembly of foundational elements with enough CSS to hold it together that is exclusive to a particular interaction of the application. Modules will come in all shapes and sizes. Larger modules may also consist of smaller modules or UI patterns.  











