# 基础信息

|      |      |
|------|------|
| 名称 | FollowListPage |
| 编码语言 | .java |
| 代码路径 | happycat/src/cn/sharesdk/onekeyshare/theme/classic/FollowListPage.java |
| 包名 | cn.sharesdk.onekeyshare.theme.classic |
| 依赖项 | ['android.app.Activity', 'android.content.Context', 'android.graphics.Bitmap', 'android.graphics.BitmapFactory', 'android.graphics.Canvas', 'android.os.Handler.Callback', 'android.os.Message', 'android.util.TypedValue', 'android.view.Gravity', 'android.view.View', 'android.view.View.OnClickListener', 'android.view.ViewGroup', 'android.widget.AdapterView', 'android.widget.AdapterView.OnItemClickListener', 'android.widget.FrameLayout', 'android.widget.ImageView', 'android.widget.LinearLayout', 'android.widget.LinearLayout.LayoutParams', 'android.widget.ProgressBar', 'android.widget.TextView', 'java.util.ArrayList', 'java.util.HashMap', 'cn.sharesdk.framework.Platform', 'cn.sharesdk.framework.PlatformActionListener', 'cn.sharesdk.framework.TitleLayout', 'com.mob.tools.gui.AsyncImageView', 'com.mob.tools.gui.BitmapProcessor', 'com.mob.tools.gui.PullToRefreshListAdapter', 'com.mob.tools.gui.PullToRefreshView', 'com.mob.tools.utils.UIHandler', 'cn.sharesdk.onekeyshare.FollowerListFakeActivity', 'com.mob.tools.utils.R.dipToPx', 'com.mob.tools.utils.R.getBitmapRes', 'com.mob.tools.utils.R.getStringRes'] |
| 概述说明 | FollowListPage类实现关注列表页面，包含标题栏、下拉刷新列表和复选框功能，支持单选多选模式，适配不同平台显示样式。 |

# 说明

该代码定义了一个社交平台的关注列表页面类FollowListPage，继承自FollowerListFakeActivity并实现了点击监听接口。页面包含标题栏、下拉刷新列表和阴影效果。标题栏有返回按钮和完成按钮，列表使用自定义适配器FollowAdapter加载关注用户数据，支持单选/多选模式。适配器处理分页加载、异步图片显示和状态更新，列表项包含头像、用户名、简介和勾选框。下拉刷新功能由PRTHeader实现，包含箭头动画和进度条。RotateImageView提供旋转动画效果。整体实现了关注列表的展示、选择和刷新功能。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| FollowListPage | class | FollowListPage类实现关注列表页面，包含标题栏、下拉刷新列表和适配器逻辑，支持单选/多选功能。适配器处理数据加载、列表项渲染及用户交互。 |



## 类 FollowListPage

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | FollowListPage |
| 说明 | FollowListPage类实现关注列表页面，包含标题栏、下拉刷新列表和适配器逻辑，支持单选/多选功能。适配器处理数据加载、列表项渲染及用户交互。 |


### UML类图

```mermaid
classDiagram
    class FollowListPage {
        -TitleLayout llTitle
        -FollowAdapter adapter
        -int lastPosition
        +onCreate()
        +onClick(View v)
        +onItemClick(AdapterView~?~ parent, View view, int position, long id)
    }

    class FollowerListFakeActivity {
        <<Interface>>
    }

    class OnClickListener {
        <<Interface>>
        +onClick(View v)
    }

    class OnItemClickListener {
        <<Interface>>
        +onItemClick(AdapterView~?~ parent, View view, int position, long id)
    }

    class FollowAdapter {
        -int FOLLOW_LIST_EMPTY
        -int curPage
        -ArrayList~Following~ follows
        -HashMap~String, Boolean~ map
        -boolean hasNext
        -Platform platform
        -PRTHeader llHeader
        -Bitmap bmChd
        -Bitmap bmUnch
        +FollowAdapter(PullToRefreshView view)
        +setPlatform(Platform platform)
        +getView(int position, View convertView, ViewGroup parent) View
        +getItem(int position) Following
        +getItemId(int position) long
        +getCount() int
        +getHeaderView() View
        +onPullDown(int percent)
        +onRequest()
        +onCancel(Platform plat, int action)
        +onComplete(Platform plat, int action, HashMap~String, Object~ res)
        +onError(Platform plat, int action, Throwable t)
        +handleMessage(Message msg) boolean
        +onReversed()
    }

    class PlatformActionListener {
        <<Interface>>
        +onCancel(Platform plat, int action)
        +onComplete(Platform plat, int action, HashMap~String, Object~ res)
        +onError(Platform plat, int action, Throwable t)
    }

    class Callback {
        <<Interface>>
        +handleMessage(Message msg) boolean
    }

    class PullToRefreshListAdapter {
        <<Interface>>
    }

    class FollowListItem {
        +AsyncImageView aivIcon
        +TextView tvName
        +TextView tvSign
        +ImageView ivCheck
    }

    class PRTHeader {
        -TextView tvHeader
        -RotateImageView ivArrow
        -ProgressBar pbRefreshing
        +PRTHeader(Context context)
        +onPullDown(int percent)
        +onRequest()
        +reverse()
    }

    class RotateImageView {
        -int rotation
        +RotateImageView(Context context)
        +setRotation(int degree)
        +onDraw(Canvas canvas)
    }

    FollowListPage --|> FollowerListFakeActivity : 继承
    FollowListPage ..|> OnClickListener : 实现
    FollowListPage ..|> OnItemClickListener : 实现
    FollowAdapter --|> PullToRefreshListAdapter : 继承
    FollowAdapter ..|> PlatformActionListener : 实现
    FollowAdapter ..|> Callback : 实现
    FollowAdapter --> FollowListItem : 包含
    FollowAdapter --> PRTHeader : 包含
    PRTHeader --> RotateImageView : 包含
```

