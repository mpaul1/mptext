If you want to list only the fields (columns) that are actively used in queries from tables in a database, you may need to check:

Database Schema – List all columns in tables.
Query Logs – Identify queries that reference those columns.
Indexes or Foreign Keys – Check referenced columns.
Here’s how to get the relevant information:

1. Get Columns from Tables in a Database
Use this query in MySQL:

sql
Copy
Edit
SELECT TABLE_NAME, COLUMN_NAME 
FROM INFORMATION_SCHEMA.COLUMNS 
WHERE TABLE_SCHEMA = 'your_database_name';
For SQL Server:

sql
Copy
Edit
SELECT TABLE_NAME, COLUMN_NAME 
FROM INFORMATION_SCHEMA.COLUMNS 
WHERE TABLE_CATALOG = 'your_database_name';
For PostgreSQL:

sql
Copy
Edit
SELECT table_name, column_name
FROM information_schema.columns
WHERE table_schema = 'public';
2. Find Columns Used in Queries
MySQL Query Logs (if enabled):

sql
Copy
Edit
SHOW GLOBAL VARIABLES LIKE 'general_log%';
If general logging is enabled, check general_log table or file.

SQL Server Query Store:

sql
Copy
Edit
SELECT query_text 
FROM sys.dm_exec_requests
CROSS APPLY sys.dm_exec_sql_text(sql_handle);
PostgreSQL Query Log (if logging enabled):

sql
Copy
Edit
SELECT query FROM pg_stat_statements;
Would you like a script to automate identifying the actively used columns?
