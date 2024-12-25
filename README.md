# Personalized Product Recommendation System with PySpark
## 1. Background
- Recommendation systems have become an essential component of e-commerce platforms, online services, and mobile applications, especially in the context of increasingly rich and diverse user data. These systems not only provide product recommendations but also utilize complex algorithms to personalize the user experience, thereby enhancing customer satisfaction and improving conversion rates. Leading companies like Amazon, Netflix, and Spotify have demonstrated the power of personalized recommendation systems in establishing deep connections with users while simultaneously driving revenue growth and customer retention.

- While traditional recommendation methods, such as Collaborative Filtering and Content-based Filtering, are still widely used, newer technologies like machine learning and big data are gradually replacing older approaches to deliver more accurate and effective results. The processing of vast amounts of data, including user behavior, product reviews, and transaction records, has become a significant challenge for companies. Consequently, the adoption of powerful data processing tools like Apache Spark and its PySpark library has emerged as an effective solution for handling and analyzing large-scale data.

- Thus, researching and developing a personalized product recommendation system using PySpark not only addresses market demands but also delivers practical value to businesses, contributing to the advancement of cutting-edge technologies in big data analytics and machine learning.

- Dataset:  
[Myntra Reviews on Women Dresses - Comprehensive](https://www.kaggle.com/datasets/surajjha101/myntra-reviews-on-women-dresses-comprehensive)

## 2. Proposed Model
<img width="800" alt="image" src="https://github.com/user-attachments/assets/59438b4f-a18a-4e72-ac2c-735b9c6a3056" />

- Pre-processing: The dataset is cleaned by understanding column meanings, removing null/NaN values, normalizing text to lowercase, eliminating special characters, punctuation, digits, and stopwords. Lemmatization is applied to standardize words, ensuring quality input data.

- Data Processing: Reviews are prepared for analysis by filtering and transforming text data into usable formats, reducing noise and improving accuracy.

- Visualization: Trends are uncovered through visualizations like average ratings by product category, Word Clouds for common keywords, and word frequency analysis to identify recurring themes such as quality and design.

- Model Building: Sentiment analysis using Vader filters positive reviews, which are aggregated by product (clothing_id). Text is transformed into numerical vectors via Word2Vec, and cosine similarity measures relationships between reviews and products.

- Output: The recommendation system suggests products based on reviews with similar sentiments, helping users discover items that match their preferences on Amazon.

## 4. Proposed Model
### 4.1. Sentiment Analysis 
Sentiment analysis is a crucial step in evaluating customer feedback. After collecting and 
preprocessing data from product reviews, the next step is to classify the sentiment of these 
reviews to better understand customer satisfaction. The team used Sentiment Analysis to 
analyze emotions, particularly through the VADER (Valence Aware Dictionary and Sentiment 
Reasoner) model. VADER is a model especially well-suited for analyzing short text segments 
like product reviews because it takes into account both the vocabulary and context to calculate 
sentiment scores.
### Implementation Process 
### 1. Initialize the VADER Model:
- We used the VADER lexicon from the NLTK library to calculate the sentiment polarity scores for the reviews. The sentiment score is computed on a scale from -1 (very negative) to 1 (very positive).
- 
![image](https://github.com/user-attachments/assets/4a6fc488-db88-45f1-abff-45af230b18d9)
### 2. Create UDF (User Defined Functions)
Two UDFs were defined:
- **get_polarity_score()**: Calculates the overall sentiment score for each review.

- **get_sentiment_label()**: Assigns a sentiment label to the reviews based on the overall sentiment score:  
  - **Positive** if the sentiment score > 0.05.  
  - **Negative** if the sentiment score < -0.05.  
  - **Neutral** if the sentiment score is between -0.05 and 0.05.
    
 ![image](https://github.com/user-attachments/assets/fc16414d-4597-4fb6-a28c-688ec05331f7)

### 3. Apply Sentiment Analysis
After registering these UDFs in PySpark, we applied them to the `review_text` column to create two new columns:
- **polarity_score**: The sentiment score for each review.
- **sentiment_label**: The corresponding sentiment label (**Positive**, **Negative**, **Neutral**).
- 
![image](https://github.com/user-attachments/assets/823e1d70-db93-4cb9-b08c-3d71c412906d)

### 4.2 Algorithm Experimentation 
In the data processing pipeline, reviews were aggregated by product ID (clothing_id) to eliminate duplicates and optimize analysis. Key attributes like department name, product class, and product title were assigned the first available value, while review texts were concatenated to summarize customer sentiments.

We calculated average metrics, including ratings, recommendation index, and sentiment score, to identify recommended products based on average recommendation scores. This streamlined approach enhanced data quality and supported efficient analysis and decision-making.

![image](https://github.com/user-attachments/assets/be163649-19ee-4bd2-b071-2e867ba14e18)

- First, to build the model, the team used the Word2Vec technique to transform both old and 
new reviews into vectors.

![image](https://github.com/user-attachments/assets/e7c9a776-ee88-4e04-9e15-f22f3f189427)
- After completing the transformation process, the next step in the workflow is to calculate 
the correlation between the new review and the old reviews to determine similarity. To 
accomplish this, the team defined a cosine similarity function, which helps evaluate the degree 
of similarity between two vectors. This function calculates a correlation value ranging from -1 
to 1, where 1 represents perfect similarity and 0 indicates no similarity.

![image](https://github.com/user-attachments/assets/2e84f0a2-bb49-4e18-8326-9ac42b56e2c5)
- After completing the calculations, the team converted the list of correlation results into a 
DataFrame, which included columns containing the words from the review, the similarity 
values, product class names, and the review content. From this, the team filtered out the top 5 
reviews with the highest similarity to the new review,, helping 
to identify the products most likely to be a good fit.

![image](https://github.com/user-attachments/assets/7dd14692-e635-45c9-abe9-9d498dbae5a3)

![image](https://github.com/user-attachments/assets/c8d786c8-aaf7-497e-a6d8-634817584b66)

### 4.3. Experimental Results and Evaluation 
### 4.3.1. Results

![image](https://github.com/user-attachments/assets/c953849a-31c7-4cb2-9b85-867fbf798955)
### 4.3.2 Model Evaluation 
The model uses the Word2Vec technique to convert reviews into vectors and calculates similarity using cosine similarity, enabling personalized product recommendations based on user reviews.
- **Accuracy:**  successfully recommends relevant products, including 'Lounge,' 'Swim,' 'Lounge,', 'Lounge,' and 'Intimates.' These products provide diverse options and are consistent with the content of the reviews. The repetition of 'Lounge' also indicates the model's ability to accurately select products that match the user’s needs and
- preferences, ensuring a comprehensive and precise recommendation
- **Consistency:** The model demonstrates consistency in providing relevant product recommendations, ensuring users receive a diverse and valuable list of suggestions. The 
presence of products from various categories, such as swimwear ('Swim'), and casual wear ('Lounge'), shows the model's ability to understand the semantic meaning of reviews and make appropriate suggestions based on them.
- **Potential for Improvement:** Enhancements could include expanding the number of recommendations and improving handling of complex reviews for greater accuracy and flexibility.
This model effectively improves the shopping experience by analyzing review semantics to suggest suitable products, with opportunities for further optimization to enhance its value.
