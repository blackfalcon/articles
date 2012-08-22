#A newb's guide to Syntactically Awesome Stylesheets (Sass)

If you are reading this article then I can assume that you have in one way or another heard of or have come in contact with Sass. But I can also assume that Sass is somewhat of a mystery to you as well. How does it work? Why do some say that it is better then CSS? How can I integrate it into my design/development process? What are the benefits? What problems does it solve? Do I have to be a Rails developer to use Sass? Etc ...

These are all important questions to consider when integrating a new language into your development stack.

##What is Sass?
Sass is a 'pre-processing' language. Meaning that the Sass documents will never be consumed by the client, but needs to be processed into another language that can be consumed by the client, Sass needs to be processed into CSS. Much like another language you may have heard of, coffee script. Where again, coffee script needs to be processed into JavaScript before being consumed by the client. 

Sass has two syntaxes, one for `foo.sass` and one for `foo.scss`. The original syntax, `foo.sass` is a white space delimitated syntax that is more lightweight then the standard CSS syntax. A return and soft tab (two spaces) are what separate a selector from it's declaration and only a colon ` : ` is needed to separate a property from it's value. It is the return that separates one decloration from another, unlike the semi-colon ` ; ` that is needed in CSS. 

*Sass*
```sass
.block
  background: orange
  border: 1px solid black

.foo
  text-align: center
  Font-size: 1.3em
```

A growing number of users that had issue with this lightweight syntax. The main issue was that there is such a huge gap between standard CSS and Sass, so converting a library of CSS files to Sass was at times a mountain of work. Sure there were syntax converters, but for a long time these were only available in the command line. To some, that is downright unusable. 

Seeing this as a real language adoption issue, Sass' core development team decided to introduce the SCSS syntax. 

SCSS, or Sassy CSS, has all the same features as the Sass syntax and directly supports vanilla CSS syntax. Unlike Sass, SCSS is deliminated by, curley brackets ` {} `, colons ` : ` and semi-colons ` ; `. This is important because now you can simply take any CSS file like `foo.css` and update to `foo.scss` and insatiately take advantage of the power of Sass without having to reformat your legacy code. To many, this was the official gateway to the language. 

*SCSS*
```scss
.block {
  background: orange;
  border: 1px solid black;
}

.foo {
  text-align: center;
  Font-size: 1.3em;
}
```

Many of the examples you will see on other sites tend to favor the SCSS syntax and it is quickly becoming the default syntax for Sass as a whole. 

###What is a Gem?
The first problem that a newcomer to Sass typically has is that Sass is not a commonly supported language, you need to install it. Going to the Sass site, the instructions are to install this thing called a 'Ruby Gem'? A Ruby Gem is a library of code that is needed to perform an operation. This leads us to the second problem, Sass has a dependency on the Ruby language. For some, this can be a real issue.  

The good news is that many other really smart and passionate Sass users also recognized this. As a result there are a handful of alternate Sass installation solutions that I am sure at least one will get you up and running. 

