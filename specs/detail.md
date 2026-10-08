# 藍天咖啡網站｜逆向工程完整規格書（Web Specification）

> **來源檔案**：`WebPage-_11515220/outline/index.html`  
> **文件用途**：依據現有網頁實作原始碼逆向分析建立標準規格文件，供後續精確修改、功能擴充與品質驗收。  
> **檔案 SHA-256**：`093D6C7641CC0FD69C59679B707083630A96A2DDFA38D2FE9A3994C56A3D0EB7`  
> **規格版本**：v1.0 (Reverse Engineered)  
> **建立日期**：2026-10-08  

---

## 1. 專案與品牌概述

### 1.1 基本資訊
| 項目 | 內容規格 |
|---|---|
| **品牌名稱** | 藍天咖啡（BLUE SKY COFFEE） |
| **品牌創立** | TAIPEI · TAIWAN · EST. 2018 |
| **品牌核心標語** | 「讓風味，在藍天下慢慢抵達。」 |
| **副標語／主張** | 「慢一點，更清楚。」（LET THE FLAVOUR SPEAK）／「BREW SLOW · LIVE BRIGHT」 |
| **網站類型** | 單頁式精品手沖咖啡品牌形象與商品導覽展示頁（One-page Landing Page） |
| **目標客群** | 喜愛單一產區手沖咖啡、重視生活儀式感與風味層次的質感咖啡愛好者 |
| **主要轉換目標 (CTA)** | 1. 探索本季咖啡選豆 (`#coffee`)<br>2. 收藏咖啡豆意向 (`data-coffee`)<br>3. 訂閱電子報「風味通信」(`#visit`) |
| **品牌語調** | 靜謐、優雅、誠懇、明亮、步調從容，文字著重風土、時間、水溫與感官描述 |

---

## 2. 技術架構與邊界限制

### 2.1 技術選型
- **HTML**：HTML5 語意化標籤架構（`header`, `nav`, `main`, `section`, `article`, `ol`, `footer`）。
- **CSS**：原生 CSS3，無使用任何外部 CSS 框架或預處理器，全域採用 CSS Custom Properties（CSS 變數）。
- **JavaScript**：原生 ES6+，無第三方套件依賴（純 Vanilla JS）。
- **字型資源**：Google Fonts（`Noto Sans TC`, `Noto Serif TC`, `Playfair Display`），採用 `<link rel="preconnect">` 加速加載。
- **視覺插畫技術**：完全不使用外部圖片檔（零 HTTP 圖片請求），所有幾何圖形、太陽、山脈、濾杯、咖啡壺均透過 CSS `clip-path`、`radial-gradient`、`linear-gradient`、`border-radius` 與陰影繪製。
- **打包模式**：單一獨立 HTML 檔案（CSS 於 `<style>` 區塊，JS 於尾端 `<script>` 區塊），可直接以瀏覽器本地開啟運行。

---

## 3. SEO 與基礎中繼資料（Metadata）

```html
<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="藍天咖啡，為手沖咖啡愛好者挑選當季精品咖啡豆，讓每一杯都清澈、明亮、值得細品。">
  <title>藍天咖啡｜讓風味，慢慢抵達</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@400;500;600;700&family=Noto+Serif+TC:wght@500;600;700;900&family=Playfair+Display:ital,wght@0,600;0,700;1,600&display=swap" rel="stylesheet">
</head>
```

---

## 4. 視覺系統與設計 Token

