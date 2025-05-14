# 基础信息

|      |      |
|------|------|
| 名称 | LoginActivity |
| 编码语言 | .java |
| 代码路径 | happycat/src/com/happycat/LoginActivity.java |
| 包名 | com.happycat |
| 依赖项 | ['java.lang.reflect.Type', 'java.util.ArrayList', 'java.util.List', 'android.R.string', 'android.app.Activity', 'android.content.Intent', 'android.content.SharedPreferences', 'android.os.Bundle', 'android.util.Log', 'android.view.View', 'android.view.View.OnClickListener', 'android.widget.Button', 'android.widget.EditText', 'android.widget.Toast', 'com.example.happucat.R', 'com.google.gson.Gson', 'com.google.gson.reflect.TypeToken', 'com.happycat.Bean.User', 'com.happycat.Bean.goodsclassify', 'com.happycat.global.GlobalContacts', 'com.happycat.util.ActivitiyUtils', 'com.happycat.util.MyApplication', 'com.happycat.util.StringUtils', 'com.lidroid.xutils.HttpUtils', 'com.lidroid.xutils.exception.HttpException', 'com.lidroid.xutils.http.RequestParams', 'com.lidroid.xutils.http.ResponseInfo', 'com.lidroid.xutils.http.callback.RequestCallBack', 'com.lidroid.xutils.http.client.HttpRequest.HttpMethod'] |
| 概述说明 | 这是一个Android登录页面代码，包含手机号密码输入框，实现登录、注册、忘记密码功能。登录时验证用户信息，成功跳转主页面并保存用户状态，失败提示错误。 |

# 说明

该代码定义了一个名为LoginActivity的Android登录界面类，继承自Activity并实现了点击监听接口。类中包含手机号和密码输入框控件，以及用户信息存储相关变量。在onCreate方法中初始化界面布局和视图组件，设置多个按钮的点击监听事件。点击事件处理包括返回、注册、忘记密码和登录功能。登录时验证输入有效性，通过HTTP POST请求与服务器交互验证用户信息，成功登录后保存用户状态并跳转到主界面，失败则提示错误信息。整个过程涉及SharedPreferences存储、Gson解析和全局状态管理。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| LoginActivity | class | 这是一个安卓登录界面代码，包含手机号密码输入、注册、忘记密码功能，通过HTTP请求验证用户信息，登录成功跳转主页面并保存用户状态。 |



## 类 LoginActivity

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | LoginActivity |
| 说明 | 这是一个安卓登录界面代码，包含手机号密码输入、注册、忘记密码功能，通过HTTP请求验证用户信息，登录成功跳转主页面并保存用户状态。 |


### UML类图

```mermaid
classDiagram
    class Activity {
        <<Android>>
    }
    
    class OnClickListener {
        <<Interface>>
        +onClick(View v) void
    }
    
    class LoginActivity {
        -EditText et_phone
        -EditText et_password
        -String username
        -String password
        -int uid
        -SharedPreferences preferences
        -SharedPreferences.Editor editor
        -List~User~ userlist
        +onCreate(Bundle savedInstanceState) void
        -initView() void
        +onClick(View v) void
        -login(String username, String password) void
    }
    
    class User {
        // 用户数据模型类
    }
    
    class HttpUtils {
        +send(HttpMethod method, String url, RequestParams params, RequestCallBack~String~ callback) void
    }
    
    class RequestParams {
        +addQueryStringParameter(String key, String value) void
    }
    
    class RequestCallBack~R~ {
        <<Interface>>
        +onFailure(HttpException error, String msg) void
        +onSuccess(ResponseInfo~R~ responseInfo) void
    }
    
    class MyApplication {
        +saveLoginStatus(String status, int uid, String phone, String password, String address) void
        +String myflag
        +int SP_user_id
    }
    
    Activity <|-- LoginActivity
    OnClickListener <|.. LoginActivity
    LoginActivity --> User : 包含
    LoginActivity --> HttpUtils : 使用
    LoginActivity --> RequestParams : 构建参数
    LoginActivity --> MyApplication : 更新状态
    HttpUtils ..> RequestCallBack~String~ : 回调
```

