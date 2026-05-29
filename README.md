# Northwind ETL Pipeline

## Overview

This project creates a Data Warehouse for Northwind sales data.
The Data Warehouse is built as a star schema with one fact table and three dimension tables.

The project also uses the Excel file ProductCatalog_Extra.xlsx from the assignment.
The Excel file contains extra product information that is loaded with SSIS and then used to update DimProduct.

## Data Warehouse Design

### FactSales

FactSales stores sales transactions from Northwind.
It contains order information, date key, customer key, product key, quantity, unit price, discount and sales amount.

### DimCustomer

DimCustomer stores customer information such as customer ID, company name, city and country.

### DimProduct

DimProduct stores product information such as product ID, product name, category and unit price.
The table is also updated with extra product information from ProductCatalog_Extra.xlsx.

The extra columns are CostPrice, CountryOfOrigin and SupplierProductCode.

### DimDate

DimDate stores date information such as date, year, quarter, month, day and weekday.

## ETL Flow

1. Data from the Northwind database is loaded into the Data Warehouse.
2. ProductCatalog_Extra.xlsx is loaded with SSIS.
3. The Excel data is loaded into the staging table StagingProductCatalogExtra.
4. The staging data is checked for missing values and duplicate ProductID values.
5. Invalid rows are removed and duplicate ProductID values are grouped.
6. The cleaned data is saved in CleanProductCatalogExtra.
7. DimProduct is updated with CostPrice, CountryOfOrigin and SupplierProductCode from the cleaned Excel data.

## Data Quality

The Excel file contains some data quality problems.

Some rows have missing values.
ProductID 5 has missing CostPrice.
ProductID 17 has missing CostPrice.
ProductID 21 has missing CountryOfOrigin.
ProductID 33 has missing CountryOfOrigin.
ProductID 56 has missing CostPrice.
ProductID 64 has missing CostPrice.

There are also duplicate ProductID values.
ProductID 7 appears twice.
ProductID 29 appears twice.
ProductID 51 appears twice.

These problems are handled by removing rows with missing values and grouping the data by ProductID.

## Screenshots

The project includes screenshots showing the SSIS connection to ProductCatalog_Extra.xlsx.
It also includes screenshots showing the columns loaded from the Excel file, the SSIS flow, the data quality check and DimProduct after it has been updated with the extra product information.

## Files

ProductCatalog_Extra.xlsx
Northwind_DW_StarSchema.drawio
SSIS_ProductCatalog_Excel_Source_Connection.png
SSIS_ProductCatalog_Excel_Source_Columns.png
SSIS_ProductCatalog_To_Staging_Flow.png
ProductCatalog_Data_Quality_Check.png
DimProduct_Updated_With_ProductCatalog_Extra.png
