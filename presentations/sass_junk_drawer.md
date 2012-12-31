#Clean out your Sass junk-drawer
__*CSS has had a long and sorted past. With every project, a developer never sets out with the goal of making a complete and total mess of things. Their intention is not to build something that is practically illegible, impractical to maintain and is limited in scale. But somehow, someway this is where many inevitably end up. Luckily, all is not lost. With some simple strategies, organizational methods and out-of-the box tools, we can really help get that junk-drawer inline.*__ 

For many of us getting started with Sass, at one time or another have created a *junk-drawer* of files. For most, this was a rookie mistake, but for others, this is a continuing issue with our architecture and file management techniques. Sass doesn't come with any real rules for file management so developers are pretty much left to their own devices.

##Large files and increased complexity
CSS started out with very simple intentions, but as [tableless web design](http://goo.gl/Td8uZ) began to really take foothold, our stylesheets quickly began to grow in size. We tried to break our stylesheets into smaller documents, but these strategies proved to have serious performance issues. Linking to multiple stylesheets meant [multiple server round-trips](http://goo.gl/vSdp3) and [CSS' @import feature](http://goo.gl/8Yvtn) had such a negative impact on [web page performance](http://goo.gl/ZkP2w) it's practice was quickly abandoned.   

Developers turned to [CSS pre-processors](http://goo.gl/SdnOh) for new solutions but sadly didn't stray from old habits. Still creating large documents, placing [mixins](http://goo.gl/a8TUR) and [variables](http://goo.gl/ce27v) at the head of the doc and simply hashing out a bunch of CSS rules in the body.

Look for better management techniques some began to break these large stylesheets into smaller documents based on common principles like *variables* and *mixins*. *Typography*, *forms* and *design* soon followed. Sure this reduced file size, but without a real strategy this process was easily doomed. As files grew in number, sub-directories quickly gave way to *junk-drawers* of haphazardly daisy-chained files. Frustrated, developers contented to look for inspiration. 

##Controller/action based CSS
Inspired by [Model-View-Controller(MVC) frameworks](http://goo.gl/STqQ), developers began to look at these file structure solutions to solve their issues. Organizing [styles based on controllers](http://goo.gl/rGecm) was a popular approach. While there is some merit to this in regards to template/layout styles, this practice inevitably lends itself to creating styles that are too specific to the view and not easily reused throughout the rest of the application.

Abuse of the [nesting rule](http://goo.gl/yTlYb) was the most egregious transgression. A feature that made it seem so right, so awesome and so natural to [build CSS that mimicked our markup](http://goo.gl/Jw84O) was so wrong. Succumbing to the pressures of specificity to dominate the cascade, developers found themselves in a [CSS selector nightmare](http://goo.gl/Wr8Tp). Style rules were difficult to reuse and extremely fragile.

Between the views, duplicated code began to reveal itself. Attempts to abstract the code, following another MVC pattern, typically resulted in the creation of a [/partials](http://goo.gl/iRHu0) directory. A repository for custom built mixins, variables and other reusable codes. In essence, a *junk-drawer*.

In other attempts to abstract away front he view, some developers have tried to organize their files based on actions. If the visual elements are part of an action, making directories based on these actions makes sense, right? Sadly, this quickly falls apart as not all UI elements can be easily categorized this way. Random files again populate the directory, universal widgets, plug-ins, and custom mixins begin to collect. Once again suffering from the *junk-drawer* effect. 

##Learn from our mistakes
Life is about journeys. It was during my journey of *doing it wrong* that I began to see clarity. Ironically, I had the right solution all along, but didn't realize it. While part of a team developing an enterprise CMS, our process was to decompose a site's UI to it's lowest common elements. From those elements we could then build modules and then finally assemble the view templates. Each step building on the previous. Although my stylesheet management techniques weren't perfected, my conceptualization of UI abstraction was. 

Working with a new team, sans a CMS, I went into the project with the same conceptual understanding, but the outcome was drastically different. Post launch, I sat down and analyzed the code I wrote. I came to the realization that we were engineering our CSS from __entirely the wrong perspective__. We were engineering our UIs from the full page perspective. Building visual elements scoped to *a specific* view and all of our code was being built from the *outside-in*. 

I started thinking back to my processes pioneered with the CMS. Patterns established in the framework dictated we start from the elemental perspective; type, colors, forms, basic UI chrome (borders, shadows, icons, etc) all coded first. Once those element styles were completed, it was a matter of applying the *skin* to the CMS modules. The modules then in-turn were used to assemble the view. It worked quickly and seamlessly. Building the UIs from the *inside-out* was clearly the solution. 

##Elements, modules and layouts
Applying these principals to new projects was the next challenge. First we need to be better at decomposing the designs. The *inside-out* approach is the key to this process, file structure and scaleable architecture. Code the element, create the module and assemble the layout. 

Here I propose the following file structure that embodies this point of view. In the root there are directories for more complex concepts, then individual Sass partials to address the elemental parts and last is a manifest file to aggregate all the awesome.

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
	_forms.scss
	_global_design.scss
	_reset.scss
	_typography.scss
	style.scss
```

##Sass partials and the manifest
[Partials](http://goo.gl/iRHu0) are a simple and powerful weapon in the Sass arsenal. Simply put, any file that has an *underscore* before the name, `_partialName.scss`, will __not__ be processed into a `.css` file by itself. It is required to be imported into a file that __will__ be processed into CSS.  

##Manifest files
In this file structure example, the only file that is processed into CSS is the `style.scss` manifest.  It's here where all your custom add-ons, configs, elements, modules, views, mixins, extends, etc., are all [imported](http://goo.gl/WhLho) and processed into a production stylesheet. It is important that this file be kept void of any CSS rules. 

This is not to say that `style.scss` is the only Sass manifest file. Manifests can import other manifests as seen in this [example manifest](http://goo.gl/Jhedp) from the Toadstool style guide framework. Manifests can import all the files within a sub-directory, a pattern that helps to keep the `style.css` manifest easy to read while keeping sub-directory files nicely organized.

Follow *The Inception Rule: don’t go more than four levels deep.* That is if you want to keep your sanity. Going beyond this rule will increase unnecessary complexity in your apps UI.

###Manual manifest files or glob-imports
*Manual* manifests are just that, manual management of imported Sass files from sub-directories. This is a good practice to follow when you need specific control over the inheritance of files. Example, rule A needs to come before rule B in the output cascade. 

*Glob-imports* on the other hand is a way for you to simply point to a directory in your manifest, `@import "directory/*";` and Sass will import all the files in alphabetical order. This is great for a directory of mixins or functions that simply need to be loaded in memory for Sass to process the CSS. If you want to use the *glob* function but require a specific order, a naming convention like `_01_mixin.scss` could work as well. 

While *glob-import* is a feature available to Rails projects, this is not a native feature of Sass. If you are not developing a Rails project, [Chris Eppstein](https://github.com/chriseppstein) wrote a [RubyGem](http://goo.gl/ww5Wo) that can be used with either Sass or Compass. 

##Configurable options
An advanced concept of using a Sass structure like this is using a `_config.scss` file to manage the [smart defaults](http://goo.gl/BZOUE) for your UI. Using this technique will help to keep all your UI configurable options easily accessible and manageable, especially when you are using extended Sass libraries like [Zurb's Foundation](http://goo.gl/lgFtD) or [Toadstool w/Stipe](http://goo.gl/PqQSK). 

It is important that there are no CSS rules in the `_config.scss` file. Typically you will include it at the head of a *Sass manifest* file, such as `style.scss`. Depending on how your architecture progresses, there may be times when you need to import your `_config.scss` file again in another module. As long as you keep any CSS rules out of this document, there is nothing wrong with this.

##Element partials
It is in the elemental partials that we get to work. Here we write Sass rules that will create your UI foundational layer. `_buttons.scss`, `_forms.scss`, `_global_design.scss`, `_reset.scss` and `_typography.scss` all contain Sass rules that will process into CSS. While they will __import__ other *partials*, *mixins* and *silent placeholder* rules, it is important to remember that these files are engineered __only to output CSS__. 

Let's take __buttons__ for example. It's amazing that something as simple as buttons have such a complex architecture. Between gradients, `:hover` and `:active` states, one could go a little mad. There are a number of really awesome [Compass Extensions](http://goo.gl/qN4IZ) you can install to help you get started, so in our `_buttons.scss` partial we only write our button styles, like so: 

```scss
button, a.button {
  @inlcude button($button-color);
}
```

Keeping logic out of these elemental partials and writing rules that we know will be processed into CSS is important for readability and scaleability. 

##Custom mixins, placeholder selectors and custom function organization 
Using our button example again, let's say that you need to roll your own from scratch. In the file structure there is a corresponding `buttons/` directory where you will keep your `_mixin.scss`, `_extend.scss` and custom function files. 

Keeping functional Sass separate from presentational Sass is important in order to maintain readability, search-ability and scaleability of your code. Patterns like placing mixins in the same file as presentational Sass leads to overly complex files to scan and not to mention opportunities for accidental pollution of your processed CSS. For example, you have a mixin inside a document that contains presentational Sass, importing the partial will cause your presentational Sass to be __duplicated__. Not to mention that it makes code harder then hell to find.  

##Modules and UI patterns
Now that we have established the architecture for our UI foundation, it is time to start assembling some modules. In essence, modular Sass is an assembly of foundational elements with only enough enough additional presentational Sass to hold it together. Use of elemental styles to build a module are strongly encouraged; while defining new elements in the scope of building a module are strongly discouraged. 

Module Sass is exclusive to a particular interaction of the application. Modules will come in all shapes and sizes, while larger modules may also consist of smaller modules or smaller UI patterns. 

UI patterns are an engineering gray area and are subject to personal interpretation. All I can say here is, that in practice when engineering a module, from one module to the next small UI patterns may begin to emerge. It is practical to try and encapsulate these smaller patterns, but I don't lose sleep over them. 

Module and UI patterns are directories unto themselves. An exploded module directory may look like the following: 

```
sass/
	modules/
		registration/
			_extends.scss
			_functions.scss
			_mixin.scss
			_module_registration.scss
			_module_personalInfo.scss
		purchase/
			_extends.scss
			_functions.scss
			_mixin.scss
			_module_summary.scss
			_module_purchase.scss
```

The idea here is that while engineering modules you may need to create complex UI logic layers that are exclusive to a module. While I strongly encourage making UI logic as abstract as possible and available to the whole app, this process strongly discourages the practice of creating *junk-drawers*.

Keeping these logic files close to the actual use-case helps maintain clean organization of your code. As shown in the example above, a primary module may consist of smaller modules. As a naming convention, I will name the primary module Sass file after the name of the directory, `_module_registration.scss` for example. Any sub-modules in this directory will simply be named by the purpose in which it serves, `_module_personalInfo.scss` for example.

Sub-modules of a UI, in most cases, will contain similar characteristics. This close relationship between a module's logic and it's presentation also serves a code reuse and management purpose. Take for example the use of a *silent placeholder*. In the `extends.scss` file you may engineer a reusable UI module that utilizes several variables. In the corresponding module file you can `@extend` this UI while resetting some of the default variables.   

All modules should be names-spaced by the semantic name of the module itself. `.registration {}` or `.purchase {}` for example. If the sub-module is exclusive to the primary module then it would extend the name like so, `.purahcse_summary {}`. It is important to keep the selectors as shallow as possible in encourage reuse throughout the application without additional engineering. Keep in mind that at the level we are working at, we are simply scoped to a module and modules are not exclusive to any view in the application. 











