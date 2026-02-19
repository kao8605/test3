# 設計文件

## 概述

本設計文件描述如何在現有的個人介紹網站中整合 Google 表單和 YouTube 影片嵌入功能。設計採用簡單直接的方法，使用標準的 HTML iframe 元素來嵌入外部內容，並透過 CSS 確保響應式設計和視覺一致性。

設計目標：
- 最小化對現有網站結構的修改
- 確保嵌入內容的響應式顯示
- 保持與現有頁面的視覺一致性
- 提供簡單的內容更新機制

## 架構

### 整體架構

網站採用傳統的多頁面架構，每個功能頁面都是獨立的 HTML 檔案。新增的嵌入功能將遵循相同的架構模式：

```
website/
├── index.html              # 首頁
├── thesis-guidance.html    # 論文指導
├── government-grants.html  # 政府補助案輔導
├── web-development.html    # 網站架設
├── about.html             # 關於我
├── contact.html           # 聯絡方式
├── survey.html            # 新增：調查表單頁面
├── videos.html            # 新增：影片頁面
├── css/
│   ├── main.css           # 主要樣式表
│   └── embed.css          # 新增：嵌入內容樣式
└── assets/
    └── images/
```

### 頁面結構

每個包含嵌入內容的頁面將遵循以下結構：

```html
<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>[頁面標題]</title>
    <link rel="stylesheet" href="css/main.css">
    <link rel="stylesheet" href="css/embed.css">
</head>
<body>
    <header>
        <!-- 導航選單 -->
        <nav>
            <!-- 現有選單項目 + 新增項目 -->
        </nav>
    </header>
    
    <main>
        <section class="embed-container">
            <h1>[內容標題]</h1>
            <div class="embed-wrapper">
                <!-- iframe 嵌入內容 -->
            </div>
        </section>
    </main>
    
    <footer>
        <!-- 頁尾內容 -->
    </footer>
</body>
</html>
```

## 元件和介面

### 1. 嵌入容器元件 (Embed Container)

**用途：** 提供一個標準化的容器來包裝嵌入內容，確保一致的樣式和響應式行為。

**HTML 結構：**
```html
<div class="embed-container">
    <h1 class="embed-title">[標題]</h1>
    <div class="embed-wrapper">
        <iframe src="[嵌入 URL]" 
                class="embed-frame"
                frameborder="0"
                allowfullscreen>
        </iframe>
    </div>
</div>
```

**CSS 類別：**
- `.embed-container`: 外層容器，提供頁面內的定位和間距
- `.embed-title`: 標題樣式，與現有頁面標題保持一致
- `.embed-wrapper`: iframe 包裝器，實現響應式比例
- `.embed-frame`: iframe 本身的樣式

### 2. Google 表單嵌入元件

**實作細節：**

```html
<div class="embed-container google-form-container">
    <h1 class="embed-title">調查表單</h1>
    <div class="embed-wrapper form-wrapper">
        <iframe src="[Google 表單嵌入 URL]" 
                class="embed-frame google-form"
                frameborder="0">
            載入中...
        </iframe>
    </div>
</div>
```

**特定樣式：**
```css
.google-form-container {
    max-width: 800px;
    margin: 0 auto;
    padding: 2rem 1rem;
}

.form-wrapper {
    position: relative;
    width: 100%;
    min-height: 600px;
}

.google-form {
    width: 100%;
    height: 800px;
    border: none;
}

@media (max-width: 768px) {
    .google-form {
        height: 1000px;
    }
}
```

### 3. YouTube 影片嵌入元件

**實作細節：**

```html
<div class="embed-container video-container">
    <h1 class="embed-title">影片內容</h1>
    <div class="embed-wrapper video-wrapper">
        <iframe src="https://www.youtube.com/embed/[VIDEO_ID]" 
                class="embed-frame youtube-video"
                frameborder="0"
                allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                allowfullscreen>
        </iframe>
    </div>
</div>
```

**特定樣式（16:9 響應式比例）：**
```css
.video-container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 2rem 1rem;
}

.video-wrapper {
    position: relative;
    padding-bottom: 56.25%; /* 16:9 比例 */
    height: 0;
    overflow: hidden;
}

.youtube-video {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    border: none;
}
```

### 4. 導航選單更新

**現有導航選單結構（假設）：**
```html
<nav class="main-nav">
    <ul>
        <li><a href="index.html">首頁</a></li>
        <li><a href="thesis-guidance.html">論文指導</a></li>
        <li><a href="government-grants.html">政府補助案輔導</a></li>
        <li><a href="web-development.html">網站架設</a></li>
        <li><a href="about.html">關於我</a></li>
        <li><a href="contact.html">聯絡方式</a></li>
    </ul>
</nav>
```

