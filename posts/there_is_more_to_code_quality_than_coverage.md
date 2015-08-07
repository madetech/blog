#There is more to code quality than coverage

As developers we always strive to write the best code possible. And while we test for it, coverage doesn’t always tell the full story of the quality of your code output.

Previously we’ve shown you our [complete deployment pipeline](https://www.madetech.com/news/continuous-delivery-with-jenkins). In this article I am going to talk about the current tooling we use during the first step of our deployment pipeline - the build step - to keep our code at a consistently high standard.

The majority of our code quality testing happens before any unit, or feature tests are run. The exception being to this being security testing. The reason being that you don’t want to be waste a build slave running "bad code”.

The areas we focus in on can be broadly separated into three areas; Complexity, Style, and Security.

###Complexity?
More specifically the complexity of Assignments, Branches and Conditionals (ABC) within a method. This metric can quickly identify potential “code smell” and overly complex methods. The ABC metric of a method is calculate by evaluating the number of variable assignments, calls to other methods or classes, and number of conditionals within said method. Our build gets failed if any method exceeds the industry standard score of 15. More in-depth explanation of the ABC metric can be found in this [article](http://www.softwarerenovation.com/ABCMetric.pdf)

###Style
Language style guides aren’t anything new, but the enforcement of a consistent code style within the team aids readability, and understanding. We run style analysis on both our Ruby and SCSS files, and fail the build for anything deemed a serious violation. For example, missing spaces around a brace will fail the build, while an unnecessary double quote will just get you a warning.

###Security
Writing secure code has to be a top priority, so identifying any potential vulnerabilities in your codebase as early as possible is a must. The vulnerabilities you should be looking are Remote code execution, cross site scripting, SQL injection, and string formating. We run this analysis on a build thats successfully passed all unit and feature test, the thinking being that this [build] is code could reach production.

To test these areas we use [at time of writing] the following gems:

- **Tailor** - Style analysis tool for Ruby, that like its peers is configurable based on the [Ruby community style guide](https://github.com/bbatsov/ruby-style-guide).
- **Cane** - Code analysis tool for Ruby that enforces the ABC metric, and some basic styles like line length, trailing whitespace, and new line at the end of a file.
- **SCSS-Lint** - Style analysis for SCSS, which like Tailor can be configured to your SCSS
- **Brakeman** - A vulnerability scanner for Ruby on Rails that will find security issues. The vulnerabilities it identifies are shown [here](http://brakemanscanner.org/docs/warning_types/) which is quite comprehensive.

Additionally all of these tools all come bundled with Rake tasks, so we can switch them in or out at will, which enables our code analysis to be flexible from project to project. So we can always evolve our code quality testing.

###Looking forward

A code analysis tool that I’d like to implement is Rubocop. Rubocop would effectively replace Tailor and Cane in our current set up as it provides an ABC metric, and style analysis. It can even rectify some issues automatically for you, which would be great, because there is nothing more annoying than a failed build because of a missing new line!

####Links
- Tailor - https://github.com/turboladen/tailor
- Cane - https://github.com/square/cane
- SCSS-Lint - https://github.com/brigade/scss-lint
- Brakeman - http://brakemanscanner.org/
- Rubocop - https://github.com/bbatsov/rubocop
