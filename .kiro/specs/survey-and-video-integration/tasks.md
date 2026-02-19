# 實作計畫：調查表單與影片整合

## 概述

本實作計畫將在現有的個人介紹網站中新增 Google 表單和 YouTube 影片嵌入功能。實作將採用漸進式方法，先建立基礎結構和樣式，然後建立各個頁面，最後進行整合和測試。

## 任務

- [ ] 1. 建立嵌入內容的 CSS 樣式表
  - 建立 `css/embed.css` 檔案
  - 實作 `.embed-container`、`.embed-wrapper`、`.embed-frame` 等基礎類別
  - 實作 Google 表單專用樣式（`.google-form-container`、`.form-wrapper`、`.google-form`）
  - 實作 YouTube 影片專用樣式（`.video-container`、`.video-wrapper`、`.youtube-video`）
  - 實作響應式媒體查詢（桌面、平板、手機）
  - _需求：1.3, 2.3, 5.2, 5.5_

- [ ]* 1.1 撰寫 CSS 樣式的單元測試
  - 驗證 CSS 檔案存在且可載入
  - 驗證關鍵 CSS 類別已定義
  - _需求：1.3, 2.3_

- [ ] 2. 建立 Google 表單頁面
  - [ ] 2.1 建立 `survey.html` 檔案
    - 複製現有頁面的基本結構（header, nav, main, footer）
    - 設定正確的 meta 標籤（charset, viewport）
    - 連結 `css/main.css` 和 `css/embed.css`
    - 設定頁面標題為「調查表單」
    - _需求：1.1, 4.1, 4.2, 4.3_

  - [ ] 2.2 在 survey.html 中實作 Google 表單嵌入
    - 建立 `.embed-container` 和 `.google-form-container` 容器
    - 新增頁面標題 `<h1>`
    - 插入 Google 表單 iframe（使用佔位符 URL）
    - 設定 iframe 屬性（frameborder="0"）
    - 新增 iframe fallback 內容
    - _需求：1.1, 1.2, 5.1, 5.2_

  - [ ]* 2.3 撰寫 survey.html 的單元測試
    - 驗證頁面包含必要的 HTML 結構元素
    - 驗證 iframe 元素存在且具有正確的類別
    - 驗證 CSS 連結正確
    - 驗證 iframe 包含 fallback 內容
    - _需求：1.1, 4.1, 4.2_

- [ ] 3. 建立 YouTube 影片頁面
  - [ ] 3.1 建立 `videos.html` 檔案
    - 複製現有頁面的基本結構（header, nav, main, footer）
    - 設定正確的 meta 標籤（charset, viewport）
    - 連結 `css/main.css` 和 `css/embed.css`
    - 設定頁面標題為「影片內容」
    - _需求：2.1, 4.1, 4.2, 4.3_

  - [ ] 3.2 在 videos.html 中實作 YouTube 影片嵌入
    - 建立 `.embed-container` 和 `.video-container` 容器
    - 新增頁面標題 `<h1>`
    - 插入 YouTube iframe（使用佔位符影片 ID）
    - 設定 iframe 屬性（frameborder="0", allowfullscreen, allow）
    - 新增 iframe fallback 內容
    - _需求：2.1, 2.2, 2.6, 5.1, 5.2_

  - [ ]* 3.3 撰寫 videos.html 的單元測試
    - 驗證頁面包含必要的 HTML 結構元素
    - 驗證 YouTube iframe 存在且具有正確的屬性
    - 驗證 CSS 連結正確
    - 驗證 iframe 包含 fallback 內容和 allowfullscreen 屬性
    - _需求：2.1, 2.2, 2.6, 4.1_

- [ ] 4. 檢查點 - 驗證新頁面結構
  - 確保 survey.html 和 videos.html 可以在瀏覽器中正常開啟
  - 確保頁面樣式正確載入
  - 如有問題請詢問使用者

- [ ] 5. 更新所有頁面的導航選單
  - [ ] 5.1 更新現有頁面的導航選單
    - 在 index.html 的導航選單中新增「調查表單」和「影片」連結
    - 在 thesis-guidance.html 的導航選單中新增連結
    - 在 government-grants.html 的導航選單中新增連結
    - 在 web-development.html 的導航選單中新增連結
    - 在 about.html 的導航選單中新增連結
    - 在 contact.html 的導航選單中新增連結
    - _需求：3.1, 3.2, 3.4_

  - [ ] 5.2 更新新頁面的導航選單
    - 在 survey.html 的導航選單中新增所有連結
    - 在 videos.html 的導航選單中新增所有連結
    - 確保所有連結的 href 屬性正確
    - _需求：3.1, 3.2, 3.4_

  - [ ]* 5.3 撰寫導航選單的單元測試
    - 驗證所有頁面包含相同數量的導航選單項目
    - 驗證「調查表單」連結指向 survey.html
    - 驗證「影片」連結指向 videos.html
    - 驗證所有連結的 href 屬性正確
    - _需求：3.1, 3.2_

