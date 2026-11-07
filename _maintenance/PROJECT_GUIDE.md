# 网站项目与维护说明

梳理日期：2026-11-07（Asia/Shanghai）。源码基线：`master`，`3a9e632a`。

本说明记录当前仓库的实际实现，供后续网站管理使用。修改前仍应检查最新 Git 状态和相关文件，不能把这里的数量、版本和问题清单视为永久不变。本目录以 `_` 开头，且未列入 Jekyll 的 `include`，用于保存维护资料。

## 1. 项目定位与发布关系

- 网站地址：`https://midasdming.github.io`，站主 Di Ming（明镝）。
- 源码仓库：`https://github.com/MidasDMing/midasdming.github.io.git`，当前分支 `master`。
- `origin` 为个人仓库；`upstream` 为 `https://github.com/alshedivat/al-folio.git`。
- 技术栈：Jekyll、Liquid、Markdown、YAML、BibTeX、Sass、少量 JavaScript，基于 al-folio 旧版定制；没有应用后端、数据库或管理后台。
- 内容编辑发生在源码文件；Jekyll 输出到 `_site/`，GitHub Actions 将产物发布。
- 本地缓存的 `origin/gh-pages` 为 `92c0941c`，提交说明指向源码 `3a9e632a`。已检查其中的生成 HTML；没有通过此次梳理确认实时线上内容或远端 Pages 设置。
- 本地 `gh-pages` 分支跟踪的是 `upstream/gh-pages`，不是个人站点发布分支；日常维护应修改源码分支，避免混用。
- 根目录 README 是上游主题说明，不是本站专用文档；现有远端分支也包含许多主题历史分支。

## 2. 页面与内容入口

| 功能 / 路由 | 内容来源 | 模板与补充数据 | 当前状态 |
| --- | --- | --- | --- |
| 首页 `/` | `_pages/about.md` | `_layouts/about.html`、`_includes/news.html`、`_includes/social.html` | 主导航 About；显示新闻和社交入口 |
| 论文 `/publications/` | `_bibliography/papers.bib`、`_pages/publications.md` | `_layouts/bib.html`、`_data/venues.yml`、`_data/coauthors.yml` | 主导航顺序 1 |
| 项目 `/projects/` | `_pages/projects.md`、`_projects/001_project.md` 至 `005_project.md` | `_layouts/page_projects.html`、`_includes/projects_horizontal.html` | 主导航顺序 2；横向项目卡片 |
| 教学 `/teaching/` | `_pages/teaching.md` | `_layouts/page.html` | 主导航顺序 3 |
| 研究组 `/advml-group/` | `_pages/advml_group.md` | `_layouts/page.html` | 主导航顺序 4；提供外部研究组链接 |
| 新闻 `/news/`、`/news/:path/` | `news.html`、`_news/*.md` | `_includes/news.html`、`_layouts/post.html` | 首页标题进入完整新闻列表 |
| 旧研究组 `/milo-group/` | `_pages/milo_group.md`、`_projects/101_project.md` 至 `110_project.md` | `_layouts/page_milo.html`、`_includes/projects_horizontal_milo.html` | `nav: false`，但仍生成页面 |
| 博客 `/blog/` | `blog/index.html`、`_posts/*.md` | post / distill / archive 模板 | 导航没有输出博客入口，但页面仍生成 |
| 404 `/404.html` | `404.html` | page → default | 3 秒后跳回首页 |
| RSS、站点地图、robots | 插件、`robots.txt` | feed / sitemap 插件 | RSS 图标启用；RSS 内容应另行核实 |

主导航在 `_includes/header.html` 中组装：首页单独处理，其余页面按 `nav_order` 排序并要求 `nav: true`。`nav: false` 仅隐藏入口，不取消生成或公开访问。

## 3. 首页与联系方式

