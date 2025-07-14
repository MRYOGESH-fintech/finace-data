### Final Project: Analyzing Stock Performance and Building a Dashboard

#### **Question 1: Use yfinance to Extract Tesla Stock Data**

```python
import yfinance as yf
import pandas as pd

# Create Ticker object
tesla = yf.Ticker("TSLA")

# Extract historical stock data
tesla_data = tesla.history(period="max")

# Reset index
tesla_data.reset_index(inplace=True)

# Display first five rows
tesla_data.head()
```

---

#### **Question 2: Use Web Scraping to Extract Tesla Revenue Data**

```python
import requests
from bs4 import BeautifulSoup

# URL of the financials page
url = "https://www.macrotrends.net/stocks/charts/TSLA/tesla/revenue"

# Send GET request
html_data = requests.get(url).text

# Parse HTML
soup = BeautifulSoup(html_data, "html.parser")

# Find the correct table
tables = soup.find_all("table")
for table in tables:
    if "Tesla Quarterly Revenue" in str(table):
        revenue_table = table
        break

# Extract revenue data
tesla_revenue = pd.read_html(str(revenue_table))[0]

# Clean column names and drop NA
tesla_revenue.columns = ["Date", "Revenue"]
tesla_revenue.dropna(inplace=True)

# Display last five rows
tesla_revenue.tail()
```

---

#### **Question 3: Use yfinance to Extract GME (GameStop) Stock Data**

```python
# Create Ticker object for GME
gme = yf.Ticker("GME")

# Extract historical stock data
gme_data = gme.history(period="max")

# Reset index
gme_data.reset_index(inplace=True)

# Display first five rows
gme_data.head()
```

---

#### **Question 4: Use Web Scraping to Extract GME Revenue Data**

```python
# URL for GameStop revenue
url = "https://www.macrotrends.net/stocks/charts/GME/gamestop/revenue"

# Fetch and parse the HTML
html_data = requests.get(url).text
soup = BeautifulSoup(html_data, "html.parser")

# Find the correct revenue table
tables = soup.find_all("table")
for table in tables:
    if "GameStop Quarterly Revenue" in str(table):
        revenue_table = table
        break

# Convert to DataFrame
gme_revenue = pd.read_html(str(revenue_table))[0]
gme_revenue.columns = ["Date", "Revenue"]
gme_revenue.dropna(inplace=True)

# Display last five rows
gme_revenue.tail()
```

---

#### **Question 6: Plot GameStop Stock Graph**

```python
import matplotlib.pyplot as plt

def make_graph(stock_data, revenue_data, stock, title):
    fig, ax1 = plt.subplots(figsize=(14, 6))

    # Plot stock price
    ax1.plot(stock_data.Date, stock_data.Close, color="tab:blue", label=f"{stock} Stock Price")
    ax1.set_xlabel("Date")
    ax1.set_ylabel("Stock Price", color="tab:blue")
    ax1.tick_params(axis='y', labelcolor="tab:blue")
    ax1.set_title(title)
    ax1.legend(loc="upper left")

    plt.show()

# Use the function
make_graph(gme_data, gme_revenue, "GME", "GameStop Stock Price Over Time")
```

---

#### 📸 **Screenshots to Submit:**

* `tesla_data.head()` output
* `tesla_revenue.tail()` output
* `gme_data.head()` output
* `gme_revenue.tail()` output
* GameStop stock plot output using `make_graph`

