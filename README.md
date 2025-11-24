# task-Moving-object-using-SMA-api-
This project provides a simple and fully working Python script for downloading 1-minute intraday data using yfinance, filtering data between specific entry/exit times, and calculating intraday High &amp; Low for each selected date.

Features

Downloads 1-minute intraday OHLCV data using yfinance
Filters data between entry time (e.g., 09:30) and exit time (15:00)
Calculates:
📌 Intraday High
📌 Intraday Low
📌 High–Low Range
Works for any stock, any date range, and any time window
clean and easy-to-modify code

How It Works (Steps + Explanation)

1️⃣ User Inputs
You provide:
Stock symbol (e.g., SBIN.NS)
Start & end date
Entry & exit time

2️⃣ Download Intraday Data
The script uses:
df = yf.download(stock, start=start_date, end=end_date, interval="1m")
This downloads:
Open
High
Low
Close
Volume
for each 1-minute candle.

3️⃣ Filter Time Window
The script keeps only rows between your chosen times:
df_between = df.between_time(entry_time, exit_time)

4️⃣ Group Data Day-Wise
Each day’s intraday prices are separated:
for date, group in df_between.groupby(df_between.index.date):

5️⃣ Calculate High–Low
For every day:
High → group["High"].max()
Low → group["Low"].min()
Range → High – Low

6️⃣ Print Result in Clean Table
You get a simple summary:
Date	High	Low	Range

STEPS TO RUN THIS PROGRAM
------------------------------------------

Follow these steps exactly.

🟩 STEP 1 — Install required libraries
Open CMD or VS Code Terminal:
pip install flask pandas

🟩 STEP 2 — Create a file
Name the file:
app.py
Paste your entire code into this file.

🟩 STEP 3 — Run the Flask API
In the terminal, run:
python app.py
You will see:
 * Running on http://127.0.0.1:5001
This means API is running successfully.

🟩 STEP 4 — Test API in Postman
Open Postman
Select POST
Paste URL:
http://127.0.0.1:5001/sma
Go to Body → raw → JSON
Enter input:
{
  "close": [100, 102, 98, 105, 110],
  "window": 3
}
Click Send

🟩 STEP 5 — You will get output like
[
  {"Date": "2006-01-01", "close": 100, "sma_3": null},
  {"Date": "2006-01-02", "close": 102, "sma_3": null},
  {"Date": "2006-01-03", "close": 98,  "sma_3": 100.0},
  {"Date": "2006-01-04", "close": 105, "sma_3": 101.66},
  {"Date": "2006-01-05", "close": 110, "sma_3": 104.33}
]