- `_pages/about.md` 保存任职、教育经历、研究方向、办公地址及头像配置。
- 当前内容为重庆理工大学计算机科学与工程学院副教授，领导 AdvML-Group；研究方向包括机器学习、优化、AI 安全、可解释 AI。
- 头像：`assets/img/my_yellow_stone_pic.jpg`；右侧显示，未使用圆形裁剪。桌面头像容器宽度 30%，小屏为 100%。
- `_layouts/about.html` **直接写入**英文名、中文名、两条邮箱及中文字体链接。只修改 `_config.yml` 不会同步改变这些文本。
- 邮箱还出现在 `_config.yml` 的 `email`、`contact_note`，以及部分新闻署名中；变更联系方式时应搜索所有位置。
- 首页开关：`news: true`、`social: true`、`latest_posts: false`、`selected_papers: false`。
- 已配置社交入口：GitHub `midasdming`、LinkedIn `di-ming-757716aa`、Google Scholar `NQRaX1oAAAAJ`、邮箱、RSS。
- 研究组外链同时存在于首页正文和研究组页面；它是另一个网站，本站仓库不包含其实现。

## 4. 论文数据与展示规则

- 唯一主数据源为 `_bibliography/papers.bib`，当前 25 条；BibTeX 文件顶部的两行 `---` 是现有结构的一部分。
- 年份分布：2026 年 9 条、2025 年 4 条、2024 年 3 条、2023 年 2 条、2022 年 1 条、2020 年 1 条、2019 年 2 条、2013 年 3 条。
- `jekyll-scholar` 在论文页面执行 bibliography 标签，通过 `_layouts/bib.html` 渲染；年份分组按降序。没有显式配置同年条目的日期排序，变更后需检查实际输出。
- 当前 BibTeX key 没有重复；更新已有论文应保留 key，避免破坏关联引用。
- 文献类型影响发表场所字段：`article` 显示 `journal`，`inproceedings` / `incollection` 显示 `booktitle`，学位论文类型显示 `school`。
- 常用字段：`title`、`author`、`year`、`month`、`journal` / `booktitle`、`pages`；`abbr` 是会议期刊徽标，`abbr_ccf` 是等级徽标。
- `_data/venues.yml` 定义徽标颜色和外链；新增缩写时通常需要同步检查。没有对应配置时模板仍能显示缩写。
- 作者姓名当前使用 HTML 标记，例如 `<b>Ming*</b>, <b>Di</b>`、`Ren<b>#</b>, Peng`；`*` 表示通讯作者，`#` 表示指导学生。需保留既有显示约定。
- `_config.yml` 中 scholar 的 `first_name` / `last_name` 仍为 `[...]` 占位，不能假设自动高亮本人姓名已正确配置；当前主要依赖手写 HTML。
- `_data/coauthors.yml` 仍是主题示例姓名，真实合作者主页没有系统配置。
- 超过 10 名作者时模板提供点击展开；JS 位于模板内。
- 资源按钮由非空字段控制：`abstract` → Abs，`arxiv` → arXiv，`bibtex_show` → Bib，另有 `html`、`pdf`、`supp`、`blog`、`code`、`poster`、`video`、`slides`、`website`。
- `pdf` / `supp` / `poster` / `video` / `slides` 含 `://` 时使用外部 URL，否则补上 `/assets/pdf/`；本地附件应填写文件名并确保大小写一致。
- 摘要和 BibTeX 由 `assets/js/common.js` 切换展开；导出的 BibTeX 经过 `_plugins/hideCustomBibtex.rb` 过滤站内字段。
- `selected: true` 只在精选论文组件被启用时决定展示；当前首页精选区关闭。
- Altmetric 和 Dimensions 开关均开启；具体徽章仍依赖 DOI、PMID 等识别信息。arXiv 按钮读取 `arxiv`，Altmetric 模板读取 `eprint`，两者字段并不相同。
- 论文接受消息、代码发布新闻与论文数据库分别存储，不会自动联动；应按更新内容同步维护相应新闻。

当前论文覆盖：Hybrid Priors / Sharpness UAP、Graph-Weighted CCA、ATR-UAP、PSD-DualRA、COPIA、TRIAD-Attack、LRS-Attack、DarkCORE、Diffusion Guidance、SMP-Attack、SL1AE-LSGLasso、Deep Robust Image Reconstruction、STFormer、ATT、EGS-TSSA、蛋白质相互作用分类、TRM-UAP、Weighted Activation UAP、ViT-P、博士论文、Exclusive L21、Probabilistic LASSO，以及 3 篇 2013 年皮肤镜分割论文。完整信息以 BibTeX 为准。

## 5. 新闻维护

