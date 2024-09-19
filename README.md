
# Programming Assignment 4

This programming assignment focuses on analyzing a dataset to extract information based on various filters. It involves manipulating a dataset using pandas DataFrame to perform operations like filtering, grouping, and retrieving specific records. It also involves visualize information from a data set the library of Seaborn.

## Table of Contents
1. [Introduction](#introduction)
2. [Dependencies](#dependencies)
3. [Code Breakdown](#code-breakdown)
   - [Loading the Data](#loading-the-data)
   - [Filtering Data by Track and Hometown](#filtering-data-by-track-and-hometown)
   - [Selecting Specific Columns](#selecting-specific-columns)
4. [Conclusion](#conclusion)

## Introduction
This notebook handles student records, focusing on filtering and analyzing their performance in subjects like Math, Electronics, GEAS, and Communication. The main tasks involve extracting data based on specific criteria such as "Track" and "Hometown."

## Dependencies
Before running the notebook, ensure the following Python packages are installed:

```bash
pip install pandas
```

## Code Breakdown

### Loading the Data
The data is loaded into a pandas DataFrame from an external file. The structure of the DataFrame contains information such as:
- Name
- Gender
- Track
- Hometown
- Subject Grades (Math, Electronics, GEAS, Communication)

The following code loads the data:

```python
import pandas as pd

df_board = pd.read_csv('data.csv')  # Assuming the file is named data.csv
```

### Filtering Data by Track and Hometown
To extract board takers who belong to the "Instrumentation" track, are from "Luzon," and scored more than 70 in Electronics, the following filtering operation is used:

```python
Instru = df_board.loc[
    (df_board['Track'] == 'Instrumentation') &  # Filter students in Instrumentation
    (df_board['Hometown'] == 'Luzon') &         # Who are from Luzon
    (df_board['Electronics'] > 70)              # And have scored above 70 in Electronics
][['Name', 'GEAS', 'Electronics']]  # Select specific columns to display
```

### Selecting Specific Columns
After filtering the DataFrame, we select only the "Name," "GEAS," and "Electronics" columns, which gives a concise view of the selected students' information. The resulting DataFrame is stored in `Instru`.

```python
Instru
```

This will output a table like:

| Name  | GEAS | Electronics |
|-------|------|-------------|
| S1    | 75   | 89          |
| S8    | 64   | 81          |
| S30   | 57   | 81          |



## Conclusion
The notebook showcases various techniques to analyze and visualize student datasets and data frames. It covers data filtering based on conditions, calculating averages, and using visualizations to compare data across different categories like tracks, genders, and hometowns.
