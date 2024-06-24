# ETL Project: Extract, Transform, Load GDP Data

## Overview

This project is an ETL (Extract, Transform, Load) process that scrapes GDP data of countries from a specific Wikipedia page, transforms the data, and then loads it into both a CSV file and an SQLite database. The project logs the progress of each step to a log file.

## Table of Contents

- [Requirements](#requirements)
- [Setup](#setup)
- [Usage](#usage)
- [Code Description](#code-description)
- [Logging](#logging)

## Requirements

- Python 3
- Required Python libraries:
  - `requests`
  - `beautifulsoup4`
  - `pandas`
  - `numpy`
  - `pyperclip`
  - `sqlite3` 

## Setup

1. **Clone the repository**:

    ```bash
    git clone https://github.com/osamaAlmehmadi1/ETL.git
    
    ```

1. **Install the required libraries**:

    ```bash
    pip install requests beautifulsoup4 pandas numpy pyperclip
    ```

## Usage

1. **Run the script**:

    ```bash
    python etl_script.py
    ```

2. **Check the output**:
    - The CSV file will be saved as `Countries_by_GDP.csv` in the current directory.
    - The SQLite database will be created as `World_Economies.db` in the current directory.
    - Logs will be recorded in `etl_project_log.txt`.

## Code Description

### Libraries Used

- `requests`: For making HTTP requests to fetch web pages.
- `BeautifulSoup`: For parsing HTML content and extracting data from it.
- `pandas`: For data manipulation and analysis.
- `numpy`: For numerical operations on the data.
- `datetime`: For handling date and time operations.
- `pyperclip`: For copying data to the clipboard.
- `sqlite3`: For interacting with the SQLite database.

### Constants

- `url`: The URL of the Wikipedia page (archived) to scrape data from.
- `table_attributs`: Column names for the DataFrame to store extracted data.
- `db_name`: The name of the SQLite database file.
- `table_name`: The name of the table in the SQLite database.
- `csv_path`: The path to save the CSV file.

### Functions

1. **extract(url, table_attributs)**:
   - Fetches the HTML content of the given URL.
   - Uses BeautifulSoup to parse the HTML content and find the relevant table.
   - Extracts the country name and GDP values from the table.
   - Stores the extracted data in a pandas DataFrame and returns it.

2. **transform(df)**:
   - Converts GDP values from strings to floats, removing commas.
   - Converts GDP values from millions to billions and rounds them to two decimal places.
   - Renames the GDP column to reflect the new unit (billions).
   - Copies the transformed DataFrame to the clipboard.
   - Returns the transformed DataFrame.

3. **load_to_csv(df, csv_path)**:
   - Saves the DataFrame to a CSV file at the specified path.

4. **load_to_db(df, sql_connection, table_name)**:
   - Loads the DataFrame into an SQLite database table.
   - Replaces the table if it already exists.

5. **run_query(query_statement, sql_connection)**:
   - Executes a SQL query on the SQLite database.
   - Prints the query and its output.

6. **log_progress(message)**:
   - Logs a message with a timestamp to a log file.

### ETL Process

1. **Extract Data**:
   - Calls the `extract` function to scrape data from the Wikipedia page and store it in a DataFrame.
   - Transforms and prints the DataFrame.

2. **Database Interaction**:
   - Connects to the SQLite database.
   - Defines and runs a SQL query to fetch countries with GDP over 100 billion USD, printing the results.
   - Logs the completion of the preliminary steps.

3. **Transform and Load Data**:
   - Extracts data again and logs the completion of the extraction step.
   - Transforms the data using the `transform` function and logs the completion of the transformation step.
   - Saves the transformed data to a CSV file and logs this action.
   - Connects to the SQLite database again and logs this step.
   - Loads the transformed data into the SQLite database table and logs this action.
   - Runs the SQL query again and logs the completion of the process.
   - Closes the database connection.

## Logging

The script logs the progress of each step in the ETL process to a file named `etl_project_log.txt` in the current directory. Each log entry includes a timestamp and a descriptive message.

### Example Log Entry:

```
2024-Jun-24-14:35:27 : Preliminaries complete. Initiating ETL process
2024-Jun-24-14:35:30 : Data extraction complete. Initiating Transformation process
2024-Jun-24-14:35:33 : Data transformation complete. Initiating loading process
2024-Jun-24-14:35:35 : Data saved to CSV file
2024-Jun-24-14:35:37 : SQL Connection initiated.
2024-Jun-24-14:35:40 : Data loaded to Database as table. Running the query
2024-Jun-24-14:35:42 : Process Complete.
```


