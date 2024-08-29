---
layout: page
title: Usage
subtitle: Upload Local Application Manifest
---

This process allows you to do a **bulk upload** of your Enterprise Applications that you maintain the installers for, or a list of verified or custom list of installers that you maintain on your file servers. Once you upload a manifest (in .csv format), Fetch will validate some basic information (*entered data is complete, data types are correct, files exist*) and then uploads the installer and creates the associated Native App in UEM.

The main aspect of this process is that you specify a **local file path** (that the Fetch Application can access) of the installers you want to upload to UEM, along with all the required metadata that is needed to add the Application to the App Catalog. This workflow does not use any of the metadata within the Fetch Database.

![Alt text](../images/image8.png?raw=true "Image")

Here is an example of the contents of the manifest template:

![Alt text](../images/image9.png?raw=true "Image")

These columns correlate to the metadata required by the Workspace ONE Application API/Console.

📋 [Click here](../examples/local_applications_manifest.csv) for an Example Local Applications Manifest for you to enter the relevant data in to.

Alternatively view the 🎬 [Overview Video](/) to see more detail.