---
layout: post
title: Identity Server 4 - setting up a simple identity server to test JWT
date: 2019-09-17 23:00:00 +0000
description: How to set up a simple identity server to test JWT token issuance
heading: How to set up a simple identity server 4 for JWT
categories: security

---
Making a simple Identity Server 4 to test JWT issuance

If you have ever looked at the Identity Server 4 project on GitHub you will be bewildered by the sheer amount of stuff you can download. There are multiple permutations and branches of the software.

The git source is located here: [https://github.com/IdentityServer/IdentityServer4](https://github.com/IdentityServer/IdentityServer4 "https://github.com/IdentityServer/IdentityServer4")

Here is how we got a very simple Identity Server 4 working to test an application which required JWT tokens. 

First we downloaded Quickstart 1_ClientCredentials from the many GitHub example projects. It can currently be found here: [https://github.com/IdentityServer/IdentityServer4/tree/master/samples/Quickstarts/1_ClientCredentials](https://github.com/IdentityServer/IdentityServer4/tree/master/samples/Quickstarts/1_ClientCredentials "https://github.com/IdentityServer/IdentityServer4/tree/master/samples/Quickstarts/1_ClientCredentials")