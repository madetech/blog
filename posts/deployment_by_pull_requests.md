# Deployments by Pull Requests

At Madetech, we experimented a number of approaches to improve our code workflow, [Continuous delivery](what-is-continuous-delivery) is currently extensively used to bring the code quicker to our users.
We are have now been using a Pull Request-based (or merge request on Gitlab / Bitbucket) development method.


## How the workflow works

The master branch now becomes a production-ready branch and the only commits on master are coming from pull requests.
Instead of everyone pushing directly to master, branches are used for every pull requests.
The pull request branch should be rebased often to the master to make sure that branch is unaffected by the latest code.

## Benefits

### Peer Review

The pull-request based deployment is enabeling an easy peer-review of the code. Instead of pushing directly though master, everyone can comment on the changes and ask questions before merging any piece of work. This approach helped to solve numerous misunderstandings during our epics at Made and greatly improved code quality.

The feedback is easier to create if the Pull Request is small so a some efforts is spend to make more concise Pull Requests.

### Better stability

### Less conflicts

The pull requests are kept opened just for a small amount of time to get enough reviews and merged as soon as possible. In order to support this workflow, the pull requests are kept as small as possible on purpose so they can be reviewed easily and merged quicker.

This workflow of staying quite close to master helps to reduce the amount of conflicts and the amount of conflicts we expecienced was close to none. Generally, team members are affected to different small tasks which also helps with this problem. 

### Ensure everything is tested properly

Every time a commit is pushed on the branch, all the continuous integration tests are ran against the codebase. This is ensuring that every piece of code reaching master is usable and production ready.
No pull request is merged without waiting for the build to finish, this ensure that the work being done is coresponding to the project standards in feature/unit tests and code quality.
Having more rigourous testing helps to reduce the work upfront to fix the codebase 

### Helps coninuous delivery

[...]

## Conclusion

