# Basic Information

|      |      |
|------|------|
| Name | PlatformListPage |
| Language | .java |
| Code Path | happycat/src/cn/sharesdk/onekeyshare/theme/skyblue/PlatformListPage.java |
| Package Name | cn.sharesdk.onekeyshare.theme.skyblue |
| Dependencies | ['android.os.AsyncTask', 'android.view.View', 'android.widget.GridView', 'android.widget.Toast', 'java.util.List', 'cn.sharesdk.framework.Platform', 'cn.sharesdk.framework.ShareSDK', 'cn.sharesdk.onekeyshare.PlatformListFakeActivity', 'com.mob.tools.utils.R.getLayoutRes', 'com.mob.tools.utils.R.getStringRes'] |
| Brief Description | The PlatformListPage class inherits from PlatformListFakeActivity and implements click event handling. View initialization includes back and confirm buttons, setting up the GridView adapter, and asynchronously loading platform data. Button clicks handle cancel and share logic, with share operations checking selected platforms and locking the button to prevent repeated clicks. |

# Description

The `PlatformListPage` class inherits from `PlatformListFakeActivity` and implements the `View.OnClickListener` interface, serving to display a list of sharing platforms. In the `onCreate` method, the layout is set and views are initialized. The `initView` method initializes the back and confirm buttons, sets click listeners, creates and configures a `GridView` adapter, and updates the adapter with platform list data fetched via an asynchronous task. The `onClick` method handles button click events, either canceling the operation or triggering sharing. The `onShareButtonClick` method validates the selected platform before executing the sharing logic and prompts the user if no platform is selected.

# Class Summary

| Name   | Type  | Description |
|-------|------|-------------|
| PlatformListPage | class | The PlatformListPage class inherits from PlatformListFakeActivity and implements click event handling. View initialization includes back and confirm buttons, with the GridView adapter asynchronously loading platform data. Button clicks handle cancel and share operations, verifying at least one platform is selected before sharing. |



## Class PlatformListPage

|      |      |
|------|------|
| Access Modifier | public |
| Type | class |
| Name | PlatformListPage |
| Description | The PlatformListPage class inherits from PlatformListFakeActivity and implements click event handling. View initialization includes back and confirm buttons, with the GridView adapter asynchronously loading platform data. Button clicks handle cancel and share operations, verifying at least one platform is selected before sharing. |


### UML Class Diagram

```mermaid
classDiagram
    class PlatformListPage {
        -PlatformGridViewAdapter gridViewAdapter
        +onCreate()
        -initView()
        +onClick(View v)
        -onShareButtonClick(View v)
    }

    class PlatformListFakeActivity {
        <<Interface>>
    }

    class View {
        <<Interface>>
        +setTag(Object tag)
        +setOnClickListener(OnClickListener l)
    }

    class OnClickListener {
        <<Interface>>
        +onClick(View v)
    }

    class PlatformGridViewAdapter {
        +setCustomerLogos(Object customerLogos)
        +setData(Platform[] platforms, Object hiddenPlatforms)
        +getCheckedItems() List~Object~
    }

    class AsyncTask~Void, Void, Platform[]~ {
        <<Interface>>
        +doInBackground(Void... params) Platform[]
        +onPostExecute(Platform[] platforms)
    }

    class ShareSDK {
        +getPlatformList() Platform[]
    }

    PlatformListPage --|> PlatformListFakeActivity : Inheritance
    PlatformListPage ..|> OnClickListener : Implementation
    PlatformListPage --> PlatformGridViewAdapter : Uses
    PlatformListPage --> View : Dependency
    PlatformListPage --> AsyncTask~Void, Void, Platform[]~ : Creates
    AsyncTask~Void, Void, Platform[]~ --> ShareSDK : Invokes
    PlatformGridViewAdapter --> Platform : Association
```

This code illustrates the implementation of a social sharing platform list page, primarily including platform list display, button click handling, and asynchronous loading of platform data. The PlatformListPage inherits from PlatformListFakeActivity and implements the OnClickListener interface, managing platform data display via PlatformGridViewAdapter and loading platform data asynchronously using AsyncTask. The class diagram clearly depicts inheritance, implementation, and dependency relationships between classes, including interactions with Android foundational components such as View and OnClickListener.


### Internal Method Call Graph

```mermaid
graph TD
    A["Class PlatformListPage"]
    B["Property: PlatformGridViewAdapter gridViewAdapter"]
    C["Method: onCreate()"]
    D["Method: initView()"]
    E["Method: onClick(View v)"]
    F["Method: onShareButtonClick(View v)"]
    G["Async Task: AsyncTask<Void,Void,Platform[]>"]
    H["Action: activity.setContentView"]
    I["Action: backImageView setup"]
    J["Action: okImageView setup"]
    K["Action: gridView set adapter"]
    L["Action: Execute async task"]
    M["Action: setCanceled(true) and finish()"]
    N["Action: onShareButtonClick(v)"]
    O["Action: Check checkedPlatforms"]
    P["Action: Toast prompt"]
    Q["Action: Call onShareButtonClick(v, checkedPlatforms)"]

    A --> B
    A --> C
    A --> D
    A --> E
    A --> F
    C --> H
    C --> D
    D --> I
    D --> J
    D --> K
    D --> G
    G --> L
    E --> M
    E --> N
    F --> O
    O -->|Empty list| P
    O -->|Non-empty| Q
```

This code illustrates the implementation flow of a platform list page class PlatformListPage. Key functionalities include view initialization, user click event handling, asynchronous loading of platform data, and share button click logic. By extending PlatformListFakeActivity and implementing the OnClickListener interface, this class manages grid view adapters, handles back and confirm button click events, and executes sharing operations after user platform selection. The async task retrieves platform list data, while the share button ensures operational correctness through state locking and input validation.

### Field List

| Name  | Type  | Description |
|-------|-------|------|
| gridViewAdapter | PlatformGridViewAdapter | Private platform grid view adapter instance. |

### Method List

| Name  | Type  | Description |
|-------|-------|------|
| onCreate | void | The method onCreate executes: calls the parent class's onCreate, sets the layout file skyblue_share_platform_list, and initializes the view initView. |
| onClick | void | Click Event Handling: Perform cancel or share operations based on view tags. Exit if the tag is invalid. Mark and terminate when canceling; call the share method when confirming. |
| initView | void | Initializing the view: Set click events and labels for the back and confirm buttons; configure the grid view adapter and load customer icons; asynchronously fetch the platform list and update the adapter data. |
| onShareButtonClick | void | The method `onShareButtonClick` handles the click of the share button: it checks if the adapter is not null and the button is not locked. If no platform is selected, it prompts a message, then locks the button and calls the reload method. |




