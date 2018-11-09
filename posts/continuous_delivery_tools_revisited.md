# Continuous Delivery Tools Revisited

Since we wrote the original [article](https://www.madetech.com/blog/continuous-delivery-tools) just a little over two years ago, we've seen a fairly big shift away from self-hosted tools to feature rich Software as Service (SaaS). We've also seen nearly all Continuous Integration (CI) tools blur their lines with Continuous Delivery (CD) providing an all-in-one solution.

We'll see who the new players are, what are the new features to look for, and then review the advice we gave regarding choosing self-hosted over SaaS.

## Self-hosted

[GitLab](https://about.gitlab.com/pricing/#self-managed) aims to provide seamless integration between self-hosted and SaaS. With multiple ways to deploy your own CI/CD instance. The added bonus of using GitLab is that you can buy support.

We have used this package microservices as Helm charts (Helm is Kubernetes' package manager) to be deployed to the Kubernetes cluster. And yes we hosted our GitLab in our cluster.

[Jenkins](https://jenkins.io/) is still our goto tool for self-hosting and combined with AWS [CodeBuild](https://aws.amazon.com/codebuild/) can allow you to dynamically scale your workers to meet with sudden demand in builds.

## SaaS

There's been a massive growth in this area with cloud independent solutions such as [Travis CI](https://travis-ci.org/), [Circle CI](https://circleci.com/). On the flip side, Microsoft's Azure Pipeline has strong integration with their cloud offering Azure.

## New Features

### Docker support

Container images have replaced buildpacks as the way to assure consistent versions of software releases. Look for baked in Docker support to reduce the complexity and overhead of your pipeline.

We use docker images as a consistent way to provide [base image](https://hub.docker.com/r/madetech/docker-rails-deps/) for Rails.

### Pipelines/Workflow

This is the heart of continuous delivery and there has been a lot of innovation in this space.

[GitHub](https://github.com/), who traditionally are the first step in building a CD pipeline now provides [GitHub Actions](https://developer.github.com/actions/) which allow pipeline functionality from within your source code repository. It provides a similar "look and feel" to [IFTTT](https://ifttt.com/) allowing build your workflow visually.

Circle CI have turned workflow steps into shareable packages called [Orbs](https://circleci.com/docs/2.0/orb-intro/).

The "deploy anywhere" approach of [Microsoft Azure Pipelines](https://azure.microsoft.com/en-us/services/devops/pipelines/) (part of the Azure DevOps suite) means you can release software to any environment: Kubernetes (Azure Kubernetes Service),  Serverless (Azure Functions) and Web. This is, of course, achievable because of the close integration with their Cloud platform Azure.

Using Azure DevOps suite meant we could commit new features through source control (VSTS) and deploy onto Azure Kubenetes Service (AKS) with relative ease.

Heroku Pipelines' [Review Apps](https://devcenter.heroku.com/articles/github-integration-review-apps) allows us to review Pull Requests in a single-use version of the application.

## Self Hosted or SaaS

To quote from our original article:

> ...if you are maintaining a single product, a SaaS solution will most likely be your best bet, as you won't have to worry about the additional infrastructure. On the flip side of the coin, if you deliver a large number of client projects, a self-hosted solution that can be tailored to your needs will most likely be a better fit.

While the general advice from our original article remains the same, we have extended this advice further to include:

If you are delivering to multiple operating systems (Windows, MacOS and Linux) then SaaS can reduce the complexity of managing an exotic build farm. A common combination used by Rust developers is to use Travis CI for Linux and MacOS and [Appveyor](https://www.appveyor.com/) for Windows when building and packaging software.

The self-hosted route is only feasible if you have a dedicated Ops team, as the chances are that if your CD goes down, your CI will be down too (nearly all self-hosted solution provide CI/CD as an all-in-one package). If both are down then your developers can't release features.

## Summary

So while the landscape has changed in the last two years, the new features we have seen have made building that all-important pipeline ergonomic and no longer the proprietary domain of the Ops team.

Also, the trade-off between self-hosted and SaaS providers remains relatively unchanged. Although perhaps self-hosted has become easier to provision and scale.

The important take away is that continuous delivery is a key component in rapid and frequent software delivery.