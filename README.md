# 🛒 Sales Data Pipeline & Web Dashboard

An end-to-end Data Engineering pipeline that ingests, cleans, validates, and integrates multi-source sales data, loads it into Microsoft SQL Server, and serves it through an interactive Flask web dashboard.

---

## 📌 Project Overview

This project implements a complete ETL and reporting workflow:
1. **Extraction:** Ingesting product, customer, and order datasets from online raw CSV sources and local data entities.
2. **Transformation & Validation:**
   - Eliminating duplicate records (e.g., duplicated `order_id`).
   - Validating transaction quantities to ensure positive, non-zero integers.
   - Cleansing currency symbols and casting `unit_price` into proper numeric formats.
   - Merging relational entities into a consolidated analytical dataset (`final_df`).
3. **Loading:** Loading the clean dataset into **Microsoft SQL Server** (`all_data` database) using parameterized batch execution via `pyodbc`.
4. **Presentation:** Serving live database records on an interactive web dashboard built with **Flask** and **Bootstrap**.

---

## 🏗️ Architecture
```Architecture
[ Raw CSV / Data Sources ]
│
▼
[ Pandas Data Pipeline ]  ──► (Cleaning, Deduplication & Validation)
│
▼
[ MS SQL Server (all_data) ]  ──► (Table: final_df)
│
▼
[ Flask Application (app.py) ]
│
▼
[ HTML / Bootstrap Dashboard ]
```

## 📂 Project Structure

```text
├── templates/
│   └── dashboard.html       # HTML UI template powered by Bootstrap
├── app.py                   # Flask web server querying SQL Server
├── pipeline.py              # Data cleaning, transformation & ingestion script
├── requirements.txt         # Project dependencies
└── README.md                # Project documentation
```

## ⚙️ Tech Stack & Tools
- Language: Python
- Data Manipulation: Pandas
- Database: Microsoft SQL Server, pyodbc
- Web Framework: Flask
- Frontend: HTML5

## 🚀 Setup & Execution
1. Prerequisites
Ensure you have installed:
- Python 3.9+
- Microsoft SQL Server & SQL Server Management Studio (SSMS)
- ODBC Driver 17 for SQL Server

2. Install Dependencies
```Bash
pip install pandas flask pyodbc requests
```

3. Database Schema
Ensure the target database all_data exists in SQL Server. The table schema:
```SQL
CREATE TABLE final_df (
    order_id INT,
    Full_Name VARCHAR(50),
    product_name VARCHAR(50),
    quantity INT,
    unit_price DECIMAL(10, 2),
    total_amount DECIMAL(10, 2)
);
```

4. Run the ETL Pipeline
Execute the transformation and loading script:
```Bash
python pipeline.py
```

5. Launch the Dashboard
Run the Flask server:
```Bash
python app.py
```

```Plaintext
[http://127.0.0.1:5000](http://127.0.0.1:5000)
```


  
