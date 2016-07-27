# Deployment by pull requests

At MadeTech, we experimented a number of approach to improve our code workflow, [Continuous delivery](/blog/what-is-continuous-delivery) is currently extensively used to bring code closer to our users.
We have now switched to a pull request-based (or merge request on Gitlab / Bitbucket terminology) development method on some of our projects and already see the benefits of it.

## How the workflow works

The master branch now becomes a production-ready branch and the only commits on master come from pull requests.
Instead of everyone pushing directly to master, branches are used for every pull request.
The pull request branch should be rebased often against master to make sure that branch remains unaffected by merge conflicts and breaking changes.

## Benefits

### Peer Review

The pull request based deployment enables easy peer-review of the code. Instead of pushing directly through master, everyone can comment on the changes and ask questions before merging any piece of work. This approach helped to solve numerous misunderstandings during our epics at Made and greatly improved code quality.

Feedback is easier to gather if the pull request is small, so some effort should be spent to make more concise pull requests.

### Sufficient testing and better stability

Every time a commit is pushed to the branch, all the continuous integration tests are executed against the codebase. This ensures that every piece of code reaching master is usable and production ready. The master branch, instead of being continuously broken on every commit can now be used locally to insure that the changes made are valid. 
No pull request is merged without waiting for the build to finish, which verifies that the work being done is corresponding to the project standards in feature/unit tests and code quality. The codebase has a better coverage and the stability of the code is greatly improved.
Having more rigourous testing helps to reduce the work upfront to fix the codebase whenever a problem occurs.

### Reducing conflicts

The pull requests are kept opened just for a small amount of time to get enough reviews and merged as quickly as possible. In order to support this workflow, the pull requests are kept as small as possible on purpose so they can be reviewed easily and merged quicker. Multiple pull requests can be opened if the work to be carried is too large to fit into a single one.

This workflow of staying close to master helps to reduce the amount of conflicts. Team members are also affected to smaller, individual tasks which also helps with this problem.

Developers, thanks to peer-review, are also increasingly aware of what is happening on the codebase, which means there is less of a need to dig into individual commits since requests for external review come quite often.

### Continuous Delivery

Because the master branch is now much more stable and production-ready, deployment to production can be triggered at any time without any additional effort.
Frequent production deployments are contributing to reduce the friction between the users and the code being produced though quicker development cycles.

### Clearer reponsibility

Each developer is now responsible of the creation of the pull request and can address the peer-reviewed feedback directly given on the pull request itself. Developers are have a greater sense of code ownership and responsability since they are the only one giving the final green light to merge and deploy their code.

## Conclusion

While this pull request based development also has some disadvantages (mainly slower merging due to the peer-review), we have witnessed a lot of positive improvements in our projects and plan to slowly roll out this development method to other projects within Made.