- 当前 51 个文件，编号最大为 `announcement_55.md`；缺少 7–10 号，不应按文件数误认下一个编号为 52。
- 所有现有新闻为 `layout: post`、`inline: false`、`related_posts: false`。列表显示标题并链接到详情；`inline: true` 才直接显示正文。
- `_includes/news.html` 对 `site.news` 使用 `reverse`；本地缓存产物呈现日期从新到旧，文件编号与时间并非完全一致。
- 首页调用带 `limit=true`，限制 50 条；完整 `/news/` 页面显示 51 条。滚动区在超过 3 条时启用，最大高度为 `60vw`。
- 当前最新为 `announcement_55.md`，2026-11-04，COPIA 代码发布。
- 代码发布详情较完整的条目：11（TRM-UAP）、17（EGS-TSSA）、24（ATT）、40（SMP-Attack）、49（LRS-Attack）、55（COPIA），包含摘要、资料链接和引用，可作为内容结构参考。
- 常用 HTML 实体：`&#58;`（冒号）、`&#34;`（双引号）、`&#37;`（百分号）、`&#42;`（星号）；YAML 标题内有 `: ` 时必须正确加引号或使用块标量。
- 新消息先确定日期、标题、正文、是否需要详情页，再选用合适结构。新日期建议使用带空格的规范格式，例如 `2026-11-07 12:00:00 +0800`，但仍须验证生成后展示日期。
- `_config.yml` 没有明确 `timezone`。缓存产物中 53 号的 `2026-09-20 00:00:00+0800` 显示为 Sep 19，54 号的 `2026-09-25 01:00:00+0800` 显示为 Sep 24：已确认存在日期偏移，具体修复应结合构建时区验证。
- 新闻使用通用 post 布局，因此详情页日期下的年份链接指向 `/blog/:year/`；这是目前模板行为。

## 6. 项目、旧成员与教学

- `_projects` 同时承载科研项目和旧研究组成员，不能把所有文件都当成科研项目。
- 当前科研项目按 `importance` 升序显示：005 国家自然科学基金（2025–2026）、004 重庆自然科学基金（2024–2027）、002 重庆教委项目（2023–2026）、001 OMRON（2023）、003 校科研基金（2022–2025）。
- 项目字段：`layout`、`title`、`description`、`img`、`redirect`、`importance`、`category`；描述使用 HTML `<br>` 分行。5 个科研项目当前没有卡片图片。
- `_pages/projects.md` 的 `display_categories: [Projects]` 过滤出科研项目；分类字符串必须完全一致。
- 旧 MILO 页面展示 `Master Students`、`Undergraduate Students`、`Alumni`；10 个成员条目中为 8 名硕士、1 名本科生、1 名校友。照片位于 `assets/students-img/`，已核对引用文件存在。
- 所有 15 个项目 / 成员条目仍带 `redirect: https://unsplash.com`；卡片因此跳往 Unsplash，而不是本站详情页。若要修复，需选择真实目标或删除 redirect 并补全详情内容。
- `_layouts/page_milo.html` 直接写入 MILO 名称、`/assets/img/milo-group-v3-1.png` 和 `https://github.com/MILO-GRP`；修改页面 front matter 的 logo 配置不一定改变实际显示。
- `_layouts/page_milo_backup20240504A.html` 和 `_backup/` 为历史材料，当前页面不引用该备份布局。
- 教学是一个手写 Markdown 页面，没有独立课程数据库或课件系统。课程包括 Data Science（CS3102 / CS2020303）、Deep Learning（CS3201 / CS2030304）、Machine Learning（CS1030068 / CS1040194 / CS6030303）。
- 当前数据科学学期列表止于 Fall 2025；深度学习与机器学习列表止于 Spring 2026。后续按用户提供的学期事实增补。

## 7. 模板、外观与资源

