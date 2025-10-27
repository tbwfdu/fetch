## Importing an Application Inventory

You can upload an existing application inventory report in **.csv** format with only 3 columns in the following order (with headers):

`app_name`, `app_package_id` & `app_version` 
> *this is the naming standard from Workspace ONE Intelligence* 

Fetch will then process this file and give you the results of what it has in its database vs. the report.

[See here](assets/examples/example_intelligence_apps_report.csv) for an Example Report from Workspace ONE Intelligence.

![Alt text](assets/images/App_Inventory.png "App Inventory Screenshot")

>### ℹ️ Note
>{: .no_toc }
>
> The results will load _incrementally_ when scrolling to the last item in the current view

## Reviewing Matches
An *“Exact Match”* is where Fetch has matched the App Name with the exact same version from its database. A partial match is where it has found the application by name, but could not match on an exact file version.

By default, the results list only shows Exact or Partial Matches. You can change the Filter to  show all results (include No Match) and if you want you can remove a result from the list using the `x` icon. On a *Partial* or *Exact Match* result, you can click the “**+**” icon and add the Application to the Upload Queue if desired.

![Alt text](/assets/images/Review_Match.png "Review Match Screenshot")


>### ℹ️ Note
>{: .no_toc }
>
> - You can remove unwanted results from the Results List by pressing the `x` button on the entry. 
> 
> - Once a matched application has been reviewed and added to the queue, you can edit the default configuration parameters by right-clicking on the queued item. When editing the application configuration, you can enable the text fields options by clicking the edit button next to the entry.


>### ℹ️ Scalability Info
>{: .no_toc }
> 
> Fetch has been tested by importing and processing application inventories of up to 5000 applications.

<br>
