# DevOps Activity Log Project

## 🧭 About This Repository

This repository automatically updates my GitHub activity log every day using GitHub Actions.

## Owner

- **Name:** Saisai568  
- **Course:** DevOps  

## My Recent GitHub Activity

<!--START_SECTION:activity-->
- 🚀 Pushed commits to [Saisai568/devops-pages-lab](https://github.com/Saisai568/devops-pages-lab) - Dec 02
- ✨ Created repository or branch [YeMiao1026/CloudFinalProject](https://github.com/YeMiao1026/CloudFinalProject) - Dec 01
- ⭐ Starred [k88hudson/git-flight-rules](https://github.com/k88hudson/git-flight-rules) - Dec 01
- 🚀 Pushed commits to [YeMiao1026/TixMaster](https://github.com/YeMiao1026/TixMaster) - Dec 01
- 🚀 Pushed commits to [YeMiao1026/TixMaster](https://github.com/YeMiao1026/TixMaster) - Dec 01
<!--END_SECTION:activity-->

## 工作流程說明（Workflow）

下面的說明與圖表描述一個典型的靜態網站（例如 Jekyll）從開發到部署到 GitHub Pages 的完整流程；已用中文說明並附上 Mermaid 圖表（GitHub 支援 Mermaid，可直接在 README 中顯示）。

### 假設

- 原始碼儲存在 `main` 分支，使用 Jekyll（有 `_config.yml`、`index.md` 等）。
- 使用 GitHub Actions 作為 CI，部署目標為 GitHub Pages（或透過 `gh-pages` branch 部署）。

### 總覽圖（Mermaid）

```mermaid
flowchart LR
 Dev[Developer\n(。local dev / branch)]
 Repo[Git Repo\n(push / PR)]
 CI[CI: GitHub Actions\n(build/test/lint)]
 Artifact[Site Artifact\n(_site 或 pages-artifact)]
 Deploy[Deploy Action\n(Pages / gh-pages)]
 CDN[CDN / Browser Cache]
 Users[End Users / Browser]
 Monitor[Monitoring & Alerts]

 Dev -->|push / PR| Repo
 Repo -->|on push/PR| CI
 CI -->|build| Artifact
 artifact -->|upload/deploy| Deploy
Deploy --> CDN
CDN --> Users
Deploy --> Monitor
CI -->|preview (optional)| Deploy
```

### ASCII fallback（簡易文字版）

- Developer -> Git Repo (push / PR)
- Git Repo -> CI (build, test, lint)
- CI -> Artifact (site build)
- Artifact -> Deploy Action -> GitHub Pages -> CDN -> Users

### 逐步說明（重點）

1. 本地開發與預覽：使用 `bundle exec jekyll serve --livereload` 或 Docker（`jekyll/jekyll` image）快速預覽。
2. Push / PR：每次 push 或建立 PR 時觸發 CI，執行 build、lint、測試與產生 artifact（`_site`）。
3. 部署：合併到 `main` 後，由 deploy job 把 artifact 發佈到 GitHub Pages 或推送至 `gh-pages` 分支。
4. 監控與通知：部署完成後執行 smoke test（檢查重要頁面回傳 200），並把結果通知 Slack/Email；必要時以 artifact 回滾到上一次成功版本。

### 簡短範例（本地檢查）

```powershell
# 安裝與預覽（若使用 Bundler）
gem install bundler
bundle install
bundle exec jekyll serve --livereload

# Docker 選項（PowerShell）：
docker run --rm -it -p 4000:4000 -v ${PWD}.Path:/srv/jekyll -w /srv/jekyll jekyll/jekyll jekyll serve

# 簡易 smoke test
Invoke-WebRequest -UseBasicParsing http://localhost:4000
```

---
