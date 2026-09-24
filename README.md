# Excel to SQL Server ETL Pipeline

A Python ETL script that loads data from a multi-sheet Excel workbook into staging tables in a SQL Server database, with automatic row-count validation.

## Overview

This project reads six related sheets from an Excel workbook (`TechCorp_PowerBI_Dataset.xlsx`) — Employees, Projects, Project Assignments, Tasks, Performance Reviews, and Milestones — and loads each one into a corresponding staging table (`stg` schema) in a SQL Server database. After loading, it validates that the row count in each SQL table matches the row count in the source Excel sheet.

The staging tables intentionally store all values as strings/NULL. Type conversion and cleanup are meant to happen in a later step when moving data from staging into final (`dbo`) tables.

## Features

- **Multi-sheet ETL**: Maps each Excel sheet to its own staging table
- **NULL-safe loading**: Preserves missing values as SQL `NULL` instead of blank strings or `NaN`
- **Idempotent loads**: Clears existing staging data before each load (`DELETE` then `INSERT`) so the script can be re-run safely
- **Automatic validation**: Compares Excel row counts against SQL row counts and reports PASS/FAIL for each table
- **Chunked inserts**: Loads data in batches of 1,000 rows for efficiency

```

## Prerequisites

- SQL Server instance (local or remote) with:
  - A database named `TechCorp_ProjectManagement_DB` (or update `DATABASE` in the config)
  - A `stg` schema with tables matching the sheet names: `Employees`, `Projects`, `ProjectAssignments`, `Tasks`, `PerformanceReviews`, `Milestones`
- ODBC Driver 18 for SQL Server installed
- Windows Authentication access to the SQL Server instance (or adjust the connection string for SQL auth)



