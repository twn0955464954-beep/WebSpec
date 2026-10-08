# 萌萃女僕手沖咖啡廳｜逆向工程完整規格書（Web Specification）

> **來源檔案**：`WebPage-_11515220/outline/index.html`  
> **文件用途**：依據女僕手沖咖啡廳網頁實作原始碼逆向分析建立標準規格文件，供後續規格微調、功能擴充與品質驗收。  
> **檔案 SHA-256**：`02A96C3B3B61AE70AA2C87D5E639027B689A2829F30E334FBA13B2619DBB3994`  
> **規格版本**：v2.0 (Reverse Engineered - Maid Pour-Over Café)  
> **建立日期**：2026-10-08  

---

## 1. 專案與品牌概述

### 1.1 基本資訊
| 項目 | 內容規格 |
|---|---|
| **品牌名稱** | 萌萃女僕手沖咖啡（MOE DRIP MAID CAFÉ） |
| **品牌核心定位** | 將「日系女僕溫暖互動與款待文化」與「SCA 精品高階手沖咖啡」深度結合的精品咖啡體驗館 |
| **品牌核心標語** | 「主人，歡迎回家！讓女僕為您親手滴濾極致芳醇的時光。」 |
| **副標語／主張** | 「把最極致的咖啡，交給最溫柔的女僕」／「PREMIUM SPECIALTY COFFEE · BREWED WITH LOVE ♡」 |
| **網站類型** | 單頁式精品女僕手沖咖啡形象展示、互動體驗與線上預約點單頁（One-page Landing Page） |
| **目標客群** | 喜愛日系女僕文化、追求莊園級手沖咖啡風味、重視陪伴感與尊榮歸宅體驗的主人與大小姐 |
| **主要轉換目標 (CTA)** | 1. 探索頂級莊園選豆並加入點單收藏 (`data-coffee`)<br>2. 體驗女僕手沖儀式互動與施展美味魔法咒語<br>3. 線上預約歸宅席次並領取「首杯 9 折與女僕拍立得紀念券」 |
| **品牌語調** | 親切溫柔、尊榮萌系（尊稱主人）、專業嚴謹（強調 SCA 莊園豆與精確沖煮參數） |

---

## 2. 技術架構與邊界限制

### 2.1 技術選型
- **HTML**：HTML5 語意化標籤架構（`header`, `nav`, `main`, `section`, `article`, `ul`, `ol`, `form`, `footer`）。
- **CSS**：原生 CSS3，無使用外部框架（Bootstrap / Tailwind 零依賴），全域透過 CSS Custom Properties（CSS 變數）統一管理主題風格。
- **JavaScript**：原生 ES6+，無外部函式庫（jQuery / Vue 零依賴），獨立維護互動事件、DOM 操作與粒子動畫。
- **字型資源**：Google Fonts，採用 `<link rel="preconnect">` 預先連線加速：
  - `Zen Maru Gothic`（圓潤日系萌感展示字體）
  - `Noto Sans TC`（清晰現代介面字體）
  - `Noto Serif TC`（精品人文標題襯線字體）
  - `Playfair Display`（高階歐文字型，用於英文字、數字與溫度標註）
- **純 CSS / 向量繪圖技術**：零外部點陣圖片依賴，全站插畫（女僕手沖濾架、玻璃分享壺、上升蒸氣愛心粒子、裝飾圓環）皆由 CSS `clip-path`、`radial-gradient`、`linear-gradient`、`border-radius` 與 `@keyframes` 動態繪製。
- **單檔自足設計**：樣式與腳本皆內嵌於 HTML 檔案內，無需額外建置或打包工具，即可直接透過瀏覽器或 GitHub Pages 本地部署與預覽。

---

## 3. SEO 與基礎中繼資料（Metadata）

```html
<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="萌萃女僕手沖咖啡廳｜專為主人挑選的頂級莊園高階咖啡豆，由溫柔女僕為您親手滴濾，享受兼具萌系互動與專業精品風味的極致時光。">
  <title>萌萃女僕手沖咖啡廳｜主人，讓女僕為您親手沖一杯極致莊園咖啡</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@400;500;600;700&family=Noto+Serif+TC:wght@600;700;900&family=Playfair+Display:ital,wght@0,600;0,700;1,600&family=Zen+Maru+Gothic:wght@500;700;900&display=swap" rel="stylesheet">
</head>
```