### 4.1 色彩變數清單（CSS Custom Properties）
| Token 名稱 | 色碼 Hex | 語意說明與主要用途 |
|---|---|---|
| `--navy` | `#062742` | 深藍色：Hero 主背景、Visit 訂閱背景、Toast 背景、第一款商品卡底色 |
| `--blue` | `#0c5b95` | 品牌主藍：區塊小標 (eyebrow)、標題強調斜體、幾何線條、品牌章卡片底色 |
| `--sky` | `#75c6e8` | 天空藍：裝飾圓環、高亮文字、深色區 eyebrow、按鈕焦點輪廓 (focus outline) |
| `--mist` | `#eaf5f7` | 晨霧淺藍灰：本季選豆區 (`#coffee`) 背景色 |
| `--cream` | `#fbfaf6` | 暖米白：網頁主體背景色 (`body background`) |
| `--ink` | `#122534` | 墨深灰藍：淺色區主要文字色彩 |
| `--muted` | `#607482` | 柔和灰藍：次要內文、描述說明、步驟補充文字 |
| `--line` | `#d7e4e8` | 淺藍灰分隔線：表格框線、步驟清單上下邊框 |
| `--sand` | `#e5b66b` | 暖沙金：主按鈕底色、Toast 左側重點裝飾邊條、商品收藏 Hover 色 |
| `--shadow`| `0 18px 50px rgba(6, 39, 66, .13)` | 全域浮層陰影（卡片、Toast、標章浮卡） |

### 4.2 字體家族與層級排版
1. **內文與通用介面字體**：`"Noto Sans TC", sans-serif`（字重 400, 500, 600, 700），基底尺寸 16px，行高 1.7。
2. **中文標題與展示字體**：`"Noto Serif TC", serif`（字重 700, 900），字距約 `.035em` 到 `.075em`。
3. **英文襯線與重點數據**：`"Playfair Display", serif`（字重 600, 700），用於品牌首字母 `B`、英文字、數字與溫度標註。
4. **字級規範**：
   - Hero 主標題 (`.hero-title`)：`clamp(42px, 5.5vw, 68px)`，行高 1.22，粗體 900。
   - 區塊標題 (`.section-title`)：`clamp(30px, 4vw, 46px)`，行高 1.28，粗體 700。
   - 眉標 (`.eyebrow`)：11px、字重 700、字距 `.18em`，大寫。
   - 內文段落 (`.section-copy`, `.hero-lede`)：14px ~ 16px，最長行寬約 `48ch`。

### 4.3 全域排版容器與通則
- **主容器 (`.wrap`)**：`width: min(1120px, calc(100% - 48px)); margin: 0 auto;`（手機版降為 `calc(100% - 34px)`）。
- **圓角規範**：主要按鈕圓角僅 `2px`，維持極簡、專業俐落質感。
- **無障礙焦點**：`:focus-visible` 統一提供 `3px solid var(--sky)`，偏移 `4px`。
- **捲動行為**：`html { scroll-behavior: smooth; }`。

---

## 5. 頁面架構與各區塊詳細規格

```
<body>
 ├── header.site-header#top          (頂部導覽列)
 └── main
      ├── section.hero               (主視覺 Hero 區)
      ├── section.intro#story        (品牌哲學區)
      ├── section.coffee-section#coffee (本季選豆商品卡)
      ├── section.brew#brew          (手沖日常與三步驟)
      └── section.visit#visit        (電子報訂閱轉換區)
 ├── footer                          (頁尾資訊與版權)
 ├── div.toast#toast                 (全域提示框)
 └── script                          (互動功能程式碼)
```

---

### 5.1 頁首導覽（Header & Navigation）

- **結構**：
  ```html
  <header class="site-header" id="top">
    <nav class="nav wrap" aria-label="主要導覽">
      <a class="brand" href="#top" aria-label="回到藍天咖啡首頁">
        <span class="brand-mark">B</span>
        <span>藍天咖啡<small>BLUE SKY COFFEE</small></span>
      </a>
      <button class="menu-toggle" type="button" aria-label="開啟導覽選單" aria-expanded="false" aria-controls="navLinks">☰</button>
      <div class="nav-links" id="navLinks">
        <a href="#story">我們的堅持</a>
        <a href="#coffee">本季選豆</a>
        <a href="#brew">沖煮日常</a>
        <a class="nav-cta" href="#visit">訂閱風味通信</a>
      </div>
    </nav>
  </header>
  ```
