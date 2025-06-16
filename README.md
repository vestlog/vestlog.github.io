# Vestlog: AI-Powered Stock Insight & Market Analysis Blog

Welcome to **Vestlog**, a fully automated financial blog built to deliver AI-driven stock analysis, global market summaries, and curated financial insights.

> 🌐 Live Blog: [https://vestlog.github.io](https://vestlog.github.io)

## 🧠 About the Project

Vestlog is an intelligent publishing system that collects and analyzes global financial data, generates investment recommendations, and publishes structured reports—all through an automated pipeline.

Powered by Python and open-source AI models, it aims to assist investors, researchers, and data-driven traders by providing:

- 🔍 **Daily Stock Market Snapshots**
- 📈 **AI-Based Stock Predictions**
- 🌎 **Top Financial News Summaries**
- 🧾 **Technical Indicator Reports (RSI, MACD, OHLCV, etc.)**
- 💡 **Investment Sentiment and Confidence Scores**

## 🔄 Automation Pipeline

The Vestlog engine consists of the following stages:

1. **Data Collection**
   - Financial APIs (e.g., Alpha Vantage, IEX Cloud)
   - Real-time news scraping from global sources
   - Google Trends data extraction

2. **AI Analysis**
   - Deep learning-based stock prediction
   - Trend forecasting by interval (1d, 1wk, 1mo)
   - Confidence scoring and signal interpretation

3. **Markdown Generation**
   - Structured `.md` and `.html` reports
   - Thematic styling for light/dark mode compatibility
   - Mobile-responsive HTML card layout

4. **Publishing**
   - Auto-generated blog posts pushed to GitHub Pages
   - Daily publishing via `GitHub Actions` or `cron` jobs

## 📌 Key Technologies

- `Python 3.10+`
- `BeautifulSoup`, `requests`, `pandas`, `re`
- `Matplotlib / Plotly` for charting (optional)
- `Jekyll` / `GitHub Pages` for static site generation
- `Selenium` or `Playwright` for platform automation (optional)

## 🚀 Getting Started

To deploy your own version of Vestlog:

1. Clone the repo and configure `config.py` with your API keys.
2. Run the daily pipeline script:
   ```bash
   python generate_report.py
