# 基础信息

|      |      |
|------|------|
| 名称 | LunboFragment |
| 编码语言 | .java |
| 代码路径 | happycat/src/com/happycay/fragments/LunboFragment.java |
| 包名 | com.happycay.fragments |
| 依赖项 | ['java.lang.reflect.Type', 'java.util.ArrayList', 'java.util.List', 'java.util.concurrent.Executors', 'java.util.concurrent.ScheduledExecutorService', 'java.util.concurrent.TimeUnit', 'org.apache.http.HttpResponse', 'org.apache.http.NameValuePair', 'org.apache.http.client.entity.UrlEncodedFormEntity', 'org.apache.http.client.methods.HttpPost', 'org.apache.http.impl.client.DefaultHttpClient', 'org.apache.http.message.BasicNameValuePair', 'org.apache.http.protocol.HTTP', 'org.apache.http.util.EntityUtils', 'org.json.JSONArray', 'org.json.JSONObject', 'com.example.happucat.R', 'com.google.gson.Gson', 'com.google.gson.reflect.TypeToken', 'com.happycat.MerchatDataActivity', 'com.happycat.Bean.Lunbobean', 'com.happycat.Bean.MerchatBean', 'com.happycat.util.MyApplication', 'com.lidroid.xutils.HttpUtils', 'com.lidroid.xutils.exception.HttpException', 'com.lidroid.xutils.http.ResponseInfo', 'com.lidroid.xutils.http.callback.RequestCallBack', 'com.lidroid.xutils.http.client.HttpRequest.HttpMethod', 'com.nostra13.universalimageloader.cache.disc.naming.Md5FileNameGenerator', 'com.nostra13.universalimageloader.core.ImageLoader', 'com.nostra13.universalimageloader.core.ImageLoaderConfiguration', 'com.nostra13.universalimageloader.core.assist.QueueProcessingType', 'android.content.Context', 'android.content.Intent', 'android.graphics.drawable.Drawable', 'android.os.AsyncTask', 'android.os.Bundle', 'android.os.Handler', 'android.os.Message', 'android.os.Parcelable', 'android.support.v4.view.PagerAdapter', 'android.support.v4.view.ViewPager', 'android.support.v4.view.ViewPager.OnPageChangeListener', 'android.util.AttributeSet', 'android.util.Log', 'android.view.LayoutInflater', 'android.view.View', 'android.view.ViewGroup', 'android.widget.FrameLayout', 'android.widget.ImageView', 'android.widget.ImageView.ScaleType', 'android.widget.LinearLayout'] |
| 概述说明 | LunboFragment实现轮播图功能，包含自动播放、点击跳转、网络图片加载及圆点指示器。使用ViewPager和定时任务控制切换，通过AsyncTask获取数据。 |

# 说明

LunboFragment是一个实现轮播图功能的Android自定义控件，继承自FrameLayout。主要功能包括：通过ViewPager展示网络图片轮播，支持自动轮播（默认5秒间隔）和手动滑动切换，底部显示圆点指示器。使用Universal Image Loader加载网络图片，通过异步任务从指定URL获取轮播数据（包含图片URL、商品ID、名称、价格等信息）。点击轮播图可跳转到商品详情页并传递相关参数。内部包含页面适配器、页面切换监听器和定时任务等组件，实现循环轮播和指示器状态同步。初始化时配置图片加载参数，并在销毁时释放资源。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| LunboFragment | class | LunboFragment实现轮播图功能，包含自动播放、图片加载、点击跳转及网络数据获取。 |



## 类 LunboFragment

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | LunboFragment |
| 说明 | LunboFragment实现轮播图功能，包含自动播放、图片加载、点击跳转及网络数据获取。 |


### UML类图

