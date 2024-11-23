# Kotlin 中文站点
[![Official project][project-badge]][project-url]
[![Qodana Code Quality Check](https://github.com/JetBrains/kotlin-web-site/actions/workflows/qodana-code-quality-check.yml/badge.svg)](https://github.com/JetBrains/kotlin-web-site/actions/workflows/qodana-code-quality-check.yml)

Kotlin 语言官方网站为 [https://kotlinlang.org](https://kotlinlang.org) 。

<a id="project-structure"></a>

## 说明

本站是 [Kotlin 中文站（url）]() 的源码仓库，Fork 自 [JetBrains/kotlin-web-site](https://github.com/JetBrains/kotlin-web-site)。

* [站点结构](#website-structure)
* [贡献指南](#contribution)
* [本地部署](#local-deployment)
* [问题反馈](#feedback-and-issues)

## 站点结构

### 内容

| 页面                                                 | 源码文件                                                     |
|----------------------------------------------------|----------------------------------------------------------|
| [首页](https://kotlinlang.org/)                      | [templates/pages/index.html](templates/pages/index.html) |
| [Kotlin 文档](https://kotlinlang.org/docs/home.html) | [docs/topics](docs/topics)                               | 
| [社区](https://kotlinlang.org/community/)            | [pages/community](pages/community)                       | 
| [教育](https://kotlinlang.org/education/)            | [templates/pages/education](templates/pages/education)   | 

请注意，[服务端落地页](https://kotlinlang.org/lp/server-side/) 与 [Kotlin 多平台落地页](https://kotlinlang.org/lp/multiplatform/) 的源文件并未公开。

#### 不同仓库的源文件

语言规范、协程文档、Lincheck、Dokka，以及库开发者指南的源文件存储在不同的仓库中：

| 网站页面                                                                      | GitHub 仓库                                                           |
|---------------------------------------------------------------------------|---------------------------------------------------------------------|
| [协程文档](https://kotlinlang.org/docs/coroutines-guide.html)                 | [kotlinx.coroutines](https://github.com/Kotlin/kotlinx.coroutines/) |
| [Lincheck 文档](https://kotlinlang.org/docs/lincheck-guide.html)            | [kotlinx.lincheck](https://github.com/Kotlin/kotlinx-lincheck/)     |
| [Dokka 文档](https://kotlinlang.org/docs/dokka-introduction.html)           | [Dokka](https://github.com/Kotlin/dokka/)                           |
| [库作者指南](https://kotlinlang.org/docs/jvm-api-guidelines-introduction.html) | [api-guidelines](https://github.com/Kotlin/api-guidelines)          |
| [语言规范](https://kotlinlang.org/spec/introduction.html)                     | [kotlin-spec](https://github.com/Kotlin/kotlin-spec)                |

#### 自动生成的内容

[API 参考文档](https://kotlinlang.org/api/latest/jvm/stdlib/) 基于 Kotlin 代码中的注释生成。  
了解更多关于 [Kotlin 代码文档化](https://kotlinlang.org/docs/kotlin-doc.html) 的信息。

[Kotlin 语法参考](https://kotlinlang.org/docs/reference/grammar.html) 由 [Kotlin 语法生成器](https://github.com/Kotlin/website-grammar-generator) 根据 [Kotlin 语法定义](https://github.com/Kotlin/kotlin-spec/tree/release/grammar/src/main/antlr) 生成。


| 配置项       | 文件                                                                  |
|-----------|---------------------------------------------------------------------|
| 导航和结构     | 文档使用 [kr.tree](docs/kr.tree)，其他页面使用 [_nav.yml](data/_nav.yml)       |
| 变量（如版本号）  | 文档使用 [v.list](docs/v.list)，其他页面使用 [releases.yml](data/releases.yml) |
| 地图上的社区活动  | [events.xml](data/events.yml)                                       |
| 视频列表（已过时） | [videos.yml](data/videos.yml)                                       |

### 模板

Kotlin 网站使用 [Jinja2](https://jinja.palletsprojects.com/en/2.11.x/) 模板，存放在 [templates](templates) 目录下。  
注意，除 [docs](docs) 外，所有 Markdown 文件在转换为 HTML 前会被处理为 Jinja 模板。  
这允许在 Markdown 文件中使用 Jinja 的全部功能（例如通过 `url_for` 函数构建 URL）。

## 贡献指南

你可以通过发送 Pull Request 为 Kotlin 中文站点做贡献。  
你也可以 [创建 YouTrack 问题](https://youtrack.jetbrains.com/newIssue?project=KT)，与 Kotlin 官方团队讨论你的建议。

- 对于 Kotlin 文档，请遵循 [风格和格式化指南](https://docs.google.com/document/d/1mUuxK4xwzs3jtDGoJ5_zwYLaSEl13g_SuhODdFuh2Dc/edit?usp=sharing)。
- 对于其他页面，请参考 [kramdown](https://kramdown.gettalong.org/syntax.html) 网站的完整语法。
- 你还可以让页面包含元数据字段，详细内容请参见 [Jekyll 文档](https://jekyllrb.com/docs/front-matter/)。

### Kotlin 用户组

要添加 Kotlin 用户组 (KUG)，请按照以下步骤操作：
1. 打开配置文件 [user-groups.yml](/data/user-groups.yml)。
2. 在已有的分组中找到合适的部分。
3. 在选定的部分中添加一个新的组，包含以下键：
   - `name`：组的名称。
   - `country`：组所在国家的名称。如果是虚拟组，请使用 "International"。
   - `url`：组的网页链接。
   - `isVirtual`：如果组仅在线活动，请将此键的值设为 `true`。
   - `position`：组的地理位置，由一对键 `lat` 和 `lng` 定义。可以运行 `scripts/user_group` 进行生成。
4. 如果该组不是虚拟组，还需要手动指定组的位置。
   你可以通过添加 `position` 键并指定 `lat` 和 `lng` 值的方式，例如： 

   ```yaml
   position:
     lat: 1.1111111
     lng: 1.1111111
   ```

   或者手动运行定位脚本 (`scripts/user_groups_geolocator.py`) 来获取组的位置。
   你需要获取 `GOOGLE_API_KEY` 并运行以下命令:

   ```
   $ GOOGLE_API_KEY="..." python scripts/universities_geolocator.py
   ```

   关于 `GOOGLE_API_KEY` 参数的更多信息，请参考 [Google 的这篇文章](https://developers.google.com/maps/documentation/geocoding/get-api-key)。 
   手动的方法有时候会更好，因为它可以让你更精确地指定组的位置。  

你可以在 [JSON schema 文件](/data/schemas/user-groups.json) 中查看预期配置的结构和类型。
提交 Pull Request 后，[GitHub Actions Workflow](.github/workflows/validate-user-groups-data.yml) 会验证更改，以防止配置错误。

### 社区活动

要在社区活动中添加事件，请执行以下操作：
1. 在 [events.yml](/data/events.yml) 中填写事件信息，具体如下：
   - `lang`：两字母代码，遵循 [ISO 639-1 格式](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)。
   - `startDate`：格式为 "yyyy-mm-dd"。
   - `endDate`：格式为 "yyyy-mm-dd"。对于单日事件，填写与 `startDate` 相同的日期。
   - `location`：格式为 “城市, 国家”。对于在线事件，可以省略。
   - `online`：如果是在线事件，将此键的值设为 `true`。
   - `speaker`：演讲者的名字。
   - `title`：事件的标题。
   - `subject`：演讲的主题。
   - `url`：事件网页的链接。
  
   你可以在 [JSON schema 文件](/data/schemas/events.json) 中查看预期配置的结构和类型。

2. 创建 Pull Request 发布更改。更改将由 [GitHub Actions Workflow](.github/workflows/validate-events-data.yml) 验证，以防止配置错误。

## 本地部署

目前无法在本地部署 Kotlin 网站。此功能正在开发中，跟踪进展请参考 [KT-47049](https://youtrack.jetbrains.com/issue/KT-47049).

你可以通过向官方发送 Pull Request 来为 Kotlin 网站做贡献。

## 问题反馈

你可以：

* 向官方的 [问题跟踪器](https://youtrack.jetbrains.com/newIssue?project=KT) 提交问题。
* 在 Kotlin 的公共 Slack 中（[前往申请](https://surveys.jetbrains.com/s3/kotlin-slack-sign-up)），通过 [#kotlin-website](https://kotlinlang.slack.com/archives/C02B3PECK6E) 频道分享反馈。
* 发送邮件至 [doc-feedback@kotlinlang.org](mailto:doc-feedback@kotlinlang.org).

[project-url]: https://confluence.jetbrains.com/display/ALL/JetBrains+on+GitHub
[project-badge]: https://jb.gg/badges/official.svg
[slack-url]: https://slack.kotlinlang.org

## 本地开发

#### 准备工作：Python3 环境

```
# 安装前端以来
yarn install

# 初次运行时需要构建静态文件
yarn run next-build-static

# 运行 NextJS 服务器
yarn run next-dev

# 为其他内容运行 webpack 开发服务器
yarn start

# 安装 Python 服务器的依赖
pip  install --no-build-isolation -r requirements.txt

# 运行 Python 服务器
python3 kotlin_website.py
```
随后在浏览器中打开 [http://localhost:9000](http://localhost:9000)。


## 使用 Next.js 的页面

你可以在 [pages](pages) 目录中找到所有的页面。

### 项目结构

- **组件（Components）**，基础构建模块。
- **块（Blocks）**，组件的组合，形成相对复杂的、独立的界面部分。
- **页面（Pages）**，每个页面根据其文件名对应的路由相关联。

### Next.js 中的图片

需要注意的是，`next/image` 不支持将图片导入 HTML 文件（SSG）。
请使用 "next-optimized-images" 中的 `Img` 和 `Svg` 组件代替。

# 测试

我们使用 Playwright 编写端到端 (e2e) 测试和截图测试。
详情请参阅 [Playwright 官方文档](https://playwright.dev/)。

## 前置条件

为了在本地运行测试，需要进行以下操作：
1. 安装支持的浏览器:

   ```
   npx playwright install
   ```

2. 启动开发服务器。

## 运行测试

- 使用 `yarn test` 在本地无头模式下运行所有测试。
- 使用 `yarn test:e2e` 在本地运行端到端测试，包括可视化测试。
- 使用 `yarn test:e2e:skip-visual` 在本地运行不包含可视化测试的端到端测试。
- 使用 `yarn test:production` 在本地运行子集端到端测试，用于验证生产环境。

还有以下其他选项可供运行测试：
- 使用 `yarn run test:e2e:ci` 或 `yarn test:production:ci` 在 CI 环境中运行测试。
- 使用 `yarn test:e2e:headed` 或 `yarn test:production:headed` 在本地有头模式下运行测试。
- 使用 `yarn test:e2e:debug` 或 `yarn test:production:debug` 在本地有头调试模式下运行端到端测试。

为了简化添加和维护端到端测试的过程：
- 使用 `yarn test:e2e:new` 生成用户交互测试。
- 使用 `yarn test:e2e:update` 更新页面有意更改后的截图。

## 编写测试

要编写端到端测试，请在 `/test/e2e/*your-page*.spec.js` 中创建规范文件。

## WebHelp 测试

部分端到端测试用于防止用于生成 [kotlinlang.org](https://kotlinlang.org) `/docs` 部分文档的 WebHelp 组件出现回归问题。  
本地运行这些测试，请按照以下步骤：

1. 在项目中创建 `dist` 文件夹
2. 打开 TeamCity 上 [Reference Docs](https://buildserver.labs.intellij.net/buildConfiguration/Kotlin_KotlinSites_KotlinlangTeamcityDsl_BuildReferenceDocs?branch=&mode=builds#all-projects) 的最后一次成功构建
3. 下载该构建的工件，并将其放入 `dist` 文件夹
4. 使用 `yarn run test:e2e` 本地运行测试
5. 使用以下命令在 Docker 容器中运行测试：
   ```shell
   docker compose -f docker-compose-e2e-statics.yml up --build  --exit-code-from playwright
   ```

## API 引用测试

部分测试旨在保护 API 引用的 HTML 标记不被 Dokka 模板扩展中的 KTL 组件破坏。  
若要在本地运行这些测试，请按照以下步骤操作：

1. 在项目中创建 `libs` 文件夹。
2. 打开 TeamCity 上每个 API 引用的最后一次成功构建。
3. 下载这些构建的工件，并根据其名称（例如 `kotlinx.coroutines`）将它们放置在 `libs` 文件夹中。
4. 启动容器：`./scripts/dokka/up.sh`。
5. 在容器或是主机上使用 `./scripts/dokka/run.sh` 运行测试。

## 翻译贡献

我们欢迎所有人为 Kotlin 中文站点的翻译做贡献。你可以对现有的翻译进行校对，或者对未翻译的内容进行翻译。

详情参阅 [TRANSLATE_CONTRIBUTING.md](TRANSLATE_CONTRIBUTING.md)。