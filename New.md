# Change Log

## Ver 1.6.1.2 (2025.02.21)

### 更新内容
- **重写大部分脚本**：提高模块稳定性，增加模块流畅度。
- **更改配置文件位置**： 新配置文件位于模块目录下 配置.prop下
- **新增功能***
#### 1.守护进程Herta
**功能描述**  
- 每次成功开机启动后 会检测音量键 3+音量键 检测 卸载更新.conf 还原其内包名 3-进入旧版本恢复模式。
**启用方法** 
-  模块目录下 配置.prop 守护进程=是
#### 一言本地化（彩蛋） 
**功能描述**  
- 利用jq和开源的一言语言包实现本地一言调用
#### 通知栏推送模块状态
- 通知栏输出信息 （参考@coolapk 10007大佬 去广告模块 感谢大佬开源 ）

## Ver 1.4.1 (2025.01.19)

### 更新内容
- **重写大部分脚本**：提高模块稳定性，增加模块流畅度。
- **优化日志管理**：日志分级且统一保存在`Log.txt`文件中。
- **修复问题**：解决救砖脚本在2-后`service.sh`脚本不延迟的问题。
- **新增功能**：安装模式C，通过将自定义包名写入`package_list.txt`文件，自定义恢复软件范围。

### 新增功能详细说明

#### 安装模式C

**功能描述**  
安装模式C允许用户通过一个包名列表文件（`package_list.txt`）批量安装APK文件。此模式特别适用于需要批量安装多个应用的场景，特别是在系统组件或模块化应用的管理中。

**使用方法**  
1. **准备文件**  
   - **`package_list.txt`**：位于模块目录下（如`/data/adb/modules/RescueHyper_alpha/`）。每行一个包名，格式如下：
     ```
     miui.systemui.plugin
     com.example.app
     ```
   - **`Camellia`目录**：包含APK文件，文件名以数字命名（如`1.apk`、`2.apk`）。APK文件的索引与`package_list.txt`中的包名顺序对应。

2. **文件结构**  
   - 模块目录：`/data/adb/modules/RescueHyper_alpha/`  
   - 包名列表文件：`/data/adb/modules/RescueHyper_alpha/package_list.txt`  
   - APK文件目录：`/data/adb/modules/RescueHyper_alpha/Camellia/`

3. **逻辑流程**  
   - 脚本读取`package_list.txt`中的包名。  
   - 根据包名索引找到对应的APK文件（如`1.apk`）。  
   - 检查APK文件是否存在。  
   - 获取包名对应的插件目录。  
   - 比较APK文件和插件目录的MD5值。  
   - 如果MD5值不匹配，则安装APK文件并记录。

**示例**  
假设`package_list.txt`文件内容如下：

`miui.systemui.plugin`
`com.example.app1`
`com.example.app2`

`Camellia`目录下的APK文件如下：
- `1.apk` 对应 `miui.systemui.plugin`  
- `2.apk` 对应 `com.example.app1`  
- `3.apk` 对应 `com.example.app2`

**注意事项**  
- 确保`package_list.txt`中的包名格式正确，每行一个包名，无多余空格或特殊字符。  
- 确保`Camellia`目录下的APK文件命名规则正确，与`package_list.txt`中的包名索引对应。  
- 确保脚本有权限读取`package_list.txt`和`Camellia`目录下的APK文件。