```mermaid
classDiagram
    class LunboFragment {
        -ImageLoader imageLoader
        -final int IMAGE_COUNT
        -final int TIME_INTERVAL
        -final boolean isAutoPlay
        -List~Integer~ p_ids
        -List~Lunbobean~ list
        -List~String~ mname
        -List~String~ longtime1
        -List~String~ mprice1
        -List~String~ tip1
        -List~String~ mimg1
        -List~String~ mtime1
        -List~String~ imageUrls
        -List~ImageView~ imageViewsList
        -List~View~ dotViewsList
        -ViewPager viewPager
        -int currentItem
        -ScheduledExecutorService scheduledExecutorService
        -Context context
        -String IP
        -String MyUrl
        -HttpPost httpRequest
        -Handler handler
        +LunboFragment(Context context)
        +LunboFragment(Context context, AttributeSet attrs)
        +LunboFragment(Context context, AttributeSet attrs, int defStyle)
        -startPlay()
        -stopPlay()
        -initData()
        -initUI(Context context)
        -destoryBitmaps()
        +initImageLoader(Context context)
    }

    class MyPagerAdapter {
        <<PagerAdapter>>
        -destroyItem(View container, int position, Object object)
        -instantiateItem(ViewGroup container, int position)
        -getCount()
        -isViewFromObject(View arg0, Object arg1)
        -restoreState(Parcelable arg0, ClassLoader arg1)
        -saveState()
        -startUpdate(View arg0)
        -finishUpdate(View arg0)
    }

    class MyPageChangeListener {
        <<OnPageChangeListener>>
        -boolean isAutoPlay
        -onPageScrollStateChanged(int arg0)
        -onPageScrolled(int arg0, float arg1, int arg2)
        -onPageSelected(int pos)
    }

    class SlideShowTask {
        <<Runnable>>
        -run()
    }

    class GetListTask {
        <<AsyncTask~String, Integer, Boolean~>>
        -doInBackground(String... params)
        -onPostExecute(Boolean result)
    }

    LunboFragment --> MyPagerAdapter : 包含
    LunboFragment --> MyPageChangeListener : 包含
    LunboFragment --> SlideShowTask : 包含
    LunboFragment --> GetListTask : 包含
    MyPagerAdapter --|> PagerAdapter : 实现
    MyPageChangeListener --|> OnPageChangeListener : 实现
    SlideShowTask --|> Runnable : 实现
    GetListTask --|> AsyncTask : 实现
```

这段代码实现了一个轮播图组件LunboFragment，继承自FrameLayout。主要功能包括：通过AsyncTask异步获取网络图片数据，使用ViewPager展示轮播图，支持自动轮播和手动滑动切换，通过圆点指示器显示当前页码。组件包含四个内部类：MyPagerAdapter处理页面适配，MyPageChangeListener监听页面切换，SlideShowTask实现自动轮播任务，GetListTask负责异步获取数据。整体采用MVC架构，数据获取与UI展示分离，通过Handler进行线程间通信。


### 内部方法调用关系图

```mermaid
graph TD
    A["类LunboFragment"]
    B["属性: ImageLoader imageLoader"]
    C["常量: IMAGE_COUNT=5, TIME_INTERVAL=5, isAutoPlay=true"]
    D["构造方法: LunboFragment(Context)"]
    E["构造方法: LunboFragment(Context, AttributeSet)"]
    F["构造方法: LunboFragment(Context, AttributeSet, int)"]
    G["核心方法: startPlay()"]
    H["核心方法: stopPlay()"]
    I["核心方法: initData()"]
    J["核心方法: initUI()"]
    K["内部类: MyPagerAdapter"]
    L["内部类: MyPageChangeListener"]
    M["内部类: SlideShowTask"]
    N["内部类: GetListTask"]
    O["辅助方法: initImageLoader()"]
    P["辅助方法: destoryBitmaps()"]

    A --> B
    A --> C
    A --> D
    A --> E
    A --> F
    A --> G
    A --> H
    A --> I
    A --> J
    A --> K
    A --> L
    A --> M
    A --> N
    A --> O
    A --> P

    D --> E --> F
    F --> I
    F -->|条件| G
    I --> N
    N --> J
    G --> M
    M -->|handler| J
    J --> K
    J --> L
```