- **樣式與行為**：
  - 定位：`position: absolute; z-index: 10; width: 100%;` 覆蓋於 Hero 區塊之上。
  - 高度：桌面版最低 78px，手機版最低 68px。
  - 下邊框：`1px solid rgba(255, 255, 255, .16)`。
  - 品牌 Logo：圓形 29px，帶 1px 天空藍框線與 Playfair 字體 "B"，右側中文 20px 搭配小字英文 `BLUE SKY COFFEE`。
  - 連結懸浮動態：一般連結 hover 時底部自右向左展開 1px 天空藍底線；CTA 按鈕帶白色邊框，hover 時反白為白底深藍字。

---

### 5.2 主視覺區（Hero Section）

- **區塊屬性**：`<section class="hero" aria-labelledby="heroTitle">`
- **外觀尺寸**：桌面版最低高度 704px，背景為深藍 `--navy`，具備多重 CSS 漸層與天空藍光暈同心圓。
- **內容配置（兩欄網格 `1.02fr .98fr`，欄距 45px）**：
  - **左欄（文字與動作引導）**：
    - Eyebrow：`HAND BREWED · SLOWLY ROASTED`（天空藍）
    - 主標題 `H1#heroTitle`：`讓風味，<br>在<span class="blue">藍天</span>下<br>慢慢抵達。`（「藍天」採用 `--sky`）
    - 導言段落：`藍天咖啡為喜歡手沖的你，挑選值得細品的單一產區咖啡豆。從第一縷花香，到最後一口回甘，每一杯都有自己的晴朗天氣。`
    - 行動按鈕組：
      1. `.button-primary`：`探索本季風味 →`（連往 `#coffee`，底色 `--sand`）
      2. `.button-outline`：`認識藍天`（連往 `#story`，白色外框）
    - 附註字樣：`TAIPEI · TAIWAN · EST. 2018`
  - **右欄（純 CSS 藝術插畫 `.hero-art`，`aria-hidden="true"`）**：
    - 太陽 (`.sun`)：直徑 166px 圓形，淡藍漸層與光暈。
    - 山脈 (`.mountain`)：多邊形 `clip-path` 裁切漸層山巒。
    - 咖啡器具組 (`.coffee-vessel`)：
      - 濾杯 (`.dripper`)：倒梯形幾何濾杯，內嵌刻度光影線。
      - 下壺 (`.carafe`)：流暢曲線玻璃分享壺，底部呈現深褐色咖啡萃取液體。
    - 溫度標籤 (`.art-label`)：`<strong>92°C</strong>理想水溫<br>細細喚醒香氣`
  - **底部捲動指引**：左下角提示 `SCROLL TO DISCOVER`，前置 38px 細水平線。

---

### 5.3 品牌哲學區（Intro / Philosophy Section）

- **區塊屬性**：`<section class="intro" id="story" aria-labelledby="storyTitle">`
- **外觀尺寸**：垂直內距 118px，純白背景。
- **內容配置（兩欄網格 `.9fr 1.1fr`）**：
  - **左欄（幾何品牌章 `.intro-stamp`，`aria-hidden="true"`）**：
    - 圓形印章 (`.stamp-circle`)：直徑 290px，同心虛線外環，內含粗體 `慢一點，<br>更清楚。` 與英文字 `LET THE FLAVOUR SPEAK`。
    - 覆蓋資訊卡 (`.stamp-card`)：右下角深藍色小卡，文字為 `BLUE SKY NOTE` 與 `一杯好咖啡，從來不是匆忙完成的事。`
  - **右欄（論述文字）**：
    - Eyebrow：`OUR PHILOSOPHY`
    - 標題 `H2#storyTitle`：`在一杯之間，<br>看見產地的<em>晴朗</em>。`（「晴朗」為品牌藍色字）
    - 內文第一段：`我們相信，精品咖啡的美好不該被複雜掩蓋。以小批次烘焙留住豆子的個性，再用穩定、誠實的手沖，讓風土與時間在杯中變得清晰。`
    - 內文第二段：`給懂得放慢腳步的人，也給每一個想重新認識咖啡的人。`
    - 導引連結：`看看我們如何沖煮 →`（連往 `#brew`，附底線動態）。

