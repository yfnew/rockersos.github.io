# 使用 yo team 在vsts或是tfs中自动创建团队项目持续交付流水线

## 背景
   如今，DevOps势头异常猛烈，从C端的互联网企业到B端传统软件企业都在陆续开展DevOps转型。有从文化/管理理念层面开始转型的，也有从技术层面（工具链）开始转型的，工具链层面要么是开源方案（Jenkins），要么引入大厂的产品（Jira、TFS），首先，想改变是非常棒的一个决定，在数字化经济时代和知识大暴炸时代，先迈出第一步拥抱敏捷开发和精益思想总比那些还固守传统工业时代的经营理念的企业具有更多机会。好，现在那问题来了，如果我们要从工具链层面入手，有没有一种办法快速搭建基础环境，一键生成持续交付流水线的方法呢？答案是：当然有，Visual Studio Team Service 和 Team Foundation Server 可以做到！！！！试想，不用自己准备虚拟机，也不用自己安装测试环境、配置环境，交付流水线也不需要自己配置，只需要点几次鼠标，是多么愉快的事情啊，可以节省非常多的时间。通过试用生成的环境，我们可以快速评估平台能力，确认是否符合自己的团队；还可以学习这其中的最佳实践，让我们快速上手。

## 概述
   要达成上面的目标我们有两种实现方式：采用云端（VSTS，微软研发云）；或者是，在Azure云端创建TFS环境，第一种方式不是我们现在的重点，这一次我们重点介绍第二种方式。

## 一、在Azure云端创建一套TFS2018环境

通过使用我们的开发测试云产品，可在Azure云端创建一套TFS2018环境，具备一键式体验，免去自己安装系统、
软件环境、配置等工作，使得我们可以只关注要实现的目标。环境模板如下图示所：

![](images/yoTeam/labs-environment.png) . 

NOTE: 当然，如果您是私有云，有自己的数据中心，则可以在自己的TFS服务器中使用yoTeam自动创建持续交付流水线，方法是通用的。

## 二、在TFS2018环境中创建持续交付流水线

### 如何创建？

**我们先看看这个工具如何使用，注意查看下面的Git操作图片:**

![](images/yoTeam/yoteam-ok.gif) . 

![](images/yoTeam/yoteam-ok-git.gif) . 




**看看创建出来的效果**

yoteam自动创建了团队项目和团队配置(如下图所示)：

