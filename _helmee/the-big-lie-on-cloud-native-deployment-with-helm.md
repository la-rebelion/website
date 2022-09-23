---
layout: post_jekflix
title: The Big Lie on Cloud Native Apps deployment with helm
description: "A big lie: 'The process to deploy and manage cloud native solutions is easy-peasy with helm'."
image: https://images.unsplash.com/photo-1583443920098-6b56d6aabdb1?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1470&q=80
references:
  photo:
    from: Pawel Czerwinski
    url: https://unsplash.com/@pawel_czerwinski?utm_source=la-rebelion&utm_medium=referral
    source: unsplash
categories: Helmee
tags: [devops, helm]
cta:
  description: "Would you like learn more about helmee? Subscribe and be notified when more material is available"
  short_text: Subscribe to our alpha testers list
  destination: https://www.patreon.com/rebelionlabs
---

## What is _helmee_?

_helmee_ leverage helm charts to help on improving developer experience with deployments on Kubernetes clusters. Sometimes it is difficult that a single person or team can maintain several environments at the same time due to the different variables and artifacts (images, secrets, config maps, etc.) per environment that needs to be updated, and sometimes a person deploying same solution on an _environment A_ use different tools or process to install same solution in other environment of the same customer/account.

## Why _helmee_?

"The process to deploy and manage cloud native solutions is easy-peasy with helm"

This statement sometimes is a "big lie"; the [big lie](https://en.wikipedia.org/wiki/Big_lie) is a gross distortion or misrepresentation of the truth, used especially as a propaganda technique.

In real deployments this is not that simple, because when a customer has **more than one environment**, the parameters to use to deploy change from environment to environment, i.e. different possible combinations: database vendor, database version, Kubernetes cluster "flavor" (i.e. OpenShift, Rancher, AWS EKS), container registry, different namespaces, sizing/resources. Additional to the infrastructure or underlying platform, there are additional factors to complicate even more the deployment, this is the version control of the solutions and testability, dependencies or connectivity with external systems.

## Facts

* `Kubernetes` is the defacto "operative system" for cloud solutions.
* `Kubernetes` can be complex.
* If there is a need to orchestrate more than one Kubernetes resource and if there are multiple clusters with different configurations, then, this is a strong use case for leveraging `Helm`.
* A Helm Chart is a **collection of files** that describe a set of Kubernetes resources.
* Helm needs to be customized to deploy it into different customer accounts and clusters, into different environments.

* Event with helm in place, each deployment would be managed different depending on each project team or sysadmin.

Multiply these not only to the number of clients and environments you are working with, but also to the different products (components or microservices) you need to deploy, because sometimes your solution's bundle include: your product itself, the database, a cache database, etc.

## What do you need to know before deploying with Helm?

What do you need to know in advance, before deploying with Helm? You need to determine the version of your application that you want to deploy. This is usually done by using a file in the repository, called CHANGELOG.md, **but is static**! In this file, you can see what has changed between versions of your application and decide which one is appropriate for your deployment. You also need to create a chart if it doesn’t already exist in your repository.

In a Helm chart, you specify the name of your application, its version, how it’s built and packaged (for example, whether it uses Docker), what dependencies are needed to run it, and how to deploy your application.

**... and is constantly changing or adding variables!**

What is in the release you are deploying?

* Solutions/products in the bundle
* Issues solved
* Enhancements/Features

What are the artifacts/components deployed?

Runtime environments

* Cluster (IP)/namespace
* Version
* Integration with external systems/APIs.

We are going to leverage `helm` with _helmee_, now it will be much easier than using `helm` alone. Not lying, seriously. Test it and confirm, give us your feedback.

If you find this project useful, please star our repository in GitHub, follow us on Twitter and subscribe for latest news. Thanks.
