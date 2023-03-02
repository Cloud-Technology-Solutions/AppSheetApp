# AppSheetApp

The AppSheetApp service lets you access the AppSheet API using Apps Script. The AppSheet API allows you to make the following changes to your AppSheet app:

- Add table records
- Delete table records
- Read a table record
- Update table records
- Invoke an action you have defined in AppSheet (limited to certain action types)

> **Note:** The AppSheet API is supported for Enterprise plans only.

## Enabling the AppSheet API

To use the AppSheetApp service you need to generate an Application Access Key for your AppSheet app. To do this read the reference documentation on [enabling the API](https://support.google.com/appsheet/answer/10105769).

## Setup

This project is already published as an Apps Script library, making it easy to include
in your project. To add it to your script, do the following in the Apps Script
code editor:

1. Click on the menu item "Resources > Libraries..."
2. In the "Find a Library" text box, enter the script ID
   `UPDATE_SCRIPT_ID` and click the "Select" button.
3. Choose a version in the dropdown box (usually best to pick the latest
   version).
4. Click the "Save" button.

Alternatively, you can copy and paste the `Code.gs` file
directly into your script project.

If you are [setting explicit scopes](https://developers.google.com/apps-script/concepts/scopes#setting_explicit_scopes)
in your manifest file, ensure that the following scope is included:

- `https://www.googleapis.com/auth/script.external_request`

### Connecting Apps Script to AppSheet and using the service

Before you can start making calls to your AppSheet app you need to use the `connect()` method to specify your app ID and Application Access Key. For security you may wish to store these values in the Property Service. Once you have connected to your app you can use methods to add, delete, read and update table records. The example below shows how to connect to your app and add two rows to a 'Staff' table:

```
/**
 * Example function for connecting your AppSheet app
 */
function addRowsToTable() {
    const AppSheet = AppSheetApp.connect('YOUR_APP_ID', 'YOUR_ACCESS_KEY');

    const rows = [
        {
            "FirstName": "Jan",
            "LastName": "Jones",
            "Age": 33,
            "Department": "Accounting",
        },
        {
            "FirstName": "Ian",
            "LastName": "Ivans",
            "Age": 22,
            "Department": "Payroll",
        }
    ];

    // Add rows to the 'Staff' table
    const resp = AppSheet.Add('Staff', rows);
    console.log(resp);
}
```

## Reference

For more detailed information on the data about the actions, properties, rows and responses, see the [AppSheet API reference documentation](https://support.google.com/appsheet/answer/10105768).

## Methods and Example

| Method                                                     | Description                            |
| :--------------------------------------------------------- | :------------------------------------- |
| [`connect(appId, applicationAccessKey)`](#connect)         | Connect to an AppSheet App.            |
| [`Add(tableName, rows, properties = {})`](#Add)            | Add records to a table.                |
| [`Delete(tableName, rows, properties = {})`](#Delete)      | Delete records from a table.           |
| [`Edit(tableName, rows, properties = {})`](#Edit)          | Update records in a table.             |
| [`Find(tableName, rows, properties = {})`](#Find)          | Read records from a table.             |
| [`Action(tableName, rows, properties = {})`](#Action)      | Invoke an action.                      |

<a name="connect"></a>

## connect(appId, applicationAccessKey) ⇒ <code>AppSheetApp</code>
Connect to an AppSheet App.

To enable the AppSheet API in your app:

1. Open the app in the app editor.
1. Select **Settings &gt; Integrations**.
1. Under **IN: from cloud services to your app**, click the **Enable** toggle. This enables the API for the application as a whole.
1. Ensure that at least one unexpired **Application Access Key** is present. Otherwise, click **Create Application Access Key**.
1. When you are done, save the app.
1. Use you app ID and Access Key to connect Apps Script to your app


```
const AppSheet = AppSheetApp.connect('YOUR_APP_ID', 'YOUR_ACCESS_KEY');
```

| Param | Type | Description |
| --- | --- | --- |
| `appId` | <code>String</code> | AppSheet App ID. |
| `applicationAccessKey` | <code>String</code> | AppSheet App Acess Key. |

<a name="Add"></a>

## Add(tableName, rows, properties) ⇒ <code>Object</code>
Add records to a table

| Param | Type | Description |
| --- | --- | --- |
| `tableName` | <code>String</code> | specifies the name of the table |
| `rows` | <code>Array.&lt;Object&gt;</code> | One or more Rows elements. Each individual Row value must normally include the key field values of the record to be added. However, if the key field contains an Initial value, you can omit the key field value. For example, you should omit the key field value when the key field has an Initial value of UNIQUEID() or RANDBETWEEN(). The system will initialize the key field to the Initial value. |
| `properties` | <code>Object</code> | **Optional**. Optional properties such as Locale, Location, Timezone, and UserId. [[Ref](https://support.google.com/appsheet/answer/10105398?hl=en#:~:text=for%20the%20table.-,Properties,-The%20properties%20of)] |

**Returns**: <code>Object</code> - AppSheet Response
<a name="Delete"></a>

## Delete(tableName, rows, properties) ⇒ <code>Object</code>
Delete records from a table

| Param | Type | Description |
| --- | --- | --- |
| `tableName` | <code>String</code> | specifies the name of the table |
| `rows` | <code>Array.&lt;Object&gt;</code> | One or more Rows elements to be deleted. Each Row value may contain field values of the key field values of the record to be deleted. |
| `properties` | <code>Object</code> | **Optional**. Optional properties such as Locale, Location, Timezone, and UserId. [[Ref](https://support.google.com/appsheet/answer/10105398?hl=en#:~:text=for%20the%20table.-,Properties,-The%20properties%20of)] |

**Returns**: <code>Object</code> - AppSheet Response

<a name="Edit"></a>

## Edit(tableName, rows, properties) ⇒ <code>Object</code>

Update records in a table

| Param | Type | Description |
| --- | --- | --- |
| `tableName` | <code>String</code> | specifies the name of the table |
| `rows` | <code>Array.&lt;Object&gt;</code> | One or more Row values to be updated. Each individual Row value must include the key field values of the record to be updated. |
| `properties` | <code>Object</code> | **Optional**. Optional properties such as Locale, Location, Timezone, and UserId. [[Ref](https://support.google.com/appsheet/answer/10105398?hl=en#:~:text=for%20the%20table.-,Properties,-The%20properties%20of)] |

**Returns**: <code>Object</code> - AppSheet Response

<a name="Find"></a>

## Find(tableName, rows, properties) ⇒ <code>Object</code>
Read records from a table

| Param | Type | Description |
| --- | --- | --- |
| `tableName` | <code>String</code> | specifies the name of the table |
| `rows` | <code>Array.&lt;Object&gt;</code> | **Optional**. You can omit the Selector property and specify input Rows containing the key values of the records to be read. |
| `properties` | <code>Object</code> | **Optional**. Optional properties such as Locale, Location, Timezone, and UserId. [[Ref](https://support.google.com/appsheet/answer/10105398?hl=en#:~:text=for%20the%20table.-,Properties,-The%20properties%20of)]. Additionaly the optional `Selector` property can used to specify an expression to select and format the rows returned [[Ref](https://support.google.com/appsheet/answer/10105770#:~:text=Read-,selected%20rows,-In%20the%20Selector)]. |

**Returns**: <code>Object</code> - AppSheet Response

<a name="Action"></a>

## Action(tableName, rows, action, properties) ⇒ <code>Object</code>
Invoke an action

| Param | Type | Description |
| --- | --- | --- |
| `tableName` | <code>String</code> | specifies the name of the table |
| `rows` | <code>Array.&lt;Object&gt;</code> | One or more Rows elements specifying the key field values of the rows to which the action is to be applied. |
| `action` | <code>String</code> | The action name. |
| `properties` | <code>Object</code> | **Optional**. Optional properties such as Locale, Location, Timezone, and UserId. [[Ref](https://support.google.com/appsheet/answer/10105398?hl=en#:~:text=for%20the%20table.-,Properties,-The%20properties%20of)] |

**Returns**: <code>Object</code> - AppSheet Response
