# Fetch

Fetch is a Windows application that allows Workspace ONE Administrators rapidly deploy native Windows Applications. Previously, the process to make applications available on managed devices was complex and time consuming.

Fetch solves these problems by allowing Administrators to automatically download the installers, upload the binaries to Workspace ONE UEM and create the related Native Windows Application entry in the environment with all the required information for it to install and uninstall on end user devices.

Currently, the Fetch database has over 6000 unique applications with a combined count of 49,000 application versions.


![Alt text](images/image1.png?raw=true "Image")


There are 4 main workflows that an Administrator can utilise with Fetch:

1. **Search for an Application** by name and **automatically create** its corresponding Native App in Workspace ONE UEM.  

2. **Upload a Software Asset Management/Application Report** of their existing Windows fleet (eg. Installed Apps report from Workspace ONE Intelligence, Software Deployment Report from SCCM, Powershell report of network devices etc.) and **Fetch will show if the Application exists** in its database. **If a matching application is available** it will allow the Administrator to **create the corresponding Native App in Workspace ONE UEM**.  

3. **Interrogate their existing Workspace ONE UEM** environment’s Applications and **report if there are known updated versions available** allow the Administrator to **automatically upload and create an updated version** of the Application.  

4. **Upload a manifest (template)** of existing Native Windows Applications used in the Organization which they have **their own installation files** available for. This workflow allows an Administrator to quickly fill out the template with the required metadata about the Application and point to existing installers on their device. Once the manifest is processed, Fetch can then **upload the installers from the filesystem and create the apps in UEM** using the metadata provided in the manifest.


### [**Download Here**](https://github.com/tbwfdu/fetch/releases)


## Required Settings

Upon first time run, you will need to enter the following settings.


![Alt text](images/image2.png?raw=true "Image")


|                		|Description                    |Notes                         |
|-----------------------|-------------------------------|-----------------------------|
|Console URL			|Your UEM environment API Server (eg. https://as1234.awmdm.com)|Ensure you use _`asXXXX`_ not _`cn`_ or _`ds`_ |
|Client ID				|An OAuth Client ID generated from the UEM Console||
|Client Secret			|An OAuth Client Secret generated from the UEM Console||
|OAuth Environment URL	|Your region’s OAuth Environment|Find yours [here](https://docs.vmware.com/en/VMware-Workspace-ONE-UEM/2209/UEM_ConsoleBasics/GUID-BF20C949-5065-4DCF-889D-1E0151016B5A.html)|
|File Download Path		|Enter a location where the downloaded installers should to be saved to (eg. C:\temp\Downloads)|Installers will stay here until they are manually deleted|

**_NOTE:_** 
No trailing slashes on any of the URLs or filepaths as per examples. OAuth environments will eventually be a selection box._
Upon saving, the Org Group ID and Org Group Uuid will be obtained from the UEM environment.


**_IMPORTANT:_** 
These settings are currently saved in `C:\Users\{your_username} \AppData\Local\Fetch\ApplicationData\LocalSettings.json`
**Ensure security of this file**. Later versions of Fetch will save these secrets to the registry using Windows’s Data Protection APIs.

## Searching Applications

The simplest way to test Fetch is to use the Search Applications functionality.

![Alt text](images/image3.png?raw=true "Image")

Upon searching and finding a result, an Administrator can see details provided by the Software Vendor about the application, choose the version, architecture and filetype (if multiple exist) and then add it to the upload queue.

**Notes:**

Results default to:

- The latest version available
- x64 (then x86, then arm64) architecture
- .msi installer type if they exist, otherwise it will default to .exe.
- Changing any of these results re-evaluates the available options.
  `Eg. If a user changes the version, it will then _attempt_ to set the other options of the dropdowns to the defaults mentioned above.`

You can queue multiple applications from each page and have them upload sequentially.

![Alt text](images/image4.png?raw=true "Image")

## Upload Application Inventory Report

You can upload an existing application report in **.csv** format with only 3 columns in the following order (with headers):

*“app_name”*, *“app_package_id”* & *“app_version”* (this is the naming standard from WS1 Intelligence). Fetch will then process this file and give you the results of what it has in its database vs. the report.

![Alt text](images/image5.png?raw=true "Image")


An *“Exact Match”* is where Fetch has matched the App Name with the exact same version from its database. A partial match is where it has found the application by name, but could not match on an exact file version.

By default, the results list only shows Exact or Partial Matches. You can change the Filter to show all results (include No Match) and if you want you can remove a result from the list using the “**x**” icon. On a *Partial* or *Exact Match* result, you can click the “**+**” icon and add the Application to the Upload Queue if desired.

![Alt text](images/image6.png?raw=true "Image")

## Application Updates

This workflow is straightforward. It will query Workspace ONE UEM and return results that have updated versions in the database.

![Alt text](images/image7.png?raw=true "Image")

From here the Administrator can review (by pressing the **+**) and add any updates to the queue. The Review results dialog will select the _next latest_ version in the version list by default.

**Note:** In the above example, 7-Zip shows multiple times as there are multiple _versions_ of 7-Zip added to the console. This allows Administrators to add and view updates when there is a use case to have multiple versions of an App in the Console.


## Upload Application Manifest

Here you can upload an existing manifest of your Enterprise Applications. Fetch will validate some basic information (*entered data is complete, data types are correct, files exist*) and then uploads the installer and creates the associated Native App in UEM.

![Alt text](images/image8.png?raw=true "Image")

Here is an example of the contents of the manifest template:

![Alt text](images/image9.png?raw=true "Image")

These columns correlate to the metadata required by the Workspace ONE Application API/Console.


## Example Files

**Application Inventory Report**
[link](examples/example_intelligence_apps_report.csv)

**Application Manifest**
[link](examples/local_applications_manifest.csv)
