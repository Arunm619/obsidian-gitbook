Pandas is a powerful data manipulation library in Python. It provides data structures and functions needed to manipulate structured data. It's built on top of two core Python libraries - **Matplotlib** for data visualization and **NumPy** for mathematical operations.

Pandas provides two main data structures: `DataFrame` and `Series`.

- A `Series` is a one-dimensional array-like object that can hold any data type.
- A `DataFrame` is a two-dimensional table of data with rows and columns.

These data structures allow you to handle and manipulate data in a manner similar to relational databases and excel spreadsheets.

Here's a simple example of how to use pandas:

```python
import pandas as pd

# Creating a simple dataframe
data = {
    'Name': ['John', 'Anna', 'Peter'],
    'Age': [28, 24, 22],
}
df = pd.DataFrame(data)

print(df)
```

In this example, we first import the pandas library using the alias `pd`. Then we create a dictionary where the keys will be used as column names and the values as column data. The `pd.DataFrame()` function is used to convert this dictionary into a DataFrame. Finally, we print the DataFrame.