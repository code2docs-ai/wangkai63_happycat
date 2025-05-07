[回到首页](../README.md)



## 工程结构

```
happycat/
├── AndroidManifest.xml  # 应用清单文件（Android标准）
├── project.properties  # 项目配置（ADT生成文件）
├── proguard-project.txt  # 代码混淆配置
├── ic_launcher-web.png  # Web版应用图标
├── .project  # Eclipse项目文件
├── README.md  # 项目说明文档
├── .classpath  # Eclipse类路径配置
├── gen/  # 自动生成代码目录
│   └── com/example/happucat/
│       ├── R.java  # 资源ID索引（AAPT生成）
│       └── BuildConfig.java  # 构建配置
├── .settings/  # IDE配置目录（Eclipse）
│   ├── org.eclipse.jdt.core.prefs
│   └── org.eclipse.core.resources.prefs
├── res/  # 资源文件目录（Android标准）
│   ├── layout/  # 界面布局文件（含40+业务页面）
│   ├── values/  # 字符串/样式等配置
│   ├── drawable*/  # 多分辨率图片资源
│   ├── menu/  # 菜单定义
│   └── anim/  # 动画效果
├── bin/  # 构建输出目录（ADT生成）
│   ├── classes/  # 编译后的Java类
│   └── res/  # 处理后的资源文件
├── src/  # 源代码目录
│   └── com/happycat/  # 主业务代码包
│       ├── *Activity.java  # 各功能Activity（约30个）
│       ├── adapter/  # 列表适配器
│       └── Bean/  # 数据模型
├── assets/  # 原始资源文件（ShareSDK配置）
├── libs/  # 第三方库
│   ├── *.jar  # 包括ShareSDK/高德地图等
│   └── armeabi/  # SO库文件
└── .git/  # Git版本控制目录（标准结构）
```

命名规约：
- 采用小写+下划线风格（如activity_main.xml）
- 资源文件前缀标识功能（如title_bar_*.xml）
- 包名遵循com.公司.项目结构

分层结构：
1. 视图层：res/layout + Activity类
2. 逻辑层：src/com/happycat/*Activity
3. 数据层：src/com/happycat/Bean + 网络请求
4. 适配器层：独立adapter目录

扩展设计：
1. 多分辨率支持：drawable-*dpi分级
2. 模块化设计：按功能分包（如wallet/order）
3. 第三方集成：libs包含社交/地图等SDK
4. 配置分离：ShareSDK.xml独立存放