- 主要渲染链：内容页 → about / page / page_projects / post → `_layouts/default.html` → head、header、footer 与 scripts。
- `assets/css/main.scss` 导入 `_sass/_variables.scss`、`_themes.scss`、`_layout.scss`、`_base.scss`、`_distill.scss`、`_cv.scss`。
- 颜色变量在 variables；浅深色 CSS 变量在 themes；通用布局在 layout；导航、头像、论文、卡片、博客、代码块等大部分规则在 base。
- 当前内容最大宽度 `800px`，导航和页脚固定；浅色强调色为紫色，深色为青色。移动端导航折叠，头像在 576px 断点改变宽度。
- 深浅色由 `assets/js/theme.js` 与 `dark_mode.js` 控制，偏好保存在 `localStorage.theme`，首次会参考系统主题。
- 数学公式、图片点击放大、Masonry、阅读进度条开启；ImageMagick 响应式 WebP 生成关闭。
- 主要前端依赖由 CDN 加载：Bootstrap 4.6.1、MDB 4.20.0、jQuery 3.6.0、Font Awesome 6.4.0、Academicons 1.9.1、MathJax 3.2.0、Masonry 4.2.2、medium-zoom 1.0.8、Bootstrap Table 1.21.4。
- `common.js` 管论文摘要 / 引用展开、目录和 notebook 样式；`no_defer.js` 管表格属性；`copy_code.js` 管代码复制；`masonry.js` 管网格；`zoom.js` 管图片放大。
- 阅读进度条实现于 `_includes/scripts/progressBar.html`；统计和站点验证开关关闭。
- favicon：`assets/img/d_icon_hign_res.jpg`，文件名中的 `hign` 为现有拼写，引用时保持一致。
- 本地论文 PDF：`AAAI19-4382.pdf`、`IJCAI19-0438.pdf`、`MING-DISSERTATION-2020.pdf`；另有主题演示 PDF。
- `_includes/figure.html` 为通用图片入口，支持尺寸、说明和缩放；`figure_logo.html` 是简化变体。
- `assets/js/distillpub/` 及 source map 是 Distill 的第三方资源，日常内容维护通常不需修改。

## 8. 博客、简历与其他模板遗留

- `_posts/` 共有 19 篇主题演示，覆盖 Markdown、图片、代码、数学、评论、Twitter、图表、表格、音视频、目录、notebook、引用等；不是站主的正式研究博客。
- 博客每页 5 篇，按日期倒序；支持 featured、标签 / 分类 / 年份归档、阅读时长和外链文章。
- `blog_name` / 描述仍为 al-folio；Giscus 和 Disqus 也仍指向主题配置，部分演示文章启用了它们。正式启用博客前需要清理这些设置。
- `_config.yml` 保留 `external_sources` 的 `https://medium.com/@al-folio/feed`。`_plugins/external-posts.rb` 会在构建时联网抓取并生成内存中的外部文章，无独立异常兜底；即使首页没有博客区，它仍会运行。
- RSS 不应默认理解为新闻订阅：news 是独立集合，现有 feed 配置没有明确将它加入，需检查实际 feed。
- `_layouts/cv.html` 支持 YAML CV 和 JSON Resume，但当前没有 CV 页面入口；`_data/cv.yml`、`assets/json/resume.json` 都是 Albert Einstein 示例。配置会把 JSON 加载到 `site.data.resume`，有数据时布局优先使用 JSON。
- `_data/repositories.yml` 也仍是主题示例仓库，没有对应的当前主导航页面。
- `_plugins/details.rb` 注册 Markdown 折叠块；`file-exists.rb` 注册文件存在性标签；其余两个插件负责外部文章和 BibTeX 过滤。
- 页面元数据由 `_includes/metadata.html` 输出；站点 description / keywords 仍是主题描述，Open Graph 与 Schema.org 均关闭。
- `robots.txt` 允许索引并声明 sitemap。隐藏导航的页面以及演示内容仍可能被访问或收录。

## 9. 构建与发布

