# 社團檔案整理報告（Task A Report）

## 1. 整理概況
* **輸入檔案總數**：12 個（位於 `input/`）
* **輸出檔案總數**：12 個文字檔副本（分別收錄於 `output/` 4 個分類資料夾）＋ 1 個 `manifest.json` ＋ 1 個 `report.md`
* **原始檔案狀態**：`input/` 資料夾內所有原始檔案皆完整保留，未刪除、未修改、未更名。

---

## 2. 分類架構與檔案配置

| 分類資料夾 | 檔案名稱 | 說明 |
|---|---|---|
| `proposals_planning/` | `proposal_final.txt` | 企劃第一版（戶外活動，30分鐘，尚未定案） |
| `proposals_planning/` | `proposal_final2.txt` | 企劃第二版（室內活動，20分鐘，仍待討論） |
| `proposals_planning/` | `meeting_notes.txt` | 會議紀錄（下次討論室內或室外方案） |
| `proposals_planning/` | `next_steps.txt` | 待辦事項（比較兩個企畫，兩者皆未定案） |
| `proposals_planning/` | `rain_plan.txt` | 雨天備案（下雨則另議室內方案） |
| `publicity/` | `announcement.txt` | 活動通知（行前提醒攜帶筆記本） |
| `publicity/` | `announcement_copy.txt` | 活動通知副本（內容完全一致） |
| `publicity/` | `poster_text.txt` | 海報文案（宣傳小卡製作） |
| `logistics_budget/` | `equipment_list.txt` | 器材清單（麥克筆4支、紙張2包） |
| `logistics_budget/` | `equipment_backup.txt` | 器材清單備份（內容完全一致） |
| `logistics_budget/` | `budget_draft.txt` | 紙張預算模擬（金額100，尚未核定） |
| `feedback/` | `feedback_questions.txt` | 回饋問題（活動滿意度調查題目） |

---

## 3. 重複檔案與版本差異分析

### (1) 內容完全相同的檔案（已各保留副本）
* `announcement.txt` 與 `announcement_copy.txt`：
  - SHA-256 雜湊值皆為 `C19164B1054EBF52ED33BC5321C88737D71C194E383BF8E0F75AE7E2DF400780`
  - 判定：內容百分之百相同。依指示不刪除副本，兩者皆複製至 `output/publicity/`。
* `equipment_list.txt` 與 `equipment_backup.txt`：
  - SHA-256 雜湊值皆為 `C21D53BA1F8D3AD06E183353993512242131976F5E370BAFBCDEAA1F88484196`
  - 判定：內容百分之百相同。依指示不刪除備份，兩者皆複製至 `output/logistics_budget/`。

### (2) 檔名相近但內容不同的檔案（不同版本完整保留）
* `proposal_final.txt` vs `proposal_final2.txt`：
  - `proposal_final.txt` 內文為戶外活動 30 分鐘；`proposal_final2.txt` 內文為室內活動 20 分鐘。
  - 兩者 SHA-256 雜湊完全不同。
  - 不以 `final` 或 `final2` 判定誰是定案，兩者皆保留於 `output/proposals_planning/` 供團隊比較。

---

## 4. 待確認問題（需人工決策）
1. **企劃定案**：目前戶外與室內兩版企劃內文皆註記「尚未定案／仍待討論」，需等下一次籌備會議決定最終方案。
2. **預算審核**：`budget_draft.txt` 標記紙張預算 100 為模擬金額且「尚未核定」，需交由社長或總務核准。
3. **重複檔案去留**：`announcement_copy.txt` 與 `equipment_backup.txt` 現已保留副本備查；後續團隊若欲精簡資料夾，可由負責人評估是否將副本封存。

---

## 5. 實際執行的檢查與未確認項目
* **已完成的檢查**：
  - [x] 核對 `input/` 12 個檔案原封不動，大小與修改日期無破壞。
  - [x] 核對 `output/` 內確實複製了 12 個 `.txt` 檔案，無遺漏。
  - [x] 比對複本 SHA-256 雜湊值與原檔完全一致，複製過程無內容損壞或竄改。
  - [x] 產出符合格式規範的 `manifest.json`，頂層為 12 筆物件陣列。
* **尚未確認項目**：
  - [ ] 企劃案究竟採納室內還是室外方案（需開會確認）。
  - [ ] 活動確切舉辦時間與地點（原檔內文皆註明尚未決定）。
