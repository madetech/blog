# Code reviews using the pull request workflow

## Code reviews

 * Code reviews and why they're good
 * Visibility
 * Knowledge share, how a project works, what features it has
 * Knowledge share, from reviewers, improvements to code, solving problems
 * Complying with standards
 * Catching bugs
 * Checking for presence of tests
 * Checking test coverage
 * Checking it doesn't reinvent the wheel
 * Readability of code (comments not required...)
 * Code reviews might help reduce bugs, help with support - could be measured depending on organisation
 * Are checklists required? Tie into Pull Request as a possible alternative to checklists, with automated tools

## Pull request workflow

 * Pull request workflow - how to do well
 * Breaking down problems into smaller tasks/single responsibility
 * Ensure descriptions for PR's have a brief overview
 * Allows for automated tools to be used code styles, test passes etc.
 * Conversations in one place on a hosted tool like Github
 * Visibility/papertrail (not in sense of blame)
 * Always get someone to look over a PR before merging, don't be tempted to self sign your PR's
 * Intergration tools, on PR submissions, notifications in Slack to everyone
 * Let anyone comment on PR's, not just people on the project team
 * Help prevent blockages in the pipeline, by not developing on master, encourages use of branches
 * Encourages people to not use master. Code only goes to master via a merge from Github
 * Lock down master branch on Github, so only merges
 * Lock down PR's to only merge in if tests/linting passes
