# Books to Scrape Scraper

This project scrapes book data from [Books to Scrape](https://books.toscrape.com) and stores it in a MySQL database. It captures details like title, price, rating, stock, genre, and number available. The project also handles duplicate entries and provides guidance for cleaning incomplete data.

---

## Features

- Scrape all pages from Books to Scrape automatically.
- Capture book details:
  - Title
  - Cost (£)
  - Rating (1-5)
  - Stock availability
  - Genre
  - Number available
- Store data in MySQL with a UNIQUE constraint on the book title.
- Handle duplicates gracefully using `ON DUPLICATE KEY UPDATE`.
- Remove rows with missing genre or number available.

---

## Requirements

- Python 3.12.1
- Libraries:
  - `requests`
  - `beautifulsoup4`
  - `mysql-connector-python`
  - `tqdm` (optional, for progress display)
- MySQL database

---

## Database Setup

Create the database and table:

```sql
CREATE DATABASE bookstoscrape;

USE bookstoscrape;

CREATE TABLE bookdata (
    id INT AUTO_INCREMENT PRIMARY KEY,
    Title VARCHAR(255) UNIQUE,
    Cost FLOAT,
    Rating FLOAT,
    Stock_Availability VARCHAR(50),
    Genre VARCHAR(100),
    Number_Available INT
);

### Adding Missing Columns

The  `bookdata` table didn't have the additional collumns to be added already for `Genre` or `Number_Available` so I add them using the `ALTER TABLE` statement:

```sql
ALTER TABLE bookdata
ADD COLUMN Genre VARCHAR(100),
ADD COLUMN Number_Available INT;

### Cleaning Up Incomplete Data

The `bookdata` table has rows where the `Genre` or `Number_Available` fields are empty or missing.  
To remove these incomplete rows, I use the following SQL command:

```sql
DELETE FROM bookdata
WHERE genre IS NULL OR genre = ''
   OR number_available IS NULL;


For further detail please view the WebScrape https://github.com/Drook93/Webscrape-Books/blob/master/WebScrape%20Python%20Code.ipynb for a break down of the steps to set up the Web Scraping, cleaning and transforming the data. It will also explain how to save to a MYSQL database.
Any other additonal details are included in the PowerPoint presentation: https://github.com/Drook93/Webscrape-Books/blob/master/Website%20Scraping%20Project.pdf.
