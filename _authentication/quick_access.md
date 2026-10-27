---
title: Quick Access
position: 1
---

A signed-in user can [generate a temporary access token]({{ site.app_url }}generate_own_access_token) for their own account. The token has every scope and expires after 30 days. Each visit to the page generates a new one.

Use it to try the API against your own data. An app that other people use should [register](#authenticationcreate_an_app) and ask each user for a token through OAuth.

These tokens belong to an application named Docs Sandbox. To revoke them all, remove Docs Sandbox under Account > [Installed]({{ site.app_url }}oauth/authorized_applications).
