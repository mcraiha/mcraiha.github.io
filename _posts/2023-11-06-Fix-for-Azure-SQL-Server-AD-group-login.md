---
layout: post
title:  "Login failed for user token-identified principal"
date:   2023-11-06 20:30:00 +0200
categories: Azure SQL server AD group Entra member owner
---
# One fix for Azure SQL Server Login failed for user token-identified principal

If you have Azure SQL Server and you set Azure AD Group as admin, but you cannot login to the database, this might be the fix you are looking for (*no guarantees are given*).

So if the login to the Azure SQL database works in case a single Azure AD user is set as Azure SQL Server admin, but it fails when that same Azure AD user is part of an AD group (and you get error like `Login failed for user '<token-identified principal>'`), then make **SURE** that the AD user also belongs to the member part of the AD group.

## What?

In Azure AD / Entra Group [owners are not members](https://learn.microsoft.com/en-us/answers/questions/1159925/deep-dive-needed-about-azure-ad-group-owners). So if you create a new Azure AD / Entra Group and assign the AD user as owner for the group, the SQL login will fail. So you also have to add that user as Azure AD / Entra Group member and then login should work.

![Azure AD / Entra member vs. owner]({{ site.url }}/images/ad_members_vs_owners.png "Azure AD / Entra member vs. owner")   
(as you can see, icons are quite similar for **Members** and **Owners**, but outcome is not)