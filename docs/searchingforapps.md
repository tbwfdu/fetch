---
title: Searching for Applications
layout: default
nav_order: 1
parent: Using Fetch
---
## Searching for Applications

The simplest way to use Fetch is to use the Search Applications functionality.

![Alt text](/assets/images/image3.png?raw=true "Image")

Upon searching and finding a result, an Administrator can see details provided by the Software Vendor about the application, choose the version, architecture and filetype (if multiple exist) and then add it to the upload queue.

{: .note-title }
> Notes
> 
> Application Search results default to:
> - The latest version available
> - x64 (then x86, then arm64) architecture
> - .msi installer type if they exist, otherwise it will default to .exe
> - Changing any of these results re-evaluates the available options
>   > **e.g.** _If a user changes the version selected in the dropdown list, it will then attempt to set the other options of the dropdowns to the defaults mentioned above._

## Queuing Multiple Applications
You can queue multiple applications from each page and have them upload sequentially.

![Alt text](/assets/images/image4.png?raw=true "Image")

## Editing Application Parameters

Once you have added an application to the queue, you can right-click on the Application entry and either remove it from the queued items or edit the default Configuration Parameters used to create the application in the Workspace ONE Catalog.

{: .info }
>
> When editing the application configuration, you can enable the text fields options by clicking the edit button next to the entry.