# 🛰️ **RCOSEA 慶生網站整體定位與目標**

* **名稱**：RCOSEA 2025 慶生活動網站
* **目標**：為我們親愛的主播 REN0809K 舉辦的生日祝福活動活動。
* **計畫**：本網站預計於 2025/08/09 日公開，在此之前僅限內部團隊試閱，在此之前須確認網站不會被找到，例如：不能是 github 公開專案。

* ## 【技術說明】

本專案前端開發採用以下組合，嚴禁使用任何 CSS 框架或預處理器（如 Tailwind、PostCSS、Bootstrap 等）：

1. **React（JSX）＋原生 HTML 結構**

   * 所有元件皆以 React 函式元件撰寫，標籤必須使用標準 HTML。
   * JavaScript 與互動效果（如 IntersectionObserver 觸發、Modal 開關）也都以手寫方式實作，搭配純 CSS 控制顯示與動態效果。

2. **AOS（Animate On Scroll）＋純 CSS 過渡／Keyframes**

   * 頁面滾動動畫、淡入淡出等動態效果必須使用 AOS；若需更高度客製的動畫，再透過純 CSS Transition 或 Keyframes 實現。
   * 所有 AOS 相關的 class 也由對應頁面／元件的 CSS 檔負責控制。

3. **純 CSS（.css 檔）＋CSS 變數＋全域 Reset**

   * `src/index.css` 只保留：
     1. 全域 Reset（例如：`* { box-sizing: border-box; margin: 0; padding: 0; }`）。
     2. CSS 變數（如：`--dark-bg`, `--primary-blue`, `--secondary-blue`, `--base-block`）。
     3. Body／#root 等全站共用排版與顏色設定（`font-family`、`background-color: var(--dark-bg)`、`color: white`）。
   * 各頁專屬樣式也改為純 CSS 編寫，嚴禁在頁面中重複定義共用樣式。要使用配色時，統一以 `var(--…)` 方式引用，避免硬碼顏色。

4. **樣式檔集中管理**

   * 原先放在 `src/pages/YourPage.jsx` 同一層級的 `YourPage.css`，已搬至 `src/styles/YourPage.css`。
   * 任何頁面要使用專屬樣式，都必須在元件檔第一行寫：

     ```js
     import '../styles/YourPage.css';
     ```
   * 共同可重複使用的元件（Header、Footer、按鈕等）的 CSS 仍放在 `src/components/` 對應元件底下。

5. **新元件樣式實作**

   * **Modal**：採用 `.modal-overlay` + `.modal-content` + `position: fixed` 等純 CSS 方式撰寫尺寸與關閉按鈕。
   * **時間軸（Timeline）**：以偽元素／絕對定位＋Media Query 控制寬版左右交替、窄版上下堆疊。整體動態由 React + 純 CSS（不靠外部框架）負責。