---

## 4. 視覺系統與設計 Token

### 4.1 色彩變數清單（CSS Custom Properties）
| Token 名稱 | 色碼 Hex | 語意說明與主要用途 |
|---|---|---|
| `--pink-primary` | `#ff7597` | 活力萌粉：主按鈕背景、愛心裝飾、濾架框線、底線動畫焦點 |
| `--pink-deep` | `#d8436b` | 深玫瑰粉：重點文字、強調底線、漸層按鈕深色端、小標文字 |
| `--pink-soft` | `#ffeef3` | 柔和粉底：本季選豆區 (`#menu`) 背景、徽章底色、資訊卡外框 |
| `--pink-light` | `#fff5f8` | 淺粉白：特色卡片背景、手沖步驟卡片背景 |
| `--cream` | `#fffaf7` | 暖米白奶油底：全站主要頁面背景底色 (`body background`) |
| `--coffee-dark` | `#3a221d` | 高階深焙咖啡棕：主標題、內文主要文字、深色按鈕、預約區主背景 |
| `--coffee-rich` | `#5c352c` | 醇厚可可棕：導覽列連結、次要按鈕 hover 狀態 |
| `--coffee-accent`| `#8b5242` | 莊園紅棕：風味筆記膠囊文字、品質標章文字 |
| `--gold` | `#d4a359` | 莊園高階金：藝伎 (Geisha) 咖啡等級徽章邊條 |
| `--gold-light` | `#fae8ca` | 柔金底色：莊園認證小標背景 |
| `--line` | `#f3d4dc` | 淺粉分隔線：表格邊框、虛線裝飾線 |
| `--text-muted` | `#826369` | 柔和灰棕：次要段落說明、副標題文字 |
| `--white` | `#ffffff` | 純白底色：卡片主體底色、彈出框底色 |
| `--shadow-pink` | `0 16px 40px rgba(216, 67, 107, 0.14)` | 粉色柔和擴散陰影（卡片浮起、Hero 右側互動卡） |
| `--shadow-soft` | `0 10px 30px rgba(58, 34, 29, 0.08)` | 咖啡深色環境陰影 |

### 4.2 圓角系統（Border Radius Tokens）
- `--radius-sm`: `8px`（表單輸入框、參數網格）
- `--radius-md`: `18px`（特色卡片、對話氣泡）
- `--radius-lg`: `32px`（Hero 互動卡、咖啡商品卡）
- `--radius-pill`: `9999px`（按鈕、膠囊徽章、圓形標籤）

### 4.3 字體階層與文字規範
1. **全站主字體**：`"Zen Maru Gothic", "Noto Sans TC", sans-serif`，基準字級 16px，行高 1.75。
2. **標題字體**：中文標題使用粗體 900，英文重要數據（溫度、價格、步驟編號）採用 `"Playfair Display", serif`。
3. **字級規範**：
   - Hero 主標題 (`.hero-title`)：`clamp(34px, 4.8vw, 56px)`，行高 1.28。
   - 各區塊主標題 (`.section-title`)：`clamp(28px, 4vw, 42px)`，行高 1.35。
   - 區塊眉標 (`.eyebrow`)：12px、字重 700、字距 `.08em`，前置粉紅愛心符號 `♡`。
   - 內文段落 (`.hero-lede`, `.section-sub`)：15px ~ 16px，行高 1.85。

---

## 5. 頁面架構與各區塊詳細規格

```
<body>
 ├── div.particles-container#particlesContainer (愛心粒子飄落特效層)
 ├── header.site-header#top                     (毛玻璃頂部導覽列)
 └── main
      ├── section.hero                          (Hero 主視覺與美味魔法卡)
      ├── section.concept#concept               (品牌堅持與三大特色)
      ├── section.menu-section#menu             (頂級莊園手沖咖啡豆菜單)
      ├── section.ritual#ritual                 (女僕手沖三段儀式與互動對話)
      └── section.reserve-section#reserve       (預約歸宅與專屬優惠表單)
 ├── footer.site-footer                         (頁尾門市資訊與版權)
 └── div.toast#toast                            (女僕語氣浮動 Toast)
```

---

### 5.1 頁首導覽（Header & Navbar）

