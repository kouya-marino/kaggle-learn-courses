# Exercise: Creating, Reading and Writing


**This notebook is an exercise in the [Pandas](https://www.kaggle.com/learn/pandas) course.  You can reference the tutorial at [this link](https://www.kaggle.com/residentmario/creating-reading-and-writing).**

---

# Introduction

The first step in most data analytics projects is reading the data file. In this exercise, you'll create Series and DataFrame objects, both by hand and by reading data files.

Run the code cell below to load libraries you will need (including code to check your answers).

```python
import pandas as pd
pd.set_option('display.max_rows', 5)
from learntools.core import binder; binder.bind(globals())
from learntools.pandas.creating_reading_and_writing import *
print("Setup complete.")
```

# Exercises

## 1.

In the cell below, create a DataFrame `fruits` that looks like this:

![](https://storage.googleapis.com/kaggle-media/learn/images/Ax3pp2A.png)

```python
# Your code goes here. Create a dataframe matching the above diagram and assign it to the variable fruits.
fruits = ____

# Check your answer
q1.check()
fruits
```

```python
#q1.hint()
#q1.solution()
```

## 2.

Create a dataframe `fruit_sales` that matches the diagram below:

![](https://storage.googleapis.com/kaggle-media/learn/images/CHPn7ZF.png)

```python
# Your code goes here. Create a dataframe matching the above diagram and assign it to the variable fruit_sales.
fruit_sales = ____

# Check your answer
q2.check()
fruit_sales
```

```python
#q2.hint()
#q2.solution()
```

## 3.

Create a variable `ingredients` with a Series that looks like:

```
Flour     4 cups
Milk       1 cup
Eggs     2 large
Spam       1 can
Name: Dinner, dtype: object
```

```python
ingredients = ____

# Check your answer
q3.check()
ingredients
```

```python
#q3.hint()
#q3.solution()
```

## 4.

Read the following csv dataset of wine reviews into a DataFrame called `reviews`:

![](https://storage.googleapis.com/kaggle-media/learn/images/74RCZtU.png)

The filepath to the csv file is `../input/wine-reviews/winemag-data_first150k.csv`. The first few lines look like:

```
,country,description,designation,points,price,province,region_1,region_2,variety,winery
0,US,"This tremendous 100% varietal wine[...]",Martha's Vineyard,96,235.0,California,Napa Valley,Napa,Cabernet Sauvignon,Heitz
1,Spain,"Ripe aromas of fig, blackberry and[...]",Carodorum Selección Especial Reserva,96,110.0,Northern Spain,Toro,,Tinta de Toro,Bodega Carmen Rodríguez
```

```python
reviews = ____

# Check your answer
q4.check()
reviews
```

```python
#q4.hint()
#q4.solution()
```

## 5.

Run the cell below to create and display a DataFrame called `animals`:

```python
animals = pd.DataFrame({'Cows': [12, 20], 'Goats': [22, 19]}, index=['Year 1', 'Year 2'])
animals
```

In the cell below, write code to save this DataFrame to disk as a csv file with the name `cows_and_goats.csv`.

```python
# Your code goes here

# Check your answer
q5.check()
```

```python
#q5.hint()
#q5.solution()
```

# Keep going

Move on to learn about **[indexing, selecting and assigning](https://www.kaggle.com/residentmario/indexing-selecting-assigning)**.

---




*Have questions or comments? Visit the [course discussion forum](https://www.kaggle.com/learn/pandas/discussion) to chat with other learners.*