- 依赖写在 `Gemfile`，没有固定 gem 版本，`Gemfile.lock` 被 Git 忽略；依赖解析随环境可能不同。
- `.github/workflows/deploy.yml` 在 master / main 的 push、pull_request 和手动触发时执行。
- 流程：checkout → Ruby 3.2 / bundler-cache → 安装 Jupyter 与 `mermaid.cli` → `JEKYLL_ENV=production bundle exec jekyll build` → 非 PR 事件部署 `_site`。
- 部署使用 `JamesIves/github-pages-deploy-action@v4`；workflow 未显式填 branch。本地缓存的个人发布产物位于 `origin/gh-pages`。实时发布分支、Pages 设置及运行状态应在实际发布时另查。
- `.github/workflows/deploy-image.yml` 限制 owner 为 alshedivat，个人仓库通常不运行该任务。
- `.github/workflows/deploy-docker-tag.yml` 在 `v*` 标签触发，仍保留上游 DockerHub 目标及 secrets 需求；常规内容更新不需要创建这类标签。
- 有两种 Docker 开发配置：预构建镜像 compose 挂载 `/srv/jekyll`；本地构建 compose 挂载 `/srv/jekyll_site`，与 Dockerfile 的工作目录 `/srv/jekyll` 不一致，不能未经验证当作可靠本地启动方式。
- `bin/cibuild` 执行带 `--lsi` 的构建，和 Actions 普通 build 略有区别。
- `bin/deploy` 是旧发布脚本，会删除 / 重建发布分支、删除工作树内容并强制推送；目前有 Actions 流程，日常维护不需执行该脚本。
- `.pre-commit-config.yaml` 配置了尾随空白、文件末尾换行、YAML 与大文件检查；存在配置不代表本机已安装 hook。

依赖准备好以后，可用以下命令进行本地验证：

```sh
bundle exec jekyll build --destination /tmp/midasdming-site-preview
bundle exec jekyll serve --host 127.0.0.1 --port 4000 --destination /tmp/midasdming-site-preview
```

生产验证应与 workflow 一样设置 `JEKYLL_ENV=production`；配置变更后需重启 serve。依赖安装和联网外部 feed 是独立前提。

## 10. 已发现问题与验证边界

以下为阅读所得，尚未修改网站行为：

1. 新闻时区偏移：已在缓存发布 HTML 中确认 53 / 54 号日期提前一天。
2. 项目及旧成员卡片全都指向 Unsplash 占位链接。
3. 部分论文资源按钮指向资料落地页，例如 LRS-Attack 的 `pdf` / `supp` 仍为 PMLR HTML 地址；若用户要求直接下载，应核实后更新。
4. 首页姓名与邮箱、旧研究组名称和 logo 存在模板硬编码，改配置不能覆盖全部。
5. 博客、评论、外部 Medium feed、CV、合作作者、仓库和 SEO 仍有主题示例数据。
6. 部分新闻 HTML 使用 `<a>` 作为结束标签，54 号标题 `<i>` 未闭合；浏览器可能自动修复，但后续编辑应使用正确闭合标签。
7. 构建依赖未锁定；目前本机系统 Ruby 为 2.6.10、Bundler 为 1.17.2，`bundle check` 报告缺少项目依赖，未执行完整构建。Actions 配置使用 Ruby 3.2。
8. 没有自动化测试套件或专门的链接检查 workflow；第三方 CDN、论文外链、实时部署结果未在本次逐一联网验证。

本次已完成：当前配置 / data / 页面 / 新闻 / 项目 / 博客的 YAML 解析检查，assets JSON 解析检查，模板 include 存在性检查，成员照片路径检查，论文 key 重复检查；均未发现相关错误。已读取缓存发布产物，确认首页 50 条新闻、完整列表 51 条新闻、论文页 25 条及年份分组。此验证不等于实时线上测试或重新构建通过。

## 11. 后续更新的操作约定

- 先检查工作区和实际文件，保留用户未提交的修改；内容事实以用户提供或经过核实的资料为准。
- 新论文：更新 BibTeX，检查徽标配置、作者标记、年份及附件；按请求同步录用 / 代码新闻。
- 新新闻：使用未占用的编号，规范 front matter 和 HTML；检查首页、完整列表、详情页及显示日期。
- 项目：核对 category 和 importance；要创建可访问详情时，还需检查 redirect 与正文。
- 联系方式或研究组信息：全仓搜索旧值，检查正文、模板、配置和历史页面中应同步的位置。
- 外观：优先在共享 Sass / 模板层修改，检查桌面、手机、深色和浅色；避免只调整一个页面而破坏共享组件。
- 更新后检查差异、语法、相关资源和链接；环境具备时构建并预览受影响页面，再按用户授权范围提交 / 推送。
- 发布后核对 Actions 状态及线上页面；只有确认成功后才报告已发布。
- 上述问题清单用于定位后续工作，不表示需要在每次更新中顺便全部重构。