- **結構**：
  ```html
  <header class="site-header" id="top">
    <div class="wrap navbar">
      <a class="brand" href="#top" aria-label="回到萌萃女僕咖啡廳首頁">
        <div class="brand-icon" aria-hidden="true">☕</div>
        <div class="brand-text">
          <div class="brand-title">萌萃<span>女僕手沖咖啡</span></div>
          <div class="brand-subtitle">MOE DRIP MAID CAFÉ</div>
        </div>
      </a>
      <button class="menu-toggle" type="button" aria-label="開啟導覽選單" aria-expanded="false" aria-controls="navMenu">☰</button>
      <nav class="nav-menu" id="navMenu" aria-label="主要導覽">
        <ul class="nav-links">
          <li><a href="#concept">品牌堅持</a></li>
          <li><a href="#menu">莊園選豆</a></li>
          <li><a href="#ritual">女僕手沖儀式</a></li>
          <li><a href="#reserve">預約歸宅</a></li>
        </ul>
        <a class="btn btn-primary nav-cta" href="#reserve">立即預約席次 ♡</a>
      </nav>
    </div>
  </header>
  ```
- **樣式與行為**：
  - 定位：`position: sticky; top: 0; z-index: 100;`，背景帶毛玻璃模糊 `backdrop-filter: blur(12px)`。
  - 高度：76px，底部帶淺粉邊框 `1px solid rgba(243, 212, 220, 0.7)`。
  - 品牌 Logo：圓形粉紅漸層外框、內含咖啡杯符號 `☕`；主標題以深棕與深玫瑰粉組合，副標題為大寫英文字距 `.16em`。
  - 導覽連結 hover 時底部由右向左展開粉紅底線；CTA 按鈕為膠囊粉紅漸層按鈕。

---

### 5.2 主視覺區（Hero Section）

- **區塊屬性**：`<section class="hero" aria-labelledby="heroHeading">`
- **外觀特徵**：淺粉米色漸層背景，右上方配置 600px 虛線裝飾圓環與三個浮動愛心符號（`@keyframes floatHeart`）。
- **左欄（品牌宣言與引導）**：
  - 雙徽章標籤：`♡ 日系女僕貼心互動`、`SCA 認證・高階莊園咖啡豆`。
  - H1 主標題：`主人，歡迎回家！<br>讓女僕為您親手<br>滴濾<span class="highlight">極致芳醇</span>的時光。`
  - 導言段落：說明萌萃嚴選 COE 卓越杯高海拔精品豆，由女僕咖啡師現場手沖並施展美味魔法。
  - 雙行動按鈕：
    - 主按鈕：`探索本季頂級選豆 →`（粉紅漸層陰影，連往 `#menu`）
    - 次按鈕：`體驗女僕手沖儀式`（白底粉邊，連往 `#ritual`）
  - 品質保證欄：三大信任承諾（100% 莊園單一產區豆、現磨 92°C 溫控注水、尊享女僕專屬互動）。
- **右欄（女僕互動手沖卡片 `.hero-visual-card`）**：
  - 頂部問候標籤：`今日值班女僕「Mizu」為您服務中`（呼吸動態縮放）。
  - 純 CSS 手沖插畫（`.visual-art-box`）：
    - 手沖架 (`.drip-stand`)：倒梯形幾何濾架，中央帶愛心符號。
    - 咖啡下壺 (`.server-pot`)：曲線玻璃壺，下半部呈現深焙咖啡液體與粉紅反光光澤。
    - 上升愛心蒸氣粒子（3 顆交錯飄起）。
  - 黃金手沖參數列（92°C 甜蜜水溫、1:15 粉水比、2'30'' 萃取時間）。
  - 魔法互動按鈕：`#magicSpellBtn`「✨ 點我！讓女僕施展美味魔法咒語」。

---

### 5.3 品牌堅持與特色理念（Concept Section）

