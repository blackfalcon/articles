#Exercises in basic Sass features
Sass is a powerhouse language that is adding new features all the time. For this introduction we will go over the basics of the language and see how they all tie together. We will discuss nesting, parent selector definitions, variables, Sass math, @extends, and @mixins.

##Code comments
Commenting your code is the number one awesome thing any developer can do. In CSS you can place comments in your code `/* */`, but this will appear in the actual CSS and sometimes you don't want or need all that stuff to be there.

In Sass comments are highly encouraged. Sass has what are called 'silent comments' using the `//` syntax. This will allow the developer to comment like crazy and none of this is exposed in the final CSS. An interesting feature is that Sass supports both types of comments.

Scss
```scss
// this is a Sass silent comment. 
// we don't need to show the world all this instructional stuff
// sometimes notes are just for the developers

/* 
This is the primary HTML style
*/ 

html {
    font-size: (12 / 16) * 1em;
}
```

CSS
```css
/* 
This is the primary HTML style
*/
html {
  font-size: 0.75em; }
```

##Nesting your selectors
Let's get into some really meaty Sass concepts. The one feature that stands out quickly with Sass is the ability to nest selectors without having to repeat it's parent selectors.

In the following CSS example, indentation is used for readability and selectors are repeated in order to show nesting. I don't know about you, but this is my biggest issue with vanilla CSS. As we start creating more complex selectors this becomes a real issue. I stated many times, "*I wish there was a way that I could just return + tab and not copy + paste!*" Little did I know, there were others in the world that felt the same way.

CSS
```css
.foo {
  background: orange; }
  .foo p {
    color: blue;
    font-size: 14px;
    font-weight: bold; }
```

Let's take that CSS example, except do what Sass does best, kill unnecessary repetition.

SCSS
```scss
.foo {
  background: orange;
  p {
    color: blue;
    font-size: 14px;
    font-weight: bold;
  }
}
```

Isn't that just cleaner? As you work your way through the UI for the site, this simple feature will pay vast dividends for easy editing and code readability. But be careful and follow the [Inception rule](http://goo.gl/XQrzz) and keep your selectors shallow. It is easy to fall into a trap of mirroring your Sass to your markup structure. I've done it.

##Nested properties
Nesting selectors is nice, but sometimes nesting CSS properties can be a real benefit for managing many of the name spaced properties. Looking at CSS again we see a vary common name spaced property, `font-family`. Learning CSS we are taught to repeat the font- namespace for each property.

CSS
```css
.foo {
  font-family: arial;
  font-weight: bold;
  font-size: 2em; }
```

With Sass we can simply write that property once and then nest the remaining attributes.

SCSS
```scss
.foo {
  font: {
    family: arial;
    weight: bold;
    size: 2em;
  }
}
```

##Redefining the parent selector w/nested selectors
While I agree that nested selectors within Sass are powerful, it wasn't till I understood the power of the & that I realized how powerful it really is. Let's look at a very common CSS use case, using pseudo classes for the hover state. In this example we find ourselves declaring the properties for the a tag, then duplicating that declaration to extend with the pseudo class.

CSS
```css
a {
  color: blue;
  text-decoration: none; }
  a:hover {
    text-decoration: underline; }
```

Using the nesting function of Sass we can extend the parent a tag by simply using the `&` reserved symbol.

SCSS
```scss
a {
  color: blue;
  text-decoration: none;
  &:hover {
    text-decoration: underline;
  }
}
```

Pseudo classes are great, but there are times where when we need to redefine a parent and create an adjoined class selector. Like in this following example.

CSS
```css
.foo {
  background: orange; }
  .foo.block {
    border: 1px solid; }
```

Sass once again rescues us from this unnecessary duplication. Much like the pseudo class example, by nesting the new class and using the `&` with no space between it and the selector we get the results we are looking for.

SCSS
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

CSS
```css
cssgradients .foo {
  background: -webkit-linear-gradient(top, #c9de96 0%, #8ab66b 44%, #398235 100%);
  background: -moz-linear-gradient(top, #c9de96 0%, #8ab66b 44%, #398235 100%);
  background: linear-gradient(top, #c9de96 0%, #8ab66b 44%, #398235 100%); }
.no-cssgradients .foo {
  background: #c9de96; }
```

Using the `&` again with a slight twist we get something I found mind-blowing. By nesting the new selector, adding the & after with a leading space, you are now redefining the parent selector from within the original selector you were styling.

SCSS
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

It should be noted that this function will redefine the parent no matter how many levels deep you go. Playing with the following example we can see how we can take a nested selector, add the `&` and move it to the parent.

SCSS
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

And we get ...

CSS
```css
.foo .awesome .class .amazing .things {
  background: orange; }
  .no-foo .foo .awesome .class .amazing .things {
    background: green; }
```

This Sass technique is invaluable when having to use fallbacks and alternative solutions for different feature support. We can keep all our style declarations under the namespace of the same selector. Code maintenance For The WIN!

##Using variables
Where CSS really fails is it's total lack of reuse. Colors for example are the worst. Not only do we have to use weird things like hexadecimal or HSL values, even RGBa is a little off for me, but we can't reuse them once we declared them.

Sass again comes to the rescue with variables. Let's say that we are defining all the border lines in our CSS. We would write something like the following.

CSS
```css
.box {
  border: 1px solid #ccc;
}
```

This line of CSS gets repeated X number of times in your CSS. Then one day your designer comes up and says that they need to make all the borders `#999`. You now need to go through all the CSS looking for the property of border and change the value from `#ccc` to `#999`. What a pain.

Using Sass we would look at that color as a reusable value and make it a variable like so.

SCSS
```scss
$border-color: #ccc;

.box {
  border: 1px solid $border-color;
}
```

