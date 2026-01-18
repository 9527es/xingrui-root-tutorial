# xingrui-root-tutorial
一个针对星瑞设备的 root 教程，使用 SuperSU 和 dd 命令获取权限
# 星瑞设备 Root 教程

这是一个针对星瑞设备（如 E01）的 root 教程，使用 SuperSU.apk 和 dd 命令安装 su 文件获取 root 权限。基于联发科（MTK）芯片设备。

**零基础警告**：Root 会修改系统文件，风险很大！可能砖机、丢数据或保修失效。先备份所有数据，自行承担后果。如果不懂，别尝试！建议先在 XDA 论坛或 YouTube 搜索“Android root tutorial for beginners”学习基础。

## 前提条件
- **设备**：星瑞系列（如 E01），Android 系统，未 root。
- **文件准备**：
  - SuperSU.apk（从可靠来源下载，如 APKMirror，搜索“SuperSU apk”）。
  - armv7 文件夹：包含 install-recovery.sh、su、libsupol.so 等文件（需自行获取或提取，通常从 root 工具包中来）。
- **工具**：ADB（Android Debug Bridge），下载 Android SDK Platform-Tools。
- **启用调试**：设备设置 > 关于手机 > 连续点击版本号开启开发者模式 > 开发者选项 > USB 调试。

## 详细步骤
1. **准备文件**：
   - 把 SuperSU.apk 和 armv7 文件夹放到设备 SD 卡根目录（/sdcard/）。
   - 先安装 SuperSU.apk（用文件管理器或 ADB：`adb install SuperSU.apk`），但不要启动它！

2. **连接设备并进入 ADB shell**：
   - 电脑连设备，打开命令提示符（Windows: cmd，Mac: Terminal）。
   - 输入 `adb shell` 进入终端（需先获取临时 root 或用 mtk-su，如果设备锁了 bootloader，可能需解锁）。

3. **执行 dd 和 chmod 命令**（复制粘贴每行，回车）：dd if=/sdcard/armv7/install-recovery.sh of=/system/bin/install-recovery.sh chmod 0755 /system/bin/install-recovery.sh
dd if=/sdcard/armv7/su of=/system/xbin/su chmod 0755 /system/xbin/su
dd if=/sdcard/armv7/su of=/system/xbin/daemonsu chmod 0755 /system/xbin/daemonsu
/system/xbin/daemonsu --auto-daemon &
dd if=/sdcard/armv7/libsupol.so of=/system/lib64/libsupol.so chmod 0755 /system/lib64/libsupol.so
4. **重启设备**：reboot
5. 5. **更新 SuperSU**：
- 重启后，打开 SuperSU.apk，会提示更新二进制文件。
- 选择“正常模式”更新，完成后重启设备。
- 现在 root 已获取！可以用 Root Checker app 测试。

## 常见问题
- **权限不足**：系统需可写，先用 `mount -o rw,remount /system`。
- **文件没找到**：确认路径，用 `ls /sdcard/armv7/` 检查。
- **砖机**：如果失败，用 recovery 模式恢复出厂（数据会丢）。
- **零基础提示**：不懂 ADB？YouTube 搜“ADB tutorial beginners”看视频。文件来源？搜“SuperSU root files for MTK”。

## 免责声明
本教程仅供学习，不保证成功、安全或合法。Root 可能违反设备条款。作者不对损害负责。

## 贡献
欢迎 Pull Request 改进！

## 许可
MIT License（见 LICENSE）
