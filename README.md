# Personalized Product Recommendation System with PySpark
## 1. Background
- Recommendation systems have become an essential component of e-commerce platforms, online services, and mobile applications, especially in the context of increasingly rich and diverse user data. These systems not only provide product recommendations but also utilize complex algorithms to personalize the user experience, thereby enhancing customer satisfaction and improving conversion rates. Leading companies like Amazon, Netflix, and Spotify have demonstrated the power of personalized recommendation systems in establishing deep connections with users while simultaneously driving revenue growth and customer retention.

- While traditional recommendation methods, such as Collaborative Filtering and Content-based Filtering, are still widely used, newer technologies like machine learning and big data are gradually replacing older approaches to deliver more accurate and effective results. The processing of vast amounts of data, including user behavior, product reviews, and transaction records, has become a significant challenge for companies. Consequently, the adoption of powerful data processing tools like Apache Spark and its PySpark library has emerged as an effective solution for handling and analyzing large-scale data.

- Thus, researching and developing a personalized product recommendation system using PySpark not only addresses market demands but also delivers practical value to businesses, contributing to the advancement of cutting-edge technologies in big data analytics and machine learning.
  
## 2. Proposed Model
<img width="583" alt="image" src="https://github.com/user-attachments/assets/59438b4f-a18a-4e72-ac2c-735b9c6a3056" />

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
- 1. Initialize the VADER Model: We used the VADER lexicon from the NLTK library to calculate the sentiment polarity scores for the reviews. The sentiment score is computed on a scale from -1 (very negative) to 1 (very positive). 
![image](https://github.com/user-attachments/assets/4a6fc488-db88-45f1-abff-45af230b18d9)
- 2. Create UDF (User Defined Functions): Two UDFs were defined: - - 
    The first function, get_polarity_score(), calculates the overall sentiment score for each review. 
    The second function, get_sentiment_label(), assigns a sentiment label to the reviews based on the overall sentiment score: 
                    + Positive if the sentiment score > 0.05. 
                    + Negative if the sentiment score < -0.05. 
                    + Neutral if the sentiment score is between -0.05 and 0.05.
     ![image](https://github.com/user-attachments/assets/c191443f-db4c-4f53-9368-7664584bf3a9)
