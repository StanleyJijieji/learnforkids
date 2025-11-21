## 项目概况
- 框架：Flutter（存在 `pubspec.yaml`、`lib/main.dart`、`ios/`、`android/`）
- Android 配置：`compileSdkVersion 34`、`minSdkVersion 21`、`applicationId vdrs.sappu.lafk.learn`（android/app/build.gradle:32、57、54）
- Android 构建工具：AGP 8.1.0 与 Kotlin 1.9.0（android/build.gradle:9、2）
- iOS 配置：`IPHONEOS_DEPLOYMENT_TARGET = 11.0`、`PRODUCT_BUNDLE_IDENTIFIER = vdrs.sappu.lafk.learn`（ios/Runner.xcodeproj/project.pbxproj:348、370）
- 依赖与资源：Dart SDK `>=3.2.0`（pubspec.yaml:21），声明了多目录资源与自定义字体（pubspec.yaml:74–91、104–107）

## 编译前准备
- 安装与检查
  - 安装 Flutter（stable，建议 3.22+）与 Dart；`flutter --version`、`dart --version`
  - Android：安装 Android Studio、SDK 34、JDK 17 并设置 `JAVA_HOME` 指向 JDK 17（AGP 8.x 需要）
  - iOS：安装 Xcode（14+），安装 CocoaPods；`sudo gem install cocoapods`
- 拉取依赖
  - 在根目录执行：`flutter pub get`
  - iOS 目录执行：`cd ios && pod install`（首次或 Pod 版本更新时）

## Android 构建
- 调试运行
  - 连接真机或启动模拟器：`flutter devices`
  - 运行：`flutter run -d android`
- 产物构建
  - APK（调试/发布）：`flutter build apk --release`
    - 输出：`build/app/outputs/apk/release/app-release.apk`
  - App Bundle（商店用）：`flutter build appbundle`
    - 输出：`build/app/outputs/bundle/release/app-release.aab`
- 可选配置
  - 如需更改包名：`applicationId`（android/app/build.gradle:54）
  - 如需升级最小/目标 SDK：`minSdkVersion` 与 `compileSdkVersion`（android/app/build.gradle:57、32）

## iOS 构建
- 签名设置
  - 打开 `ios/Runner.xcworkspace`，在 Xcode 选择 Team 并开启 Automatic Signing（Bundle ID：`vdrs.sappu.lafk.learn`，project.pbxproj:370）
  - 部署目标保持 11.0（project.pbxproj:348/475/524），必要时统一到更高版本
- 调试运行
  - 选择模拟器或真机：`flutter run -d ios`
- 产物构建
  - Flutter 构建：`flutter build ios --release`（生成 `Runner.app`）
  - 导出 IPA：在 Xcode 使用 Archive → Distribute（或：`flutter build ipa --export-method ad-hoc` 进行本地分发）

## 验证与联调
- 资源校验：确认 `pubspec.yaml` 中 assets 与字体加载正常（pubspec.yaml:74–91、104–107）
- 包功能检查：`just_audio`、`flutter_tts`、`url_launcher`、`shared_preferences` 等在真机环境是否工作
- 运行自检：`flutter analyze`、`flutter test`（如有测试）

## 常见问题处理
- JDK 不匹配：AGP 8.1.0 要求 JDK 17；如构建失败，检查 `JAVA_HOME`
- iOS Pod 兼容：若 `pod install` 报错，执行 `pod repo update` 并重试
- 权限与签名：iOS 需开发者账号与签名；Android 发布需签名 `keystore`（可后续补充）

## 交付物
- Android：`app-release.apk` 与 `app-release.aab`（build/app/outputs/...）
- iOS：`Runner.app`（本地测试）与 `Runner.ipa`（Archive 导出）

## 下一步
- 我将按上述步骤在本机为 Android 与 iOS 分别执行依赖拉取、签名配置（iOS需你提供 Team/证书）、构建与产物导出，并把生成的 APK/AAB/IPA 放到仓库的 `dist/` 目录或给出具体路径说明，附带运行验证截图与说明。请确认后我开始执行。