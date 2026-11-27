Ticker list: StockService owns the Instrument table (AAPL, AVGO, SPY…). The admin manages it.

Ingestor startup: it reads the active tickers and tells Alpaca over its WebSocket: "send me AAPL, AVGO, SPY".

Price arrives: Alpaca sends AAPL = 321.23 to the Ingestor.

Ingestor → Redis, two commands:
SET price:AAPL 321.23 → overwrites the latest price (the "notice board").
PUBLISH prices:AAPL 321.23 → broadcasts it (the "loudspeaker"). Not stored.

Every StockService instance hears the broadcast. Each one subscribed to prices:* at startup, so all of them get AAPL = 321.23.

User connects: the browser opens a WebSocket to the gateway. The gateway checks the token, picks one StockService instance (say #2), and from then on just copies messages back and forth. To the browser it feels like talking directly to #2.

User subscribes: through that connection the browser says "subscribe AAPL". Instance #2 remembers: "this user wants AAPL".

Forwarding: when #2 hears AAPL = 321.23 from Redis (step 5), it sends it to every one of its users subscribed to AAPL. Users on other instances get it from their own instance.

Browser: receives the price and updates the last candle on the chart.