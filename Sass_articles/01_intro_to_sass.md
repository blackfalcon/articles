#A newb's guide to Syntactically Awesome Stylesheets (Sass)
If you are reading this article, I can assume that you have in one way or another heard of or, through a colleague, have come in contact with Sass. I can also assume that Sass is somewhat of a mystery to you as well. How does it work? Why do some say that it is better then CSS? How can I integrate it into my design/development process? What are the benefits? What problems does it solve? Do I have to be a Rails developer to use Sass? Etc ...

These are all important questions to consider when integrating a new language into your development stack.

##What is Sass?
Sass is a 'pre-processing' language. Meaning that the Sass documents cannot consumed by the browser, but need to be processed into another language that can. Sass is processed into CSS, similar to the way that CoffeeScript is processed into JavaScript.

Sass has two syntaxes, one for foo.sass and one for foo.scss. The original syntax, foo.sass is a white space delimitated syntax that is more lightweight then the standard CSS syntax. A return and soft tab (two spaces) are what separate a selector from it's declaration. Only a colon : is needed to separate a property from it's value. It is the return that separates one declaration from another, unlike the semi-colon ; that is needed in CSS.

Sass
```sass
.block
  background: orange
  border: 1px solid black

.foo
  text-align: center
  Font-size: 1.3em
```

Many users had issue with this lightweight syntax. The main problem is the huge gap between standard CSS syntax and Sass, so converting a whole library of CSS files to Sass was, at times, a mountain of work. Sure, there were syntax converters, but for a long time these were only available in the command line. To some, that is downright unusable.

Seeing this as a real language adoption issue, Sass' core development team decided to introduce the SCSS syntax.

SCSS, or 'Sassy CSS', has all the same features as the Sass syntax and directly supports vanilla CSS. Unlike Sass, SCSS is delimited by, curly brackets `{}`, colons `:` and semi-colons `;`. This is important because now you can simply take any CSS file like `foo.css`,  rename to `foo.scss` and instantly take advantage of the power of Sass without having to reformat your legacy code. To many, this is the official gateway to the language.

SCSS
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

##What is a Gem?
The first problem a newcomer to Sass encounters is that Sass is not a commonly supported language; it needs to be installed. Going to the Sass site, the instructions are to install this thing called a 'Ruby Gem'? A Ruby Gem is a library of code that is needed to perform an operation. This leads us to the second problem, Sass has a dependency on the Ruby language. For some, this can be a real issue. What if you?ve never used Ruby or don?t understand the command line? How can you use Sass without learning all of the developer stuff?

##GUI Sass compilers
If you don't want to bother with the command line process of using Sass, then read this short article about how to set up a GUI Sass compiler. The GUI compilers do the same thing as the command line, but you?ll never have to crack open terminal.

Once, you've got a GUI compiler installed, come back and learn about all the great features that Sass has to offer. You'll be able to follow all the exercises, but you won't have to touch the command line.

If you are comfortable with the command line and want to dive right in, continue on!

##Installing Sass from the command line
Assuming you are on a Mac or Unix flavored machine with Ruby installed and running RVM (typical Ruby development environment configuration), the process is quite simple. Using the command line app, called Terminal, enter the following:

`$ gem install sass`

If you are running a Mac with the Darwin version of Ruby installed and not running RVM, there is a subtle difference.

`$ sudo gem install sass` This command will require you to enter the admin password for that computer.

Macs come preinstalled with Ruby, but Windows does not. In order to get a setup like this going on Windows you may want to look at installing [Ruby for Windows](http://rubyinstaller.org/).

Once the gem is installed, you have all that you need to start processing your Sass.

##Your first processed CSS
Once Sass is installed, it's primary role is to watch for updated Sass files and convert them to CSS.

For this exercise let's create a folder on the desktop and call it sass-test-project. Inside that folder create two new folders, one called sass and the other stylesheets. Inside the Sass folder, let's create a file called style.scss.

Going back to the command line, we need to do a couple of things. First, change directories so that you are inside the projects folder you created. The example would be:

`$ cd Desktop/sass-test-project/`

Then enter the following command to launch the Sass watching application.

`sass --watch sass:stylesheets`

What is this command doing? `sass --watch` is the base command, there isn't anything to alter here. But the second part `sass:stylesheets`, these are the folders we just set up. Using this format, Sass will watch for any .scss file in the sass folder, process and create a new CSS file in the stylesheets folder.

And that's it. Open your text editor, open the style.scss file and add a selector with some declarations like you would any other CSS file. Then save the edits. When you are done, go back into the projects folder, open the 'Stylesheets' folder and there will be style.css waiting for you with the newly processed SCSS into CSS.

Looking back at the command line application, you should see something like the following:

```
>>> Change detected to: /Users/[you]/Desktop/sass-test-project/sass/style.scss
  overwrite stylesheets/style.css
>>> Change detected to: sass/style.scss
```

It is important to understand what just happened here. Every time `sass --watch` is executed, Sass will destroy and overwrite the CSS file. If someone were to edit the CSS file without making the same edits to the Sass file, upon next compile all edits on the CSS file will be lost. The Sass files should be the single source of record for any CSS from here on out.

##Error reporting
Looking back at the command line, not only is this great to see a log of updated files, but this is where you will see error reporting if there is a bug in your code. But don't worry, you don't have to keep a close watch on the command line, errors will also appear in your browser at the top of the view.

Sass' error reporting isn't all about alerting you that you did it wrong, it's very informative as well. The report will tell you the file that has the error, the line number and hint as to what was incorrect.

Errors aren't just on the surface either. As you get into a more complicated Sass file structure, the error reports the full stack trace so that you can dig deep into the issue.

##Sass is NOT a Rails only tool
While there is a dependency on Ruby, in our first exercise we processed a SCSS file to CSS on our desktop. Be it Rails, PHP or .NET, there is no dependency on a development framework to use Sass.

##In summary
As you hopefully have seen in this exercise, gettingSass installed has a few small hurdles to overcome but it is achievable. Either by using the command line or a GUI desktop app, getting Sass installed and processing your first CSS is an exciting experience. In our followup article, Exercises in basic Sass features, we will cover the essential features that makes Sass such an exciting alternative to vanilla CSS.

##The Author, Dale Sande
[Dale Sande](www.dalesande.com) is a Senior UI Engineer at [GettyImages](http://www.gettyimages.com/) in Seattle, WA. Organizer for the Seattle Sass Meetup ([@SassMeetup](https://twitter.com/sassmeetup)) and creator/producer for [SassCast](http://sasscast.tumblr.com/).  Dale prides himself as being the 'bridge' of communication between the designers and developers. Having a career background as a designer, print and web, Dale has successfully transitioned to developer and strives for solutions that reduces friction and increases communication.