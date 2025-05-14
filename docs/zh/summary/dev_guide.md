[回到首页](../README.md)



## 工程结构

```text
happycat/
├── AndroidManifest.xml  # 应用清单文件（Android标准）
├── project.properties   # 项目配置文件（Eclipse ADT）
├── proguard-project.txt # 混淆配置文件
├── ic_launcher-web.png  # Web版应用图标
├── .project            # Eclipse项目文件
├── README.md           # 项目说明文档
├── .classpath          # Eclipse类路径配置
├── gen/                # 自动生成文件目录（R.java等）
│   └── com/example/happucat/
│       ├── R.java         # 资源ID映射
│       └── BuildConfig.java # 构建配置
├── .settings/          # IDE配置目录（Eclipse）
│   ├── org.eclipse.jdt.core.prefs
│   └── org.eclipse.core.resources.prefs
├── res/                # 资源文件目录（Android标准）
│   ├── layout/         # 布局文件（含50+业务页面）
│   ├── values-*/       # 多维度资源适配（v14/sw600dp等）
│   ├── drawable-*/     # 多分辨率图片资源（hdpi/xhdpi等）
│   ├── menu/           # 菜单定义文件
│   ├── anim/           # 动画资源
│   └── color/          # 颜色定义
├── bin/                # 编译输出目录（Eclipse）
│   ├── classes/        # 编译后的Java类
│   └── res/            # 处理后的资源文件
├── src/                # 源代码目录
│   ├── cn/sharesdk/    # 社会化分享SDK集成
│   ├── image/          # 图片加载模块
│   └── com/happycat/   # 主业务代码
│       ├── activities/    # 活动页面（未明确分层）
│       ├── adapter/       # 列表适配器
│       ├── Bean/          # 数据模型
│       └── util/          # 工具类
├── assets/             # 原始资源文件（ShareSDK配置）
└── libs/               # 第三方库
    ├── *.jar           # 依赖库（ShareSDK/gson等）
    └── armeabi/        # SO库目录
```

命名规约：
- 采用小写蛇形命名（如activity_my_order.xml）
- 资源文件前缀标识类型（如ic_/bg_）
- 包名采用反向域名（com.example.happucat）

分层结构：
1. 基础层：libs/assets 包含第三方依赖
2. 资源层：res/ 集中管理UI资源
3. 业务层：src/ 按功能模块组织，但未严格遵循MVVM
4. 生成层：gen/ 由系统自动维护

扩展设计：
1. 多分辨率适配：drawable-*/values-* 目录体系
2. 模块化设计：独立分享模块（cn.sharesdk）
3. 配置分离：proguard-project.txt 支持灵活混淆
4. 本地化支持：values/strings.xml 多语言扩展点

注：存在可优化点：
- src/com/happycat 目录可进一步按功能分包
- 业务逻辑与UI未完全解耦（如Activity含大量业务代码）
- 缺少明确的网络层目录结构