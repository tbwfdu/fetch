---
layout: page
title: Usage
subtitle: Searching For Applications
---

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


:information_source:

Once you have added an application to the queue, you can right-click on the Application entry and either remove it from the queued items or edit the default Configuration Parameters used to create the application in the Workspace ONE Catalog.

When editing the application configuration, you can edit the available options by clicking the edit button next to the entry.