- [ ]* 6. 撰寫屬性測試
  - [ ]* 6.1 撰寫響應式容器調整的屬性測試
    - **屬性 1：響應式容器調整**
    - 使用 Playwright 或 Puppeteer 在不同視窗寬度下測試
    - 驗證容器在桌面（1200px）、平板（768px）、手機（375px）尺寸下正確調整
    - 驗證內容不會溢出容器邊界
    - **驗證需求：需求 1.3, 2.3**

  - [ ]* 6.2 撰寫頁面結構一致性的屬性測試
    - **屬性 2：頁面結構一致性**
    - 解析所有 HTML 檔案
    - 驗證每個頁面包含 header, nav, main, footer 元素
    - 驗證這些元素的 class 屬性在所有頁面中一致
    - **驗證需求：需求 4.1, 4.3**

  - [ ]* 6.3 撰寫導航選單一致性的屬性測試
    - **屬性 3：導航選單一致性**
    - 解析所有 HTML 檔案的導航選單
    - 驗證每個頁面的導航選單 HTML 結構相同
    - 驗證選單項目數量一致
    - 驗證連結的 href 屬性正確
    - **驗證需求：需求 3.4**

  - [ ]* 6.4 撰寫容器溢出處理的屬性測試
    - **屬性 4：容器溢出處理**
    - 驗證 .embed-wrapper 和相關容器有 overflow 樣式
    - 驗證容器有最大寬度設定
    - **驗證需求：需求 5.5**

  - [ ]* 6.5 撰寫跨瀏覽器相容性的屬性測試
    - **屬性 5：跨瀏覽器 iframe 相容性**
    - 使用 Selenium WebDriver 在 Chrome、Firefox、Safari、Edge 中測試
    - 驗證 iframe 元素正確渲染
    - 驗證 iframe 尺寸和位置符合預期
    - **驗證需求：需求 6.1**

- [ ] 7. 新增錯誤處理和無障礙功能
  - [ ] 7.1 新增 Content Security Policy meta 標籤
    - 在 survey.html 和 videos.html 中新增 CSP meta 標籤
    - 允許來自 Google 和 YouTube 的 frame-src
    - _需求：6.3_

  - [ ] 7.2 改善 iframe fallback 內容
    - 確保 fallback 內容包含直接連結
    - 新增有意義的說明文字
    - _需求：6.3_

  - [ ]* 7.3 撰寫錯誤處理的單元測試
    - 驗證 CSP meta 標籤存在且正確
    - 驗證 iframe fallback 內容包含連結
    - _需求：6.3_

- [ ] 8. 檢查點 - 執行所有測試
  - 執行所有單元測試和屬性測試
  - 確保所有測試通過
  - 如有失敗的測試，修正問題
  - 如有問題請詢問使用者

- [ ] 9. 最終整合和文件更新
  - [ ] 9.1 建立使用說明文件
    - 說明如何更新 Google 表單 URL
    - 說明如何更新 YouTube 影片 ID
    - 說明如何新增更多嵌入內容
    - _需求：1.1, 2.1_

  - [ ] 9.2 進行最終的手動測試
    - 在實際瀏覽器中測試所有頁面
    - 驗證導航連結正常工作
    - 驗證嵌入內容正確顯示（使用實際的 Google 表單和 YouTube 影片）
    - 在不同裝置尺寸下測試響應式設計
    - _需求：所有需求_

- [ ] 10. 最終檢查點
  - 確保所有功能正常運作
  - 確保所有測試通過
  - 詢問使用者是否有任何問題或需要調整的地方

## 注意事項

- 標記為 `*` 的任務是可選的，可以跳過以加快 MVP 開發
- 每個任務都參考了特定的需求以確保可追溯性
- 檢查點確保漸進式驗證
- 屬性測試驗證通用的正確性屬性
- 單元測試驗證特定的範例和邊緣情況

## 實作提示

### 獲取 Google 表單嵌入 URL
1. 在 Google 表單編輯器中點擊「傳送」
2. 選擇「<>」（嵌入 HTML）標籤
3. 複製 iframe 的 src 屬性值

### 獲取 YouTube 影片 ID
- 從 YouTube 影片 URL `https://www.youtube.com/watch?v=VIDEO_ID` 中提取 `VIDEO_ID` 部分
- 嵌入 URL 格式：`https://www.youtube.com/embed/VIDEO_ID`

### 測試工具建議
- **HTML/CSS 驗證**：W3C Validator API
- **自動化瀏覽器測試**：Playwright 或 Puppeteer
- **跨瀏覽器測試**：Selenium WebDriver
- **視覺回歸測試**：BackstopJS（可選）
