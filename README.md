# books-data-scraper-python
# Books to Scrape: Automated Web Scraper & SQLite Data Pipeline (Python)

## Executive Summary
This project demonstrates an end-to-end automated web scraping, data cleaning, and relational database persistence pipeline using **Python** in **Google Colab**. The script programmatically crawls multi-page catalog records from [Books to Scrape](http://books.toscrape.com), extracts book metadata, cleans raw price characters, and persists structured records into an **SQLite database** and exportable CSV format.

---

## Technical Architecture & Tools
* **Environment:** Google Colab / Jupyter Notebook
* **Programming Language:** Python 3.x
* **Libraries:** `requests`, `beautifulsoup4`, `pandas`, `sqlite3`
* **Database Engine:** SQLite 3 (`scraped_data.db`)
* **Target Website:** [Books to Scrape](http://books.toscrape.com)

---

## Pipeline & Data Extraction Workflow

1. **HTTP Request & Parsing:**
   - Used `requests` to fetch page HTML and checked response codes (`200 OK`) to confirm connectivity.
   - Used `BeautifulSoup` with `html.parser` to traverse DOM elements across catalog pages.
2. **Data Wrangling & String Normalization:**
   - Isolated `<article class="product_pod">` tags for item details.
   - Extracted exact book titles from the `title` attribute inside `<h3><a>` tags.
   - Stripped currency symbols (`Â`, `£`) and extra spaces from price strings before casting to `float`.
3. **Multi-Page Crawling:**
   - Programmatically traversed pagination routes (`/catalogue/page-1.html` through `page-3.html`).
   - Tracked originating `page_number` for each extracted record to verify pagination flow.
4. **SQLite Database Persistence:**
   - Established a connection using `sqlite3.connect("scraped_data.db")`.
   - Written data into the `scraped_books` table via Pandas `.to_sql()` and verified storage integrity using standard SQL queries (`SELECT COUNT(*)...`).

---

## Dataset Summary & Metrics

| Metric | Value |
| :--- | :--- |
| **Total Pages Scraped** | 3 Pages |
| **Total Book Records Extracted** | 60 Books (20 per page) |
| **Average Book Price** | **£35.00** |
| **Minimum Book Price** | **£12.84** |
| **Maximum Book Price** | **£57.31** |
| **Primary Output Files** | `scraped_books_data.csv`, `scraped_data.db` |

---

## Sample Data Extracted

| Title | Price (£) | Page Number |
| :--- | :--- | :--- |
| A Light in the Attic | £51.77 | Page 1 |
| Tipping the Velvet | £53.74 | Page 1 |
| Soumission | £50.10 | Page 1 |
| Sharp Objects | £47.82 | Page 1 |
| Sapiens: A Brief History of Humankind | £54.23 | Page 1 |

---

## Repository Structure
```text
├── web_scrapping_portfolio_project_3.ipynb  # Google Colab Jupyter Notebook
├── scraped_books_data.csv                   # Exported CSV dataset (60 records)
├── scraped_data.db                          # SQLite Database File
└── README.md                                # Documentation
