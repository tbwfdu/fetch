---
title: Bulk Upload of Local Apps
layout: default
nav_order: 4
parent: Using Fetch
---
## Bulk Upload of Local Apps


This process allows you to do a **bulk upload** of your Enterprise Applications that you maintain the installers for, or a list of verified or custom list of installers that you maintain on your file servers. Once you upload a manifest (in .csv format), Fetch will validate some basic information (*entered data is complete, data types are correct, files exist*) and then uploads the installer and creates the associated Native App in UEM.

The main aspect of this process is that you specify a **local file path** (that the Fetch Application can access) of the installers you want to upload to UEM, along with all the required metadata that is needed to add the Application to the App Catalog. This workflow does not use any of the metadata within the Fetch Database.

![Alt text](/fetch/assets/images/image8.png?raw=true "Image")

Here is an example of the contents of the manifest template:

![Alt text](/fetch/assets/images/image9.png?raw=true "Image")

These columns correlate to the metadata required by the Workspace ONE Application API/Console.

{: .new }
> There are also now additional options in the manifest templates that allows you to change _any_ or _all_ of the available configuration options that are available in the UEM Console UI. This means you can enter all the custom information needed to deploy and install the application directly in the manifest.

The [manifest template](/examples/local_applications_manifest_template.xlsx) is now saved as a `.xslx` file, and where there are multiple choice options for configuration settings, they are shown in a dropdown inside this spreadsheet allowing simpler and more accurate manifests.

{: .important-title }
> Important
> 
> You need to ensure you still **save as** or **export** your manifest as a `.csv` file.


[See here](/examples/local_applications_manifest.csv) for an Example Local Applications Manifest for you to enter the relevant data in to.

Alternatively view the 🎬 [Overview Video](/) to see more detail.