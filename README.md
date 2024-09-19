
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

This will output a table such as this:

| Name  | GEAS | Electronics |
|-------|------|-------------|
| S1    | 75   | 89          |
| S8    | 64   | 81          |
| S30   | 57   | 81          |

### Calculating Average Scores
A new column, Average, is added to the DataFrame, which calculates the average of students' grades in Math, GEAS, and Electronics. The mean function is used across these columns. It will later be used to create the data frame 'Mindy.'

``` python
df_board['Average'] = df_board[['Math', 'GEAS', 'Electronics']].mean(axis=1)  # Calculate average across subjects
df_board
```

### Filtering Female Students from Mindanao with Average >= 55
This section filters female students from Mindanao with an average score of 55 or more. The filtered results include their name, track, electronics grade, and average score.

```python
Mindy = df_board[
    (df_board['Hometown'] == 'Mindanao') &  # Hometown is Mindanao
    (df_board['Gender'] == 'Female') &      # Gender is Female
    (df_board['Average'] >= 55)             # Average score is 55 or more
][['Name', 'Track', 'Electronics', 'Average']]  # Select specific columns

Mindy
```

The data frame 'Mindy' will output a table as such:

|     | Name | Track           | Electronics | Average  |
|-----|------|-----------------|-------------|----------|
| 1   | S2   | Communication   | 75          | 72.33333 |
| 2   | S3   | Instrumentation | 74          | 78.00000 |
| 16  | S17  | Microelectronics| 79          | 79.00000 |
| 19  | S20  | Communication   | 60          | 60.33333 |


## Conclusion
The notebook showcases various techniques to analyze and visualize student datasets and data frames. It covers data filtering based on conditions, calculating averages, and using visualizations to compare data across different categories like tracks, genders, and hometowns.
