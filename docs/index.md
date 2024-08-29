---
layout: home
title: Fetch
subtitle: Workspace ONE Application Management Tool
---

Fetch is a Windows application that allows Workspace ONE Administrators rapidly deploy native Windows Applications. Previously, the process to make applications available on managed devices was complex and time consuming.

Fetch solves these problems by allowing Administrators to automatically download the installers, upload the binaries to Workspace ONE UEM and create the related Native Windows Application entry in the environment with all the required information for it to install and uninstall on end user devices.

<video muted controls>
    <source src="/images/Overview.mp4" type="video/mp4" object-position="center">
</video>

Currently, the Fetch database has over 6000 unique applications with a combined count of 49,000 application versions.


![Alt text](../images/image1.png?raw=true "Image")


There are 4 main workflows that an Administrator can utilise with Fetch:

1. **Search for an Application** by name and **automatically create** its corresponding Native App in Workspace ONE UEM.  

2. **Upload a Software Asset Management/Application Report** of their existing Windows fleet (eg. Installed Apps report from Workspace ONE Intelligence, Software Deployment Report from SCCM, Powershell report of network devices etc.) and **Fetch will show if the Application exists** in its database. **If a matching application is available** it will allow the Administrator to **create the corresponding Native App in Workspace ONE UEM**.  

3. **Interrogate their existing Workspace ONE UEM** environment’s Applications and **report if there are known updated versions available** allow the Administrator to **automatically upload and create an updated version** of the Application.  

4. **Upload a manifest (template)** of existing Native Windows Applications used in the Organization which they have **their own installation files** available for. This workflow allows an Administrator to quickly fill out the template with the required metadata about the Application and point to existing installers on their device. Once the manifest is processed, Fetch can then **upload the installers from the filesystem and create the apps in UEM** using the metadata provided in the manifest.


### [**Download Here**](https://github.com/tbwfdu/fetch/releases)


## Example Files

**Application Inventory Report**
[link](examples/example_intelligence_apps_report.csv)

**Application Manifest**
[link](examples/local_applications_manifest.csv)