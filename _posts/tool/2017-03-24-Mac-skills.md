---
layout: post
category: 工具
title: Mac的小东西
---
## 显示已损坏打开办法
```bash
sudo xattr -r -d com.apple.quarantine 路径（在应用程序中直接拖入终端）
```

## Mac Win7双系统, Win7时间少8小时解决方法
1. Win + R(开始 > 运行), 输入 regedit 回车 打开注册表
2. 找到 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation\
3. 右侧窗口内新建 DWORD, 命名RealTimeIsUniversal, 值为1, 编码格式默认即可
4. 重启后Win7下的时间即可恢复。
5. 修改后尽量不要使用在线时间同步功能

## 显示Mac隐藏文件的命令
```bash
defaults write com.apple.finder AppleShowAllFiles  YES
```

## 隐藏Mac隐藏文件的命令
```bash
defaults write com.apple.finder AppleShowAllFiles  NO
```

## 允许所有来源
```bash
sudo spctl --master-disable
```

## 启用root用户

**打开设置-> 用户和群组-> 点击左下角的输入密码解锁-> 点击登录选项-> 点击网络账户服务器
-> 打开目录实用工具-> 点击小锁解锁-> 点击屏幕左上角的编辑-> 启用/停用root**

`Win与Mac共享文件,前提在同一个网络下`

`Windows 共享目录给 Mac 使用:`

**Windows: 选择文件夹-> 右击属性-> 共享-> 高级共享-> 共享此文件夹打勾-> 权限-> 允许下全部打勾**

**Mac: 打开 Finder，按快捷键：Command + K，输入：smb://IP地址(windows的ip地址)**

## Mac 共享目录给 Windows 使用

注意共享时候的IP地址

**Mac: 打开菜单-> 系统偏好设置-> 共享-> 文件共享-> 点击"+" -> 选择要共享的文件(也可以在文件夹的显示简介中选择共享)-> 选项-> 打勾**

**Windows: 搜索框输入->\\\IP地址**