---

### 5.4 本季選豆商品卡（Coffee Section）

- **區塊屬性**：`<section class="coffee-section" id="coffee" aria-labelledby="coffeeTitle">`
- **外觀尺寸**：上下內距 110px / 120px，背景色為晨霧藍 `--mist`。
- **區塊標題**：
  - Eyebrow：`SEASONAL SELECTION`
  - 標題 `H2#coffeeTitle`：`今天，想喝哪一片<em>藍天</em>？`
  - 說明：`三款當季單品，為不同的晨光、午後與靜夜而選。`
- **商品卡網格（3 欄等寬，欄距 19px）**：
  每個品項為獨立 `<article class="coffee-card reveal">`，最小高度 384px，卡片背景均帶右下半透明裝飾同心圓。

| 項目編號 | 序號與調性 | 產區標示 | 中文商品名稱 | 風味描述 (Notes) | 規格與定價 | 卡片底色 | 按鈕屬性與文案 |
|---|---|---|---|---|---|---|---|
| **01** | `01 / BRIGHT` | `ETHIOPIA · YIRGACHEFFE` | 衣索比亞<br>耶加雪菲 | 白花、佛手柑、蜂蜜 | NT$ 520 / 200g | `--navy` (`#062742`) | `data-coffee="衣索比亞・耶加雪菲"`<br>「加入收藏 ＋」 |
| **02** | `02 / JUICY` | `KENYA · KIRINYAGA` | 肯亞<br>祈安布 | 黑醋栗、洛神、葡萄柚 | NT$ 580 / 200g | `#106396` | `data-coffee="肯亞・祈安布"`<br>「加入收藏 ＋」 |
| **03** | `03 / ROUND` | `COLOMBIA · HUILA` | 哥倫比亞<br>慧蘭 | 黃桃、焦糖、可可尾韻 | NT$ 460 / 200g | `#164c68` | `data-coffee="哥倫比亞・慧蘭"`<br>「加入收藏 ＋」 |

- **收藏按鈕行為**：點擊觸發 Toast 提示：「已將「{咖啡名稱}」加入你的收藏。」，不轉跳。

---

### 5.5 沖煮日常與三步驟（Brew Ritual Section）

- **區塊屬性**：`<section class="brew" id="brew" aria-labelledby="brewTitle">`
- **外觀尺寸**：上下內距 118px，純白背景。
- **內容配置（兩欄網格 `.93fr 1.07fr`）**：
  - **左欄（沖煮幾何視覺 `.brew-visual`，`aria-hidden="true"`）**：
    - 背景帶斜向淺藍灰漸層分割線。
    - 注水漣漪同心圓 (`.pour-ring`) 與 V60 幾何濾杯圖樣 (`.brew-v60`)。
    - 參數標籤 (`.brew-caption`)：`V60 / 15G : 240ML<br>2'45''`。
  - **右欄（步驟流程）**：
    - Eyebrow：`A QUIET RITUAL`
    - 標題 `H2#brewTitle`：`把時間交給水，<br>讓咖啡說<em>自己的話</em>。`
    - 說明：`不需要繁複儀式，只要三個安靜的步驟。每一個參數，都是為了讓你更靠近豆子原本的樣子。`
    - 步驟有序清單 `<ol class="brew-steps">`：
      1. **步驟 01**：
         - 標題：`研磨，先聞見期待`
         - 內容：`15g 中細研磨，讓香氣從指尖開始展開。`
      2. **步驟 02**：
         - 標題：`悶蒸，等待第一個呼吸`
         - 內容：`以 92°C 熱水浸潤 30 秒，喚醒甜感與層次。`
      3. **步驟 03**：
         - 標題：`注水，保持自己的節奏`
         - 內容：`穩定畫圈，讓 240ml 的清澈在 2 分 45 秒完成。`

