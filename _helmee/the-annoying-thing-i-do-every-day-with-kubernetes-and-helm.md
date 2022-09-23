---
layout: post_jekflix
title: The Annoying Thing I Do every day with Kubernetes and Helm
description: "Let's face it, Kubernetes and Helm is great and even essential for many DevOps setups. Yet it requires exceptional patience and skill to use. Here I share my 'aha' moments in case you also struggle with the same things"
image: https://images.unsplash.com/photo-1501673618753-48ce9418287b?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1374&q=80
references:
  photo:
    from: Michelle Phillips
    url: https://unsplash.com/@@robotmoth?utm_source=la-rebelion&utm_medium=referral
    source: unsplash
  articles:
    - url: https://helm.sh/docs/topics/charts/
      text: Helm Charts
    - url: https://helm.sh/docs/topics/advanced/
      text: Helm Advanced Techniques
    - url: https://github.com/kubernetes-sigs/kustomize
      text: Kustomize tool
categories: Helmee
tags: [cloud devops helm]
cta:
  description: "Would you like learn more about helmee? Apply for closed beta"
  short_text: Experience it first
  destination: https://rebelion-21339207.hubspotpagebuilder.com/helmee-early-adopters
---

Kubernetes (and Helm) has made life easier for many of us. However, like any other tool, it can be challenging to use. The learning curve is steeper than most new technologies due to its complexity. Even the simplest tasks require several commands and can be easily forgotten or overlooked. Every day, I find myself struggling with multiple Kubernetes cluster I created for my company for different environments (Dev, Test, Staging; excluding Production which is on customer responsibility). While working on a side project that requires Kubernetes as a backend service, I had multiple ‘aha’ moments and wanted to share them with you guys in case you also struggle with the same things.

## Deploying and upgrade applications with helm is tedious

Helm uses a packaging format called [charts](https://helm.sh/docs/topics/charts/). A chart is a collection of files that describe a related set of **Kubernetes resources**, when you run `helm install`, behind scenes, `helm` generates all those required resources and apply the artifact into the Kubernetes cluster, like magic and easy, right?

But, what happen when you need to deploy the chart on different environments (dev, test, staging, prod)? There are charts that are customizable with so many variables and many resources, then, deployment becomes tedious and annoying on each upgrade, because you need to be sure you are replicating changes in all those different environments. You can use `helm` [advanced techniques](https://helm.sh/docs/topics/advanced/) to customize and manipulate the charts and it's resources, but as the name states, these are **advanced techniques** and we are mere mortals, right? :)

It is not a good idea to depend on resources that are not under your control, [helm charts](https://helm.sh/docs/topics/charts/) is one of these things. One [Kustomize](https://github.com/kubernetes-sigs/kustomize)'s best practice is to maintain a local, "inflated fork" of a remote configuration (i.e. git), and have a human rebase / reinflate that fork from time to time to capture upstream changes. That is in fact one the `helmee` premises it is based on, and this is done automatically when `helmee` is executed.

## Scripted Away and Forgotten

Annoying tedious things are immediately scripted away and forgotten, that was the 'aha' moment, how and why `helmee` idea get born. I was frustrated with this repetitive tasks on deploying and upgrading more than one integrated application stacks, frontend, backend, database of application *X* requiring stack from *Y* application, application Y based on microservices architecture with tenths of different pods and containers versions!

This is how I solved that problem: _Templating_ the templates with JavaScript, I will show you how. To keep you on track join [here](https://rebelion-21339207.hubspotpagebuilder.com/helmee-early-adopters).

In my previous article, I talked about the things Kubernetes has taught me. Having used and implemented Kubernetes in production environments, I’ve discovered a different way which helps with increasing your time invested in preparing the helm charts and manifest files effectively. These kubernetes tips and tricks are what I call “lessons learned” from working with Kubernetes on a daily basis.

These lessons have been implemented as a set of scripts and YAML files that automatically generates the required `helm` resources to the desired state depending the environment to deploy. I call it `helmee`; you can test beta version when available, [subscribe here](https://rebelion-21339207.hubspotpagebuilder.com/helmee-early-adopters) to get access for early adopters interested in optimize their processes deploying Kubernetes applications.

Helmee will help you deploying your helm charts easy and fast using your configuration on multiple different Kubernetes environments. You can implement this if you will, here is how:

**Create Helper Scripts**

When I create a new project, I like to create a few helper scripts to make the deployment and operations easier. In the past, I have used Ansible, Chef, and Terraform to bootstrap new projects. For this project, I chose to use JavaScript. The reason is, it would be a simple deployment that does not require any external dependencies. The scripts I created help me create new Kubernetes resources and maintain these with different versions in `Git`, deploy and manage application secrets and configurations, still leveraged on `helm` and `Kubernetes`. This will make the project more consistent and allow you to focus on the application instead of the deployment and operations.

**Don't Forget to Set the Context before Running a Command**

When you are trying to run a specific command, be sure to set the context to the correct namespace where the resource exists. If you don’t set the context, the command may run on the wrong cluster. Your cluster may have other namespaces with resources you would like to control. For example, if you have a namespace named “myapp”, and you want to run a command on the “myapp” namespace, you need to set the context to “myapp” before executing the command. You can do that with either of the following options: - Use the “-c” flag to set the context. - Create a shell script and set the context before executing the command.

**Use Scripts to Manage Secrets and Configurations**

Secrets and configurations are often saved in a file, like a file named “config.yml” or “secrets.yml”. If you ever need to find that file, you may find yourself searching through your computer. You may even open up your editor and search for the file. Once you find the file, you will need to open it, copy the value from the file, and then paste it into the terminal. The terminal can quickly become messy if you are pasting multiple values. I recommend creating a script to manage your secrets and configurations. You can then either call the script from the terminal or create automation to run the script to populate your values in the terminal.

**View Your Cluster’s Resource Usage**

While working in the cluster, you may want to view the overall resource usage. You can view the resource usage with the “kubectl get” command. The output of the command displays the resource usage for pods, services, nodes, and the cluster. If you would like to view the resource usage of a specific pod, you can run the command with “-o wide”. This will display the resource usage of pods and services along with the name of the pod or service.

## Conclusion

Start by creating a few helper scripts that make deployment and management easier. Next, don’t forget to set the context of the terminal before executing a command. It’s also important to use scripts to manage secrets and configurations. Finally, view your cluster’s resource usage to see where you can optimize. With these tips, you’ll be well on your way to a smoother Kubernetes experience.
