# BXH ARENA v13.29.3 部署順序

1. 確認 Firebase CLI 指向 BXH ARENA 正式專案。
2. 執行 `npm --prefix functions ci`。
3. 執行 `npm --prefix functions run check`。
4. 部署 `firebase deploy --only firestore:rules`。
5. 部署 `firebase deploy --only functions`。
6. 最後部署或上傳 `index.html`。

## 初次上線

1. 最高管理員進入「帳號管理 → 稱號與每日簽到」。
2. 先載入簽到統計，確認 Callable 與 Rules 正常。
3. 歷史補算只按「預覽下一批」，先確認可補算／跳過數量。
4. 確認無誤後再按「執行這一批補算」。
5. 每批完成後觀察 Functions 日誌，再處理下一批。
6. 開拓者、初代戰士及資料不足的進階稱號保持停用。

## 部署後最低驗證

- 玩家首頁稱號服務失敗時不會反覆刷新。
- 每日簽到成功後 `engagementDailyStats` 只增加一次。
- tester 只增加測試計數，不增加正式計數。
- 歷史補算預覽不寫入玩家統計。
- 同一批補算執行兩次不重複累計、不重複發稱號。
- community、tester、一般賽與取消賽事均被跳過。
- 隱藏稱號對未取得玩家保持隱藏，已取得玩家仍顯示完整名稱。
- 登入、報名、報到、計分、天梯及封存各執行一次冒煙測試。

## 緊急停止

先關閉 `automaticTitleAwardsEnabled` 與 `checkInTitleAwardsEnabled`。歷史補算為人工逐批操作，停止按下一批即可，不需要刪除任何資料。
