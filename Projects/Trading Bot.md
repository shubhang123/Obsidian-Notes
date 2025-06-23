# Documentation: NIFTY 500 AI Trading Signal Bot

  

This document provides a comprehensive explanation of the `trading_bot.py` script, detailing its functionality, architecture, and the role of each component.

  

---

  

## 1. Overall Workflow

  

The script is a self-contained, automated system designed to identify potential short-term trading opportunities within the NIFTY 500 stock universe. The process runs from Monday to Friday at a scheduled time and can be summarized in these steps:

  

1. **Fetch Universe**: It begins by scraping the latest list of NIFTY 500 constituent stocks from Wikipedia.

2. **Data Collection**: For each stock, it gathers three key pieces of information:

* **Technical Data**: 14-day Relative Strength Index (RSI) using 30 days of historical prices from `yfinance`.

* **Fundamental Data**: Trailing Twelve-Month (TTM) Price-to-Earnings (P/E) ratio from `Finnhub`.

* **News Sentiment**: The top 3 recent news headlines from `NewsAPI`.

3. **Screening**: It filters this universe to find stocks that meet specific value and oversold criteria: **RSI < 30** and **P/E < 20**.

4. **AI Analysis**: It takes the top 3 stocks from the screened list (sorted by the lowest RSI) and sends their data to the **Groq API (using the Gemini 1.5 Flash model)**. It prompts the AI for a detailed trading plan.

5. **Reporting**: It aggregates the AI-generated reports for the top 3 candidates into a single, well-formatted Markdown message.

6. **Notification**: It sends this consolidated report to a specified Telegram channel.

7. **Scheduling**: The entire process is automated to run every weekday at 18:30 IST using a scheduler.

  

---

  

## 2. Setup & Configuration

  

Before running the script, two setup steps are required:

  

### `requirements.txt`

This file lists all the necessary Python libraries. They are installed using a virtual environment to avoid conflicts with system packages:

  

```bash

# 1. Create a virtual environment

python3 -m venv venv

  

# 2. Install packages into the environment

./venv/bin/pip install -r requirements.txt

```

  

### `.env` File

This file is essential for securely storing your secret API keys and configuration variables. The script uses the `python-dotenv` library to load these values into the environment at runtime. You must create this file in the same directory as the script.

  

**File Content (`.env`):**

```

GROQ_API_KEY="YOUR_GROQ_API_KEY"

TELEGRAM_TOKEN="YOUR_TELEGRAM_BOT_TOKEN"

TELEGRAM_CHANNEL="@your_channel_name"

FINNHUB_API_KEY="YOUR_FINNHUB_API_KEY"

NEWSAPI_KEY="YOUR_NEWSAPI_KEY"

```

  

---

  

## 3. Core Components (Function Breakdown)

  

### `get_nifty500_tickers()`

- **Purpose**: To get an up-to-date list of all stocks in the NIFTY 500 index.

- **How it Works**: It sends an HTTP request to the Wikipedia page for the "NIFTY 500". It then uses `BeautifulSoup` to parse the HTML, find the table with the ID `constituents`, and extract the ticker symbol from the second column of each row. It appends `.NS` to each ticker to make it compatible with the `yfinance` library for stocks listed on the National Stock Exchange of India.

  

### `calculate_rsi(data, window=14)`

- **Purpose**: To calculate the Relative Strength Index (RSI), a momentum indicator.

- **How it Works**: It takes a pandas DataFrame of historical price data as input. It calculates the price changes (`delta`), separates them into gains and losses, and computes the average gain and average loss over a 14-day rolling window. The final RSI value is calculated using the standard formula: `100 - (100 / (1 + RS))`, where RS is the ratio of average gain to average loss.

  

### `get_stock_data(ticker)`

- **Purpose**: To act as a data aggregator for a single stock.

- **How it Works**: This function fetches data from three different sources:

1. **yfinance**: Downloads the last 45 days of daily price data to ensure a stable RSI calculation. It then calls `calculate_rsi()` on this data.

2. **Finnhub**: It queries the Finnhub API for basic financial metrics, specifically extracting the trailing-twelve-month P/E ratio (`peTTM`).

3. **NewsAPI**: It fetches the 3 most recent English headlines related to the company.

- **Output**: It returns a dictionary containing the ticker, latest close price, RSI, P/E, and a list of headlines. It includes `time.sleep(1)` to respect API rate limits.

  

### `get_ai_analysis(stock_info)`

- **Purpose**: To generate a qualitative trading plan using a Large Language Model (LLM).

- **How it Works**: This function constructs a detailed, multi-part prompt. The prompt includes the stock's ticker, price, RSI, P/E, and news headlines. It then sends this prompt to the Groq API, asking the `gemini-1.5-flash` model to provide a BUY/HOLD/SELL call, entry/stop/target prices, position sizing advice, and a concise rationale. The `temperature` is set to `0.3` to encourage more deterministic and factual responses.

  

### `send_telegram_message(message)`

- **Purpose**: To send the final report to the designated Telegram channel.

- **How it Works**: It initializes the Telegram bot using the `python-telegram-bot` library and the token from your `.env` file. It then sends the formatted message text to the channel specified in `TELEGRAM_CHANNEL`, using `parse_mode='Markdown'` to ensure the formatting (like bold text and italics) is rendered correctly.

  

### `main_job()`

- **Purpose**: To orchestrate the entire end-to-end process.

- **How it Works**: This is the main driver of the script. It calls the other functions in sequence:

1. Calls `get_nifty500_tickers()` to get the list of stocks.

2. Loops through each ticker, calling `get_stock_data()` to fetch its data.

3. Screens the results based on the `RSI < 30` and `P/E < 20` criteria.

4. If candidates are found, it sorts them by RSI and selects the top 3.

5. For each of the top 3, it calls `get_ai_analysis()` to get the trading report.

6. It compiles all the reports into a single message and calls `send_telegram_message()` to send it.

7. If no stocks meet the criteria, it sends a message stating so.

  

---

  

## 4. Scheduling and Execution

  

The final part of the script, inside the `if __name__ == "__main__":` block, handles the execution.

  

- **Environment Check**: It first checks if all required environment variables are loaded. If not, it logs an error and exits.

- **Scheduling**: It uses the `schedule` library to set up the job. `schedule.every().<weekday>.at("18:30").do(main_job)` lines tell the script to run the `main_job` function only on weekdays at 18:30. **Note**: This relies on the server's local time. For 18:30 IST, the server's timezone must be set to `Asia/Kolkata`.

- **Execution Loop**: The `while True:` loop is the engine for the scheduler. It continuously checks if a scheduled job is pending and runs it if it is. `time.sleep(1)` prevents the loop from consuming excessive CPU.