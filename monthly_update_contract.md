# 月度觀測更新契約（2026-10-22）
適用：既有需求雷達 Site appgprj_6ad426892de08191ba45a16385ed329d，以及本 repo 的 monthly-observations.json。使用者已要求由週改月、月比與逐月累積。本節優先於舊週度流程；不改動其他產業週報、GEO客戶週報或OS排程。

## 唯一資料流與權限
- 公開外部研究與案例沿用 source_registry.csv、reports/、courses/；monthly-observations.json 是既有來源的月度觀測索引，不另建案例庫。
- Site 每次開啟會讀取本 repo 的 monthly-observations.json；一般月更新只改資料，無需重發佈 Site。
- 只能在本公開 repo 保存公開研究與非機敏彙整。Mandy私人投入建議、未公開客戶資料、財務、回饋及聯絡資訊保留既有受保護站／Drive，不寫入此 JSON。
- 用已連線 GitHub 原生工具讀取並寫入；不把密鑰放檔案，不依賴本機 checkout 或簽入瀏覽器。

## 每輪執行
1. 以 Asia/Taipei 計算前一個完整曆月。先讀 AGENTS.md、本契約、source_registry.csv、courses/ 與 monthly-observations.json；比對同月份最新 revision、來源與已知缺口。
2. 研究台灣企業主／主管的八類需求：工作效率、企業營運、管理決策、AI Agent、人才培訓、行銷業務、GEO／AI搜尋、創業／個人事業。優先官方公告／原始資料，最多新增10個有效公開案例；不硬湊每類數量。不把供給、搜尋熱度、詢問、報名、成交混成一種需求數。
3. 與緊鄰前一曆月比較；若缺該月或口徑不同，標未能比較，不跳月冒充月比。識別新出現、延續、反覆出現、轉弱、未觀測；轉弱必須有同口徑量測支持，沒找到不等於消失。
4. 每個領域最多一段重點，附來源、事件日／資料期間、查核日、事實與推論，以及是否足以調整下一步。沒有可靠量測，state=insufficient。不可把市場供給資訊當付費驗證。私人適配建議不在公開 JSON 更新。
5. 舊 course-radar-data.js 的 runs 保留歷史，不再新增「週」任務。需要更新來源庫或公開報告時先去重。報告路徑 reports/YYYY-MM_monthly-radar.md，內容為該月公共研究與月比，最多提出一個候選；不自動新開課、改價、聯繫、付費或發信。
6. 在 monthly-observations.json.observations 追加一個月快照。已存在相同月份、相同證據／結論則不追加；有新證據需修正時 revision+1、保留舊 revision。新月份不得覆寫舊月份。GitHub fetch_file 取得當前 blob SHA，update_file 寫入（遇衝突先重新讀取合併，禁止強覆寫）。

## JSON schema（新增快照）
- id: 唯一穩定字串；month: YYYY-MM；revision: 正整數；recordedAt: 查核日期；asOf: 資料截至日。
- coverage: closed_month（已結月的本次研究）、partial_month、historical_samples。closed_month 表示研究期間結束，不表示全市場普查。
- summary: 本月一句結論；topics: 字串陣列；sources: [{date,url,label}]。
- researchRuns/newTaiwan/newGlobal/newCases/totalCases: 有可核對依據才填非負數，否則 null。說明 metricsBasis；newCases 只計新增去重案例，totalCases 依正式來源庫；不可將月收錄筆數稱市場成長。
- demandObservations: 8筆（domain 為1至8）；每筆 {domain,state,signal,basis,sources}。state 只用 emerging/continuing/cooling/insufficient；basis 為量測口徑／限制；sources 為URL陣列。cooling 只能有可比證據才用，否則 insufficient。
- limits: 字串陣列，列實測缺口；updatedAt 在根層更新。完整舊 observations 必須保留。

## 驗收與通知
- 寫後以 GitHub fetch_file 讀回，確認新快照／來源、歷史筆數未減少、月份/revision唯一。
- 回報完成月份、與上月的三項主要差異、累積月份與尚缺證據。沒有新證據只簡短說明，不重發舊建議。
- 同月執行重試先以 id、來源及 revision 去重；沒有驗證寫入，不宣稱網站資料已更新。
- 後續網站若來源暫時失敗，顯示已隨站保存的快照日期；不得把它標成最新。
