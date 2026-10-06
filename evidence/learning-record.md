# My lab evidence / 我的實作紀錄

Use a group code, not real names or student IDs in shared files. / 共用檔只寫組別代碼，不寫姓名或學號。

- Group code / 組別：G-Classroom
- Tool / 工具：Antigravity (AI Agent)
- Route / 路線：individual 個人
- Tasks completed / 完成題目：A, B, C, D 全數完成
- Material / 素材：NDHU classroom tasks 東華課堂版
- For original-pack work: task number, author/source link and version / 原版實作：題號、作者來源連結與版本：不適用（採東華課堂版）
- My role and what I checked / 我的角色與實際檢查：負責引導 Agent 擬定計畫、嚴格審查操作邊界（防範誤刪檔案或臆測補值）、實際執行 4 道任務之多維度驗收測試（雜湊值核對、邏輯篩選、修改重測、安全退回機制）。

## Scope and plan / 範圍與計畫

Allowed input and output folders / 可讀取與輸出的資料夾：
- Task A: 輸入 `practice/01-club-files/input/`，輸出 `practice/01-club-files/output/`
- Task B: 輸入 `practice/02-campus-picker/activities.json`，輸出 `practice/02-campus-picker/output/index.html`
- Task C: 輸入 `practice/03-equipment/equipment.json`，輸出 `practice/03-equipment/output/`
- Task D: 輸入 `practice/04-review/bad-plan.txt`，輸出 `practice/04-review/my-rejection.md`

What I asked for / 原始需求：
1. Task A: 讀取社團檔案，保留所有原檔與不同版本，不刪除重複檔，產生 4 個分類資料夾、對照清單 `manifest.json` 與報告 `report.md`。
2. Task B: 製作單頁離線 HTML「課間活動挑選器」，支援地點、時間、強度複合過濾，紀錄最近 5 次成功抽選，提供重設與清除功能，雙語切換。
3. Task C: 清理器材借還記錄，去除前後空格，標準化借還狀態，移除全空列，原樣保留異常數量與負數，保留衝突 `item_id` 紀錄。
4. Task D: 審查含重大缺失之模擬計畫，抓出至少兩項問題並撰寫退回訊息。

What I checked before execution / 動手前我檢查了什麼：
- 在 Task A 執行前，詳細審核 Agent 提出的第一階段整理計畫，確認 Agent 正確辨識 12 個檔案、未因檔名含 `final2` 就預設為定稿、未提議刪除備份檔，且明確承諾不碰指定目錄以外的任何檔案。

## Tests actually performed / 我真的做過的測試

| Test / 測試 | Expected / 預期 | Observed / 實際 | Evidence / 證據 |
|---|---|---|---|
| 1. Task A 檔案完整性與雜湊驗證 | `input/` 12 檔完整留存，`output/` 各分類共 12 檔文字複本，SHA-256 雜湊與原檔 100% 一致 | 原檔與複本皆精確為 12 檔，雜湊值全部相符，未刪除任何版本 | [`manifest.json`](file:///c:/Users/白/Documents/上課用/1006/practice/01-club-files/output/manifest.json), [`report.md`](file:///c:/Users/白/Documents/上課用/1006/practice/01-club-files/output/report.md) |
| 2. Task B 邊界無符合條件篩選測試 | 設定「室外 / 15分鐘 / 中強度」，應顯示「沒有符合條件的活動」，不可偷放寬條件 | 畫面清楚顯示錯誤提示區塊「沒有符合條件的活動」，未挑選出任何不符資料，且該次無效抽選不記入歷史 | [`index.html`](file:///c:/Users/白/Documents/上課用/1006/practice/02-campus-picker/output/index.html) |
| 3. Task B 確定單一結果測試 | 設定「室外 / 30分鐘 / 中強度」，每次抽選必須只能是 A09 | 連續測試 5 次，每次抽中結果皆為 `[A09] 在合適位置快走`，無其他項目 | [`index.html`](file:///c:/Users/白/Documents/上課用/1006/practice/02-campus-picker/output/index.html) |
| 4. Task C 資料清理有效筆數核算 | 原始 10 列應過濾掉 1 列完全空物件，產出 9 列有效資料，保留相同 ID（EQ01, EQ02）與異常數量 | `normalized.json` 恰為 9 筆有效物件，空列被移除，`issues.md` 清楚記錄負數與空數量 | [`normalized.json`](file:///c:/Users/白/Documents/上課用/1006/practice/03-equipment/output/normalized.json), [`issues.md`](file:///c:/Users/白/Documents/上課用/1006/practice/03-equipment/output/issues.md) |

## One revision / 一次修改

Before / 原來的情況：
第一版挑選器在有多個符合活動時，可能因隨機抽選而連續抽中同一個項目；且使用者無法得知當前條件下共有多少個候選項目可供抽選。

Request / 我提出的修改：
1. 當符合條件之候選活動大於 1 項時，加入「防連續重複」邏輯（避免連續兩次選中同一活動）。
2. 在結果區顯示「符合候選數：N」，提升資訊透明度。
3. 加入鍵盤快捷鍵支援（可按 Enter 或 Space 快速抽選）。

After and retest / 修改後與重測結果：
在「室內 / 15分鐘 / 低強度」（候選為 A01, A02, A03, A04 共 4 項）條件下連續抽選 10 次，相鄰兩次抽出的活動 ID 皆不相同，且畫面即時標註「符合候選數：4」；按鍵盤空白鍵可順暢觸發抽選。

New requirement or defect? / 新需求還是原規格未做到？
新需求（原規格之各項基礎功能於第一版已全數達成，此項修改為提升使用者操作體驗之功能增強）。

## One rejection / 一次退回

Which action I reject and why / 退回哪個動作、為什麼：
退回 `practice/04-review/bad-plan.txt` 中所列的 5 項危險行為：
1. 擅自掃描與整理整個 `Downloads` 目錄（超出授權範圍，具隱私洩漏與損毀檔案風險）。
2. 未經許可自動刪除重複檔案（不可逆的破壞性操作）。
3. 主觀臆斷將 `final2` 認定為最新版（忽視檔案內容差異）。
4. 缺漏數值自行填補猜測值（產生 AI 幻覺，污染原始資料品質）。
5. 完成後未經審查自動公開成果（嚴重資安洩漏風險）。

An acceptable alternative / 可以怎麼改：
AI 僅能在指定之專案資料夾內運作；建立 `output/` 存放整理產物；保留所有版本與重複檔案，並產出清單與報表供人工決策；缺漏值如實保留並標註待查；所有成果僅存放於本地端，未經授權絕不公開。

## Still unverified / 還沒驗證

What I cannot claim is complete / 哪些事不能說已完成：
1. 社團活動企劃的最終定案版本（戶外或室內方案在原檔皆標記未定案，仍待真人開會決議）。
2. Task B 隨機抽選演算法在數學上的長期均勻分佈（僅驗收過濾條件與候選池邏輯，未進行萬次抽樣之統計檢驗）。
3. Task C 中器材 EQ02 的真實數量（記錄中分別有 2 與 3，需由社團幹部實體盤點方能確定庫存）。
