# Code reviews using the pull request workflow

As developers we always appreciate a second pair of eyes and an extra brain. The eyes are really helpful for catching that extra whitespace you might have missed, or the code you had for debugging. The additional brain power might help you solve a problem in your code with 5 fewer lines. All of this results in better code and more collaboration.

A way of formalising code reviews within your organisation can be the pull request workflow, which aims to encourage regular code reviews with minimal disruption to your productivity, while gaining tremendous value.

## Why code review?

### Knowledge share

If you're new to an existing project, what better way to get valuable insight to the workings of it than getting someone familiar to have a look over your changes. It's really difficult to sit and read through the many lines of existing code to fully understand what is available to you to use. They'll have used existing functions a lot more than you, and will help to reduce code duplication, between you there might be a more efficient combination.

The code review encourages the start of conversations that lead to improvement of the overall codebase, sharing of best practices and experience from both the reviewee and reviewer.

It's important that reviews are treated as a positive tool, while it's easy to be defensive of your work there's probably a reason a reviewer is suggesting an alternative. However the reviewee should feel comfortable to start a discussion about suggestions provided, it's a good chance to learn.

Developers shouldn't fear having their code picked over as comments provided should be constructive and it allows to them to gain real insight from their peers. Likewise a reviewer should always feel comfortable providing constructive criticism if they feel it will lead to improvements.

### Visibility

You may not just be a new developer joining an existing project, but in fact a new starter to the organisation. Having frequent code reviews is a great onboarding mechanism to get new starters involved in the process early on, helping them to become familiar with alien codebases.

More often than not, they'll also have new ideas, or other experiences that you can benefit from. Making the code review process as transparent and as open as possible will only encourage this. It also doesn't restrict the conversation to single teams, but the wider organisation can always input too.

### Standards

Code standards aid in readability and maintainability of code. Sometimes standards can come in written form, a large set of rules to follow, but other times they can be unwritten rules that you'll only really learn the more you develop within an organisation.

This is where that extra set of eyes come in. Ensuring that standards are followed don't require much brain power, but they are often easy to miss, especially if you're unfamiliar with them.

Catching these violations early on save time in the long run and allows everyone to be on the same page, ensuring good readability. Also the opportunity to open conversations around the standards themselves. Whitespace vs tabs... _ducks_

### Testing

 * Checking for presence of tests
 * Checking test coverage

### Catching bugs

 * Code reviews might help reduce bugs, help with support - could be measured depending on organisation

### Readability of code (comments not required...)

### Checklists not required?

 * Are checklists required? Tie into Pull Request as a possible alternative to checklists, with automated tools

## Pull request workflow

 * Pull request workflow - how to do well
 * Encourages people to not use master. Code only goes to master via a merge from Github
 	* Lock down master branch on Github, so only merges
 	* Work on seperate features and areas with lower risk of conflicting
 * Breaking down problems into smaller tasks/single responsibility
 	* Smaller amounts of code easier to review
 	* Easier to write/ensure code is tested
 	* Should be shortlived where possible
 		* Set a limit to their lifespan
 		* Less chance of merge conflicts 
 		* Don't be afraid to open issues out of a PR
 * Ensure descriptions for PR's have a brief overview
 	* Allows for understanding the purpose of the review quickly
 		* what you've changed/are trying to acheive 
 * Allows for automated tools to be used code styles, test passes etc.
 	* Lock down PR's to only merge in if tests/linting passes
 	* Intergration tools, on PR submissions, notifications in Slack to everyone
 	* Help prevent blockages in the pipeline, by not developing on master, encourages use of branches
 * Conversations in one place on a hosted tool like Github
 	* Keep these inside your review platform
 		* don't deviate to email/slack/face-to-face if possible
 			* knowledge loss and siloing 
 * Visibility/papertrail (not in sense of blame)
	 * why is the code like this?
	 * what was the aim?
	 * see reasons for design coming from conversation potentially 
 * Always get someone to look over a PR before merging, don't be tempted to self sign your PR's
 	* Let anyone comment on PR's, not just people on the project team
 
