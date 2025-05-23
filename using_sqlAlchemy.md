# Connecting PostgreSQL with SQLAlchemy in Python

## Introduction
This guide explains how to **connect a PostgreSQL database** using Python and SQLAlchemy's `create_engine()`. SQLAlchemy simplifies database connections and interactions without requiring manual connection handling.

## Prerequisites
Ensure you have:
- **Python 3.x** installed
- **PMySQL** running locally or remotely
- Necessary Python libraries installed:
  ```bash
  pip install sqlalchemy 
## Setting Up the Connection
### 1. Import the Required Libraries
   ```Python
  import mysql.connector
  from sqlalchemy import create_engine
  ```
This imports create_engine, which allows us to establish a connection.
### 2. Define Connection URL
The PostgreSQL connection URL follows this format:
  ```Python
  DATABASE_URL = "mysql+mysqlconnector://{DB_USER}:{DB_PASSWORD}@{DB_HOST}:{DB_PORT}/{DB_NAME}"
  ```
Given that all variables will be inside the .env file and it will get loaded using dotenv.load_dotenv()
```Python
from dotenv import load_dotenv
import os

# Load environment variables
load_dotenv()

DB_USER = os.getenv("DB_USER")
DB_PASSWORD = os.getenv("DB_PASSWORD")
DB_HOST = os.getenv("DB_HOST", "localhost")
DB_PORT = os.getenv("DB_PORT", "3306")
DB_NAME = os.getenv("DB_NAME")
```
### 3. Create SQLAlchemy Engine
```Python
engine = create_engine(DATABASE_URL)
```
This establishes a connection with the MySQL database.
### 4. Test the Connection
```Python
connection = engine.connect()
print("✅ Successfully connected to MySQL!")
connection.close()
```
## Working with Pandas and SQLAlchemy
SQLAlchemy works seamlessly with Pandas for reading/writing data.
### Insert Pandas DataFrame into MySQL
```Python
import pandas as pd

# Sample DataFrame
df = pd.DataFrame({
    "id": [1, 2, 3],
    "name": ["Alice", "Bob", "Charlie"],
    "age": [25, 30, 28]
})

# Load DataFrame into MySQL table
df.to_sql("employees", con=engine, if_exists="replace", index=False)
print("✅ Data successfully inserted into MySQL!")
```
### Read Data from PostgreSQL
```
query = "SELECT * FROM employees"
df_new = pd.read_sql(query, con=engine)
print(df_new)
```
### Conclusion
Using SQLAlchemy, you can easily manage MySQL connections, execute queries, and interact with Pandas. This approach helps in efficient database operations without manual connection handling.

