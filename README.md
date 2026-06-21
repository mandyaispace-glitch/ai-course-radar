# AI 課程多代理系統

這套架構用於每週一次的課程市場研究，以及兩個主課產品家族的持續開發。

## 怎麼啟動

對 Codex 說：

> 啟動本週節流版 LV6 課程市場雷達，依 `weekly_brief_template.md` 執行。

預設使用三個子代理：台灣市場、國際案例、指定來源與偏好審查。主代理負責去重、評分、轉譯與更新課程卡。

## 產品家族

1. **個人 AI 工作台**：個人可控制、可重複、可檢查的一條 AI 工作流程。
2. **企業／主管戰情室**：把資料推進成訊號、決策與行動追蹤的管理閉環。

六個題目仍可獨立研究：

1. 多份資料轉主管決策摘要
2. Excel／銷售資料異常與機會分析
3. AI Agent 工作流程
4. Codex／AI Studio 個人小工具
5. 個人 AI 工作台
6. 企業／主管戰情室

市場證據決定題目維持獨立課程，或成為兩個主課的插入模組。

## 每週節流限制

- 每週一次
- 最多三個子代理
- 每週研究一至兩題
- 最多新增十個案例
- 最多深度拆解五個案例
- 最終只推薦一個優先課程方案
- 本輪不製作完整教材、簡報或招生頁
- 先讀案例庫，再搜尋外部缺口

## 檔案說明

- `AGENTS.md`：代理角色、流程與硬性規則
- `weekly_brief_template.md`：每週任務輸入與固定輸出
- `source_registry.csv`：外部案例與鎖定來源
- `packaging_scorecard.md`：課程包裝評分標準
- `courses/`：兩個主課產品卡
- `course-radar-dashboard.html`：每週視覺儀表板
- `course-radar-data.js`：每週歷史資料；每次雷達完成後新增一筆

## 每週視覺比較

每次雷達完成後，主代理需在 `course-radar-data.js` 的 `runs` 陣列新增本週資料，不覆蓋歷史紀錄。儀表板會自動顯示：

- 本週對上週增減
- 案例庫累積
- 個人 AI 工作台與主管戰情室最佳分數走勢
- 每週新增台灣／國際案例
- 每週耗時與研究題目

## GitHub 發布與維護

- `index.html` 是 GitHub Pages 首頁，會導向完整儀表板。
- 推送到 `main` 後，`.github/workflows/pages.yml` 會自動發布最新版。
- 第一次使用時，在 repository 的 Settings > Pages 將 Source 設為 GitHub Actions。
- 每週代理執行完成後，要一起更新 `course-radar-data.js`、`source_registry.csv` 與當週報告，再提交並推送。
- GitHub Pages 只負責發布；三代理研究由 Codex 每週自動化執行，避免把模型金鑰放進公開網頁。