---

### 5.6 訂閱風味通信（Visit / Newsletter CTA Section）

- **區塊屬性**：`<section class="visit" id="visit" aria-labelledby="visitTitle">`
- **外觀尺寸**：上下內距 96px，背景 `--navy`，中央對齊，兩側具大型天空藍半透明裝飾圓環。
- **內容要素**：
  - Eyebrow：`THE BLUE SKY LETTER`（居中對齊）
  - 標題 `H2#visitTitle`：`把下一杯好咖啡，<br>寄到你的日常裡。`
  - 說明：`每月一封風味通信，分享新豆、沖煮靈感與只給會員的小小驚喜。`
  - 訂閱表單 `<form class="subscribe" id="subscribeForm">`：
    - 輸入框：`<input type="email" aria-label="電子郵件地址" placeholder="留下你的 Email" required>`
    - 提交按鈕：`<button type="submit">訂閱風味通信</button>`（背景 `--sand`）
  - 表單行為：提交時攔截預設事件、清空欄位並觸發 Toast：「謝謝訂閱，下一封晴朗的風味通信即將寄出。」。

---

### 5.7 頁尾（Footer）

- **外觀尺寸**：背景深墨藍 `#031c31`，文字次級白 `rgba(255,255,255,.67)`。
- **上半部配置 (`.footer-top`，3 欄 `1.7fr 1fr 1fr`，間距 40px)**：
  1. **品牌簡介欄**：Logo 符號、`藍天咖啡 / BLUE SKY COFFEE`、願景描述段落「為喜愛手沖咖啡的你，留下一段慢慢品味、微微放晴的時間。」
  2. **EXPLORE 導覽連結**：`#story` 我們的堅持、`#coffee` 本季選豆、`#brew` 沖煮日常。
  3. **CONTACT 聯絡資訊**：
     - 電子信箱：`<a href="mailto:hello@bluesky.coffee">hello@bluesky.coffee</a>`
     - 實體地址：`台北市大安區晴朗路 18 號`
     - 營業時間：`每日 10:00 — 19:00`
- **下半部版權列 (`.footer-bottom`)**：
  - 左側：`© 2026 BLUE SKY COFFEE. ALL RIGHTS RESERVED.`
  - 右側：`BREW SLOW · LIVE BRIGHT`

---

### 5.8 浮動通知元件（Toast）

- **結構**：`<div class="toast" id="toast" role="status" aria-live="polite"></div>`
- **樣式**：固定定位於右下角（`bottom: 22px; right: 22px; z-index: 20;`），背景為 `--navy`，左側 3px 沙金線，文字白色 13px。
- **過渡動態**：預設透明度為 0 且垂直下偏 12px，加入 `.show` 類別時滑入顯示。
- **停留時間**：2,600 毫秒（2.6 秒）後自動淡出。具備計時器重設邏輯（避免連續點擊互相覆蓋）。

---

## 6. JavaScript 互動邏輯規格

### 6.1 手機版漢堡選單切換
1. 監聽 `.menu-toggle` 點擊事件：
   - 切換 `#navLinks` 的 `open` 樣式類別。
   - 同步更新按鈕的 `aria-expanded`（`true` / `false`）。
   - 切換按鈕無障礙描述 `aria-label`（「關閉導覽選單」/「開啟導覽選單」）。
   - 切換按鈕符號文字（展開時為 `×`，收合時為 `☰`）。
2. 監聽 `#navLinks` 內部所有 `<a>` 連結：
   - 點擊後立即移除 `open` 類別關閉選單，並重置漢堡按鈕為收合狀態。

### 6.2 商品加入收藏
- 選取所有具備 `[data-coffee]` 屬性之按鈕。
- 點擊時讀取其 `button.dataset.coffee` 咖啡名稱。
- 呼叫 `showToast("已將「" + name + "」加入你的收藏。")`。