这段代码实现了一个Android轮播图组件，主要功能包括：通过异步任务获取网络图片数据，初始化ViewPager和指示器，实现自动轮播和手动滑动切换功能。核心流程包含三个构造方法的链式调用，初始化时启动数据加载和自动轮播，通过Handler机制控制页面切换，使用ImageLoader加载网络图片，并实现了页面点击跳转功能。组件通过线程池定时任务实现自动轮播，同时处理了页面边界循环和指示器状态同步等细节。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| longtime1 | List<String> | 长时间存储的字符串列表变量longtime1。 |
| p_ids | List<Integer> | 私有整型列表p_ids，用于存储整数数据。 |
| TIME_INTERVAL = 5 | int | 定义私有静态常量TIME_INTERVAL，值为5。 |
| IMAGE_COUNT = 5 | int | 定义了一个私有静态常量IMAGE_COUNT，值为5。 |
| imageUrls | List<String> | 私有字符串列表，存储图片URL地址。 |
| scheduledExecutorService | ScheduledExecutorService | 私有定时任务执行服务 |
| list = new ArrayList<Lunbobean>() | List<Lunbobean> | 创建了一个存储Lunbobean对象的ArrayList列表。 |
| mprice1 | List<String> | 声明一个私有字符串列表变量mprice1。 |
| currentItem = 0 | int | 定义整型变量currentItem并初始化为0。 |
| imageLoader = ImageLoader.getInstance() | ImageLoader | 初始化ImageLoader单例实例。 |
| mimg1 | List<String> | 声明一个私有字符串列表变量mimg1。 |
| isAutoPlay = true | boolean | 私有静态常量isAutoPlay，值为true，表示自动播放开启。 |
| MyUrl = "http://" + IP + ":8080/happycat/GetUpload" | String | 定义字符串变量MyUrl，由HTTP协议、IP地址、端口8080和路径/happycat/GetUpload拼接而成。 |
| IP = MyApplication.getIp() | String | 获取应用IP地址并赋值给字符串变量IP。 |
| dotViewsList | List<View> | 私有视图列表，存储View对象，用于管理点状视图集合。 |
| tip1 | List<String> | 声明一个私有字符串列表变量tip1。 |
| imageViewsList | List<ImageView> | 定义私有图像视图列表变量imageViewsList。 |
| context | Context | 私有上下文变量context。 |
| viewPager | ViewPager | 私有视图分页控件viewPager |
| httpRequest = new HttpPost(MyUrl) | HttpPost | 创建HttpPost请求对象，目标URL为MyUrl。 |
| handler = new Handler() {		@Override		public void handleMessage(Message msg) {			// TODO Auto-generated method stub			super.handleMessage(msg);			viewPager.setCurrentItem(currentItem);		}	} | Handler | 定义Handler处理消息，设置ViewPager当前页。 |
| mtime1 | List<String> | 私有字符串列表变量mtime1。 |
| mname | List<String> | 声明一个私有字符串列表变量mname。 |

### 方法列表

| 名称  | 类型  | 说明 |
|-------|-------|------|
| stopPlay | void | 停止播放时关闭定时执行服务。 |
| initImageLoader | void | 初始化图片加载器配置：设置线程优先级、禁止缓存多尺寸图片、使用MD5生成缓存文件名、任务处理顺序为后进先出、开启调试日志，最后初始化ImageLoader实例。 |
| startPlay | void | 该方法启动一个单线程定时任务，初始延迟1秒后每隔4秒执行一次SlideShowTask。 |
| initUI | void | 初始化轮播图UI，检查图片URL列表，动态创建图片视图和指示点，设置ViewPager适配器和页面切换监听。 |
| initData | void | 初始化数据方法：创建多个空列表（ID、图片视图、点视图、图片URL、名称、时长、价格、提示、图片、时间），并启动异步任务获取数据。 |
| destoryBitmaps | void | 销毁位图资源：遍历图片视图列表，解除每个视图的Drawable引用以避免内存泄漏。 |