![](https://raw.githubusercontent.com/lean-soft/labs-templates/master/lsproj101-yoteam-asp/labs/images/image1.png)


基础代码已经导入到Git存储库(如下图所示)：

![](https://raw.githubusercontent.com/lean-soft/labs-templates/master/lsproj101-yoteam-asp/labs/images/image2.png)


持续集成 CI 已经配置完成(如下图所示)：

![](https://raw.githubusercontent.com/lean-soft/labs-templates/master/lsproj101-yoteam-asp/labs/images/image3.png)


自动化部署流水线已经配置完成，并链接到了Azure云中的Paas服务，直接触发即可完成部署(如下图所示)：

![](https://raw.githubusercontent.com/lean-soft/labs-templates/master/lsproj101-yoteam-asp/labs/images/image4.png)


## 三、关于 yoTeam

yoTeam 是一个基于 Yeoman 的开源的生成器，代码托管到 [Github](https://github.com/DarqueWarrior/generator-team)。通过执行工具中提供的命令，可以帮助我们在TFS或是VSTS中快速创建 一套CI/CD 部署流水线. 作者是微软的一位` Principal DevOps Manager`, yo team 使用介绍 可以参考[大神的博客](http://donovanbrown.com/post/yo-Team)。

![](images/yoTeam/image-5e2cc025-c041-4e2f-918f-f9fc3f066a18.png)

  [Yeoman](http://yeoman.io/) 是一款神器，简单来说通过Yeoman的生成器可以快速创建建一套项目，项目包含种最佳实践，并可以集成最流行的工具，使我们在项目开始时可立即上手，提升效率，而不是从0开始搭建自己的框架，引入开发环境所需的工具。Yeoman的生成器的插件市场中有很多实用的生成器，如 JHipster,做Java开发的应该会知道此生成器，号称让程序员失业的神器，[详细可参考知乎的讨论](https://www.zhihu.com/question/51082079/answer/146337049)

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

## 四、yo Team 使用方式

yo Team 本质上是由一些命令组成，包括父命令和子命令。通过组合这 些命令来实现按需生成流水线。比如 yo team:app 是一个父命，通过此命令即可完成TFS流水线的创建。要使用yo Team, 我们有两种使用方式：交互模式和命令模式。

**交互模式**：即文中开篇处的Gif图片中使用的方式。这种方式简单易用，推荐采用此方式。

**命令模式**：采用`yo team:app`命令或是组合子命令的方式。除非有特别的定制化或是集成的需求可采用这种方式。


## 五、命令模式的使用示例

**yo team:app** 命令参数说明(`yo team:asp -help`)

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

**命令示例：**

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

## 六、以组合命令的方式来执行

以组合命令的方式来运行的好处是我们可以决定何时候创建Demo项目里面的内容，并与自己的工具进行集成，以下是 yo team:app 命令中包含的子命令：

yo team:project {参数} 
yo team:azure {参数} 
yo team:build {参数} 
yo team:pipeline {参数} 
yo team:git {参数} clone {参数} 
yo team:asp {参数} 
yo team:git {参数} commit {参数} 


## 七、总结

yo Team介绍完毕，除了TFS，yo Team 还支持微软研发云(VSTS), 使用方式与TFS类似。 如果想偿试其他类型的项目，修改上面命令中的参数 type 即可，支持的参数值有：asp, node, java、aspFull。这里记录了对yo team的探索的过程，如果您只是想使用yo team 创建Deom项目，那不必折腾：

 - 直接安装yo team官方版本
 - 创建TFS Build定义，使用上面提供的命令做为任务的命令
 - 修改参数值，建议参数化变量
 - 触发Build 定义即可

更详细的使用帮助，请参考这篇文章：[使用 yo team 在vsts或是tfs中自动创建团队项目持续交付流水线](https://liminany.github.io/m/#!./blog/4article/yoTeam.md)
__________________________________________


**最终，我们已将yo team 集成到了自己的研发测试云产品中：**

![](images/yoTeam/labs-project.png) . 

如果您想拥有一键式体验，敬请期待吧，新版本即将上线，特性介绍见下面的视频：

https://v.youku.com/v_show/id_XMzc2MTI5OTI2MA==.html



### **除此之外：**


- Azure针对VSTS有项功能，可实现类似的效果，功能更完善，叫 Azure DevOps Project，[详情请参阅这里](https://docs.microsoft.com/zh-cn/vsts/pipelines/apps/cd/azure/azure-devops-project-aspnetcore?toc=%2Fvsts%2Fdeploy-azure%2Ftoc.json&;bc=%2Fvsts%2Fdeploy-azure%2Fbreadcrumb%2Ftoc.json&view=vsts)

- 针对VSTS，有一套更丰富的动手实验，可以使用一个叫 VSTS DemoGenerator 的工具来生成示例项目，参考地址：https://almvm.devopshub.cn/labs/vsts/

- 针对TFS，也有一套更丰富的动手实验，但需自行下载虚拟镜像到本地，并将虚拟机运行起来才可以体验这套动手实验。如果想省事，我们的研发测试去产品提供了一套环境模板，具有一键式体验, 如下图所示：
    
![](images/yoTeam/labs-environment-almvm.png) . 

对应的练习文档请参考以下两个地址：

[中文版，由我们翻译并托管在github上 ](https://almvm.devopshub.cn/labs/tfs/agile/)，结合上图的 [TFS2018培训环境使用]()

[英文原版](https://almvm.azurewebsites.net/labs/tfs/), 需自行下载虚拟机来使用
  
