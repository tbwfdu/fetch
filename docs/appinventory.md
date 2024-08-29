---
layout: page
title: Usage
subtitle: Importing an Application Inventory
---

You can upload an existing application inventory report in **.csv** format with only 3 columns in the following order (with headers):

*“app_name”*, *“app_package_id”* & *“app_version”* (this is the naming standard from WS1 Intelligence). 

Fetch will then process this file and give you the results of what it has in its database vs. the report.

📋 [Click here](../examples/example_intelligence_apps_report.csv) for an Example Report from Workspace ONE Intelligence. 

Alternatively view the 🎬 [Overview Video](/) to see more detail.

![Alt text](../images/image5.png?raw=true "Image")

An *“Exact Match”* is where Fetch has matched the App Name with the exact same version from its database. A partial match is where it has found the application by name, but could not match on an exact file version.

By default, the results list only shows Exact or Partial Matches. You can change the Filter to show all results (include No Match) and if you want you can remove a result from the list using the “**x**” icon. On a *Partial* or *Exact Match* result, you can click the “**+**” icon and add the Application to the Upload Queue if desired.

![Alt text](../images/image6.png?raw=true "Image")