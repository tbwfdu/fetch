---
layout: page
title: FAQs
include_in_header: true
order: 3
---

# Frequently Asked Questions
{: .no_toc }

## Page Contents
{: .no_toc .text-delta }

* TOC
{:toc}




### How often is the Fetch Database updated?
Fetch has a corresponding Web Service that automatically obtains the latest list of source applications and generates an updated database **daily** at approx. 00:05 UTC.
When querying for database updates in Fetch, the application communicates with this Web Service API to check for the updated database file and then replaces the local copy.

### What Operating Systems does Fetch support?
The Fetch application itself has installers that will run on Windows 10/11 (x64 & ARM64).

Applications that Fetch can *upload* to Workspace ONE is whatever version/format/architecture the Software Vendor provides in their manifests. As long as it is supported by Workspace ONE and provided in the correct format, Fetch will upload it to the Catalog.  

### Where do I get help or support if something isn't working?

[Raise an issue here](https://github.com/tbwfdu/fetch/issues) and I will get back you as soon as I can 🐛.

### What is the source of Application Information in the Fetch Database?

The Fetch database is populated by a separate microservice that downloads the entire package manifest list from the **Official** Microsoft Winget repository. These manifest files (over 140k) are parsed, correlated and imported into the database that Fetch uses.

Each day, the service pulls the latest manifests from the Microsoft Winget repository and generates a new database. This is then made available via a webhost that Fetch queries to get a copy of the updated database (if its newer than its current one).

Any application binaries, metadata, information etc. is the exact same information that the Winget command line tools use within Window. This is provided by the Software Vendor and vetted by Microsoft, however Fetch nor Microsoft grant any licenses, ownership or responsibility for the applications obtained or installed.

### How does Fetch provide `How To Install`, `When To Call Install Complete` & `Uninstall` commands/criteria?

If the application’s installer is a **.msi file**, this allows Fetch to use the built-in defaults of Workspace ONE UEM and how the Software Deployment Agent handles **msiexec.exe**.

For **.exe files**, Fetch uses the information provided in the Winget manifests to find the correct installation commands. It will attempt to find *“Silent”* or *“Silent with Progress”* switches and add these to the install commands in UEM.

To determine a _successful install_ and _how to uninstall_, Fetch uploads (before the installer) two generic Powershell scripts: **InstallSuccessCriteria.ps1** & **Uninstall.ps1**

These scripts are used for determining when to call an application installed and to get the correct uninstallation commands.


**InstallSuccessCriteria.ps1**

This script runs and looks for an “Uninstall” entry in the device’s registry for the application. Because we know the name of the Application, the name the Application in Add/Remove programs and the version as it is in the Winget manifest, we pass these as variables to the script and it returns a 0 (found) or 1 (not found) exit code.

``` ps
<# 
  .DESCRIPTION
    Takes two input variables and then searches the registry to report if an Uninstall entry exists for the Application name and Version. Then uses the uninstallcommand to remove the application.
  .EXAMPLE
    .\Uninstall.ps1 "7-Zip" "24.07"
  .PARAMETER 0
    Application Name used to do a lookup using a "-LIKE" function to remove the need for an exact match on the name.
  .PARAMETER 1
    The Application Version to ensure we are only looking for the exact version in case the application allows multiple versions to be installed.
  .NOTES 
    Created:   	    July, 2024
    Created by:	    Pete Lindley, @tbwfdu
#>

param(
    [Parameter(Position=0,mandatory=$true)]
    [string] $DisplayName,
    [Parameter(Position=1,mandatory=$true)]
    [string] $DisplayVersion
)

$UninstallString = Get-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\* | Where-Object {($_.DisplayName -Like "$DisplayName*") -and ($_.DisplayVersion -eq $DisplayVersion)} | Select-Object -ExpandProperty "UninstallString";
$QuietUninstallString = Get-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\* | Where-Object {($_.DisplayName -Like "$DisplayName*") -and ($_.DisplayVersion -eq $DisplayVersion)} | Select-Object -ExpandProperty "QuietUninstallString";

if($null -ne $QuietUninstallString)
{
    Invoke-Expression "& $QuietUninstallString"
}

elseif($null -ne $UninstallString)
{
    Invoke-Expression "& $UninstallString"
}

```

**When To Call Installation Complete** *example*:

``` 
powershell.exe -ExecutionPolicy Bypass -File InstallSuccessCriteria.ps1 "VMware Horizon Client" "8.5.0.26981"
```

**Uninstall.ps1**
Each application that gets installed in Windows creates a registry key with it’s uninstall command so that when a user uses Add/Remove Programs it is able to uninstall the application correctly. The uninstall script provided by Fetch firstly searches the registry (using the same parameters above for detection), obtains the uninstall command from the registry, and then runs the command to uninstall the application.
``` ps
<# 
  .DESCRIPTION
    Takes two input variables and then searches the registry to report if an Uninstall entry exists for the Application name and Version. Then uses the uninstallcommand to remove the application.
  .EXAMPLE
    .\Uninstall.ps1 "7-Zip" "24.07"
  .PARAMETER 0
    Application Name used to do a lookup using a "-LIKE" function to remove the need for an exact match on the name.
  .PARAMETER 1
    The Application Version to ensure we are only looking for the exact version in case the application allows multiple versions to be installed.
  .NOTES 
    Created:   	    July, 2024
    Created by:	    Pete Lindley, @tbwfdu
    Current Version: 0.3
    VERSION HISTORY
    0.3 - Made changes to the order of detect and how it runs. No exit codes for success seems to work.
    0.2 - Added the capability that it looks at other registry locations for installers that don't use standard installers/methods or when installing 32-bit on 64-bit Windows.
    0.1 - This looks at the normal Uninstall keys in the registry

#>

param(
    [Parameter(Position=0,mandatory=$true)]
    [string] $DisplayName,
    [Parameter(Position=1,mandatory=$true)]
    [string] $DisplayVersion
)

$UninstallString = Get-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\* | Where-Object {($_.DisplayName -Like "$DisplayName*") -and ($_.DisplayVersion -eq $DisplayVersion)} | Select-Object -ExpandProperty "UninstallString";

$QuietUninstallString = Get-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\* | Where-Object {($_.DisplayName -Like "$DisplayName*") -and ($_.DisplayVersion -eq $DisplayVersion)} | Select-Object -ExpandProperty "QuietUninstallString";

$UninstallString_WOW6432Node = Get-ItemProperty -Path HKLM:\SOFTWARE\WOW6432Node\Microsoft\Windows\CurrentVersion\Uninstall\* | Where-Object {($_.DisplayName -Like "$DisplayName*") -and ($_.DisplayVersion -eq $DisplayVersion)} | Select-Object -ExpandProperty "UninstallString";

$QuietUninstallString_WOW6432Node = Get-ItemProperty -Path HKLM:\SOFTWARE\WOW6432Node\Microsoft\Windows\CurrentVersion\Uninstall\* | Where-Object {($_.DisplayName -Like "$DisplayName*") -and ($_.DisplayVersion -eq $DisplayVersion)} | Select-Object -ExpandProperty "QuietUninstallString";


if($null -ne $QuietUninstallString)
{
    Invoke-Expression "& $QuietUninstallString"
}

elseif($null -ne $UninstallString)
{
    Invoke-Expression "& $UninstallString";

}

elseif($null -ne $QuietUninstallString_WOW6432Node)
{
    Invoke-Expression "& $QuietUninstallString_WOW6432Node";
}

elseif($null -ne $UninstallString_WOW6432Node)
{
    Invoke-Expression "& $UninstallString_WOW6432Node";
}

else {
  exit 0;
}
```

**How To Uninstall** *example*:
```
powershell.exe -ExecutionPolicy Bypass -File Uninstall.ps1 "7-Zip" "19.00.00.0"
```

> Note
>
> These Powershell files are embedded into the Application. Fetch automatically populates the App Name/Version variables so the commands for verifying a successful install/uninstall (the parameters of the script) so these are shown here for completeness.