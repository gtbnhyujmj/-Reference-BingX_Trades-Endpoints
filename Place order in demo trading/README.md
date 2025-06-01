模擬交易下單
當前帳戶在指定的合約品種下單。（支持限價單、市價單、計劃委託市價單、計劃委託限價單、持倉止盈止損單、強制平倉單等）

模擬交易域名：open-api-vst.bingx.com

根據下單類型，不同參數是必填的：

LIMIT（限價單）： 必填參數：quantity（數量）、price（價格）

MARKET（市價單）： 必填參數：quantity（數量）

TRAILING_STOP_MARKET（跟蹤止損單）或 TRAILING_TP_SL（跟蹤止盈止損單）： 需要填寫 price 欄位或 priceRate 欄位

TRIGGER_LIMIT、STOP、TAKE_PROFIT（條件限價單/止損單/止盈單）： 必填參數：quantity、stopPrice、price

STOP_MARKET、TAKE_PROFIT_MARKET、TRIGGER_MARKET（條件市價單/市價止盈止損/觸發市價單）： 必填參數：quantity、stopPrice

1. 開/平倉說明：如何用同一個接口來開倉（多/空）和平倉（多/空）？
請參考下列請求內容組合：

開多倉/買入多單： side=BUY & positionSide=LONG

平多倉/賣出多單： side=SELL & positionSide=LONG

開空倉/賣出空單： side=SELL & positionSide=SHORT

平空倉/買入空單： side=BUY & positionSide=SHORT

範例：

json
複製
編輯
{"symbol": "ETH-USDT","side": "BUY","positionSide": "LONG", "type": "MARKET", "quantity": 5}
2. 設定止盈/止損：
這個接口也能用來設置止盈/止損，但前提是已經有持倉。

範例：

json
複製
編輯
{"symbol": "ETH-USDT","side": "BUY","positionSide": "LONG", "type": "TAKE_PROFIT_MARKET", "quantity": 3, "stopPrice": 31968.0}
3. 下單時同時設定止盈/止損：
利用 takeProfit 和 stopLoss 欄位

範例：

json
複製
編輯
{"symbol": "BTC-USDT","side": "BUY","positionSide": "LONG","type": "MARKET","quantity": 5,"takeProfit": "{\"type\": \"TAKE_PROFIT_MARKET\", \"stopPrice\": 31968.0,\"price\": 31968.0,\"workingType\":\"MARK_PRICE\"}"}
條件單的觸發規則：
STOP/STOP_MARKET（止損單/市價止損單）：

待觸發止損單的累計數量不可大於持倉數量

買單：標記價格 ≥ 觸發價格 stopPrice

賣單：標記價格 ≤ 觸發價格 stopPrice

TAKE_PROFIT/TAKE_PROFIT_MARKET（止盈單/市價止盈單）：

待觸發止盈單的累計數量不可大於持倉數量

買單：標記價格 ≤ 觸發價格 stopPrice

賣單：標記價格 ≥ 觸發價格 stopPrice

最小下單數量可從 API /openApi/swap/v2/quote/contracts 查詢：tradeMinQuantity, tradeMinUSDT

交易規則

交易規則：https://bingx.com/en/tradeInfo/perpetual/trading-rules/BTC-USDT/

價格精度、數量精度參考接口：https://open-api.bingx.com/openApi/swap/v2/quote/contracts
若超出精度限制，API 下單仍會成功，但會自動截斷至合規範圍。例如價格精度為 0.0001，你填 0.123456，系統將自動截成 0.1234。
