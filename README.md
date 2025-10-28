# uni-app 多功能示例

本项目基于 uni-app 构建，按照“一个功能一个页面”的要求实现了以下 5 个功能示例：

1. **系统信息展示**（`pages/system-info/system-info`）：页面加载时自动获取手机的品牌、型号、屏幕信息等，并把“手机型号”以及完整的系统信息保存到本地缓存。
2. **网络状态监听**（`pages/network-status/network-status`）：实时显示当前网络类型与连接状态，并在网络变化时弹出提示。
3. **图片选择功能**（`pages/image-picker/image-picker`）：允许用户从相册或相机选择图片，显示缩略图，并把图片路径写入缓存。
4. **本地存储演示**（`pages/storage/storage`）：集中展示缓存中的手机型号与图片路径，支持一键刷新与清空。
5. **剪贴板功能**（`pages/clipboard/clipboard`）：一键复制缓存中的手机型号到系统剪贴板。

## 使用方式

1. 将本项目导入 HBuilderX 或使用 `@dcloudio/uni-app` CLI。
2. 安装依赖并运行：
   ```bash
   npm install
   npm run dev:%PLATFORM%
   ```
   其中 `%PLATFORM%` 可替换为 `mp-weixin`、`h5`、`app-plus` 等目标平台。
3. 通过首页的导航按钮进入各个功能页面进行体验。

> ⚠️ 由于剪贴板、系统信息、网络监听等能力依赖真实设备运行环境，请在真机或支持这些 API 的平台上体验完整效果。
