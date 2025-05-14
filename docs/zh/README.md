# happycat

## 概述  
该工程是Android移动开发生态中的复合型解决方案，核心定位为"社交化应用资源管理中枢"，整合了资源构建配置与跨平台分享能力两大维度。系统采用分层架构设计，下层通过R.java/BuildConfig.java实现资源调度（类似Maven依赖管理），上层依托ShareParams/SmartImage接口处理社交交互（类似Twitter SDK）。  

主要解决移动端开发中资源碎片化与社交功能集成问题，例如通过R.style统一管理144个Drawable资源，或使用OnekeyShare实现静默分享。架构特征呈现混合模式：资源模块采用静态编译的单体结构，而社交模块通过PlatformGridView等组件实现微服务化交互。核心资源包括R.java生成的ID索引库、WebImageCache缓存系统，以及集成的高德定位SDK等第三方服务。  

## 什么是HappyCat?  
该工程由资源管理引擎和社交功能框架构成双核模块。资源模块通过R.java建立类似字典树的ID映射体系，例如R.anim.dialog_in关联动画资源；社交模块则基于观察者模式实现，如ThemeShareCallback处理异步响应。模块间通过BuildConfig.DEBUG标志联动，形成"资源加载-界面渲染-用户交互"的闭环，类似App工厂的装配流水线。  

技术实现上，采用Gson解析FollowersResult等JSON数据，通过URLConnection实现WebImage网络加载。典型应用场景包括电商App的多语言切换（R.string）、社交平台的摇一摇分享功能。例如登录流程中，LoginActivity调用R.id控件渲染界面，同时使用HttpUtils发送验证码请求，最终通过SmartImageView加载用户头像，完整呈现移动应用的CRUD生命周期。

## 快速导航

### 👨‍💻 开发者
- [开发指南](summary/dev_guide.md) - 快速上手项目开发
- [模块说明](docs/_module.md) - 项目模块详细说明