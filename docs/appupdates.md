---
title: Finding Available Application Updates
layout: default
nav_order: 3
parent: Using Fetch
---
## Application Updates

This workflow allows you to identify which of your **existing** managed applications in your Workspace ONE Applications have updates available. Fetch queries your Workspace ONE UEM environment and attempts to match applications using the "App Name" configured in UEM. If Fetch can match the application it will query the database for updated application versions.

![Alt text](/fetch/assets/images/image7.png?raw=true "Image")

From here the Administrator can review (by pressing the `+`) and add any updates to the queue. The 'Review Results` dialog will select the _next latest_ version in the version list by default. 

{: .important }
> When reviewing an update for a matched application, Fetch will only show versions that are _newer_ than version returned from Workspace ONE UEM.

Fetch also identifies the `filetype` (exe/msi) of the existing installer to select the appropriate type in the results selection view. 

{: .note-title }
> Note
> 
> In the above example, 7-Zip shows multiple times as there are multiple _versions_ of 7-Zip added to the console. This allows Administrators to add and view updates when there is a use case to have multiple versions of an App in the Console.

{: .info }
> Once you have added an application to the queue, you can right-click on the Application entry and either remove it from the queued items or edit the default Configuration Parameters used to create the application in the Workspace ONE Catalog.
> 
> When editing the application configuration, you can edit the available options by clicking the edit button next to the entry.
