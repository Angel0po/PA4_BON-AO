
# Programming Assignment 4

This programming assignment focuses on analyzing a dataset to extract information based on various filters. It involves manipulating a dataset using pandas DataFrame to perform operations like filtering, grouping, and retrieving specific records. Additionally, the assignment includes visualizing the data using the Seaborn library.

## Table of Contents
1. [Introduction](#introduction)
2. [Dependencies](#dependencies)
3. [Code Breakdown](#code-breakdown)
   - [Loading the Data](#loading-the-data)
   - [Filtering Data by Track and Hometown](#filtering-data-by-track-and-hometown)
   - [Selecting Specific Columns](#selecting-specific-columns)
   - [Calculating Averages](#calculating-averages)
   - [Mindy Data Frame](#filtering-female-students-from-mindanao-with-average--55)
   - [Visualizing Data](#visualizing-data)
     - [Average Score by Track](#average-score-by-track)
     - [Average Score by Gender](#average-score-by-gender)
     - [Average Score by Hometown](#average-score-by-hometown)
4. [Conclusion](#conclusion)
5. [Author](#author)
6. [Program and Python Version](#program-and-python-version)

## Introduction
This notebook handles student records, focusing on filtering and analyzing their performance in subjects like Math, Electronics, GEAS, and Communication. The main tasks involve extracting data based on specific criteria such as "Track" and "Hometown."

## Dependencies
Before running the notebook, ensure the following Python packages are installed:

```bash
pip install pandas seaborn matplotlib
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
    (df_board['Electronics'] > 70)              # Scored more than 70 in Electronics
]
Instru
```

### Selecting Specific Columns
To focus on specific columns in the DataFrame:

```python
Instru[['Name', 'Track', 'Electronics']]
```

### Calculating Averages
To calculate the average score of Math, GEAS, and Electronics:

```python
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

### Visualizing Data

#### Average Score by Track
A boxplot is created using Seaborn to visualize the average score distribution by the chosen track of the bar takers.

```python
import seaborn as sb
sb.boxplot(x='Track', y='Average', data=df_board, palette='Set3').set_title('Average Score by Track')
sb.despine()
```

#### Average Score by Gender
A violin plot is generated to compare the distribution of average scores between the genders of the bar takers.

```python
sb.violinplot(x='Gender', y='Average', data=df_board, palette='Set2').set_title('Average Score by Gender')
sb.despine()
```

#### Average Score by Hometown
A bar plot is created to show the average score across different hometowns of the bar takers.

```python
sb.barplot(x='Hometown', y='Average', data=df_board, palette='Set1').set_title('Average Score by Hometown')
sb.despine()
```

## Conclusion
This assignment demonstrates the use of pandas for data manipulation and Seaborn for data visualization. The code successfully filters and presents the required information from the dataset, focusing on specific groups and their performance.

## Author
This assignment was completed by [Angelo Bon-ao].

## Program and Python Version
- Program: Jupyter Notebook
- Python Version: 3.8+
