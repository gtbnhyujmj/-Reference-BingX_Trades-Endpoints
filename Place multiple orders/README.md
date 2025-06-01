批量下單
當前帳戶在指定的合約品種上執行批量下單操作。
具體的下單條件與規則，與單筆下單一致。

批量下單（BatchOrders）有點複雜，但請依照下方四個步驟操作：

1. 將你的 payload 轉成字串格式

原始參數範例：
batchOrders=[{"symbol":"ETH-USDT","type":"MARKET","side":"BUY","positionSide":"LONG","quantity":1},{"symbol":"BTC-USDT","type":"MARKET","side":"BUY","positionSide":"LONG","quantity":0.001}]×tamp=1692956597902

2. 對原始參數進行簽名

範例簽名：
signature: bab521321a62a1381a76b485b92dd0f4a8b16b4616cfa4c75ffba899f80dfc86

3. 將每個值進行 URL encode，例如 batchOrders 欄位的值（除了 timestamp 不需 encode，不需 encode 鍵名，不要把全部一起 encode）
處理完後像這樣：

URL encode 後：
batchOrders=%5B%7B%22symbol%22%3A%22ETH-USDT%22%2C%22type%22%3A%22MARKET%22%2C%22side%22%3A%22BUY%22%2C%22positionSide%22%3A%22LONG%22%2C%22quantity%22%3A1%7D%2C%7B%22symbol%22%3A%22BTC-USDT%22%2C%22type%22%3A%22MARKET%22%2C%22side%22%3A%22BUY%22%2C%22positionSide%22%3A%22LONG%22%2C%22quantity%22%3A0.001%7D%5D×tamp=1692956597902

4. 最終請求範例：

perl
複製
編輯
POST https://open-api.bingx.com/openApi/swap/v2/trade/batchOrders?batchOrders=%5B%7B%22symbol%22%3A%22ETH-USDT%22%2C%22type%22%3A%22MARKET%22%2C%22side%22%3A%22BUY%22%2C%22positionSide%22%3A%22LONG%22%2C%22quantity%22%3A1%7D%2C%7B%22symbol%22%3A%22BTC-USDT%22%2C%22type%22%3A%22MARKET%22%2C%22side%22%3A%22BUY%22%2C%22positionSide%22%3A%22LONG%22%2C%22quantity%22%3A0.001%7D%5D×tamp=1692956597902&signature=bab521321a62a1381a76b485b92dd0f4a8b16b4616cfa4c75ffba899f80dfc86
批量下單會並行處理，撮合順序無法保證。

最小下單數量可由 API /openApi/swap/v2/quote/contracts 查詢：
tradeMinQuantity, tradeMinUSDT

交易規則

交易規則：https://bingx.com/en/tradeInfo/perpetual/trading-rules/BTC-USDT/

價格精度、數量精度請參考接口：https://open-api.bingx.com/openApi/swap/v2/quote/contracts
若精度超出允許範圍，API 下單仍會成功，但多餘部分會被截斷。例如，價格精度是 0.0001，若你輸入 0.123456，會自動截斷成 0.1234。

