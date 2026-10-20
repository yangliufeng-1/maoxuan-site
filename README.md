# 毛泽东选集 · 数字阅读

一个基于 [OINK](https://oink.pgsty.com/)（Hugo 文档框架）搭建的《毛泽东选集》篇目索引与阅读导航站点。

站点只收录**篇目信息与本站撰写的导读文字**，不提供著作正文。正文请以人民出版社《毛泽东选集》（第二版）为准。

## 站点结构

| 路径 | 内容 |
| --- | --- |
| `/` | 首页（hero / cards / cta 三段式） |
| `/book/` | 书目：第一至第四卷的篇目结构，按历史时期分章 |
| `/docs/guide/` | 怎么读：三条读法、按主题找篇目、常见误区 |
| `/docs/jingdu/` | 名篇精读：九篇高频引用文章的逐篇导读 |
| `/docs/editions/` | 版本沿革与常引篇目索引 |
| `/blog/` | 随笔：单篇细读与阅读方法 |

## 本地构建

主题以**本地目录**方式装在 `themes/oink`（`hugo.yaml` 中 `theme: oink`），不需要 Go Modules。SCSS 由 **Dart Sass** 编译，因此用普通版 Hugo 即可（不要求 extended）。

```bash
# 需要 Hugo 0.167.0+ 与 Dart Sass（sass 可执行文件）
export DART_SASS_BINARY="/path/to/sass"   # Windows 为 sass.exe

hugo server --port 1313        # 本地预览 http://127.0.0.1:1313/
hugo --gc --minify --cleanDestinationDir   # 生成静态文件到 public/
```

注意两点：

- `hugo.yaml` 的 `security.exec.allow` 必须放行 `sass`，否则 Hugo 拒绝执行转译器。
- 不要用 `rm -rf public` 清理，改用 `--cleanDestinationDir`。

## 部署

### GitHub Pages（自动）

推送到 `main` 即触发 `.github/workflows/github-pages.yaml`：安装 Hugo 与 Dart Sass → 构建 → 发布到 Pages。`baseURL` 由 `actions/configure-pages` 自动注入，支持 `https://<user>.github.io/<repo>/` 子目录。

### 其他静态托管

`public/` 是纯静态产物，可直接上传到任意静态托管：

```bash
hugo --gc --minify --cleanDestinationDir --baseURL "https://你的域名/"
```

## 主要编辑位置

- `hugo.yaml`：站点标题、语言、主题色、输出格式。
- `data/home/zh.yaml`：首页所有文案。
- `content/book/`：四卷篇目表。
- `content/docs/jingdu/`：名篇导读。
- `static/favicon.svg`：站点图标。

## 内容准确性说明

篇目名称与写作时间依据求是网、人民网公布的《毛泽东选集》目录整理。个别篇目的具体日期与编排顺序请以人民出版社正式出版物为准。
