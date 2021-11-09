---
title: "Getting Started"
weight: 20
---

Idem is an idempotent dataflow programming language. It exposes stateful programming constructs that makes things like enforcing the state of an application, configuration, SaaS system, or others very simple.

Idem State and Exec modules
In Idem we enforce the desired state using State and exec modules.

Idem state modules generally have three functions :

<b>describe:</b> This function is is used to describe the current state of the environment. For e.g. We can run describe on a AWS idem module to describe all the VPCs in a region. 

<b>present:</b> This function is used to achieve the desired state by creating or updating components in environment. The desired state is represented in SLS file. For e.g we can define the VPCs to be created in a region in SLS file and apply it.

<b>absent:</b> This function is used to achieve desired state by deleting the components from environment. This desired state is also represented in SLS file. For e.g. we can specify that a VPC with certain configuration should never exist in a region and apply it.

Idem is based on the concept of [Plugin Oriented Programming](https://pop.readthedocs.io/en/latest/)
More documentation [readthedocs](https://idem.readthedocs.io/en/latest/)