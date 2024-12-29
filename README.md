# Personalized Product Recommendation System with PySpark

## 1. Background
Recommendation systems are a critical part of e-commerce platforms, online services, and mobile applications. They personalize user experiences, enhancing satisfaction and improving conversion rates. Leading companies like Amazon, Netflix, and Spotify demonstrate how personalized recommendations drive revenue growth and customer retention.

While traditional recommendation methods like Collaborative Filtering and Content-based Filtering are effective, machine learning and big data approaches are replacing them for better accuracy and efficiency. The challenge of processing vast amounts of user data, including behaviors, reviews, and transactions, has led to the adoption of powerful tools like Apache Spark and its PySpark library.

### Dataset
We use the [Myntra Reviews on Women Dresses - Comprehensive](https://www.kaggle.com/datasets/surajjha101/myntra-reviews-on-women-dresses-comprehensive) dataset for our study.

---

## 2. Proposed Model

![Model Flow](https://github.com/user-attachments/assets/0a74c972-8166-48bb-92b4-c9f5a0e1f85e)

### Steps:
1. **Pre-processing**
   - Clean the dataset: remove null values, normalize text, and apply lemmatization.

2. **Data Processing**
   - Filter and transform text into usable formats for analysis.

3. **Visualization**
   - Use Word Clouds, average ratings, and word frequency analysis to uncover trends.

4. **Model Building**
   - Perform sentiment analysis using VADER for positive reviews.
   - Convert text to vectors using Word2Vec.
   - Measure relationships using cosine similarity.

5. **Output**
   - Provide personalized product recommendations based on reviews with similar sentiments.

---

## 3. Experimentation and Model Evaluation

### 3.1 Sentiment Analysis
Sentiment analysis helps classify customer feedback as Positive, Negative, or Neutral using the VADER model. 

#### Implementation:
1. **Initialize VADER Model**
   - Use the NLTK library for sentiment polarity scores.
   
![image](https://github.com/user-attachments/assets/4a6fc488-db88-45f1-abff-45af230b18d9)

2. **Define UDFs**
   - `get_polarity_score()`: Computes sentiment scores.
   - `get_sentiment_label()`: Assigns sentiment labels based on scores.

![image](https://github.com/user-attachments/assets/da4aa760-448a-41a4-b965-0f75b77dd968)

3. **Apply Sentiment Analysis**
   - Add `polarity_score` and `sentiment_label` columns to the dataset.

![image](https://github.com/user-attachments/assets/823e1d70-db93-4cb9-b08c-3d71c412906d)

### 3.2 Algorithm Experimentation
- Aggregate reviews by `clothing_id` to eliminate duplicates.
- Calculate metrics like average ratings and sentiment scores.
- Convert reviews to vectors using Word2Vec.
- Measure similarity using cosine similarity to recommend the top 5 relevant products.

![Workflow](https://github.com/user-attachments/assets/7dd14692-e635-45c9-abe9-9d498dbae5a3)

---

## 4. Experimental Results and Evaluation

### Results:
The model successfully recommends relevant products based on user reviews, showing high accuracy and consistency. 

![image](https://github.com/user-attachments/assets/c953849a-31c7-4cb2-9b85-867fbf798955)

### Evaluation:
1. **Accuracy**
   - The model effectively recommends products that align with user reviews.
2. **Consistency**
   - Provides diverse and relevant recommendations across categories.
3. **Improvements**
   - Expand recommendations and refine handling of complex reviews.

---

## Summary
This personalized recommendation system, built with PySpark, demonstrates how big data analytics and machine learning can enhance user experiences. While the model performs well, further optimization can make it even more robust and versatile.
