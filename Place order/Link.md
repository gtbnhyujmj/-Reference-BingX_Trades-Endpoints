最小下單數量可從 API /openApi/swap/v2/quote/contracts 查詢：tradeMinQuantity, tradeMinUSDT\
\
交易規則\
交易規則：https://bingx.com/en/tradeInfo/perpetual/trading-rules/BTC-USDT/\
\
價格精度、數量精度參考接口：https://open-api.bingx.com/openApi/swap/v2/quote/contracts\
若超出精度限制，API 下單仍會成功，但會自動截斷至合規範圍。例如價格精度為 0.0001，你填 0.123456，系統將自動截成 0.1234。\