### 6.3 電子信箱訂閱表單
- 監聽 `#subscribeForm` 的 `submit` 事件。
- 執行 `event.preventDefault()` 阻止瀏覽器重載。
- 執行 `event.currentTarget.reset()` 清空輸入欄位。
- 呼叫 `showToast("謝謝訂閱，下一封晴朗的風味通信即將寄出。")`。

### 6.4 元素捲動進場動態（Scroll Reveal）
- 偵測使用者系統是否偏好減少動態：`window.matchMedia('(prefers-reduced-motion: reduce)').matches`。
- 若支援 `IntersectionObserver` 且未啟用減少動態：
  - 觀察門檻為 `threshold: 0.12`。
  - 元素進入可視範圍時加入 `.visible` 樣式類別（透明度恢復為 1，位移歸零，動畫時長 0.65 秒）。
  - 進場後立即執行 `observer.unobserve(entry.target)` 解除監聽，節省渲染效能。
- 若不支援或啟用減少動態：直接為所有 `.reveal` 元素賦予 `.visible` 類別。

---

## 7. 響應式斷點規格（RWD）

### 7.1 中型螢幕斷點：`@media (max-width: 820px)`
- **導覽列**：
  - 高度縮減為 68px。
  - 顯示漢堡選單按鈕（`.menu-toggle`）。
  - 導覽連結群改為絕對定位抽屜式選單，展開時背景為 `#05233c`，最大高度限制 300px。
- **Hero 區**：
  - 網格從 2 欄改為單欄縱向排列。
  - Hero 插畫高度降低為 278px，器具縮放比例 `scale(.72)`。
- **理念與手沖區**：
  - `.intro-grid` 與 `.brew-grid` 轉為單欄。
  - 品牌印章容器最大寬度限制 510px。
- **本季選豆區**：
  - 商品網格改為 2 欄排列。
  - 第 3 款咖啡卡橫跨 2 欄（`grid-column: span 2`）。
- **頁尾**：
  - 頁尾網格由 3 欄改為 2 欄（`1.4fr 1fr`），品牌欄橫跨全寬。

### 7.2 小型手機螢幕斷點：`@media (max-width: 560px)`
- **全域容器**：`.wrap` 邊距縮減，寬度為 `min(100% - 34px, 1120px)`。
- **垂直留白**：各大區塊（`.intro`, `.coffee-section`, `.brew`, `.visit`）上下內距由 110~118px 縮小為 76px。
- **Hero 區**：
  - 主標題字級鎖定為 40px。
  - 隱藏右側水溫與沖煮參數標籤（`.art-label { display: none; }`）。
  - 插畫高度進一步縮減至 240px。
- **理念區**：
  - 印章直徑縮為 245px，覆蓋小卡縮為 185px。
- **本季選豆區**：
  - 區塊標題由橫向 flex 改為垂直排列。
  - 商品卡網格改為單欄（1 欄），每張卡取消跨欄，卡片最小高度設為 330px。
- **手沖步驟區**：
  - 沖煮幾何示意區最小高度降至 310px，注水圓環直徑縮至 190px。
- **訂閱區**：
  - 表單從橫向並排改為直向堆疊（輸入框與送出按鈕均為 100% 滿寬）。
- **頁尾**：
  - 全部欄位轉為單欄垂直排列。
  - 底部版權與 Slogan 由左右兩端改為直向堆疊排列。

### 7.3 動態無障礙支援：`@media (prefers-reduced-motion: reduce)`
- 取消全域平滑捲動（`scroll-behavior: auto`）。
- 強制將所有過渡與動畫時長降至極限（`transition-duration: .01ms; animation-duration: .01ms;`）。
- 所有 `.reveal` 元素預設直接顯示，不帶有任何位移或透明度過渡。

---

## 8. 無障礙（Accessibility / A11y）合規檢核