- **區塊屬性**：`<section class="concept" id="concept" aria-labelledby="conceptHeading">`
- **結構**：純白背景，頂部置中標題列，下方為 3 欄式特色卡片網格。
- **三大核心特色卡片**：
  1. **頂級高階咖啡豆 (Specialty Grade)**：
     - 圖示：👑
     - 文案：嚴選巴拿馬翡翠莊園、衣索比亞等頂級微批次莊園豆，新鮮烘焙，花果香明亮。
  2. **女僕一對一手沖 (Tableside Drip)**：
     - 圖示：🎀
     - 文案：於主人桌邊現場手沖，依照主人口味調整水流注水節奏，細心解說產區風土。
  3. **幸福專屬互動 (Heartfelt Interaction)**：
     - 圖示：💖
     - 文案：專屬杯面拉花魔法、手寫風味小卡、品飲互動與拍照紀念，傳遞充沛幸福感。

---

### 5.4 頂級莊園手沖咖啡菜單（Menu Section）

- **區塊屬性**：`<section class="menu-section" id="menu" aria-labelledby="menuHeading">`
- **背景**：柔和淡粉底 `--pink-soft`。
- **副標註記**：全品項皆附贈【女僕現場手沖服務】與【專屬拍立得手寫風味紀念卡】。
- **商品卡網格（3 款頂級單品）**：

| 卡片 | 商品名稱 | 產區與等級 | 焙度與處理法 | 風味輪筆記 (Notes) | 價格 | 互動按鈕屬性 |
|---|---|---|---|---|---|---|
| **01 (推薦款)** | **巴拿馬・翡翠莊園 粉紅標藝伎** | PANAMA · BOQUETE<br>藝伎 GEISHA | 淺焙<br>日曬 Slow Dry<br>海拔 1,800m+ | 茉莉花香、佛手柑、荔枝甜感、高山蜂蜜 | NT$ 480 | `data-coffee="巴拿馬・翡翠莊園 藝伎"`<br>「點單收藏 ＋」 |
| **02** | **衣索比亞・耶加雪菲 粉櫻果漾** | ETHIOPIA · YIRGACHEFFE<br>G1 水洗處理 | 極淺焙 Cinnamon<br>雙重水洗<br>海拔 2,100m | 粉紅葡萄柚、白桃、接骨木花、綠茶回甘 | NT$ 360 | `data-coffee="衣索比亞・粉櫻果漾"`<br>「點單收藏 ＋」 |
| **03** | **肯亞・涅里高地 紅寶石黑加侖** | KENYA · NYERI<br>TOP AA 水洗 | 淺中焙 Medium-Light<br>肯亞式水洗<br>海拔 1,750m | 黑醋栗、洛神花茶、覆盆莓、黑糖尾韻 | NT$ 380 | `data-coffee="肯亞・紅寶石黑加侖"`<br>「點單收藏 ＋」 |

- **點單行為**：點擊「點單收藏 ＋」時觸發全螢幕愛心粒子飄落，並顯示女僕親切語調之 Toast。

---

### 5.5 女僕手沖儀式與互動（Ritual Section）

- **區塊屬性**：`<section class="ritual" id="ritual" aria-labelledby="ritualHeading">`
- **排版佈局**：兩欄網格（左欄為動態對話互動卡，右欄為三步驟清單）。
- **左欄（動態對話互動卡）**：
  - 女僕圓形頭像（帶緞帶 🎀 標誌與立體粉紅光暈）。
  - 對話氣泡 (`#maidDialogue`)：預設文字「主人～今天上班辛苦了！讓女僕為您調製一杯香甜的花果香手沖，掃去一整天的疲憊吧♡」。
  - 三組即時對話切換按鈕 (`[data-phrase]`)：
    1. `💬 請女僕推薦今日咖啡豆`
    2. `🪄 施展美味加倍魔法咒語`（萌え萌えキュン！）
    3. `📝 索取女僕手繪風味紀念卡`
- **右欄（三段式手沖流程）**：
  - **步驟 01**：聞香選豆・傾聽心事（女僕將現磨莊園粉帶至主人面前嗅吸乾香）。
  - **步驟 02**：92°C 溫控滴濾・美味魔法（優雅穩健注水，念出美味加倍咒語）。
  - **步驟 03**：分享杯品飲・手寫拍立得（分裝溫熱手作陶杯，親筆寫下沖煮參數小卡）。

---

### 5.6 預約歸宅與專屬優惠（Reservation Section）

