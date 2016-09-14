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

While a reviewer is normally checking over implementation code, a review offers the opportunity to ensure good practices have been followed while developing code, for example Test Driven Development (TDD). It's important to make sure tests are present as part of a review if this is a practice your organisation adheres to.

Tests, hopefully, allow the reviewer to follow the design of the implementation while also opening up another area for improvement. Reviews are a great way to ensure that the test provided are valuable and efficient. An important question to ask here; do the tests cover all the changes?

### Catching bugs

Having another developer look over your work also provides an opportunity to catch any bugs you may not have noticed. While you might have a wonderful green test suite a peer might be aware of another edgecase within the project that would otherwise has slipped by.

### Readability of code (comments not required...)

At Made we feel that if code isn't understandable without comments then this represents a smell. While it's common to see this crop up as a suggestion is it really required if your functions and variables are clearly and consistenly named throughout and have obvious and sensible data returned. Comments _can_ provide value in some cases but they should never be a hard requirement for a code review for us.

### Checklists not required?

While some of the above may look like a checklist it's not. We're more trying to present some best practices for code reviews, not rules that you have to follow. 

We'll dive deeper into this idea as we expand on the value we derive from having adopted a Pull Request Workflow. Some of the things we've covered above can be easily automated to make code reviewing more valuable as a result of this.

## Pull request workflow

Pull Requests (PRs) allow for a standard and efficient way of doing code reviews within an organisation. Most popular tools these days, such as Github or Bitbucket offer features that allow for easy adoption of the pull request workflow.

### Adopting the flow

PRs revolve around the idea of using dedicated branches for small feature sets. The branches of work are then submitted to your source control tool (we'll use Github from here on in our examples), and are opened up for review amongst your team. Only when the majority of people involved are happy with the work, will it then be merged into your master branch.

#### Branches
Working in isolated branches reduces the risk of conflicting with other developer's work. By not working in master, you can remain focused on your goal rather than constantly having to pull in others code.

#### Single Responsibility Pull Requests
The core idea behind this area is that the less code there is to review the more valuable the review will most likely be. Small features covering only a single area allow for a hyper-focused review and clear understanding of what's trying to be achieved. 

A reviewer can easily tell if the tests are present, valuable and covering these small chunks. Working in this style makes it easier for the reviewee themselves to write the tests and feature.

#### Short lifespans
A great way to avoid merge conflicts with other features and stale code is to impose a completely artificial lifespan on a PR. Whether it's a day or just 15 minutes making sure these don't hang around in limbo is an efficient way to maintain momentum on a project.

If more work arrises out of a review don't just stop the conversation, move it out to an issue or issues and assuming everything has been signed off merge the PR. This allows for more time to be spent on the conversation and potentially more opinions to be provided and more thought around the area.

#### Sign off
While it can be tempting to review your own work if others are busy **don't**

* Always get someone to look over a PR before merging, don't be tempted to self sign your PR's
 	* Let anyone comment on PR's, not just people on the project team

 * Tooling/Allows for automated tools to be used code styles, test passes etc.
 	* Lock down PR's to only merge in if tests/linting passes
 	* Lock down master branch on Github, so only merges
 	* Intergration tools, on PR submissions, notifications in Slack to everyone
 	* Help prevent blockages in the pipeline, by not developing on master, encourages use of branches
 	* Ensure descriptions for PR's have a brief overview
 		* Allows for understanding the purpose of the review quickly
 		* what you've changed/are trying to acheive 
 	* Conversations in one place on a hosted tool like Github
 		* Keep these inside your review platform
 			* don't deviate to email/slack/face-to-face if possible
 				* knowledge loss and siloing 
 * Visibility/papertrail (not in sense of blame)
	 * why is the code like this?
	 * what was the aim?
	 * see reasons for design coming from conversation potentially 
  
