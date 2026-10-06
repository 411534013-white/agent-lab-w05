# My lab evidence / 我的實作紀錄

Use a group code, not real names or student IDs in shared files. / 共用檔只寫組別代碼，不寫姓名或學號。

- Group code / 組別：G-Classroom
- Tool / 工具：Antigravity (AI Agent)
- Route / 路線：individual 個人
- Tasks completed / 完成題目：A、B、D（必做）；C 為選做，是否列入請依實際情況填寫
- Material / 素材：NDHU classroom tasks 東華課堂版
- For original-pack work: task number, author/source link and version / 原版實作：題號、作者來源連結與版本：不適用（採東華課堂版）
- My role and what I checked / 我的角色與實際檢查：請依本人實際操作填寫。下方列出的檔案內容可供核對；未實際執行的測試或未留存的截圖不可填成已完成。

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

## Tests to perform and record / 請實際測試後填寫

以下保留你原先填寫的實測結果。repo 目前沒有附上測試截圖；請把實際截圖放入 `evidence/`，並確認以下六組測試都已實際執行。

| Test / 測試 | Expected / 預期 | Observed / 實際 | Evidence / 證據 |
|---|---|---|---|
| Task A 檔案完整性與雜湊 | 12 個輸入檔完整保留；12 個輸出副本雜湊相符 | 原紀錄：12 檔完整，SHA-256 全部相符 | [`manifest.json`](practice/01-club-files/output/manifest.json)、[`report.md`](practice/01-club-files/output/report.md) |
| 室內／15／低 | 僅 A01–A04 | 原紀錄未列觀察結果，請確認是否已測 | 請附截圖 |
| 室外／15／中 | 顯示沒有符合的活動，不放寬條件 | 原紀錄：顯示「沒有符合條件的活動」，未加入抽選歷史 | 請附截圖 |
| 室外／30／中 | 僅 A09 | 原紀錄：連續 5 次皆為 A09 | 請附截圖 |
| 不限／60／不限，成功抽 6 次 | 僅保留最近 5 筆，最新在前 | 原紀錄未列觀察結果，請確認是否已測 | 請附截圖 |
| 重設篩選 | 回到不限／30／不限，紀錄仍在 | 原紀錄未列觀察結果，請確認是否已測 | 請附截圖 |
| 清除紀錄，再切英文 | 紀錄清空，控制項和活動名稱變英文 | 原紀錄未列觀察結果，請確認是否已測 | 請附截圖 |
| Task C 資料清理有效筆數 | 原始 10 列去除 1 列全空物件，保留 9 列有效資料及異常數量 | 原紀錄：9 筆、重複 ID 與異常數量保留 | [`normalized.json`](practice/03-equipment/output/normalized.json)、[`issues.md`](practice/03-equipment/output/issues.md) |

## One revision / 一次修改

Before / 原來的情況：
第一版挑選器在有多個符合活動時，可能因隨機抽選而連續抽中同一個項目；且使用者無法得知當前條件下共有多少個候選項目可供抽選。

Request / 我提出的修改：
1. 當符合條件之候選活動大於 1 項時，加入「防連續重複」邏輯（避免連續兩次選中同一活動）。
2. 在結果區顯示「符合候選數：N」，提升資訊透明度。
3. 加入鍵盤快捷鍵支援（可按 Enter 或 Space 快速抽選）。

After and retest / 修改後與重測結果：
原紀錄：在室內／15／低條件連抽 10 次，相鄰結果皆不同；候選數顯示 4；Space 可觸發抽選。請附修改前後截圖。注意：依課程規格，隨機結果重複不算錯；避免重複是新增需求，會改變抽選分布。

New requirement or defect? / 新需求還是原規格未做到？
待本人依實際修改前狀態判定。課程原規格沒有要求避免連續重複或顯示候選數；若新增這些功能，應標示為新需求，不能宣稱修正原始缺陷。

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