- **區塊屬性**：`<section class="reserve-section" id="reserve" aria-labelledby="reserveHeading">`
- **背景與視覺**：深焙咖啡棕漸層背景（`#3a221d` 到 `#57332a`），融合粉紅圓環光暈。
- **優惠承諾**：首次預約享【首杯莊園手沖 9折】與【女僕拍立得紀念合照乙張】。
- **預約表單 (`#reserveForm`) 欄位規格**：
  1. `masterName`：主人的尊稱或暱稱（`required`，placeholder："例如：宛芯主人 / 呂大人"）
  2. `masterEmail`：電子信箱（`required`，`type="email"`）
  3. `reserveDate`：預計歸宅日期（`required`，`type="date"`，腳本自動初始化為次日）
  4. `coffeePreference`：偏好咖啡風味（下拉選單：花香果酸系、飽滿果汁系、焦糖堅果系、全權交由女僕推薦）
  5. 提交按鈕：`送出預約・等候女僕迎接主人 ♡`（滿寬粉紅漸層按鈕）

---

### 5.7 頁尾（Footer）

- **背景色**：天空藍 `#2a1713`，文字次級白。
- **三欄佈局**：
  1. **品牌簡介**：萌萃女僕手沖咖啡願景。
  2. **NAVIGATION 導覽**：品牌堅持、莊園選豆、手沖儀式、預約席次錨點連結。
  3. **VISIT US 門市資訊**：
     - 地址：台北市大安區晴朗路 99 號 2 樓
     - 電話：(02) 2345-6789
     - 營業時間：每日 11:00 — 21:00
     - 電子信箱：hello@moedrip.coffee
- **底部列**：版權宣告與 `PREMIUM SPECIALTY COFFEE · BREWED WITH LOVE ♡`。

---

### 5.8 浮動通知與特效元件

1. **愛心粒子飄落特效容器 (`#particlesContainer`)**：
   - 滿版覆蓋、穿透點擊 (`pointer-events: none; z-index: 9999;`)。
   - 粒子符號集：`♡`、`♥`、`✨`、`💖`、`☕`，隨機位置、隨機顏色（`#ff7597` / `#d8436b`），帶有掉落旋轉動畫。
2. **Toast 提示彈窗 (`#toast`)**：
   - 固定於右下角（`bottom: 24px; right: 24px; z-index: 999;`），白底粉紅左邊線，淡入淡出時長 3 秒，具備計時器重設保護。

---

## 6. JavaScript 互動邏輯規格

### 6.1 行動版導覽抽屜
- 點擊 `.menu-toggle` 時，在 `#navMenu` 上切換 `open` 樣式類別（最高展開 380px）。
- 同步切換按鈕文字（展開為 `×`，收合為 `☰`）與 `aria-expanded` 狀態。
- 點擊選單內部任何錨點連結，自動收合選單並重設按鈕圖示。

### 6.2 愛心粒子噴發函式 (`burstHearts(count)`)
- 動態於 `#particlesContainer` 生成指定數量之粒子元素。
- 透過隨機計算橫向座標 (`vw`) 與垂直座標 (`vh`)，並在 2 秒後自動從 DOM 移除。

### 6.3 Hero 美味魔法按鈕 (`#magicSpellBtn`)
- 點擊時生成 22 顆愛心粒子。
- 觸發 Toast：「✨ 萌え萌えキュン～女僕已為咖啡注入美味魔法！甜感升級 100% ♡」。

### 6.4 菜單商品收藏按鈕 (`[data-coffee]`)
- 讀取按鈕之 `dataset.coffee` 咖啡名稱。
- 觸發 8 顆愛心粒子。
- 觸發 Toast：「主人～已為您記下「{咖啡名稱}」，女僕期待親自為您沖煮唷 (◍•ᴗ•◍)♡」。

### 6.5 女僕互動對話框按鈕 (`[data-phrase]`)
- 點擊時讀取按鈕之 `dataset.phrase`，動態替換 `#maidDialogue` 內文。
- 觸發 10 顆愛心粒子。
- 觸發 Toast：「女僕開心地給了主人一個溫柔的微笑 ♡」。

### 6.6 預約表單提交處理 (`#reserveForm`)
- 攔截 `event.preventDefault()`。
- 讀取主人暱稱 `#masterName`。
- 噴發 25 顆慶祝愛心粒子。
- 彈出 Toast：「預約成功！歡迎 {主人暱稱} 歸宅，9 折禮券已寄至您的信箱囉 ♡」。
- 重置表單輸入。

