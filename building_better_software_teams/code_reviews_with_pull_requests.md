# Code reviews using the pull request workflow

## Code reviews

 * Code reviews and why they're good
 * Visibility
 	* Getting new staff familiar with codebases
 	* People not on project might have suggestions and clear perspective 
 * Knowledge share
 	* Checking it doesn't reinvent the wheel
 	* how a project works, what features it has
 	* from reviewers, improvements to code, solving problems
 * Complying with standards
 * Testing
	 * Checking for presence of tests
	 * Checking test coverage
 * Readability of code (comments not required...)
 * Catching bugs
 	* Code reviews might help reduce bugs, help with support - could be measured depending on organisation
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
 
