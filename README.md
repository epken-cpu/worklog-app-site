# 記工e指算 — 上架用公開網站（GitHub Pages）

這個資料夾就是要發佈到 GitHub Pages 的靜態網站，提供 App Store / Play Console 要求的公開網址：

| 頁面 | 路徑 | 上架欄位 |
|---|---|---|
| 首頁／行銷 | `/` | Marketing URL |
| 隱私權政策 | `/privacy/` | Privacy Policy URL（**必填**）|
| 服務條款 | `/terms/` | Apple 訂閱 App 必填 EULA |
| 客服支援 | `/support/` | Support URL（**必填**）|

## 部署步驟（一次性，Ken 手動）

> GitHub 帳號沿用 `epken-cpu`（點工e指簽的站台在同一個帳號下），
> repo 命名 `worklog-app-site`，完成後網址是
> `https://epken-cpu.github.io/worklog-app-site/`。

1. 在 GitHub 建一個**新的 public repo**，名稱 `worklog-app-site`（不要勾 Add README）。
2. 在這個 `site/` 資料夾開終端機，執行：

```powershell
cd "C:\Users\Ken\Ken agent\workspace\Engineering\worklog_app\site"
git init
git add .
git commit -m "記工e指算 上架公開頁：隱私權／條款／客服"
git branch -M main
git remote add origin https://github.com/epken-cpu/worklog-app-site.git
git push -u origin main
```

3. 到 repo 的 **Settings → Pages**：
   - Source 選 **Deploy from a branch**
   - Branch 選 **main**、資料夾選 **/(root)** → Save
4. 等 1～2 分鐘，確認以下四個都打得開：
   - `https://epken-cpu.github.io/worklog-app-site/`
   - `https://epken-cpu.github.io/worklog-app-site/privacy/`
   - `https://epken-cpu.github.io/worklog-app-site/terms/`
   - `https://epken-cpu.github.io/worklog-app-site/support/`
5. 回頭把 `app/lib/core/config/subscription_constants.dart` 的
   `privacyPolicyUrl` / `termsOfUseUrl` 換成上面的網址（目前已預填，網址若不同要改）。

> ⚠️ 這個 `site/` 是**獨立的 git repo**（自己的 `.git`），
> 跟 `Ken agent` 主 repo（純本機、絕不推遠端）是兩回事，不要搞混。

## 之後要改內容

直接改這資料夾的 `.html`，再：

```powershell
git add . ; git commit -m "更新內容" ; git push
```

過 1～2 分鐘自動更新。

## 本機預覽

```powershell
cd "C:\Users\Ken\Ken agent\workspace\Engineering\worklog_app\site"
python -m http.server 8777
# 瀏覽器開 http://localhost:8777/
```

## 上架欄位怎麼填（對照表）

| 商店欄位 | 填這個 |
|---|---|
| Google Play 隱私權政策 | `https://epken-cpu.github.io/worklog-app-site/privacy/` |
| App Store Privacy Policy URL | `https://epken-cpu.github.io/worklog-app-site/privacy/` |
| App Store Support URL | `https://epken-cpu.github.io/worklog-app-site/support/` |
| App Store Marketing URL（選填）| `https://epken-cpu.github.io/worklog-app-site/` |
| App Store EULA（訂閱必填）| `https://epken-cpu.github.io/worklog-app-site/terms/` |

## 樣式

主色定義在 `style.css` 最上面的 `--brand` / `--brand-soft`，
以及 `header.site .logo` 裡的那個字。**要跟 App 的主色一致**
（`app/pubspec.yaml` 的 splash 色與 `app/lib/core/theme/app_theme.dart` 的 `_primary`）。
