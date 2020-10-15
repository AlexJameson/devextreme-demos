Our **DataGrid** widget manages the edit state automatically. However, if your use case requires full control over editing, you can use the API members below to manage the state manually.

**Widget Options**

- **editing**.[editRowKey](/Documentation/ApiReference/UI_Widgets/dxDataGrid/Configuration/editing/#editRowKey)        
The key of the row being edited.

- **editing**.[editColumnName](/Documentation/ApiReference/UI_Widgets/dxDataGrid/Configuration/editing/#editColumnName)        
The name or data field of the column being edited.

- **editing**.[changes](/Documentation/ApiReference/UI_Widgets/dxDataGrid/Configuration/editing/#changes)       
Pending row changes.

You can get and set these options at runtime to access and change the edit state. In this demo, the [onOptionChanged](/Documentation/ApiReference/UI_Widgets/dxDataGrid/Configuration/#onOptionChanged) function gets the **editRowKey** and **changes** option values and displays them under the **DataGrid**.

**Utility Method**

- [DevExpress.data.applyChanges(data, changes, options)](/Documentation/ApiReference/Data_Layer/Utils/#applyChangesdata_changes_options)      
Applies an array of changes to a source data array.

**Event Handlers**

- [onSaving](/Documentation/ApiReference/UI_Widgets/dxDataGrid/Configuration/#onSaving) / [onSaved](/Documentation/ApiReference/UI_Widgets/dxDataGrid/Configuration/#onSaved)        
Functions that are called before / after pending row changes are saved from the UI or programmatically.

- [onEditCanceling](/Documentation/ApiReference/UI_Widgets/dxDataGrid/Configuration/#onEditCanceling) / [onEditCanceled](/Documentation/ApiReference/UI_Widgets/dxDataGrid/Configuration/#onEditCanceled)      
Functions that are called before / after editing is canceled and pending row changes are discarded.

Use these functions to perform custom actions. In this demo, the **onSaving** function sends pending changes to a server. The function's parameter `e` contains fields that can be useful for this functionality. To implement it in your application, follow these steps:

1. **Disable the built-in edit state management**       
Set the `e.cancel` field to **true**.

1. **Send a request to the server**      
Pending changes are stored in the `e.changes` array. It has only one element in all [edit modes](/Documentation/ApiReference/UI_Widgets/dxDataGrid/Configuration/editing/#mode), except batch. Check if this element is not empty and send it to the server.

1. **Apply the same changes to a local array**       
If the server successfully saves the changes, call the **applyChanges** method to save the same changes in a local array.

1. **Update the widget's data source and reset the edit state**         
Assign the local array to the [dataSource](/Documentation/ApiReference/UI_Widgets/dxDataGrid/Configuration/#dataSource), **null** to the **editRowKey**, and an empty array to the **changes** option.

[note] This functionality is available as a <a href="https://www.devexpress.com/aboutus/pre-release.xml" target="_blank">community technology preview (CTP)</a>. Should you have any questions or suggestions prior to its official release, please email your comments to <a href="mailto:support@devexpress.com">support@devexpress.com</a>.