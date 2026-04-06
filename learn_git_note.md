# GitHub 初学者入门学习笔记
核心学习思路：先理解**Git**底层逻辑再学**GitHub**平台操作，先掌握核心命令再动手实操，边用边学、允许试错，无需一开始掌握所有知识点。

## 一、基础认知：分清 Git 和 GitHub
这是入门最关键的一步，二者概念极易混淆，学习顺序**先Git后GitHub**。
1. **Git**：本地版本控制工具，安装在电脑上，无需网络即可使用，核心作用是记录代码的每一次变更，为代码提供“无限次撤销”功能。
2. **GitHub**：云端代码托管平台，基于Git实现，核心作用是将本地Git仓库同步到云端，支持多人协作，还新增Issue、Pull Request、Actions、Pages等社交/协作功能。
3. 通俗类比：Git是相机（拍照片/管理本地代码），GitHub是相册平台（存照片/托管云端代码），可单独使用Git，也可仅浏览GitHub不写代码。

## 二、核心命令：先掌握6个，覆盖90%独立开发场景
Git命令虽多，入门只需吃透以下6个，其余知识点用到再查：
```bash
git init    # 在当前目录创建新的本地Git仓库
git add     # 把工作区文件的变更加入「暂存区」
git commit  # 把暂存区的改动打包为一个版本，保存到本地仓库
git push    # 把本地仓库的版本推送到远程GitHub仓库
git pull    # 把GitHub远程仓库的最新版本拉到本地
git clone   # 把GitHub上的远程仓库完整复制到本地
```

### 关键概念：Git的三个核心区域流转
理解该流程能解决80%的Git困惑，改动需按步骤流转，不可直接一键上传：
**工作区** →`git add`→ **暂存区** →`git commit`→ **本地仓库** →`git push`→ **远程仓库（GitHub）**
- 工作区：本地正在编辑代码的目录，改动最初存于此；
- 暂存区：筛选改动的“中转站”，可选择部分改动提交为一个版本，其余留到后续；
- 本地仓库：保存代码所有版本的本地空间，是Git的核心存储区。

## 三、实操入门：搭建第一个GitHub仓库（完整工作流）
看完基础后立即动手，完成从创建到推送的闭环，所有复杂操作都是该流程的变体。
1. 注册GitHub账号，安装Git（Windows从git-scm.com下载，Mac自带，Linux用包管理器安装）；
2. 本地Git基础配置（用户名/邮箱会出现在commit记录中）：
   ```bash
   git config --global user.name "你的名字"
   git config --global user.email "你的邮箱"
   ```
3. GitHub网页端创建新仓库：右上角「+」→「New repository」，命名后勾选「Add a README file」并创建；
4. 将远程仓库克隆到本地并进入目录：
   ```bash
   git clone https://github.com/你的用户名/仓库名.git
   cd 仓库名
   ```
5. 本地修改、提交并推送到GitHub：
   ```bash
   echo "Hello GitHub" > hello.txt  # 新建文件
   git status                       # 查看文件改动状态
   git add hello.txt                # 加入暂存区
   git commit -m "添加了hello.txt"  # 提交到本地仓库（备注提交信息）
   git push                         # 推送到GitHub远程仓库
   ```
6. 刷新GitHub仓库页面，验证文件是否同步成功。

## 四、协作基础：分支的核心用法
单人开发可暂用基础命令，**协作开发必须掌握分支**，也是GitHub协作的核心。
1. **分支的意义**：复制一条平行的代码时间线，可在分支上尝试新功能/修改代码，不影响主分支代码；尝试成功则合并到主分支，失败则直接删除分支。
2. **分支核心命令**：
   ```bash
   git checkout -b new-feature  # 创建新分支并立即切换
   git checkout main            # 切回主分支（main为默认主分支）
   git merge new-feature        # 将新分支的改动合并到主分支
   ```
3. **GitHub协作核心流程（GitHub Flow）**：
   fork目标仓库 → 本地创建分支 → 分支上修改代码 → 提交并推送分支 → 提Pull Request（PR）→ 项目维护者review → 合并到主仓库。

## 五、实用功能：快速做出有产出的成果
学工具的最佳方式是做实际项目，GitHub的这些功能入门即可用，零成本易上手。
### 1. GitHub Pages：免费搭建个人网站
无需服务器、域名（可绑定自定义域名），步骤极简：
- 创建新仓库，仓库名必须为「你的用户名.github.io」；
- 向仓库中放入`index.html`文件并推送；
- 几分钟后访问「https://你的用户名.github.io」，即可打开个人网站（可放介绍、项目、笔记等）。

### 2. .gitignore 文件：过滤无需提交的文件
部分文件（临时文件、编译产物、密钥、node_modules等）无需推送到仓库，可通过.gitignore文件过滤：
- 在仓库根目录创建`.gitignore`文件，写入需忽略的文件/文件夹名称；
- 可直接复用GitHub官方模板仓库：[github/gitignore](sslocal://flow/file_open?url=https%3A%2F%2Fgithub.com%2Fgithub%2Fgitignore&flow_extra=eyJsaW5rX3R5cGUiOiJjb2RlX2ludGVycHJldGVyIn0=)，包含各语言/框架的.gitignore模板。

### 3. 学会看优秀的开源仓库
GitHub最有价值的是他人的开源项目，入门先看**项目运作方式**（而非代码细节）：
- 目录结构、README文档的编写方式；
- Issue和PR的管理逻辑、CI/CD自动化配置；
- 项目的代码规范。
**推荐入门仓库**：
- github/docs：结构清晰的官方文档仓库；
- firstcontributions/first-contributions：专门指导新手完成第一次PR的项目；
- EbookFoundation/free-programmingbooks：学习如何组织大量信息的README范例。

## 六、高效学习：一周入门路径（每天1-2小时）
为纯新手设计的路径，完成后具备基本的代码管理和协作能力，拥有“活着”的GitHub主页。
1. 第1天：理解Git与GitHub的区别，安装Git并配置用户名/邮箱；
2. 第2天：创建第一个GitHub仓库，走通`add→commit→push`完整流程；
3. 第3天：学会`git status`/`git log`/`git diff`，能查看代码变更记录；
4. 第4天：掌握分支的核心操作（创建、切换、合并）；
5. 第5天：在first-contributions仓库完成第一次Pull Request；
6. 第6天：用GitHub Pages搭建个人专属页面；
7. 第7天：找感兴趣的开源项目，阅读其README并翻看Issue区。

## 七、进阶理念：从“会用”到“懂”Git
1. **无需一步学完**：Git的rebase、cherry-pick、submodule、GitHub Actions等进阶知识点，**用到再学**即可，专业开发者也未必完全掌握；
2. **理解底层模型**：使用一段时间后，可了解Git底层（.git目录的内容、commit对象、分支本质是指针），从“照着敲命令”变成“理解命令背后的逻辑”，遇到问题不再慌乱；
3. **拒绝“只准备不实操”**：收藏教程、买书籍不如敲下第一个`git init`，很多人在“准备学”上花的时间远多于实际学习；
4. **允许试错**：入门时的错误（如force push覆盖远程仓库）是正常的，试错后的理解远比纯看教程更深刻；
5. **核心原则**：**今天就开始**，哪怕只是创建一个只有README的仓库，第一步是最难的，也是唯一重要的，剩下的边用边学即可。