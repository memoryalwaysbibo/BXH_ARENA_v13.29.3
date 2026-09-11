# BXH ARENA v13.29.3 更新說明

## 本版定位

v13.29.3 補齊稱號與每日簽到的最高管理工具：歷史正式賽事補算、隱藏／限定稱號狀態管理、簽到彙總與異常檢查。v13.29.2 的玩家端崩潰修正完整保留。

## 已完成

- 歷史補算固定先預覽、再執行，每批最多 25 筆。
- 僅核對官方、積分賽、非測試、非取消且已完成天梯結算的賽事。
- 以 `playerEventResults/{eventCode_uid}` 防止同一玩家同一賽事重複累計。
- 補算只判定 `retroactiveEnabled=true` 的稱號。
- 每批結果寫入 `titleBackfillRuns`，保存游標、模式、摘要與錯誤樣本。
- 最高管理員可調整稱號啟用、隱藏及絕版狀態。
- 絕版會同步停用，但不刪除玩家已取得紀錄。
- 隱藏稱號未取得前只顯示問號；已取得玩家仍能讀取完整內容。
- 每日簽到 Transaction 同步更新 `engagementDailyStats/{YYYY-MM-DD}`。
- 管理端顯示今日、近 7 日、本月正式／測試簽到、連續簽到排行。
- 異常掃描最多讀取 250 份 `playerStats`，檢查負數、目前連續高於歷史最高、月累積高於總累積及日期格式錯誤。

## 安全邊界

- 新管理 Callable 全部要求 `super_admin`。
- 瀏覽器不能寫入 `engagementDailyStats`、`titleBackfillRuns`、稱號定義、進度或已取得稱號。
- 歷史補算不改寫 `tournaments`。
- tester、community 與一般非積分賽不納入正式補算。
- 開拓者前 100 名仍維持停用，不會因本版自動開放。

## 回復

可先關閉四個 engagement 功能開關，再退回 v13.29.2。新增彙總與補算紀錄可保留，不需刪除；原有賽事與玩家資料不需回復。

## 驗證

- HTML 內嵌 JavaScript 語法
- Functions JavaScript 語法與模組載入
- v13.29.3 專項測試
- v13.29.2 玩家崩潰防護回歸
- v13.28.9 帳號管理回歸
- v13.28.8 登入／Session 回歸
- Functions production dependency audit

Firestore Emulator 仍須在可下載執行元件的 Firebase 部署環境補做。
