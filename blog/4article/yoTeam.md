# 使用 yo team 在vsts或是tfs中自动创建团队项目持续交付流水线

## 背景
   如今，DevOps势头异常猛烈，从C端的互联网企业到B端传统软件企业都在陆续开展DevOps转型。有从文化/管理理念层面开始转型的，也有从技术层面（工具链）开始转型的，工具链层面要么是开源方案（Jenkins），要么引入大厂的产品（Jira、TFS），首先，想改变是非常棒的一个决定，在数字化经济时代和知识大暴炸时代，先迈出第一步拥抱敏捷开发和精益思想总比那些还固守传统工业时代的经营理念的企业具有更多机会。好，现在那问题来了，如果我们要从工具链层面入手，有没有一种办法快速搭建基础环境，一键生成持续交付流水线的方法呢？答案是：当然有，Visual Studio Team Service和Team Foundation Server 可以做到！！！！试想，不用自己准备虚拟机，也不用自己安装测试环境、配置环境，交付流水线也不需要自己配置，只需要点几次鼠标，是多么愉快的事情啊，可以节省非常多的时间。通过试用生成的环境，我们可以快速评估平台能力，确认是否符合自己的团队；还可以学习这其中的最佳实践，让我们快速上手。

## 概述
   要达成上面的目标我们有两种实现方式：采用云端（VSTS，微软研发云）；或者是，在Azure云端创建TFS环境，第一种方式不是我们现在的重点，这一次我们重点介绍第二种方式。

## 一、在Azure云端创建一套TFS2018环境

通过使用我们的[研发测试去产品]()，可在Azure云端创建一套TFS2018环境，具备一键式体验，免去自己安装系统、软件环境、配置等工作，使得我们可以只关注要实现的目标。环境模板如下图示所：

![](images/yoTeam/labs-environment.png) . 

NOTE: 当然，如果您是私有云，有自己的数据中心，则可以在自己的
TFS服务器中使用yoTeam自动创建持续交付流水线，方法是通用的。

## 二、在TFS2018环境中创建持续交付流水线

### 如何创建？

- 我们先看看这个工具如何使用，注意查看下面的Git操作图片:

创建TFS团队项目和相关内容：

![](images/yoTeam/yoteam-ok.gif) . 

推送代码并触发持续集成：

![](images/yoTeam/yoteam-ok-git.gif) . 

- 看看创建出来的效果

