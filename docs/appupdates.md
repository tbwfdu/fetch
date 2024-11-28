---
layout: page
title: Usage
subtitle: Checking for Existing Application Updates
---

This workflow is quite straightforward. It will query Workspace ONE UEM and return matched results that have updated application versions.

![Alt text](../images/image7.png?raw=true "Image")

From here the Administrator can review (by pressing the `+`) and add any updates to the queue. The Review results dialog will select the _next latest_ version in the version list by default. 

Fetch also identifies the `filetype` (exe/msi) of the existing installer to select the appropriate type in the results selection view. 

**Note:** In the above example, 7-Zip shows multiple times as there are multiple _versions_ of 7-Zip added to the console. This allows Administrators to add and view updates when there is a use case to have multiple versions of an App in the Console.

:information_source:

Once you have added an application to the queue, you can right-click on the Application entry and either remove it from the queued items or edit the default Configuration Parameters used to create the application in the Workspace ONE Catalog.

When editing the application configuration, you can edit the available options by clicking the edit button next to the entry.