### 6.7 預約日期初始化
- 網頁載入時自動將 `#reserveDate` 設定為次日（Tomorrow）之 ISO 日期字串。

---

## 7. 響應式排版（RWD）斷點規格

### 7.1 平板與中型螢幕：`@media (max-width: 860px)`
- 啟用漢堡選單按鈕，導覽連結改為垂直抽屜排列。
- Hero 網格轉為單欄，右側手沖卡最大寬度限制 480px 置中。
- 特色理念與菜單商品網格改為單欄縱向排列（限制 500px 置中）。
- 儀式區與預約表單均改為單欄排列。
- 頁尾改為單欄排列。

### 7.2 手機螢幕：`@media (max-width: 540px)`
- 容器邊距縮為左右各 16px（`calc(100% - 32px)`）。
- Hero 標題字級縮減至 32px，區塊標題縮至 26px。
- Hero 雙按鈕改為直向 100% 滿寬排列。
- 各主要區塊上下內距由 100px 調整為 70px。

### 7.3 動態無障礙：`@media (prefers-reduced-motion: reduce)`
- 取消全域平滑捲動（`scroll-behavior: auto`）。
- 強制過渡與動畫時長降為 0.01ms。

---

## 8. 無障礙（Accessibility / A11y）合規檢核

1. **語意結構**：`header`, `nav`, `main`, `section`, `article`, `footer` 劃分清晰。
2. **ARIA Landmarks**：
   - 導覽列具備 `aria-label="主要導覽"`。
   - 漢堡按鈕具備 `aria-controls="navMenu"`、動態 `aria-expanded` 與 `aria-label`。
   - 所有純視覺裝飾元素（粒子容器、背景同心圓、手沖幾何圖形、表情圖示）皆標記 `aria-hidden="true"`。
   - 浮動 Toast 具備 `role="status"` 及 `aria-live="polite"`。
3. **鍵盤導覽友善**：所有按鈕、輸入框與連結均提供 3px 粉紅外框與 4px 偏移的 `:focus-visible` 焦點樣式。

---

## 9. 規格修改與擴充指南

| 修改目標 | 建議修改位置 | 注意事項 |
|---|---|---|
| **新增／更換咖啡豆品項** | `#menu` 內的 `<article class="coffee-card">` | 需同步更新按鈕之 `data-coffee` 屬性，確保 Toast 提示名稱吻合 |
| **增加女僕互動對話** | `#ritual` 內的 `.maid-buttons-group` 按鈕 | 設定 `data-phrase="女僕台詞"` 即可自動支援點擊替換對話 |
| **調整店鋪資訊與營業時間** | Footer `.site-footer` 內各欄位 | 門市地址、電話與信箱資訊集中維護 |
| **串接後端預約 API** | 腳本 `#reserveForm` submit 監聽函式 | 加入 `fetch('/api/reserve', { ... })` 串接後端伺服器 |

---

## 10. 驗收檢驗清單（Acceptance Test Matrix）

- [ ] **SEO 與文件設定**：標題為「萌萃女僕手沖咖啡廳｜主人，讓女僕為您親手沖一杯極致莊園咖啡」，語系為 `zh-Hant`。
- [ ] **純 CSS 插畫呈現**：Hero 區之濾架、咖啡壺、蒸氣愛心粒子正常呈現，無遺失圖片。
- [ ] **美味魔法互動**：點擊「點我！讓女僕施展美味魔法咒語」可見愛心飄落動畫與專屬 Toast。
- [ ] **商品點單收藏**：點擊任一咖啡卡的「點單收藏 ＋」會跳出含有該咖啡名稱的主人專屬 Toast。
- [ ] **女僕對話切換**：點擊三組互動按鈕時，上方對話氣泡內文會即時切換為對應台詞。
- [ ] **預約歸宅表單**：填寫尊稱與信箱後點擊送出，欄位重設並跳出個人化歡迎歸宅 Toast。
- [ ] **響應式排版**：在 $\le 860\text{px}$ 與 $\le 540\text{px}$ 測試時無橫向捲軸溢出，漢堡選單正常收合。
- [ ] **無障礙模式**：啟用減少動態效果時，動畫能正確停用且介面依然完全可讀。
