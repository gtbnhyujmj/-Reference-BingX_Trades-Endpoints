最小下單數量：\
可以從 API /openApi/swap/v2/quote/contracts 查詢 =>> tradeMinQuantity, tradeMinUSDT\
\
交易規則：\
交易規則詳見：https://bingx.com/en/tradeInfo/perpetual/trading-rules/BTC-USDT/\
\
價格精度、數量精度參考接口：\
https://open-api.bingx.com/openApi/swap/v2/quote/contracts\
\
如果精度超過當前允許範圍，API 下單仍會成功，但系統會直接截斷。\
例如價格要求為 0.0001，但你下單 0.123456，最終會以 0.1234 成功提交。\
