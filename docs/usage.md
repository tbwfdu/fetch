---
layout: page
title: Search
subtitle: Searching for Individual Apps
---

## Searching Applications

The simplest way to test Fetch is to use the Search Applications functionality.

![Alt text](../images/image3.png?raw=true "Image")

Upon searching and finding a result, an Administrator can see details provided by the Software Vendor about the application, choose the version, architecture and filetype (if multiple exist) and then add it to the upload queue.

**Notes:**

Results default to:

- The latest version available
- x64 (then x86, then arm64) architecture
- .msi installer type if they exist, otherwise it will default to .exe.
- Changing any of these results re-evaluates the available options.
  `Eg. If a user changes the version, it will then _attempt_ to set the other options of the dropdowns to the defaults mentioned above.`

You can queue multiple applications from each page and have them upload sequentially.

![Alt text](../images/image4.png?raw=true "Image")

## Upload Application Inventory Report

You can upload an existing application report in **.csv** format with only 3 columns in the following order (with headers):

*“app_name”*, *“app_package_id”* & *“app_version”* (this is the naming standard from WS1 Intelligence). Fetch will then process this file and give you the results of what it has in its database vs. the report.

![Alt text](../images/image5.png?raw=true "Image")


An *“Exact Match”* is where Fetch has matched the App Name with the exact same version from its database. A partial match is where it has found the application by name, but could not match on an exact file version.

By default, the results list only shows Exact or Partial Matches. You can change the Filter to show all results (include No Match) and if you want you can remove a result from the list using the “**x**” icon. On a *Partial* or *Exact Match* result, you can click the “**+**” icon and add the Application to the Upload Queue if desired.

![Alt text](../images/image6.png?raw=true "Image")

## Application Updates

This workflow is straightforward. It will query Workspace ONE UEM and return results that have updated versions in the database.

![Alt text](../images/image7.png?raw=true "Image")

From here the Administrator can review (by pressing the **+**) and add any updates to the queue. The Review results dialog will select the _next latest_ version in the version list by default.

**Note:** In the above example, 7-Zip shows multiple times as there are multiple _versions_ of 7-Zip added to the console. This allows Administrators to add and view updates when there is a use case to have multiple versions of an App in the Console.


## Upload Application Manifest

Here you can upload an existing manifest of your Enterprise Applications. Fetch will validate some basic information (*entered data is complete, data types are correct, files exist*) and then uploads the installer and creates the associated Native App in UEM.

![Alt text](../images/image8.png?raw=true "Image")

Here is an example of the contents of the manifest template:

![Alt text](../images/image9.png?raw=true "Image")

These columns correlate to the metadata required by the Workspace ONE Application API/Console.