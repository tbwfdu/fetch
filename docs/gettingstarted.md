---
title: Getting Started
layout: default
nav_order: 2
---
## Getting Started

{: .new }
Fetch now supports up to two Workspace ONE UEM Environments. Once you've added the first environment, you can add another from the `+` button in the tab menu.

### Required Settings

When you run Fetch for the first time you will need to enter the following settings.

 
![Alt text](/assets/images/image2.png "Image")


| Setting               | Description                                                                                            | Notes                                                                                                                                        |
|:----------------------|:-------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------|
| Friendly Name         | Any text based value you wish to help identify the environment                                         |                                                                                                                                              |
| Console URL           | Your UEM environment API Server <br/> (eg. `https://as1234.awmdm.com`)                                 | Ensure you use _`asXXXX`_ not _`cn`_ or _`ds`_                                                                                               |
| Client ID             | An OAuth Client ID generated from the UEM Console                                                      |                                                                                                                                              |
| Client Secret         | An OAuth Client Secret generated from the UEM Console                                                  |                                                                                                                                              |
| OAuth Environment URL | Your region’s OAuth Authentication Environment                                                         | Find yours [here](https://docs.vmware.com/en/VMware-Workspace-ONE-UEM/2209/UEM_ConsoleBasics/GUID-BF20C949-5065-4DCF-889D-1E0151016B5A.html) |
| File Download Path    | Enter a location where the downloaded installers should to be saved to <br/> (eg. `C:\temp\Downloads`) | Installers will stay here until they are manually deleted                                                                                    |

{: .info }
> Application Configuration is saved to: <br>
> `C:\Users\{your_username}\AppData\Local\Fetch\ApplicationData\LocalSettings.json`


> Org Group Name, Org Group ID and Org Group UUID will be retrieved automatically from Workspace ONE during validation of the settings entered above.


> No trailing slashes on any of the URLs or file paths as per examples.
> Upon saving, the Org Group ID and Org Group Uuid will be obtained from the UEM environment.

{: .important-title }
> IMPORTANT
>
> Fetch **encrypts** the entered Client ID and Client Secret before saving the value as an encrypted Base64 string to the Application Configuration file.
> 
> These credentials can **only** be decrypted by the _same user_ on the _same machine_ in which they were entered and saved on.

