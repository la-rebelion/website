---
layout: post
title: My Journey as System integrator
date: 2021-10-29 11:32:20 -0600
description:  > # this means to ignore newlines until next YAML property
    Some issues I face in my day by day activities, and how overcome on it with a solution or hack.
external_image: true
img: https://images.unsplash.com/photo-1536825211030-094de935f680?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=735&q=80 #https://images.unsplash.com/photo-1600705722738-d39380209f19?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=687&q=80
fig-caption: # Add figcaption (optional)
tags: [Cloud, SysAdmin, Code, DevOps, Product Management]
cta_description: "DevOps, SysAdmin, Cloud... how to survive the SI journey?:"
cta_short_text: Follow my steps here
cta_destination: https://mexa.rebelion.la
---

"Don't trust anyone", Zero Trust is a security constraint that states that organizations should not automatically trust anything inside or outside its perimeters and instead must verify anything and everything trying to connect to its systems before granting access

Many times Independent Software Vendors (ISVs) and System Integrators (SI) working on Enterprise projects face with many difficulties delivering solutions, for instance, there are several security policies and restrictions to follow, when infrastructure needs to be provisioned and configured for a new project or installing new applications it becomes a nightmare, it needs to be done in an "[air gap network](https://en.wikipedia.org/wiki/Air_gap_(networking))" or "[Zero trust network access (ZTNA)](https://www.gartner.com/en/information-technology/glossary/zero-trust-network-access-ztna-)" environment where the applications are hidden from discovery, and access is restricted; hence, you won't have access to the minimum resources you need, i.e.: Git (GitHub or GitLab), public image Containers registry, then, installation and configuration is harder because you need to tweak the "standard" product deployment scripts. RnD should be aware of this and take actions to improve the SIs delivery journey, but we will discuss this in another post.

Setting up the environments (Dev, Testing, Staging, Prod) becomes a repetitive, tedious and manual task because you don't have the tools or platforms you used in a previous project. With "My journey" posts I share what I expect to be helpful onboarding and managing your new projects.

{% include elements/button.html style="primary" %}
