# Basic Information

|      |      |
|------|------|
| Name | ActivitiyUtils |
| Language | .java |
| Code Path | happycat/src/com/happycat/util/ActivitiyUtils.java |
| Package Name | com.happycat.util |
| Dependencies | ['android.app.ActionBar', 'android.app.Activity', 'android.app.ActionBar.LayoutParams', 'android.content.Context', 'android.view.LayoutInflater', 'android.view.View'] |
| Brief Description | The ActivityUtils class provides two static methods: setActionBarLayout for customizing the ActionBar layout, and finish for closing the Activity. |

# Description

The ActivityUtils class contains two static methods. The setActionBarLayout method is used to configure a custom layout for the ActionBar, including disabling default display options, loading a specified layout file via LayoutInflater, setting full-screen layout parameters, and applying the custom view. The finish method is used to terminate the current Activity, with commented-out code for page transition animations. Both methods include null safety checks or directly call system APIs.

# Class Summary

| Name   | Type  | Description |
|-------|------|-------------|
| ActivitiyUtils | class | The ActivityUtils class provides two static methods: setActionBarLayout for customizing the ActionBar layout, and finish for terminating an Activity. |



## Class ActivitiyUtils

|      |      |
|------|------|
| Access Modifier | public |
| Type | class |
| Name | ActivitiyUtils |
| Description | The ActivityUtils class provides two static methods: setActionBarLayout for customizing the ActionBar layout, and finish for terminating an Activity. |


### UML Class Diagram

```mermaid
classDiagram
    class ActivityUtils {
        +setActionBarLayout(ActionBar actionBar, Context context, int layoutId) void
        +finish(Activity activity) void
    }

    class ActionBar {
        +setDisplayShowHomeEnabled(boolean showHome) void
        +setDisplayShowCustomEnabled(boolean showCustom) void
        +setDisplayShowTitleEnabled(boolean showTitle) void
        +setCustomView(View view, ActionBar~LayoutParams~ layout) void
    }

    class Context {
        <<Interface>>
    }

    class Activity {
        +finish() void
    }

    class LayoutInflater {
        +from(Context context) LayoutInflater
        +inflate(int resource, ViewGroup root) View
    }

    class View {
    }

    class ActionBar~LayoutParams~ {
        +ActionBar~LayoutParams~(int width, int height)
    }

    ActivityUtils --> ActionBar : "uses"
    ActivityUtils --> Context : "depends on"
    ActivityUtils --> Activity : "invokes"
    ActivityUtils --> LayoutInflater : "creates"
    LayoutInflater --> View : "generates"
    ActionBar --> ActionBar~LayoutParams~ : "uses"
```

Class diagram description: This diagram illustrates the structure of the ActivityUtils utility class and its associations. ActivityUtils provides two static methods: setActionBarLayout for customizing ActionBar layout (dependent on ActionBar, Context, and LayoutInflater), and finish for closing an Activity. ActionBar uses LayoutParams to configure custom view parameters, while LayoutInflater converts XML layouts into View objects. All classes are connected through clear dependency relationships, demonstrating a typical pattern for Android UI control.


### Internal Method Call Graph

```mermaid
graph TD
    A["Class ActivityUtils"]
    B["Static method: setActionBarLayout(ActionBar, Context, int)"]
    C["Check actionBar not null"]
    D["Set actionBar property: setDisplayShowHomeEnabled(false)"]
    E["Set actionBar property: setDisplayShowCustomEnabled(true)"]
    F["Set actionBar property: setDisplayShowTitleEnabled(false)"]
    G["Create LayoutInflater: LayoutInflater.from(context)"]
    H["Inflate layout: inflator.inflate(layoutId, null)"]
    I["Create LayoutParams: ActionBar.LayoutParams(MATCH_PARENT, MATCH_PARENT)"]
    J["Set custom view: actionBar.setCustomView(v, layout)"]
    K["Static method: finish(Activity)"]
    L["Finish Activity: activity.finish()"]
    M["Commented-out transition animation settings"]

    A --> B
    B --> C
    C -->|Yes| D
    D --> E
    E --> F
    F --> G
    G --> H
    H --> I
    I --> J
    C -->|No| K
    A --> K
    K --> L
    L -.-> M
```

This flowchart illustrates two core functionalities of the ActivityUtils utility class: 1) The configuration process for custom ActionBar layouts, including null checks, property settings, view inflation, and parameter configuration; 2) The Activity termination method and its commented-out transition animation settings. The diagram clearly presents conditional branches and sequential call relationships, particularly showcasing the complete procedure from parameter validation to final view setup in the setActionBarLayout method, as well as the simple call chain of the finish method.

### Field List

| Name  | Type  | Description |
|-------|-------|------|

### Method List

| Name  | Type  | Description |
|-------|-------|------|
| setActionBarLayout | void | Set a custom layout for the ActionBar, disable the default title and icon, enable the custom view, and inflate the specified layout. |
| finish | void | The static method `finish` is used to close the specified Activity, with the option to add transition animations (commented out in the example). |