CSS
```css
.box {
  border: 1px solid #cccccc; }
```

Using the variable feature and this technique we have made our lives so much simpler. When we get the color update, we now say, "Sweet!" and simply update the value of the `$border-color` variable and we are done.

##Sass math
Let's face it, sometimes doing math in CSS is hard to keep track of. There are many math functions in Sass, but for this example we will address the issues of calculating ems. Again, Sass to the rescue. Following a popular pattern, we will reset the font size from the default browser size to the size that you want to use on the site.

SCSS
```scss
html {
  font-size: (12 / 16) * 1em;
}
```

CSS
```css
html {
  font-size: 0.75em; }
```

What just happened there? To calculate an em, the formula is to divide the target by it's context, so within the parenthesis we can place the first calculation. To get the final em value we take the result of the first calculation and multiply that by 1em. Sass has the power to recognize this value and return the proper response.  

So you don't use ems, you use percents? Ok, Sass can do that too. Using the same formula, but adjusting the multiplier we get a different return. 

SCSS
```scss
html {
  font-size: (12 / 16) * 100%;
}
```

CSS
```css
html {
  font-size: 75%; }
```

##Extending classes
Any good CSS author will tell you that when you reuse the declaration(s) of another class you 'should' extend the previous class. I say 'should' because many CSS developers do not do this, but why? Simply because with vanilla CSS over time selectors can get a out of hand and it becomes very difficult to see what can be extended. Sass helps with the `@extend` function. We can create a new style rule, extend a previous one and update with new values all without having to update the previous rule.

SCSS
```scss
// Our reusable variables 
$standard-border-color: gray;
$winning-border-color: green;

// Our reusable default presentational class
.user-dialog-box {
  border: 10px solid $standard-border-color;
  padding: 10px;
  box-shadow: 0 0 30px rgba(0,0,0,0.5);
}

// Semantic class used in the DOM
.alert-winning-user {
  @extend .user-dialog-box;
  border-color: $winning-border-color;
}
```

CSS
```css
.user-dialog-box, .alert-winning-user {
  border: 10px solid gray;
  padding: 10px;
  box-shadow: 0 0 30px rgba(0, 0, 0, 0.5); }

.alert-winning-user {
  border-color: green; }
```

With the recent release of Sass 3.2 a new feature, silent classes, was released. For the OOCSS fans in the world this is a great solution for creating reusable standardized presentational classes that can be easily extended in CSS versus the DOM and without all the litter of purely presentational classes in our CSS.    

Using our previous example, we could create a standardized CSS rule for any dialogue box. But by simply replacing the `.` with a `%` Sass will not process this rule as CSS unless it is extended with another selector. 

SCSS
```scss
// Our reusable variables 
$standard-border-color: gray;
$winning-border-color: green;

// Our reusable default silent class
%standard-dialog-box {
  border: 10px solid $standard-border-color;
  padding: 10px;
  box-shadow: 0 0 30px rgba(0,0,0,0.5);
}

// Semantic class used in the DOM
.user-notification {
  @extend %standard-dialog-box;
}

// Semantic class used in the DOM
.alert-winning-user {
  @extend .user-dialog-box;
  border-color: $winning-border-color;
}
```

CSS
```css
.user-notification, .alert-winning-user {
  border: 10px solid gray;
  padding: 10px;
  box-shadow: 0 0 30px rgba(0, 0, 0, 0.5); }

.alert-winning-user {
  border-color: green; }
```
##Mixins
Much like Extends, Mixins are very powerful tools for creating reusable chunks of code to better manage your UI. But unlike Extends, Mixins have the ability to take arguments. Using a combination of the `@mixin` declaration to define the Mixin and then use the `@include` declaration to call the Mixin into a class you can create intelligent reusable code.

There is an important distinction that needs to be made between Extends and Mixins. Unlike an Extend, when a Mixin is evoked, it does not concatenate selectors that share the same rules. A Mixin will insert the rules from the Mixin into the selector written each time it is evoked. 

Let's look at a simple Mixin using our dialog-box example.

SCSS
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

CSS
```css
.alert-winning-user {
  border: 10px solid green;
  padding: 10px;
  box-shadow: 0 0 30px rgba(0, 0, 0, 0.5); }
```

But what if you want to use a Mixin without always having to set that value? When setting the argument variable, using a `:` to delineate, you can add a default value. In the following example, we will update the previous example with a local default value.

SCSS
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

CSS
```css
.alert-winning-user {
  border: 10px solid gray;
  padding: 10px;
  box-shadow: 0 0 30px rgba(0, 0, 0, 0.5); }
```

By setting a default value, we can call in the Mixin into the class without passing in a new value and the default carries through. In order to get the green color we desire, we simply pass in the new value with the Mixin like so, `@include dialog-box(green);` and this will override the default.

The real strength of Mixins is their ability to create really intelligent and reusable chunks of code. Couple this with the ability to pass in variables you can easily customize the output.

##Sass in summary
As you hopefully have seen in this review, Sass has some small hurdles to overcome but the basics are achievable. Starting out with simple concepts like nesting, parent selector definitions and variables will amount to a whole lot of WIN. Then working your way up to Sass math, @extends and @mixins you will soon be a Sass Master.

##The Author, Dale Sande
[Dale Sande](www.dalesande.com) is a Senior UI Engineer at [GettyImages](http://www.gettyimages.com/) in Seattle, WA. Organizer for the Seattle Sass Meetup ([@SassMeetup](https://twitter.com/sassmeetup)) and creator/producer for [SassCast](http://sasscast.tumblr.com/).  Dale prides himself as being the 'bridge' of communication between the designers and developers. Having a career background as a designer, print and web, Dale has successfully transitioned to developer and strives for solutions that reduces friction and increases communication.













