**更新後的導航選單：**
```html
<nav class="main-nav">
    <ul>
        <li><a href="index.html">首頁</a></li>
        <li><a href="thesis-guidance.html">論文指導</a></li>
        <li><a href="government-grants.html">政府補助案輔導</a></li>
        <li><a href="web-development.html">網站架設</a></li>
        <li><a href="survey.html">調查表單</a></li>
        <li><a href="videos.html">影片</a></li>
        <li><a href="about.html">關於我</a></li>
        <li><a href="contact.html">聯絡方式</a></li>
    </ul>
</nav>
```

## 資料模型

本功能主要處理靜態 HTML 內容和外部嵌入，不涉及複雜的資料模型。主要的配置資料包括：

### 嵌入內容配置

```javascript
// 如果未來需要動態管理嵌入內容，可使用以下結構
{
  googleForm: {
    url: "https://docs.google.com/forms/d/e/[FORM_ID]/viewform?embedded=true",
    title: "調查表單",
    height: "800px"
  },
  youtubeVideos: [
    {
      id: "VIDEO_ID_1",
      title: "影片標題",
      embedUrl: "https://www.youtube.com/embed/VIDEO_ID_1"
    }
  ]
}
```

目前階段，這些配置將直接硬編碼在 HTML 中。

## 正確性屬性


屬性是一種特徵或行為，應該在系統的所有有效執行中保持為真——本質上是關於系統應該做什麼的正式陳述。屬性作為人類可讀規範和機器可驗證正確性保證之間的橋樑。

### 屬性 1：響應式容器調整

*對於任何* 嵌入內容容器（Google 表單或 YouTube 影片），當視窗寬度改變時，容器應該根據 CSS 媒體查詢規則調整其尺寸，並且內容應該保持在容器邊界內而不溢出。

**驗證需求：需求 1.3, 2.3**

### 屬性 2：頁面結構一致性

*對於所有* 網站頁面（包括新增的嵌入內容頁面），每個頁面應該包含相同的基本 HTML 結構元素（`<header>`, `<nav>`, `<main>`, `<footer>`），並且這些元素的 class 屬性應該保持一致。

**驗證需求：需求 4.1, 4.3**

### 屬性 3：導航選單一致性

*對於所有* 網站頁面，每個頁面的導航選單 HTML 結構應該相同，包含相同數量的選單項目，並且連結的 href 屬性應該指向正確的頁面。

**驗證需求：需求 3.4**

### 屬性 4：容器溢出處理

*對於任何* 嵌入內容容器，容器的 CSS 樣式應該包含適當的 `overflow` 處理（如 `overflow: hidden` 或 `overflow: auto`），並且容器應該有明確的最大寬度設定，以防止內容破壞頁面佈局。

**驗證需求：需求 5.5**

### 屬性 5：跨瀏覽器 iframe 相容性

*對於任何* 主流瀏覽器（Chrome、Firefox、Safari、Edge），當載入包含 iframe 嵌入內容的頁面時，iframe 元素應該正確渲染，並且其尺寸和位置應該符合 CSS 規則的預期值。

**驗證需求：需求 6.1**

## 錯誤處理

### iframe 載入失敗

**情境：** 外部內容（Google 表單或 YouTube 影片）無法載入

**處理方式：**
- 在 iframe 標籤內提供 fallback 文字內容
- 使用 CSS 為 iframe 設定背景色和邊框，讓使用者知道內容區域的位置

**實作：**
```html
<iframe src="[URL]" class="embed-frame">
    <p>您的瀏覽器不支援 iframe，或內容無法載入。請直接訪問：<a href="[URL]">[URL]</a></p>
</iframe>
```

### 瀏覽器不支援 iframe

**情境：** 使用者的瀏覽器不支援 iframe 元素（極少見）

**處理方式：**
- 提供 fallback 內容和直接連結
- 在頁面頂部添加提示訊息

**實作：**
```html
<noscript>
    <p>此頁面需要支援 iframe 的瀏覽器。請更新您的瀏覽器或訪問以下連結：</p>
</noscript>
```

### 響應式佈局問題

**情境：** 在極小的螢幕上，嵌入內容可能難以使用

**處理方式：**
- 為小螢幕設定最小高度
- 提供「在新視窗開啟」的連結選項

**實作：**
```css
@media (max-width: 480px) {
    .embed-wrapper {
        min-height: 400px;
    }
    .open-external {
        display: block;
        margin-top: 1rem;
    }
}
```

### 內容安全政策 (CSP) 問題

**情境：** 如果網站有嚴格的 CSP 設定，可能會阻止 iframe 載入

**處理方式：**
- 確保 CSP 標頭允許來自 Google 和 YouTube 的 frame-src
- 在 HTML meta 標籤中設定適當的 CSP

**實作：**
```html
<meta http-equiv="Content-Security-Policy" 
      content="frame-src https://docs.google.com https://www.youtube.com;">
```

## 測試策略

### 雙重測試方法

本專案將採用單元測試和屬性測試的組合方式：

- **單元測試**：驗證特定的 HTML 結構、CSS 類別存在性、特定範例
- **屬性測試**：驗證跨多個輸入的通用屬性（如響應式行為、結構一致性）