该代码实现了一个Android登录界面，主要功能包括：初始化视图组件、处理用户点击事件、验证登录信息、通过HTTP请求与服务器交互。LoginActivity继承自Activity并实现OnClickListener接口，包含用户输入处理、网络请求（使用HttpUtils）、数据解析（Gson）和状态保存（MyApplication）等核心功能。类图展示了各组件间的依赖关系，特别是网络请求模块与回调机制的交互方式。


### 内部方法调用关系图

```mermaid
graph TD
    A["LoginActivity"]
    B["属性: EditText et_phone, et_password"]
    C["属性: String username, password"]
    D["属性: int uid"]
    E["属性: SharedPreferences preferences"]
    F["属性: List<User> userlist"]
    G["onCreate方法"]
    H["initView方法"]
    I["onClick方法"]
    J["login方法"]
    K["HTTP请求回调处理"]

    A --> B
    A --> C
    A --> D
    A --> E
    A --> F
    A --> G
    G -->|"super.onCreate"| G1["父类初始化"]
    G -->|"setContentView"| G2["设置布局"]
    G -->|"ActivitiyUtils.setActionBarLayout"| G3["设置标题栏"]
    G --> H
    H -->|"findViewById"| H1["绑定控件"]
    H -->|"setOnClickListener"| H2["设置5个按钮点击监听"]
    A --> I
    I -->|"switch(v.getId)"| I1["处理5种按钮事件"]
    I1 -->|"R.id.login_btn"| I2["调用login方法"]
    I1 -->|"其他按钮"| I3["跳转Activity或结束"]
    A --> J
    J -->|"HttpUtils.send"| J1["发起POST请求"]
    J -->|"RequestParams"| J2["设置请求参数"]
    J --> K
    K -->|"onSuccess"| K1["解析JSON保存用户数据"]
    K1 -->|"MyApplication.saveLoginStatus"| K2["保存登录状态"]
    K1 -->|"startActivity"| K3["跳转MainActivity"]
    K -->|"onFailure"| K4["显示错误提示"]
```

流程图描述：该流程图展示了Android登录功能的完整流程，从LoginActivity的初始化开始，包括视图绑定和事件监听设置。核心流程包含按钮点击事件分发（返回/注册/登录等操作），重点描述了登录按钮触发的网络请求过程：构造参数、发送POST请求、处理成功响应（解析JSON数据并跳转主界面）和失败处理（显示错误提示）。整个过程体现了从UI交互到网络通信的数据流转和状态管理。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| et_password | EditText | 定义两个EditText控件变量：et_phone和et_password。 |
| password | String | 声明字符串变量password |
| userlist = new ArrayList<User>() | List<User> | 创建存储用户对象的动态数组。 |
| username | String | 声明字符串变量username。 |
| preferences | SharedPreferences | 定义SharedPreferences对象preferences，用于存储轻量级键值对数据。 |
| uid | int | 整型变量uid，用于存储唯一标识符。 |
| editor | SharedPreferences.Editor | SharedPreferences.Editor用于修改SharedPreferences数据，提供键值对存储的编辑操作。 |

### 方法列表

| 名称  | 类型  | 说明 |
|-------|-------|------|
| onCreate | void | Android登录Activity的onCreate方法：调用父类方法、设置布局、自定义标题栏、初始化视图。 |
| initView | void | 初始化视图方法，绑定手机号、密码输入框及五个控件的点击事件监听器。 |
| onClick | void | 点击返回按钮关闭当前页面；点击注册、忘记密码或登录页注册按钮跳转对应页面；点击登录按钮验证输入后执行登录。 |
| login | void | 登录功能：获取用户名密码，POST请求验证，成功跳转主界面保存用户信息，失败提示错误。 |




