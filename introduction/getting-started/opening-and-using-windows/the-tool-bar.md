---
description: Details on the main Tool Bar used in most windows.
---

# The Tool Bar

![The Application Menu and the Tool Bar that appears in most windows.](../../../.gitbook/assets/toolbarswing.PNG)

![The equivalent toolbar in the Web Application.](../../../.gitbook/assets/webui_toolbar%20%281%29.PNG)

Most windows are organized the same way in ADempiere. At the top of the window is a tool bar of icons, shown above, that is common across all Windows.

{% hint style="info" %}
While the Web Application and the Java Client are mostly similar, there are a few differences. Specifically, the web application:

* does not have both print and print-preview. In the Web Application there are the same thing so there is only one icon.
* does not have a Home icon. 
* does not have an Exit icon.
* does have a button to allow "quicksheet" entry
{% endhint %}

The details of the various toolbar icons follow:

| Client Icon | Web Icon | Function | Description |
| :--- | :--- | :--- | :--- |
| ![](../../../.gitbook/assets/undo24.gif) | ![](../../../.gitbook/assets/ignore24.webicon.png) | Undo | Reverts any changes made to the record since the last save. Enabled if there are changes to be saved. |
| ![](../../../.gitbook/assets/help24.gif) | ![](../../../.gitbook/assets/help24.webicon.png) | Help | Opens a help dialog where the field descriptions and help text are displayed. |
| ![](../../../.gitbook/assets/new24.gif) | ![](../../../.gitbook/assets/new24.webicon.png) | New | Creates a new record. Fields colored red are mandatory. They turn blue once data has been entered. Enabled if creating a new record is possible. |
| ![](../../../.gitbook/assets/delete24.gif) | ![](../../../.gitbook/assets/delete24.webicon.png) | Delete | Deletes the current record. Enabled if it is possible to delete the record. |
| ![](../../../.gitbook/assets/deleteselection24.gif) | ![](../../../.gitbook/assets/deleteselection24.webicon.png) | Delete Selection | Opens a dialog Listing all the records in the current tab. You can select all or a subset of these for deletion. It is helpful to use the Search function to limit the number of records. Enabled if it is possible to delete records. |
| ![](../../../.gitbook/assets/save24.gif) | ![](../../../.gitbook/assets/save24.webicon.png) | Save | Saves any changes to the current record. Saves are made automatically any time you move from record to record, tab to tab or close the window. Enabled if there are any changes to save. |
| ![](../../../.gitbook/assets/refresh24.gif) | ![](../../../.gitbook/assets/refresh24.webicon.png) | Requery | Requery the records using the last search criteria. Requery is useful if another process or user has added or changed the information in the table since the last search was performed or the tab was opened. |
| ![](../../../.gitbook/assets/find24.gif) | ![](../../../.gitbook/assets/find24.webicon.png) | [Lookup](http://wiki.adempiere.net/Lookup) | Lookup or search for records in the current tab. There is a basic search based on common fields and an advanced search where complex queries can be developed. See [Lookup](http://wiki.adempiere.net/Lookup) functionality for more information. |
| ![](../../../.gitbook/assets/attachment24d.gif) | ![](../../../.gitbook/assets/attachment24.webicon.png) | [Attachment](http://wiki.adempiere.net/Attachment) | Every record can have a file and/or notes added to it. See [Attachment](http://wiki.adempiere.net/Attachment) for more info.  If attachment already exist for the record, the icon will look yellow. ![](../../../.gitbook/assets/attachmentx24.gif) |
| ![](../../../.gitbook/assets/chat24.gif) | ![](../../../.gitbook/assets/chat24.webicon.png) | [Chat](http://wiki.adempiere.net/Chat) | Chat allows users to share a series of timestamped notes on the current record. |
| ![](../../../.gitbook/assets/multi24.gif) | ![](../../../.gitbook/assets/multi24.webicon.png) | Multi View | A toggle to switch from the form view to a multi-record spreadsheet style view. |
| ![](../../../.gitbook/assets/multix24.gif) | ![](../../../.gitbook/assets/multi24.webicon%20%281%29.png) | Form View | A toggle to switch from the multi-record view to a single-record view form view. |
| ![](../../../.gitbook/assets/history24.gif) | ![](../../../.gitbook/assets/historyx24.webicon.png) | [History](http://wiki.adempiere.net/History) | Shows the history for the selected record. |
| ![](../../../.gitbook/assets/home24.gif) | N/A | Home | Brings the main window to the front of the desktop. Useful for people with messy desks. |
| ![](../../../.gitbook/assets/parent24.gif) | ![](../../../.gitbook/assets/parent24.webicon.png) | Parent Record | Move up to or towards the parent tab of the current tab. Doesn't jump tabs. |
| ![](../../../.gitbook/assets/detail24.gif) | ![](../../../.gitbook/assets/detail24.webicon.png) | Detail Record | Move down to the next tab. |
| ![](../../../.gitbook/assets/first24.gif) | ![](../../../.gitbook/assets/first24.webicon.png) | First Record | Move to the first record in the current tab. |
| ![](../../../.gitbook/assets/previous24.gif) | ![](../../../.gitbook/assets/previous24.webicon.png) | Previous Record | Move to the previous record in the current tab. |
| ![](../../../.gitbook/assets/next24.gif) | ![](../../../.gitbook/assets/next24.webicon.png) | Next Record | Move to the next record in the current tab. |
| ![](../../../.gitbook/assets/last24.gif) | ![](../../../.gitbook/assets/last24.webicon.png) | Last Record | Move to the Last record in the current tab. |
| ![](../../../.gitbook/assets/report24.png) | ![](../../../.gitbook/assets/report24.webicon.png) | [Report](http://wiki.adempiere.net/Report) | Create a report based on the current record. |
| ![](../../../.gitbook/assets/archive24.gif) | ![](../../../.gitbook/assets/archive24.webicon.png) | [Archive](http://wiki.adempiere.net/Archived_Documents) | View archived reports or documents for the current record. See [Archived Documents](http://wiki.adempiere.net/Archived_Documents) for more information. |
| ![](../../../.gitbook/assets/printpreview24.gif) | N/A | Print Preview | Preview the defined print layout. See [Printing and Print Preview](http://wiki.adempiere.net/Printing_and_Print_Preview) for more information. |
| ![](../../../.gitbook/assets/print24.gif) | ![](../../../.gitbook/assets/print24.webicon.png) | Print | Print the defined print layout. See [Printing and Print Preview](http://wiki.adempiere.net/Printing_and_Print_Preview) for more information. |
| ![](../../../.gitbook/assets/zoomacross24.gif) | ![](../../../.gitbook/assets/zoomacross24.webicon.png) | [Zoom Across](http://wiki.adempiere.net/Zoom_Across) | Zoom to related records in other tables. For example, zoom to payments from invoices. See [Zoom Across](http://wiki.adempiere.net/Zoom_Across) for more information. |
| ![](../../../.gitbook/assets/workflow24.gif) | ![](../../../.gitbook/assets/workflow24.webicon.png) | Workflow | Opens the [**Workflow Process Window**](http://wiki.adempiere.net/ManPageW_WorkflowProcess). See [Workflow](http://wiki.adempiere.net/Workflow) for more information. |
| ![](../../../.gitbook/assets/request24.gif) | ![](../../../.gitbook/assets/request24.webicon.png) | Check [Requests](http://wiki.adempiere.net/Request) | Check or create Requests for service. See [Request](http://wiki.adempiere.net/Request) for more information. |
| ![](../../../.gitbook/assets/process24.gif) | ![](../../../.gitbook/assets/process24.webicon.png) | Process | Execute a predefined process associated with the displayed record. |
| ![](../../../.gitbook/assets/product24.gif) | ![](../../../.gitbook/assets/product24.webicon.png) | [Product Info](http://wiki.adempiere.net/Product_Info) | Open the Product Info page where information concerning a product's pricing and availability can be displayed. See [Product Info](http://wiki.adempiere.net/Product_Info) for more information. |
| ![](../../../.gitbook/assets/end24.gif) | N/A | Exit | Close the current window. The window's state is saved and if the window is reopened in the same session, the record and tab last viewed will be displayed. |
| N/A | ![](../../../.gitbook/assets/quickentry24.webicon.png) | Quick Entry | Opens a dialog where data can be entered much like a spreadsheet. |

