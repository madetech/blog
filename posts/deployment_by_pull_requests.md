# Deployment by Pull Requests

At Madetech, we experimented a number of approach to improve our code workflow, [Continuous delivery](/blog/what-is-continuous-delivery) is currently extensively used to bring code closer to our users.
We have now switched to a Pull Request-based (or merge request on Gitlab / Bitbucket terminology) development method on some of our projects and already see the benefits of it.

## How the workflow works

The master branch now becomes a production-ready branch and the only commits on master are coming from Pull Requests.
Instead of everyone pushing directly to master, branches are used for every pull requests.
The pull request branch should be rebased often to the master to make sure that branch is unaffected by the latest code.

## Benefits

### Peer Review

The pull-request based deployment is enabling an easy peer-review of the code. Instead of pushing directly though master, everyone can comment on the changes and ask questions before merging any piece of work. This approach helped to solve numerous misunderstandings during our epics at Made and greatly improved code quality.

Feedback is easier to gather if the Pull Request is small, some efforts are spend to make more concise Pull Requests.

### Better stability

Every individual piece of code added though a Pull Request is tested and validated before being merge into the codebase. The codebase has a better coverage and the stability of the code is greatly improved.

### Sufficient testing

Every time a commit is pushed on the branch, all the continuous integration tests are executed against the codebase. This is ensuring that every piece of code reaching master is usable and production ready.
No pull request is merged without waiting for the build to finish, this ensure that the work being done is corresponding to the project standards in feature/unit tests and code quality.
Having more rigourous testing helps to reduce the work upfront to fix the codebase whenever a problem occurs.

### Reducing conflicts

The pull requests are kept opened just for a small amount of time to get enough reviews and merged as quickly as possible. In order to support this workflow, the pull requests are kept as small as possible on purpose so they can be reviewed easily and merged quicker. Multiple Pull Requests can be opened if the work to be carried is too large to fit into a single one.

This workflow of staying close to master helps to reduce the amount of conflicts and the amount of conflicts. Team members are also affected to smaller tasks which also helps with this problem.

Developers, thanks to peer-review are also increasingly aware of what is happening on the codebase, there is less a need to dig into individual commits since requests to review external come quite often.

### Continuous Delivery

Because the master branch is now much more stable and production-ready, deployment to production can be triggered at any time without any additional effort.
Frequent production deployments are contributing to reduce the friction between the users and the code being produced though quicker development cycles.

### Clearer reponsibility

Each developer is now responsible of the creation of the Pull-Request and address the peer-reviewed feedback directly given on the Pull Request itself. Developers are have a greater sense of code ownership and responsability since they are the only one giving the final green light to merge and deploy their code.

## Conclusion

While this Pull-Request based development also has some disadvantages (mainly slower merging due to the peer-review), we have witnessed a lot of prositive improvements in our projects and plan to slowly roll out this development method to other projects within Made.
