import yfinance as yf
portfolio = {
    "AAPL": {"shares": 10, "buy_price": 150},
    "MSFT": {"shares": 5, "buy_price": 280},
    "GOOGL": {"shares": 2, "buy_price": 2500},
}

def get_current_price(ticker):
    stock = yf.Ticker(ticker)
    data = stock.history(period="1d")
    return data["Close"].iloc[-1]

def display_portfolio(portfolio):
    total_value = 0
    total_cost = 0

    print(f"{'Ticker':<10}{'Shares':<10}{'Buy Price':<12}{'Current Price':<15}{'Value':<12}{'P/L':<10}")
    print("-" * 70)

    for ticker, info in portfolio.items():
        shares = info["shares"]
        buy_price = info["buy_price"]
        current_price = get_current_price(ticker)
        value = shares * current_price
        cost = shares * buy_price
        profit_loss = value - cost

        print(f"{ticker:<10}{shares:<10}{buy_price:<12.2f}{current_price:<15.2f}{value:<12.2f}{profit_loss:<10.2f}")

        total_value += value
        total_cost += cost

   print("-" * 70)
    print(f"{'TOTAL':<47}{total_value:<12.2f}{(total_value - total_cost):<10.2f}")
display_portfolio(portfolio)
