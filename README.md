# L_CN_KIDTRAK
本仓库只是一个记录<br>

关于主题，本仓库用于记录我是如何对 [Windows Kid Trak软件](https://kidtrak.cn/) 进行无密码卸载的。但实际上这并不能称作卸载，应为强制删除。<br>

## 原理

Kid Trak的外部执行文件一直就放在C盘下Windows目录中

但这些并不重要，真正重要的文件的内部目录是 `C:\Program Files (x86)\SafeEngine` ，这玩意说是 `Safe` ,那很会控制了，挺好笑。在平时你看不到它，因为它把自己隐藏了起来，我们只需要在安全模式下删除它，并删除残留服务即可。

**也许是保卫措施:** 你将会在删掉其文件后看见其恢复，原因是它的 SC 服务，它包含一个被保护的服务 `slservice` 它会调用 SC(服务系统) 来维持自己的存在，而当它不在了以后，开机自动检查的 `UpdateSafe` 就会自动下载补全文件。

据上文内容，实际上的保护逻辑就是：

```
开机->UpdateSafe-->补全-->开启SLSERVICE-->复制主程序-->开启监控
```

但是它的每一部分文件都有权限需要(电脑管理员)，所以我们只能通过粉碎进行。

## 我的步骤

我的没什么管控，我是进入安全模式，然后使用CommandLine: 

```
SC DELETE slservice
SC DELETE UpdateSafe
explorer
```

进入文件管理器，进入Windows文件夹，删除: `slmenu.exe` `ts****.exe`

启动火绒，用文件粉碎粉碎 `C:\Program Files (x86)\SafeEngine` `C:\Program Files (x86)\CommonFiles/UpdateSafe` 

你还可以用regedit 删除残留在注册表中的一些关于服务的你可访问的项目。

## 我的意见

最好就试试更强的手段，做成一款病毒类型的。真给你 [独立删了](https://kidtrak.cn/docs/can-kid-uninstall/) 你又不能说话，而且我找不到你们邮箱反馈。所以我就贴在这了。
