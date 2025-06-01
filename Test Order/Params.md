根據下單類型，部分參數是必填的：\
\
LIMIT（限價單）： 必填參數：\
quantity（數量）、price（價格）\
\
MARKET（市價單）： 必填參數：\
quantity（數量）\
\
TRAILING_STOP_MARKET（跟蹤止損單）/ TRAILING_TP_SL（跟蹤止盈止損單）： \
必須填寫 price 或 priceRate 欄位\
\
TRIGGER_LIMIT、STOP、TAKE_PROFIT（條件限價單/止損單/止盈單）： 必填參數：\
quantity、stopPrice、price\
\
STOP_MARKET、TAKE_PROFIT_MARKET、TRIGGER_MARKET（條件市價單/市價止盈止損/觸發市價單）： 必填參數：\
quantity、stopPrice\
