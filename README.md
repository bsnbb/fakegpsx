# fakegpsx# FakeWalker X（初始工程）

这是一个 Android 原生 Java 项目骨架，面向 Android 15 / NoRoot 的开发者模拟位置测试。

## 已实现的初始功能
- 高德地图 SDK 页面（需要配置有效的 Android 地图 Key）
- 地图点击设置起点和终点，并绘制直线路线
- 直线路线的连续位置点模拟
- 速度、步频滑杆
- 屏幕内虚拟摇杆控制
- Android 系统模拟 GPS provider（需将本应用设置为“选择模拟位置信息应用”）

## 重要限制
1. 当前路线是起点到终点的直线，不是沿真实道路的导航路线；下一阶段再接入高德路线规划服务。
2. Android 系统会将通过测试 provider 发布的位置标记为模拟位置。部分第三方软件会检测并拒绝模拟位置；不能保证兼容所有地图、计步或运动软件。
3. 当前版本仅在应用前台更新位置，未实现锁屏后的持续后台模拟。
4. 步频目前用于估算速度和界面展示，不会注入真实硬件计步传感器事件；第三方计步软件未必会增加步数。
5. 高德 Key 必须由你在高德控制台创建，且需与应用包名 `com.fakewalkerx` 和实际签名 SHA-1 匹配。不要把正式 Key 公开提交到公开仓库。
6. 这是第一阶段源码骨架，尚未在你的手机上实机验证。构建前应先确认高德 SDK 版本可从配置的仓库解析；如果构建失败，按官方当前 SDK 文档调整依赖版本。

## 配置高德 Key
编辑 `app/src/main/AndroidManifest.xml`，把 `YOUR_AMAP_KEY` 替换成你的 Android 地图 Key。

官方入口：
- 高德开放平台：https://lbs.amap.com/
- Android 地图 SDK：https://lbs.amap.com/api/android-sdk/summary/
- Android 模拟位置 API：https://developer.android.com/reference/android/location/LocationManager

## 用 GitHub Actions 构建 APK（可用手机操作）
1. 在 GitHub 创建一个新仓库。
2. 上传本项目全部文件到仓库根目录。
3. 打开仓库的 Actions，运行 `Build Android APK`。
4. 成功后在构建记录的 Artifacts 中下载 `FakeWalkerX-debug-apk`。
5. 安装前先在手机“开发者选项 → 选择模拟位置信息应用”中选择 FakeWalker X。

如果高德地图显示空白，先检查 Key 的包名、SHA-1、服务类型和 SDK 版本。
