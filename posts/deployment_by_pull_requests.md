# Deployments by Pull Requests

At Madetech, we experimented a number of approaches to improve our code workflow, [Continuous delivery](what-is-continuous-delivery) is currently extensively used to bring the code closer to our users.
We are have now been using a Pull Request-based (or merge request on Gitlab / Bitbucket) development method.


## How the workflow works

The master branch instead of reflecting the current progress becomes a production-ready branch and the only commits on master are coming from pull requests.

[...]


## Benefits

### Peer Review

The pull-request based deployment is enabeling an easy peer-review of the code. Instead of pushing directly though master, everyone can comment on the changes and ask questions. This approached helped to solve numerous misunderstandings during our epics.

- Better stability

### Less conflicts

The pull requests are kept opened just for a small amount of time to get enough reviews and merged as soon as possible. In order to support this workflow, the pull requests are kept as small as possible on purpose so they can be reviewed easily and merged quicker.

This workflow of staying quite close to master helps to reduce the amount of conflicts and the amount of conflicts we expecienced was close to none. Generally, team members are affected to different small tasks which also helps with this problem. 

- Ensure everything is tested properly
- Helps coninuous delivery

[...]

