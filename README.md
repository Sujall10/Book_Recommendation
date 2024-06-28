# Book Recommendation System Based on Book Names

This repository contains Python code that demonstrates how to recommend books based on their titles and ratings using pandas and basic data manipulation techniques.

## Overview

The book recommendation system uses a dataset containing ratings for books and recommends books based on their popularity or average ratings. It leverages pandas for data loading, filtering, and aggregation to calculate recommendations.

## Requirements

- Python 3.x
- pandas
- Jupyter Notebook (optional for interactive exploration)

## Steps to Implement

### Step 1: Load and Prepare Data

1. **Load Data**: Replace `'ratings.csv'` and `'books.csv'` with your actual dataset paths containing ratings and book information.

    ```python
    import pandas as pd

    # Example DataFrames (replace with your actual data loading)
    ratings = pd.read_csv('ratings.csv')  # Replace with your ratings dataset path
    books = pd.read_csv('books.csv')      # Replace with your books dataset path

    # Merge ratings and books on 'ISBN' or 'Book-Title'
    ratings_with_name = ratings.merge(books, on='ISBN')
    ```

### Step 2: Filter by Book Name

2. **Filter by Book Title**: Define a list of book titles (`books_to_recommend`) that you want to recommend.

    ```python
    # Example book titles to recommend
    books_to_recommend = ['Harry Potter and the Philosopher\'s Stone', 'The Catcher in the Rye', 'To Kill a Mockingbird']

    # Filter ratings for the books to recommend
    filtered_ratings = ratings_with_name[ratings_with_name['Book-Title'].isin(books_to_recommend)]
    ```

### Step 3: Calculate Recommendations

3. **Calculate Recommendations**: Calculate recommendations based on aggregated ratings for each book.

    ```python
    # Calculate average rating for each book
    book_ratings_avg = filtered_ratings.groupby('Book-Title')['Book-Rating'].mean().reset_index()

    # Sort books by average rating in descending order
    recommended_books = book_ratings_avg.sort_values(by='Book-Rating', ascending=False)

    # Print recommended books
    print("Recommended books:")
    for index, row in recommended_books.iterrows():
        print(f"{row['Book-Title']}: Average Rating {row['Book-Rating']:.2f}")
    ```

### Summary

- **Step 1**: Load and merge your ratings and books datasets.
- **Step 2**: Define a list of book titles (`books_to_recommend`) that you want to recommend.
- **Step 3**: Filter the merged dataset (`ratings_with_name`) to include only ratings for the specified books. Then, calculate the average rating for each book and sort them by rating to recommend the highest-rated books.

Adjust the dataset paths (`'ratings.csv'` and `'books.csv'`), book titles (`books_to_recommend`), and any other parameters according to your specific dataset and recommendation criteria. This approach provides a basic framework to recommend books based on their average ratings using Python and pandas.