![](https://raw.githubusercontent.com/lean-soft/labs-templates/master/lsproj101-yoteam-asp/labs/images/image1.png) .

![](https://raw.githubusercontent.com/lean-soft/labs-templates/master/lsproj101-yoteam-asp/labs/images/image2.png) .

![](https://raw.githubusercontent.com/lean-soft/labs-templates/master/lsproj101-yoteam-asp/labs/images/image3.png) .

![](https://raw.githubusercontent.com/lean-soft/labs-templates/master/lsproj101-yoteam-asp/labs/images/image4.png) .


## 三、关于 yoTeam

yoTeam 是一个基于 Yeoman 的开源的生成器，代码托管到 [Github](https://github.com/DarqueWarrior/generator-team)。通过执行工具中提供的命令，可以帮助我们在TFS或是VSTS中快速创建 一套CI/CD 部署流水线. 作者是微软的一位` Principal DevOps Manager`, yo team 使用介绍 可以参考[大神的博客](http://donovanbrown.com/post/yo-Team)


  [Yeoman](http://yeoman.io/) 是一款神器，简单来说通过Yeoman的生成器可以快速创建建一套项目，项目包含种最佳实践,并可以集成最流行的工具，使我们在项目开始时可立即上手，提升效率，而不是从0开始搭建自己的框架，引入开发环境所需的工具。Yeoman的生成器的插件市场中有很多实用的生成器，如 JHipster,做Java开发的应该会知道此生成器，号称让程序员失业的神器，[详细可参考知乎的讨论](https://www.zhihu.com/question/51082079/answer/146337049)

回到yoTeam，可以看到支持以下开发语言

- Java using Tiles and bootstrap
- Node using Pug and bootstrap
- ASP.net Core using Razor and bootstrap
- ASP.net Full Framework using Razor and bootstrap

支持发布到以下平台：

- Azure App Service
- Docker to private host
- Docker images in Azure App Service on Linux
- Azure Container Instances

## 四、yo Team 使用指南

### 安装

**必须环境要求：**

- 安装 git, 需要用到git 推送示例代码
- nodejs环境,Yeoman是用nodejs编写的，必须要有nodejs环境
- npm，用来安装yo（Yeoman）
- Azure Powershell
- 如果采用的是私有云或是自己内部的数据中心，需保证TFS所在的服务器可以连接到外网

**Net项目所需的环境**

- DotNet Core SDK 
- Net Framework 3.5 或以上

**Azure及Docker**

- 如果想要示例程序部署成功，必须要一Azure订阅
- 如果使用Docker的方式部署，还需要准备Docker镜像仓库

参考此文档：http://donovanbrown.com/post/Yo-Team-meet-Azure-Container-Instances


**安装**

- `npm install yo`
- `npm install generator-team`
- 分别运行 `yo和yoTeam`命令，测试是否安装成功


    注意：yo team 在Windows中默认会安装在当前命令行所处路径，建议安装到NPM包存放目录中，保证路径已经添加到环境变量 `Path`中。否则每次运行时，需要进入yo team安装的路径运行命令，稍微有不便。

### 命令介绍

- 查看已经安装的yo生成器: `yo --help`,可以看到命令行输出的低部，会显示已安装的生成器(team)和子生成器(asp等)

```
Available Generators:
  team
    asp
    aspFull
    azure
    build
    docker
    git
    java
    node
    pipeline
    profile
    project
    registry
    release
```

- 查看 yoteam 的使用方法,运行命令： `yo team -h 或yo team --help`.子命令：`yo team:asp -h 或yo team:project --help`

```
 yo team:app [options] [<type>] [<applicationName>] [<tfs>] [<azureSub>] [<azureSubId>] [<tenantId>] [<servicePrincipalId>] [<queue>] [<target>] [<installDep>] [<groupId>] [<dockerHost>] [<dockerCertPath>] [<dockerRegistry>] [<dockerRegistryId>] [<dockerPorts>] [<dockerRegistryPassword>] [<servicePrincipalKey>] [<pat>] [<customFolder>]

Options:
  -h,   --help          # 使用帮助
        --skip-cache    # 是否记住输入的参数       Default: false
        --skip-install  # 是否自动安装依赖（VSTS/TFS 扩展）  Default: false

Arguments:
  type                    # 项目类型：asp, node, java or aspFull，Type: String  Required: false
  applicationName         # 要创建的项目名称                              Type: String  Required: false
  tfs                     # TFS 项目集合URL地址 或者是 VSTS account(URL地址的前缀) or Profile  Type: String  Required: false
  azureSub                # Azure Subscription name                                Type: String  Required: false
  azureSubId              # Azure Subscription ID                                  Type: String  Required: false
  tenantId                # Azure Tenant ID                                        Type: String  Required: false
  servicePrincipalId      # Azure Service Principal Id                             Type: String  Required: false
  queue                   # Agent queue to use                                     Type: String  Required: false
  target                  # Docker or Azure app service                            Type: String  Required: false
  installDep              # If true dependencies are installed                     Type: String  Required: false
  groupId                 # Group ID of Java project                               Type: String  Required: false
  dockerHost              # Docker host url including port                         Type: String  Required: false
  dockerCertPath          # Path to Docker certs folder                            Type: String  Required: false
  dockerRegistry          # Server of your Docker registry                         Type: String  Required: false
  dockerRegistryId        # Username for Docker registry                           Type: String  Required: false
  dockerPorts             # Port mapping for container and host                    Type: String  Required: false
  dockerRegistryPassword  # Password for your Docker registry                      Type: String  Required: false
  servicePrincipalKey     # Azure Service Principal Key                            Type: String  Required: false
  pat                     # Personal Access Token to TFS/VSTS                      Type: String  Required: false
  customFolder            # Path to folder of build & release templates            Type: String  Required: false

```

## 五、直接以一问一答的交互模式来运行命令

通常，我们如果仅仅是人个学习使用VSTS或者是TFS，在命令行直接运行 `yo team`即可，在命令行根据提示采用一问一答的交互方式来创建示例项目，比较简单，这里不作详细说明了。

## 六、以单个命令的形式运行命令

我们有很多客户，而且每个客户也有多个试点团队，要求每个人都去命令行敲这些命令，并准备一堆参数，这基本上不太可能，所以，我们在想，是否有更好的方式来应对这些个场景？答案是有！！！

看到前面介绍的子命令了吧？没看到，再往上看看，有感觉了吧？-_-!

**team:app 命令**

有一个 `team:app`的子命令，配以参数后可以直接触发Demo的创建，以下是TFS的示例：

```
yo team:app --skip-cache false asp YoTeamDemoApplxm1 "http://{TFS登陆帐号}:{密码}@{tfs集合URL地址}" "Visual Studio Enterprise - MPN" 5132f8c8-ccfc-4613-9424-d08bf5e6d1f6 31270f2c-e7a0-4267-8efc-907830f44d12 d0bdbd2f-b9e9-47a1-8d5a-179d153f5bff Default paasslots true 1 1 1 1 1 1 1 {servicePrincipalKey} {tfsPAT} YoTeamDemoApplxm1
```

以下内容是命令行输出：

```
+ Found Team project
+ Cloning repository http://******:********@tfs.devopshub.cn/TestCollection/_git/YoTeamDemoApplxm1
fatal: destination path 'YoTeamDemoApplxm1' already exists and is not an empty directory.
+ Found Azure Service Endpoint 'Visual Studio Enterprise - MPN'
+ Found build definition
+ Found release definition
identical YoTeamDemoApplxm1\README.md
identical YoTeamDemoApplxm1\.gitignore
 conflict YoTeamDemoApplxm1\YoTeamDemoApplxm1.sln
? Overwrite YoTeamDemoApplxm1\YoTeamDemoApplxm1.sln? overwrite
    force YoTeamDemoApplxm1\YoTeamDemoApplxm1.sln
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1\wwwroot\css\site.css
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1\wwwroot\css\site.min.css
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1\wwwroot\favicon.ico
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1\wwwroot\images\banner1.svg
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1\wwwroot\images\banner2.svg
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1\wwwroot\images\banner3.svg
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1\wwwroot\images\banner4.svg
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1\wwwroot\js\site.js
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1\wwwroot\js\site.min.js
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1\Views\Home\About.cshtml
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1\Views\Home\Contact.cshtml
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1\Views\Home\Index.cshtml
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1\web.config
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1\.bowerrc
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1\appsettings.json
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1\bower.json
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1\bundleconfig.json
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1\Views\_ViewStart.cshtml
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1\Views\Shared\_ValidationScriptsPartial.cshtml
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1\Views\Shared\Error.cshtml
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1\appsettings.Development.json
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1\Dockerfile
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1\Program.cs
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1\Startup.cs
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1\YoTeamDemoApplxm1.csproj
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1\Models\ErrorViewModel.cs
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1\Views\_ViewImports.cshtml
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1\Views\Shared\_Layout.cshtml
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1\Controllers\HomeController.cs
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1.Tests\YoTeamDemoApplxm1.Tests.csproj
identical YoTeamDemoApplxm1\src\YoTeamDemoApplxm1.Tests\HomeControllerTest.cs
identical YoTeamDemoApplxm1\templates\parameters.xml
identical YoTeamDemoApplxm1\templates\website.json
identical YoTeamDemoApplxm1\templates\website.parameters.json
identical YoTeamDemoApplxm1\templates\acilinux.json
identical YoTeamDemoApplxm1\templates\acilinux.parameters.json
identical YoTeamDemoApplxm1\templates\docker.json
identical YoTeamDemoApplxm1\templates\docker.parameters.json
+ Running bower install
bower                           ENOENT No bower.json present
+ Running dotnet restore
+ Adding initial files
+ Configuring email and name as yo team
+ Committing initial files
= Now all you have to do is push when ready
```

此时可以去查看TFS中已经生成的团队项目。可以看到，代码还未推送到TFS服务器，我们还需要执行下面的命令推送代码，并触发CI/CD:

```
cd YoTeamDemoApplxm1
git push
```

#### 至此，大功告成！

NOTE: 如果想偿试其他类型的项目，修改参数 `type` 即可，支持的参数值有：asp, node, java、aspFull

#### 在微软研发云vsts中创建Demo项目

参考以下命令，使用方式类似,此处不在详细解释

```
yo team:app  --skip-cache false "asp" "DemoApp122" "lean-soft-lxm-demo" "Visual Studio Enterprise – MPN" "5132f8c8-ccfc-4613-9424-d08bf5e6d1f6" "31270f2c-e7a0-4267-8efc-907830f44d12" "d0bdbd2f-b9e9-47a1-8d5a-179d153f5bff"  "Hosted VS2017" "paasslots" false "1" "1" "1" "1" "1" "1" "1" "{servicePrincipalKey}" "{TFS PAT}" "DemoApp122"

```

## 七、以组合命令的方式来执行

以组合命令的方式来运行的好处是我们可以决定何时候创建Demo项目里面的内容，并与自己的工具进行集成，以下是 yo team:app 命令中包含的子命令：

- `yo team:project` 创建团队项目

```
yo team:project --skip-cache false "YoTeamDemoApp"  https://tfs.devopshub.cn/TestCollection {TFS PAT}
```

- `yo team:azure` 创建Azure订阅的服务终结点，用于部署网站到指定的订阅帐户中

```
yo team:azure --skip-cache false "YoTeamDemoApp"   https://tfs.devopshub.cn/TestCollection "Visual Studio Enterprise - MPN" 5132f8c8-ccfc-4613-9424-d08bf5e6d1f6 31270f2c-e7a0-4267-8efc-907830f44d12 d0bdbd2f-b9e9-47a1-8d5a-179d153f5bff {servicePrincipalKey} {TFS PAT}
```

- `yo team:build` 创建构建定义

```
yo team:build --skip-cache false asp "YoTeamDemoApp" https://tfs.devopshub.cn/TestCollection default paasslots "1" "1" "1" {TFS PAT} YoTeamDemoApp
```

- `yo team:pipeline` 创建部署流水线

```
yo team:pipeline --skip-cache false asp "YoTeamDemoApp" https://tfs.devopshub.cn/TestCollection default paasslots "Visual Studio Enterprise - MPN" 5132f8c8-ccfc-4613-9424-d08bf5e6d1f6 31270f2c-e7a0-4267-8efc-907830f44d12 d0bdbd2f-b9e9-47a1-8d5a-179d153f5bff 1 1 1 1 1 1 {servicePrincipalKey} {TFS PAT} "YoTeamDemoApp"
```

- `yo team:git **** clone` 从创建好的Demo项目中克隆git仓库

```
yo team:git --skip-cache false "YoTeamDemoApp" http://tfs帐号:tfs密码@tfs.devopshub.cn/TestCollection clone {TFS PAT}
```

- `yo team:asp` 创建示例程序代码到指定的本地git目录

```
yo team:asp --skip-cache false "YoTeamDemoApp" false 1
```

- `yo team:git **** commit` 将上一步创建的代码添并提交到git仓库

```
yo team:git --skip-cache false "YoTeamDemoApp" 
http://{tfs 帐号}:{密码}@tfs.devopshub.cn/TestCollection commit {TFS PAT}
```

- 推送到TFS服务器，推送成功后，会自动触发上面创建的Build 定义,成功后会触发上面创建部署流水线

```
cd YoTeamDemoApp
git push
```

NOTE: 以上命令中的`YoTeamDemoApp`表示一个将要创建的TFS 团队项目名称，执行以上整套命令时，需保证此名称在TFS项目集合不存在。

接下来，我们偿试在TFS Build的执行上面的命令。

NOTE: queue 参数值建议用Default（执行yo team命令的构建服务器也注册到Default队列下），不能包含 横杠，否则会报以下错误（也许是一个yoteam 的一个BUG）：

```
+ Found Azure Service Endpoint 'Visual Studio Enterprise - MPN'                                  
C:\Users\liminany\node_modules\generator-team\generators\app\utility.js:668                      
         callback(null, obj.value[0].id);                                                        
                                    ^  
TypeError: Cannot read property 'id' of undefined                                                
    at Request._callback (C:\Users\liminany\node_modules\generator-team\generators\app\utility.js
:668:37)                                                                                         
    at Request.self.callback (C:\Users\liminany\node_modules\request\request.js:186:22)          
    at emitTwo (events.js:106:13)                                                                
    at Request.emit (events.js:191:7)                                                            
    at Request.<anonymous> (C:\Users\liminany\node_modules\request\request.js:1163:10)           
    at emitOne (events.js:96:13)                                                                 
    at Request.emit (events.js:188:7)                                                            
    at IncomingMessage.<anonymous> (C:\Users\liminany\node_modules\request\request.js:1085:12)   
    at IncomingMessage.g (events.js:292:16)                                                      
    at emitNone (events.js:91:20)                                                                
```

## 八、使用TFS Build来创建TFS Demo项目

我们需要做两件事情：

 - 在TFS中创建一个Build定义，添加一个命令行或是Powershell任务
 - 把上面命令中的输入参数使用TFS Build变量 参数化


如下图所示：

![](images/yoTeam/ci-1.png) . 

![](images/yoTeam/ci-2.png) . 


可以看到，yo team的参数都已经改成了参数化的形式，而不是hard Code命令中，这样有更灵活，不仅仅是在我自己的TFS服务器中执行、创建Demo项目，可以是任何人，只要把对应的参数修改成自己的值即可（另外在VSTS也是一样的道理）。

上面的任务中还包含了`Replace tokens in labs-result-template.json和发布生成项目`等任务，这些任务是将yo team 创建好的TFS Demo项目信息提取出来了，以便我们后续的步骤中与其他系统或功能进行集成时，可以显示和快速的访问这些地址（如TFS团队项目地址、Git仓库地址等）


总算完成了，经过使用，示例项目中的示例Web程序部署到Azure后，可以在Azure资源组中找到，并访问此网站：

```
http://{Demo项目名}{四位随机数}Dev.azurewebsites.net
http://{Demo项目名}{四位随机数}QA.azurewebsites.net
http://{Demo项目名}{四位随机数}Prod.azurewebsites.net
```

但是但是,问题又来了,用户怎么访问到这个地址呢?不可能登陆Azure Portal吧? 看来需要自动获取Web程序的访问地址。其实这个地址有规律,但是为什么会加一串数字? 


原来为了保证项目名称及其他资源唯一性,他这里加了随机数.这个时候去查看了代码,果然是,那怎么解决?改代码是下下策,先看看Azure中的资源组是怎么创建的.

经过研究，发现 文件`generator-team/generators/release/templates/tfs_2018_release.json` 有以下代码：


![](images/yoTeam/cd-source-uuid.png) . 

喔,原来是这样创建的,用的就是ARM模板,那直接改模板就好啦.

## 九、修改yo team源码

从Github Fork仓库,在Clone到本地,开改.

找到文件 `generator-team/generators/release/templates/tfs_2018_release.json`：去掉随机数变量{uuid}：

![](images/yoTeam/cd-source-uuid.png) . 

然后打开`package.json`,修改一下源码版本:

![](images/yoTeam/source-package-ver.png)

运行`NPM Link`，链接本地代码，进行测试,此处不在详细解释。

最后附上修改好的源码地址： https://github.com/lean-soft/generator-team

最后，TFS的构建服务器如何安装修改后的版本？
yoteam这个命令是通过运行NPM命令从NPM仓库获取下来安装的，看来我也要搭建一个包管理仓库才可以啊！正好，TFS有一个Packages Manage的功能（VSTS也有），目前支持四种类型源包（TFS2018 Update2）。如下图所示：

![](images/yoTeam/tfs-package-info.png) . 

## 十、使用TFS中的包管理来发布 定制化的yo team 包

请参以下考官方文档：

[Quickstart: Use npm to store JavaScript packages in VSTS or TFS](https://docs.microsoft.com/zh-cn/vsts/package/get-started-npm?view=vsts)

[Publish an npm package](https://docs.microsoft.com/zh-cn/vsts/packageteam:app 命令/npm/publish?view=vsts)


## 十一、总结

这里记录了对yo team的探索的过程，如果您只是想使用yo team 创建Deom项目，那不必折腾:

 - 直接安装yo team官方版本
 - 创建TFS Build定义，使用上面提供的命令做为任务的命令
 - 修改参数值
 - 触发Build 定义即可


最终，我们已将yo team 集成到了自己的研发测试云产品中：

![](images/yoTeam/labs-project.png) . 

如果您想拥有一键式体验，敬请期待吧，新版本即将上线！

**除此之外：**

- Azure针对VSTS有项功能，可实现类似的效果，功能更完善，叫 Azure DevOps Project，[详情请参阅这里](https://docs.microsoft.com/zh-cn/vsts/pipelines/apps/cd/azure/azure-devops-project-aspnetcore?toc=%2Fvsts%2Fdeploy-azure%2Ftoc.json&;bc=%2Fvsts%2Fdeploy-azure%2Fbreadcrumb%2Ftoc.json&view=vsts)

- 针对VSTS，有一套更丰富的动手实验，可以使用一个叫 VSTS DemoGenerator 的工具来生成示例项目，参考地址：https://almvm.devopshub.cn/labs/vsts/

- 针对TFS，也有一套更丰富的动手实验，但需自行下载虚拟镜像到本地，并将虚拟机运行起来才可以体验这套动手实验。如果想省事，我们的研发测试去产品提供了一套环境模板，具有一键式体验, 如下图所示：
    
    ![](images/yoTeam/labs-environment-almvm.png) . 

    对应的练习文档请参考以下两个地址：

     - [中文版，由我们翻译并托管在github上 ](https://almvm.devopshub.cn/labs/tfs/agile/)，结合上图的 [TFS2018培训环境使用]()

     - [英文原版](https://almvm.azurewebsites.net/labs/tfs/), 需自行下载虚拟机来使用
  