这段代码展示了一个社交应用中关注列表页面的实现。FollowListPage作为主类，继承自FollowerListFakeActivity并实现了点击监听接口，负责页面布局和用户交互。核心组件FollowAdapter继承自PullToRefreshListAdapter，实现了下拉刷新功能，并处理关注列表数据的获取与展示。PRTHeader和RotateImageView共同实现了下拉刷新时的动画效果。整个设计采用了组合模式，通过多个嵌套类协同工作，实现了关注列表的完整功能，包括数据加载、列表展示、选择操作和下拉刷新等特性。


### 内部方法调用关系图

```mermaid
graph TD
    A["类FollowListPage"]
    B["属性: TitleLayout llTitle"]
    C["属性: FollowAdapter adapter"]
    D["属性: int lastPosition"]
    E["方法: void onCreate()"]
    F["方法: void onClick(View v)"]
    G["方法: void onItemClick(AdapterView<?>, View, int, long)"]
    H["内部类: FollowAdapter"]
    I["内部类: FollowListItem"]
    J["内部类: PRTHeader"]
    K["内部类: RotateImageView"]

    A --> B
    A --> C
    A --> D
    A --> E
    A --> F
    A --> G
    A --> H
    H --> I
    H --> J
    J --> K

    E --> E1["创建LinearLayout页面容器"]
    E --> E2["设置标题栏布局和事件"]
    E --> E3["添加下拉刷新列表视图"]
    E --> E4["初始化FollowAdapter并绑定数据"]
    E --> E5["触发首次数据加载"]

    F --> F1["处理右侧按钮点击事件"]
    F --> F2["收集选中项并返回结果"]
    F --> F3["关闭当前Activity"]

    G --> G1["处理列表项点击选择状态"]
    G --> G2["更新adapter数据变更"]

    H --> H1["实现分页加载逻辑"]
    H --> H2["处理平台回调事件"]
    H --> H3["管理列表项视图复用"]
```

这段代码实现了一个社交关注列表页面，主要包含页面布局构建、下拉刷新功能、列表项选择交互以及数据分页加载等核心功能。流程图展示了类结构关系，其中FollowListPage作为主类，通过内部类FollowAdapter处理复杂的数据绑定和分页逻辑，PRTHeader实现自定义下拉刷新头部，RotateImageView提供箭头旋转动画。整个流程从页面初始化开始，通过适配器管理数据加载和视图更新，最终实现完整的关注列表交互功能。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| lastPosition = -1 | int | 变量lastPosition初始值为-1，用于记录最后位置。 |
| llTitle | TitleLayout | 私有标题布局变量llTitle |
| adapter | FollowAdapter | 私有成员变量adapter，类型为FollowAdapter。 |

### 方法列表

| 名称  | 类型  | 说明 |
|-------|-------|------|
| onClick | void | 点击右按钮时，收集选中项名称并返回结果，最后关闭界面。 |
| onCreate | void | 创建垂直布局页面，设置标题栏和返回按钮，添加可刷新列表视图并加载数据。 |
| onItemClick | void | 点击列表项时，若为单选模式则取消上次选中项并记录当前位置；切换当前项选中状态并刷新列表。 |




