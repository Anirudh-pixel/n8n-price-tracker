# 📈 Multi-Product Price Tracker Automation (n8n)

An automated, self-hosted multi-product price tracking system built
using **n8n**.\
This workflow monitors multiple e-commerce product pages at scheduled
intervals and sends Telegram alerts when prices drop below configured
thresholds.

------------------------------------------------------------------------

## 🚀 Features

-   ⏰ Scheduled price monitoring (Cron-based)
-   📄 Dynamic multi-product configuration via Google Sheets
-   🌐 Automated HTTP scraping of product pages
-   🧩 Per-product CSS selector support
-   🔎 Real-time price extraction & normalization
-   ⚖️ Conditional price comparison logic
-   📲 Telegram notifications on price drop
-   🔁 Scalable looping over multiple products
-   🔄 Automatic retry & fault tolerance

------------------------------------------------------------------------

## 🏗 Workflow Architecture

Schedule Trigger\
↓\
Google Sheets (Fetch product list)\
↓\
Loop Over Items\
↓\
HTTP Request (Fetch product page)\
↓\
HTML Extract (Dynamic CSS selector)\
↓\
Clean & Normalize Price\
↓\
Compare with Target Price\
↓\
Telegram Alert (if price drops)\
↓\
Loop continues

------------------------------------------------------------------------

## 📊 Google Sheets Configuration

Your Google Sheet must contain the following columns:

  productName   productUrl                      cssSelector   targetPrice
  ------------- ------------------------------- ------------- -------------
  Product A     https://example.com/product-a   span.price    499

  Product B     https://example.com/product-b   div.price     999

### Column Descriptions

-   **productName** -- Name of product (used in alert message)
-   **productUrl** -- URL to scrape
-   **cssSelector** -- CSS selector for price element
-   **targetPrice** -- Alert threshold

------------------------------------------------------------------------

## ⚙️ Required Credentials

### 1️⃣ Google Sheets Credentials

-   Google Cloud Project
-   Google Sheets API enabled
-   OAuth2 credentials (Client ID + Client Secret)

### 2️⃣ Telegram Bot Credentials

-   Telegram Bot Token
-   Telegram Chat ID

### 3️⃣ n8n Instance

-   Self-hosted n8n (Docker / local / server)
-   Workflow activated
-   Proper timezone configured

------------------------------------------------------------------------

## 🛠 Installation & Setup

### Step 1: Import Workflow

1.  Open n8n
2.  Click **Import Workflow**
3.  Paste the JSON file
4.  Replace:
    -   YOUR_GOOGLE_SHEET_ID
    -   YOUR_TELEGRAM_CHAT_ID

### Step 2: Configure Credentials

Attach: - Google Sheets credential to `Get row(s) in sheet` - Telegram
credential to `Notify User`

### Step 3: Activate Workflow

-   Click **Publish**
-   Ensure workflow is Active
-   Cron runs every 6 hours (configurable)

------------------------------------------------------------------------

## 💰 Price Cleaning Logic

``` js
Number($json["rawPrice"].replace(/[^0-9.]/g, ""))
```

------------------------------------------------------------------------

## 📬 Sample Alert Message

🚨 Price Drop Alert!\
The Product is available.\
Current price updated!

Link to product included.

------------------------------------------------------------------------

## 📈 Future Improvements

-   Prevent duplicate alerts
-   Store price history
-   Add database integration
-   Add email/Slack notifications
-   Handle JavaScript-rendered pages

------------------------------------------------------------------------

## 🧩 Technologies Used

-   n8n
-   Google Sheets API
-   Telegram Bot API
-   Cron Scheduling
-   HTTP Requests
-   HTML Parsing
-   Conditional Workflow Logic

------------------------------------------------------------------------

## 🏆 Use Cases

-   Deal monitoring
-   Competitive price tracking
-   Market research
-   Automated discount alerts
