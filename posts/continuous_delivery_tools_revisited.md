# Continuous Delivery Tools Revisited

Since we wrote the original [article](https://www.madetech.com/blog/continuous-delivery-tools) just a little over two years ago, we've seen a fairly big shift away from self-hosted tools to feature rich Software as Service (SaaS). We've also seen nearly all Continuous Integration (CI) tools blur their lines with Continuous Delivery (CD) providing an all-in-one solution.

We'll see who are the new players, what are the new features to look for, and then review the advice we gave regarding choosing self-hosted over SaaS.

## Self-hosted

[GitLab](https://about.gitlab.com/pricing/#self-managed) aims to provide seamless integration between self-hosted and SaaS. With multiple ways to deploy your own CI/CD instance. The added bonus of using GitLab is that you can buy support.

## SaaS

There's been a massive growth in this area with cloud independent solutions such as [Travis CI](https://travis-ci.org/), [Circle CI](https://circleci.com/). At the same time, Microsoft's Azure Pipeline strong integration with their cloud offering.

## New Features

### Docker support

Container images have replaced buildpacks as the way to assure consistent versions of software releases. Look for baked in Docker support, to reduce the complexity and overhead of your pipeline.

### Pipelines/Workflow

This is the heart of continuous delivery and there has been a lot of innovation in this space.

[GitHub](https://github.com/) who traditionally are the first step in building a CD pipeline now provides [GitHub Actions](https://developer.github.com/actions/) which allow pipeline functionality from within your source code repository. It provides a similar "look and feel" to [IFTTT](https://ifttt.com/) allowing build your workflow visually.

Circle CI have turned workflow steps into shareable packages called Orbs.

The "deploy anywhere" approach of [Microsoft Azure Pipelines](https://azure.microsoft.com/en-us/services/devops/pipelines/) (part of the Azure DevOps suite) means you can release software to any environment Kubernetes (Azure Kubernetes Service),  Serverless (Azure Functions) and Web. This is, of course, achievable because of the close integration with their Cloud platform Azure.

## Self Hosted or SaaS

The general advice from our original article remains the same, if it's a single product then SaaS will provide the least amount of friction whereas if you have multiple products or at enterprise scale then self-hosted is still worth considering.

In addition to this advice, we now also recommend that if you are delivering to multiple operating systems (Windows, MacOS and Linux) then SaaS can reduce the complexity of managing an exotic build farm. A common combination used by Rust developers is to use Travis CI for Linux and MacOS and [Appveyor](https://duckduckgo.com/?q=appveyor&t=ffab&ia=web) for Windows when building and packaging software.

The self-hosted route is only feasible if you have a dedicated Ops team, as the chances are if your CD goes down, your CI will be down too (nearly all self-hosted solution provide CI/CD as an all-in-one package). If both are down then your developers can't release features.

## Summary

To be continued...