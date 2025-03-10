List Columns Used in Views

SELECT v.TABLE_NAME AS ViewName, c.COLUMN_NAME 
FROM INFORMATION_SCHEMA.VIEW_COLUMN_USAGE c
JOIN INFORMATION_SCHEMA.VIEWS v ON c.VIEW_NAME = v.TABLE_NAME
ORDER BY v.TABLE_NAME, c.COLUMN_NAME;

Find Views and Their Source Tables with Columns

SELECT 
    v.name AS ViewName, 
    t.name AS TableName, 
    c.name AS ColumnName
FROM sys.views v
JOIN sys.sql_expression_dependencies d ON d.referencing_id = v.object_id
JOIN sys.tables t ON d.referenced_id = t.object_id
JOIN sys.columns c ON c.object_id = t.object_id
ORDER BY v.name, t.name, c.name;

Get View Definition (Check SQL Code of Views)

SELECT name AS ViewName, definition 
FROM sys.sql_modules 
JOIN sys.objects ON sys.sql_modules.object_id = sys.objects.object_id 
WHERE type = 'V';


This query retrieves columns from tables that are used in views:

SELECT 
    vcu.VIEW_NAME AS ViewName,
    vcu.TABLE_NAME AS SourceTable,
    vcu.COLUMN_NAME AS SourceColumn
FROM INFORMATION_SCHEMA.VIEW_COLUMN_USAGE vcu
ORDER BY vcu.VIEW_NAME, vcu.TABLE_NAME, vcu.COLUMN_NAME;
