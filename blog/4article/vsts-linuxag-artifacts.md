# 在TFS Linux Agent 构建环境中，将 TFS Build 构建包存放到外部存储服务器中

## 背景

在TFS的CI/CD中，构建包的存储方式有两种： `Visual Studio Team Services/TFS | Server 和 a file share`

- Visual Studio Team Services
这种方式简单粗暴，是将构建包直接存放至TFS的后台数据库中。**这种方式固然简单，但是构建包比较大、团队规模较大、构建数量比较多时，数据库将迅速增长**，对于比较在意DB存储成本的团队或组织来说，这种存放方式变得不太合适
- a file share
这种方式是将构建包存放至Windows共享目录中，但是不支持Linux构建环境，**仅支持Windows构建环境**。如果偿试将Linux 构建环境中的构建包复制至Windows 共享目录，在TFS的构建定义中将会收到以下错误：`无法将来自 OSX 或 Linux 代理的项目发布到文件共享。可将项目类型更改为服务器或使用 Windows 代理`

为解决这个问题，我们需要考虑其他方案，**这里给出了两种可选方案：ftp的方式和SSH的方式**，FTP的方式会比较通用，对于Windows的构建环境也支持。SSH的方式针对纯Linux环境，纯Linux的构建环境建议采用这种方式

## 一、 使用FTP 服务器存放构建包


#### 1. 准备一个FTP服务器，配置好访问帐户和密码


## 二、使用SSH 将构建包存放至linux 文件服务器中

#### 1. 在构建定义中添加一个 `通过SSH复制文件`的Task，配置好以下参数：

- ssh 终结点：`在TFS的 设置->服务 处，添加一个SSH终结点`
- 源文件夹：`(Build.SourcesDirectory)`,构建包的存放地址，如jar包或是dll。这里直接将源码文件做为构建结果
- 目标文件夹： `/home/azureuser/artifacts/$(Build.DefinitionName)/$(Build.BuildNumber)`,存放构建包的目录。建议采用这里的为默认值（替换azureuser部分），此值表示构建包根据当前构建定义的名称和构建编号来存放

#### 2. 上传 build-artifacts.json

	注：此任务是可选的，适应场景：当构建包存放的地址、目录及其他信息希望自动传递给生成定义时，可以添加此步，将需要的参数存放一个JSON配置文件中。当前添加此任务时，需要添加额外的参数生成任务，此处不再阐述。

- 在对应的Git代码仓库中添加一个文件：`build-artifacts.json`,内容请根据需要自行定义
- 添加一个 发布生成项目的 任务
- 要发布的路径: 选择 `build-artifacts.json`
- 项目名称： `drop`
- 项目类型： `Server`