* [Scout](http://goo.gl/a2lI5) - Mac/Windows
* [Compass.app](http://goo.gl/A8Rd6) - Mac/Windows/Linux
* [CodeKit](http://goo.gl/mNz46) - Mac(Lion+)
* [LiveReload](http://goo.gl/9Gx6D) - Mac/Windows(pre-alpha)/Linux(limited) 

###Installing Sass from the command line
For the purpose of this article, we are going to discuss the prescribed install from the Sass site. If you are choosing to use one of the GUI apps, please refer to **Your first processed CSS**.

Assuming you are on a Mac or Unix flavored machine with Ruby installed and running RVM (typical Ruby development environment configuration), the process is quite simple. Using the command line app, called Terminal, enter the following:

`$ gem install sass`

If you are running a Mac with the Darwin version of Ruby installed and not running RVM, there is a subtle difference. 

`$ sudo gem install sass` This command will require you to enter the admin password for that computer. 

Macs come preinstalled with Ruby, but Windows does not. In order to get a setup like this going on Windows you may want to look at installing [Ruby for Windows](http://rubyinstaller.org/).

Once the gem is installed, you have all that you need to start processing your CSS. 

###Your first processed CSS 
Once Sass is installed, it's primary role is to watch for updated Sass files and convert them to CSS. 

On your computer, anywhere really, let's create a new project folder. For this exercise let's create a folder on the desktop and call it `sass-test-project`. Inside that folder create two new folders, one called `sass` and the other `stylesheets`. Inside the Sass folder, let's create a file called `style.scss`. 

Going back to the command line, we need to do a couple of things. First, change directories so that you are inside the projects folder you created. The example would be:

`$ cd Desktop/sass-test-project/`

Then enter the following command to launch the Sass watching application. 

`sass --watch sass:stylesheets`

What is this command doing? `sass --watch` is the base command, there isn't anything to alter here. But the seocnd part `sass:stylesheets`, these are the folders we just set up. Using this format, Sass will watch for any `.scss` file in the `sass` folder, process and create a new CSS file in the `stylesheets` folder. 

And that's it. Open your text editor, open the `style.scss` file and add a selector with some declarations like you would any other CSS file. Then save the edits. When you are done, go back into the projects folder, open the 'Stylesheets' folder and there will be `style.css` waiting for you with the newly process SCSS into CSS. 

Looking back at the command line application, you should see something like the following:

```
>>> Change detected to: /Users/[you]/Desktop/sass-test-project/sass/style.scss
  overwrite stylesheets/style.css
>>> Change detected to: sass/style.scss
```

It is important to understand what just happened here. Every time `sass --watch` is executed, Sass will destroy and overwrite the CSS file. If someone were to edit the CSS file without making the same edits to the SCSS file, upon next compile all edits on the CSS file will be lost. The Sass files should be the single source of record for any CSS from here on out. 

###Error reporting
Looking back at the command line, not only is this great to see a log of updated files, but this is where you will see error reporting if there is a bug in your code. But don't worry, you don't have to keep a close watch on the command line, errors will also appear in your browser at the top of the view. 

Sass' error reporting isn't all about alerting you that you did it wrong, it's very informative as well. The report will tell you the file that has the error, the line number and hint as to what was incorrect. 

Errors aren't just on the surface either. As you get into a more complicated Sass file structure, the error reports the full stack trace so that you can dig deep into the issue. 

###Sass is NOT a Rails only tool
While there is a dependency on Ruby, in our first exercise we processed a SCSS file to CSS on our desktop. Be it Rails, PHP or .NET, there is no dependency on a development framework to use Sass.

##Exercises in basic Sass features
Sass is a powerhouse language that is adding new features all the time. For this introduction we will go over the basics of the language and see how they all tie together. We will discuss nesting, parent selector definitions, variables, Sass math, @extends, and @mixins. 

###Code comments
Commenting your code is the number one awesome thing any developer can do. In CSS you can place comments in your code `/* */`, but this will appear in the actual CSS and sometimes you don't want or need all that stuff to be there. 

In Sass comments are highly encouraged. Sass has what are called 'silent comments' using the `//` syntax. This will allow the developer to comment like crazy and none of this is exposed in the final CSS. An interesting feature is that Sass supports both types of comments. 

*SCSS*
```scss
// this is a Sass silent comment. 
// we don't need to show the world all this instructional stuff
// sometimes notes are just for the devlopers

/* 
This is the primary HTML style
*/ 

html {
	font-size: (12 / 16) * 1em;
}
```

*CSS*
```css
/* 
This is the primary HTML style
*/
html {
  font-size: 0.75em; }
```

###Nesting your selectors 
Let's get into some really meaty Sass concepts. The one feature that stands out quickly with Sass is the ability to nest selectors without having to repeat it's parent selectors.

In the following CSS example, indentation is used for readability and selectors are repeated in order to show nesting. I don't know about you, but this is my biggest issue with vanilla CSS. As we start creating more complex selectors this becomes a real issue. I stated many times, "*I wish there was a way that I could just return + tab and not copy + paste!*" Little did I know, there were others in the world that felt the same way.

*CSS*
```CSS
.foo {
  background: orange; }
  .foo P {
    color: blue;
    font-size: 14px;
    font-weight: bold; }
```

Let's take that CSS example, except do what Sass does best, kill unnecessary repetition. 

*SCSS*
```scss
.foo {
  background: orange;
  P {
    color: blue;
    font-size: 14px;
    font-weight: bold;
  }
}
```

Isn't that just cleaner? As you work your way through the UI for the site, this simple feature will pay vast dividends for easy editing and code readability. But be careful and follow the [Inception rule](http://goo.gl/XQrzz) and keep your selectors shallow. It is easy to fall into a trap of mirroring your Sass to your markup structure. I've done it. 

###Nested properties
Nesting selectors is nice, but sometimes nesting CSS properties can be a real benefit for managing many of the name spaced properties. Looking at CSS again we see a vary common name spaced property, `font-family`. Learing CSS we are taught to repeat the `font-` namespace for each property. 

*CSS*
```css
.foo {
  font-family: arial;
  font-weight: bold;
  font-size: 2em; }
```

With Sass we can simply write that property once and then nest the remaining attributes.

*SCSS*
```scss
.foo {
  font: {
    family: arial;
    weight: bold;
    size: 2em;
  }
}
```

###Redefining the parent selector w/nested selectors
While I agree that nested selectors within Sass are powerful, it wasn't till I understood the power of the `&` that I realized how powerful it really is. Let's look at a very common CSS use case, using psudo clases for the hover state. In this common CSS example, we find ourselves declaring the properties for the `a` tag, then duplicating that declaration to extend with the psudo class. 

*CSS*
```css
a {
  color: blue;
  text-decoration: none; }
  a:hover {
    text-decoration: underline; }

```

Using the nesting function of Sass we can extend the parent `a` tag by simply using the `&` reserved symbol.  

*SCSS*
```scss
a {
  color: blue;
  text-decoration: none;
  &:hover {
    text-decoration: underline;
  }
} 
```

Psudo classes are great, but there are times where when we need to redefine a partent and create an adjoined class selector. Like in this following example. 

*CSS*
```css
.foo {
  background: orange; }
  .foo.block {
    border: 1px solid; }
```

Sass once again rescues us from this unnecessary duplication. Much like the psudo class example, by nesting the new class and using the `&` with no space between it and the selector we get the results we are lookig for. 

*SCSS*
```scss
.foo {
  background: orange;
  &.block {
    border: 1px solid;
  }
}
```

Adjoining selectors and pseudo classes is pretty cool, but for some who leverage tools like [Modernizer](http://goo.gl/qMf19), there are times when you need to redefine which selector is actually the parent in order to address a UI based on a selector higher up in the DOM. 

Let's say for example you are working on a CSS3 property that is not supported by all browsers, like our old friend css gradients. Using CSS we will need declare our first property then duplicate the selector prefixing with the new parent we need to declare. 

*CSS*
```css
.cssgradients .foo {
  background: -webkit-linear-gradient(top, #c9de96 0%, #8ab66b 44%, #398235 100%);
  background: -moz-linear-gradient(top, #c9de96 0%, #8ab66b 44%, #398235 100%);
  background: linear-gradient(top, #c9de96 0%, #8ab66b 44%, #398235 100%); }
.no-cssgradients .foo {
  background: #c9de96; }
```

Using the `&` again with a slight twist we get something I found mind-blowing. By nesting the new selector, adding the `&` after with a leading space, you are now redefining the parent selector from witin the original selector you were styling. 

*SCSS*
```scss
.foo {
  .cssgradients & {
    background: -webkit-linear-gradient(top, #c9de96 0%,#8ab66b 44%,#398235 100%);
    background: -moz-linear-gradient(top, #c9de96 0%,#8ab66b 44%,#398235 100%);
    background: linear-gradient(top, #c9de96 0%,#8ab66b 44%,#398235 100%);
  }
  .no-cssgradients & {
    background: #c9de96;
  }
}
```

It should be noted that this function will redefne the parent no matter how many levels deep you go. Playing with the follwing example we can see how we can take a nested selector, add the `&` and move it to the parent. 

*SCSS*
```scss
.foo {
  awesome {
    .class {
      .amazing {
        .things {
          background: orange;
          .no-foo & {
            background: green;
          }
        }
      }
    }
  }
}
```

And we get  ...

*CSS*
```css
.foo .awesome .class .amazing .things {
  background: orange; }
  .no-foo .foo .awesome .class .amazing .things {
    background: green; }
```

This Sass technique is invaluable when having to use fallbacks and alternative solutions for different feature support. We can keep all our style declorations under the namespace of the same selector. Code maintenance For The WIN!

###Using variables 
Where CSS really fails is it's total lack of reuse. Colors for example are the worst. Not only do we have to use weird things like hexadecimal or HSL values, even RGBa is a little off for me, but we can't reuse them once we declared them. 

Sass again comes to the rescue with variables. Let's say that we are defining all the border lines in our CSS. We would write something like the following.

*CSS*
```css
.box {
  border: 1px solid #ccc;
}
```

This line of CSS gets repeated X number of times in your CSS. Then one day your designer comes up and says that they need to make all the borders `#999`. You now need to go through all the CSS looking for the property of `border` and change the value from `#ccc` to `#999`. What a pain. 

Once again, Sass to the rescue. Using Sass we would look at that color as a resuable value and make it a variable like so. 

*SCSS*
```scss
$border-color: #ccc;

.box {
  border: 1px solid $border-color;
}
```

*CSS*
```css
.box {
  border: 1px solid #cccccc; }
```

Using the variable feature and this technique we have made our lives to much simpler. When we get the update, we now say, "Sweet!" and simply update the value of the `$border-color` and we are done.

###Sass math
Let's face it, sometimes doing math in CSS is hard to kepe track of. There are many math functions in Sass, but for this example we will address the issues of calculating ems. Again, Sass to the rescue. Following a populare pattern, we will reset the font size from the default browser size to the size that you want to use on the site. 

*SCSS*
```scss
html {
  font-size: (12 / 16) * 1em;
}
```

*CSS*
```css
html {
  font-size: 0.75em; }
```

What? You don't use ems, you use percents? Ok, Sass can do that too. 

*SCSS*
```scss
html {
  font-size: (12 / 16) * 100%;
}
```

*CSS*
```css
html {
  font-size: 75%; }
```

###Extending classes
Any good CSS author will tell you that when you reuse the declaration(s) of another class you 'should' extend the previous class. I say 'should' because many CSS developers do not do this, but why? Simply because with vanilla CSS over time selectors can get a out of hand and it becomes very difficult to see what can be extended. Sass helps with the `@extend` function. We can create a new style rule, extend a previous one and update with new values all without having to update the previous rule. 

For the OOCSS fans in the world this is a great solution for creating reusable standardized presentational classes that can be easily extended in CSS versus the DOM. 


*SCSS*
```scss
// Our reusable variables 
$standard-border-color: gray;
$winning-border-color: green;

// Our reusable default presentational class
.dialog-box {
  border: 10px solid $standard-border-color;
  padding: 10px;
  box-shadow: 0 0 30px rgba(0,0,0,0.5);
}

// Semantic class used in the DOM
.alert-winning-user {
  @extend .dialog-box;
  border-color: $winning-border-color;
}
```

*CSS*
```css
.dialog-box, .alert-winning-user {
  border: 10px solid gray;
  padding: 10px;
  box-shadow: 0 0 30px rgba(0, 0, 0, 0.5); }

.alert-winning-user {
  border-color: green; }
```

###Mixins
Much like Extends, Mixins are very powerful tools for creataing reusable chuncks of code to better manage your UI. But unlike Extends, Mixins have the ability to take arguments. Using a combination of the `@mixin` declaration to define the mixin and then use the `@include` declaration to call the mixin into a class you can create intelligent resuable code.

Let's look at a simple mixin using our dialog-box example.

*SCSS*
```scss
@mixin dialog-box($border-color) {
  border: 10px solid $border-color;
  padding: 10px;
  box-shadow: 0 0 30px rgba(0,0,0,0.5);
}

.alert-winning-user {
  @include dialog-box(green);
}
```

*CSS*
```css
.alert-winning-user {
  border: 10px solid green;
  padding: 10px;
  box-shadow: 0 0 30px rgba(0, 0, 0, 0.5); }
```

But what if you want to use a mixin without always having to set that value? When setting the argument variable, using a ` : ` to delinate, you can add a default value. In the following example, we will update the previous example with a local default value.  

*SCSS*
```scss
@mixin dialog-box($border-color: gray) {
  border: 10px solid $border-color;
  padding: 10px;
  box-shadow: 0 0 30px rgba(0,0,0,0.5);
}

.alert-winning-user {
  @include dialog-box;
}
```

*CSS*
```css
.alert-winning-user {
  border: 10px solid gray;
  padding: 10px;
  box-shadow: 0 0 30px rgba(0, 0, 0, 0.5); }
```

By setting a default value, we can call in the mixin into the class without passing in a new value and the default carries through. In order to get the green color we desire in this example, we simply pass in the new value with the mixin like so, `@include dialog-box(green);` and this will override the default. 

The real strength of mixins is their ability to create really intelligent and reusable chunks of code. Couple this with the ability to pass in variables you can easily customize the output.  

##Sass in summary
As you hopefully have seen in this review, Sass has some small hurdles to overcome but the basics are achievable. Starting out with simple concepts like nesting, parent selector definitions and variables will amount to a whole lot of WIN. Then working your way up to Sass math, @extends and @mixins you will soon be a Sass Master. 

##The Author, Dale Sande
[Dale Sande](www.dalesande.com) is a Senior UI Engeinner at [Getty Images](http://www.gettyimages.com/) in Seattle, WA. Dale prides himself as being the 'bridge' of communication between the designers and developers. Having a career background as a designer, print and web, Dale has successfuly transitioned to developer and strives for solutions that reduces friction and increases communication. 









