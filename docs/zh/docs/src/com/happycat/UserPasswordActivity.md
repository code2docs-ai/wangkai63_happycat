# 基础信息

|      |      |
|------|------|
| 名称 | UserPasswordActivity |
| 编码语言 | .java |
| 代码路径 | happycat/src/com/happycat/UserPasswordActivity.java |
| 包名 | com.happycat |
| 依赖项 | ['com.example.happucat.R', 'com.happycat.util.ActivitiyUtils', 'com.happycat.util.MyApplication', 'com.lidroid.xutils.HttpUtils', 'com.lidroid.xutils.exception.HttpException', 'com.lidroid.xutils.http.RequestParams', 'com.lidroid.xutils.http.ResponseInfo', 'com.lidroid.xutils.http.callback.RequestCallBack', 'com.lidroid.xutils.http.client.HttpRequest.HttpMethod', 'com.lidroid.xutils.http.client.entity.UploadEntity', 'android.app.Activity', 'android.content.Intent', 'android.os.Bundle', 'android.util.Log', 'android.view.View', 'android.view.View.OnClickListener', 'android.widget.Button', 'android.widget.EditText', 'android.widget.ImageButton', 'android.widget.TextView', 'android.widget.Toast'] |
| 概述说明 | 用户密码修改活动类，包含旧密码、新密码输入框及确认按钮，验证密码一致性后提交至服务器修改，处理成功或失败提示。 |

# 说明

UserPasswordActivity是一个用于修改用户密码的Android活动类。界面包含三个文本输入框（旧密码、新密码、确认新密码）、四个文本标签、一个修改密码按钮和一个返回按钮。点击返回按钮会跳转至UserActivity并结束当前活动。修改密码时，会验证旧密码是否正确、新密码是否一致，通过后发送HTTP POST请求到服务器进行密码更新，请求参数包括用户手机号和新密码。操作结果通过Toast提示用户，包括网络错误、密码不一致、修改成功或失败等状态。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| UserPasswordActivity | class | 用户密码修改活动类，包含界面初始化、密码验证、网络请求功能，处理旧密码校验、新密码一致性检查及修改结果反馈。 |



## 类 UserPasswordActivity

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | UserPasswordActivity |
| 说明 | 用户密码修改活动类，包含界面初始化、密码验证、网络请求功能，处理旧密码校验、新密码一致性检查及修改结果反馈。 |


### UML类图

```mermaid
classDiagram
    class UserPasswordActivity {
        -TextView t1
        -TextView t2
        -TextView t3
        -TextView t4
        -EditText et1
        -EditText et2
        -EditText et3
        -Button xgPassword
        -ImageButton fanhui
        -String xinpsd1
        -String xinpsd2
        -String jiupsd
        +void onCreate(Bundle savedInstanceState)
        -void initView()
        -void Tool()
        -void password()
    }

    class Activity {
        <<Interface>>
    }

    class OnClickListener {
        <<Interface>>
        +void onClick(View view)
    }

    class HttpUtils {
        +void send(HttpMethod method, String url, RequestParams params, RequestCallBack~String~ callback)
    }

    class RequestCallBack~T~ {
        <<Interface>>
        +void onFailure(HttpException error, String msg)
        +void onSuccess(ResponseInfo~T~ responseInfo)
    }

    UserPasswordActivity --> Activity : 继承
    UserPasswordActivity --> OnClickListener : 实现
    UserPasswordActivity --> HttpUtils : 调用
    HttpUtils --> RequestCallBack~String~ : 回调
```

这段代码展示了一个Android用户密码修改活动（UserPasswordActivity），继承自Activity基类。主要功能包括：初始化视图组件（TextView、EditText、Button等），处理返回按钮点击事件，验证旧密码与新密码一致性，通过HttpUtils发起网络请求修改密码，并使用Toast显示操作结果。类图清晰地反映了其与Activity的继承关系、OnClickListener接口的实现，以及通过HttpUtils进行网络通信的协作流程。密码修改逻辑包含多层验证，确保操作安全性和用户提示完整性。


### 内部方法调用关系图

```mermaid
graph TD
    A["UserPasswordActivity"]
    B["onCreate"]
    C["initView"]
    D["findViewById 初始化控件"]
    E["设置fanhui点击监听"]
    F["设置xgPassword点击监听"]
    G["Tool方法: 获取输入密码"]
    H["password方法: 发送修改请求"]
    I["HttpUtils.send POST请求"]
    J["RequestCallBack处理响应"]

    A --> B
    B -->|"super.onCreate/setContentView"| C
    C --> D
    C --> E
    C --> F
    F -->|"点击事件"| G
    G -->|"验证密码逻辑"| H
    H --> I
    I --> J
    E -->|"点击返回"| K["finish活动"]
```

```mermaid
sequenceDiagram
    participant User
    participant UserPasswordActivity
    participant HttpUtils
    participant Server

    User->>UserPasswordActivity: 输入密码并点击修改
    UserPasswordActivity->>UserPasswordActivity: Tool()获取输入值
    alt 旧密码为空
        UserPasswordActivity->>User: 显示"请输入密码"
    else 旧密码错误
        UserPasswordActivity->>User: 显示"当前密码错误"
    else 新密码不一致
        UserPasswordActivity->>User: 显示"前后密码不一致"
    else 验证通过
        UserPasswordActivity->>HttpUtils: 构建RequestParams
        HttpUtils->>Server: POST /User
        Server-->>HttpUtils: 返回结果
        alt 请求成功
            HttpUtils->>UserPasswordActivity: onSuccess("success")
            UserPasswordActivity->>User: 显示"密码修改成功"
        else 请求失败
            HttpUtils->>UserPasswordActivity: onFailure()
            UserPasswordActivity->>User: 显示"请检查网络"
        end
    end
```

该流程图描述了Android密码修改功能的完整执行过程，从活动初始化到界面控件绑定，再到密码验证逻辑和网络请求处理。时序图重点展示了用户交互、本地验证和网络通信三个关键阶段，包括输入验证、密码比对、HTTP请求发送以及响应处理的全链路流程，其中包含4种验证分支和2种网络请求结果状态。整个流程涉及7个核心步骤和3个异常处理路径，典型体现了移动端表单提交的数据流控制模式。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| xgPassword | Button | 按钮变量xgPassword |
| et3 | EditText | 定义了三个EditText控件变量：et1、et2、et3。 |
| t4 | TextView | 定义了四个TextView变量：t1、t2、t3、t4。 |
| jiupsd | String | 声明三个字符串变量：新密码1、新密码2、旧密码。 |
| fanhui | ImageButton | 返回按钮控件 |

### 方法列表

| 名称  | 类型  | 说明 |
|-------|-------|------|
| Tool | void | 获取三个输入框的文本内容并去除前后空格，分别赋值给新密码1、新密码2和旧密码变量。 |
| password | void | 该方法用于修改用户密码，通过POST请求发送手机号和新密码到服务器，返回成功或失败提示。 |
| initView | void | 初始化视图组件，设置密码修改逻辑：验证旧密码、新密码一致性，错误提示，成功则提交并关闭页面。 |
| onCreate | void | Android Activity的onCreate方法：调用父类方法、设置布局、初始化自定义标题栏和视图。 |