### 單元測試

單元測試將專注於：

1. **HTML 結構驗證**
   - 測試每個頁面是否包含必要的元素（header, nav, main, footer）
   - 測試 iframe 元素是否存在且具有正確的屬性
   - 測試導航選單是否包含正確的連結

2. **CSS 連結驗證**
   - 測試每個頁面是否引用正確的 CSS 檔案
   - 測試 CSS 檔案是否存在

3. **特定範例測試**
   - 測試 survey.html 頁面包含 Google 表單 iframe
   - 測試 videos.html 頁面包含 YouTube iframe
   - 測試導航選單包含「調查表單」和「影片」連結

4. **錯誤處理測試**
   - 測試 iframe 是否包含 fallback 內容
   - 測試 CSP meta 標籤是否正確設定

### 屬性測試

由於本專案主要是靜態 HTML/CSS，傳統的屬性測試（需要程式碼執行）較難應用。但我們可以使用以下方法：

1. **HTML 驗證工具**
   - 使用 HTML 驗證器確保所有頁面的 HTML 結構有效
   - 使用 CSS 驗證器確保樣式表有效

2. **響應式測試**
   - 使用自動化工具（如 Puppeteer 或 Playwright）在不同視窗尺寸下截圖
   - 驗證元素尺寸是否符合預期

3. **跨瀏覽器測試**
   - 使用 Selenium WebDriver 在多個瀏覽器中載入頁面
   - 驗證 iframe 元素是否正確渲染

4. **結構一致性測試**
   - 編寫腳本解析所有 HTML 檔案
   - 比較每個頁面的基本結構是否一致

### 測試工具建議

- **HTML/CSS 驗證**：W3C Validator API
- **自動化瀏覽器測試**：Playwright 或 Puppeteer
- **跨瀏覽器測試**：Selenium WebDriver 或 BrowserStack
- **視覺回歸測試**：Percy 或 BackstopJS

### 測試配置

對於自動化測試：
- 每個屬性測試應該在至少 3 種不同的視窗尺寸下執行（桌面、平板、手機）
- 跨瀏覽器測試應該在至少 4 個主流瀏覽器中執行
- 每個測試應該標記為：**Feature: survey-and-video-integration, Property {number}: {property_text}**

### 手動測試檢查清單

由於這是靜態網站，某些測試最好手動執行：

1. 視覺檢查
   - [ ] 嵌入內容與現有頁面風格協調
   - [ ] 間距和排版看起來正確
   - [ ] 在不同裝置上的顯示效果良好

2. 功能檢查
   - [ ] Google 表單可以正常填寫和提交
   - [ ] YouTube 影片可以正常播放
   - [ ] 所有導航連結正常工作

3. 相容性檢查
   - [ ] 在 Chrome 中正常顯示
   - [ ] 在 Firefox 中正常顯示
   - [ ] 在 Safari 中正常顯示
   - [ ] 在 Edge 中正常顯示

## 實作注意事項

### Google 表單嵌入 URL 格式

Google 表單的嵌入 URL 格式為：
```
https://docs.google.com/forms/d/e/[FORM_ID]/viewform?embedded=true
```

要獲取嵌入 URL：
1. 在 Google 表單編輯器中點擊「傳送」
2. 選擇「<>」（嵌入 HTML）標籤
3. 複製 iframe 的 src 屬性值

### YouTube 影片嵌入 URL 格式

YouTube 影片的嵌入 URL 格式為：
```
https://www.youtube.com/embed/[VIDEO_ID]
```

要獲取影片 ID：
- 從 YouTube 影片 URL `https://www.youtube.com/watch?v=VIDEO_ID` 中提取 `VIDEO_ID` 部分
- 或使用 YouTube 的「分享」→「嵌入」功能獲取完整的 iframe 程式碼

### 響應式設計最佳實踐

1. **使用相對單位**：使用 `%`、`vw`、`vh` 而非固定的 `px`
2. **設定 viewport meta 標籤**：確保所有頁面都有 `<meta name="viewport" content="width=device-width, initial-scale=1.0">`
3. **使用 CSS Grid 或 Flexbox**：提供更靈活的佈局
4. **測試多種裝置**：使用瀏覽器開發者工具的裝置模擬功能

### 效能考量

1. **延遲載入**：考慮使用 `loading="lazy"` 屬性延遲載入 iframe
2. **減少 iframe 數量**：每個頁面不要放置過多的嵌入內容
3. **優化 CSS**：確保 CSS 檔案精簡，避免不必要的樣式

### 無障礙考量

1. **提供替代文字**：在 iframe 中提供有意義的 fallback 內容
2. **鍵盤導航**：確保使用者可以使用 Tab 鍵導航到 iframe
3. **標題層級**：確保頁面標題使用正確的 h1-h6 層級
4. **顏色對比**：確保文字和背景有足夠的對比度