1. **語意標籤**：導覽 `<nav>`、主要內容 `<main>`、各獨立內容 `<section>` 與獨立商品 `<article>` 劃分明確。
2. **區塊可識別性**：主要 `<section>` 皆具備 `aria-labelledby` 與對應標題 ID 連結。
3. **無障礙導覽**：
   - 導覽列具備 `aria-label="主要導覽"`。
   - 品牌 Logo 首頁連結具備 `aria-label="回到藍天咖啡首頁"`。
   - 漢堡按鈕具備 `aria-controls="navLinks"`、動態 `aria-expanded` 與切換型 `aria-label`。
4. **裝飾元素忽略**：所有由 CSS 繪製之純視覺元素（Hero 插畫、印章幾何、手沖示意圖）均標記 `aria-hidden="true"`，防止螢幕閱讀器冗餘讀取。
5. **動態宣告**：Toast 浮動通知使用 `role="status"` 及 `aria-live="polite"`，確保螢幕閱讀器能適時朗讀操作結果。
6. **表單易用性**：訂閱輸入框具備清晰的 `aria-label="電子郵件地址"` 與原生 `required` 驗證。

---

## 9. 規格修改與功能擴充指南

| 修改需求目標 | 建議修改之原始碼位置 | 關鍵注意事項 |
|---|---|---|
| **更換品牌識別與名稱** | Header `.brand`、Hero 標題、Footer 品牌欄 | 記得同步更新 `<title>`、`<meta description>` 與 Logo 中英文名稱 |
| **調整品牌色票系統** | `:root` 變數定義（第 12–23 行） | 優先變更 `--navy`、`--blue`、`--sky`、`--sand`，避免破壞文字對比度 |
| **新增／更換咖啡品項** | `#coffee` 內之 `<article class="coffee-card">` | 務必同步更新按鈕上的 `data-coffee` 屬性，確保 Toast 提示名稱正確 |
| **調整手沖參數與步驟** | `#brew` 內之 `.brew-caption` 與 `.brew-steps` | 保持步驟編號 01~03 與文字格式階層統一 |
| **串接後端訂閱 API** | JavaScript `#subscribeForm` 提交監聽區 | 保留 `event.preventDefault()`，在發送 `fetch()` 請求完成後再呼叫 `showToast` |
| **串接真實購物車／收藏清單** | JavaScript `[data-coffee]` 點擊監聽區 | 可在點擊時將商品資訊存入 `localStorage` 或呼叫購物車 API |

---

## 10. 驗收檢驗清單（Acceptance Test Matrix）

- [ ] **SEO 與結構**：網頁 title 為「藍天咖啡｜讓風味，慢慢抵達」，語系為繁體中文 `zh-Hant`。
- [ ] **頁首與導覽**：桌面版 Header 覆蓋於 Hero 之上，錨點點擊可平滑滾動至各章節。
- [ ] **行動版選單**：螢幕寬度 $\le 820\text{px}$ 時漢堡選單可正常展開／收合，點擊任一項目自動收合選單。
- [ ] **純 CSS 插畫**：全站無遺失圖片圖標，太陽、山脈、濾杯、下壺、同心圓正常呈現。
- [ ] **選豆商品卡**：三款商品卡（衣索比亞、肯亞、哥倫比亞）資訊完整，點擊「加入收藏 ＋」會跳出包含該商品名稱之 Toast。
- [ ] **沖煮日常**：呈現 15g:240ml 參數與三個依序步驟（01 研磨、02 悶蒸、03 注水）。
- [ ] **訂閱功能**：未填寫 Email 時觸發 HTML5 原生防呆，填寫正確 Email 點擊送出後欄位清空並跳出感謝訂閱 Toast。
- [ ] **響應式佈局**：在桌面版（> 820px）、平板（561~820px）與手機（$\le 560\text{px}$）皆無水平捲軸溢出問題。
- [ ] **無障礙支援**：在開啟「減少動態效果」偏好時，所有動態與進場動畫自動停用，內容保持完全可讀。
