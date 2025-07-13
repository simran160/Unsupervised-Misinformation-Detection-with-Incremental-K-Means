Unsupervised Misinformation Detection with Incremental K-Means
==============================================================

This repository contains my implementation of the unsupervised misinformation detection model using incremental K-Means, inspired by the research paper "Unsupervised Misinformation Detection Model using Incremental K-Means Algorithm" by Yashoda Barve and Jatinderkumar R. Saini. The project focuses on clustering misinformation (such as fake news), adapting to new data over time without requiring labeled examples.

Overview
--------

The main objective of this project is to detect misinformation in news articles using an **unsupervised learning** approach. I extract both textual and user-specific features from news data and apply incremental K-Means clustering to group articles as credible or non-credible. This approach allows the model to adapt to new, unlabeled data as it arrives, making it suitable for real-world, time-sensitive scenarios.

Key Features
------------

*   **Text and User Feature Extraction:** I generate 30 features, including content-based (e.g., word count, sentiment, readability, topic modeling) and user-based (e.g., country, publisher reliability, political bias) features, as described in the reference paper.
    
*   **Incremental K-Means Clustering:** The model is trained in batches, updating clusters as new data arrives, which is essential for handling data streams or evolving news.
    
*   **Feature Importance:** I use a Random Forest classifier to identify the most influential features in cluster formation.
    
*   **Evaluation Metrics:** The model is evaluated using silhouette score and purity score, following the methodology in the paper.
    
*   **No Labeled Data Required:** The approach works without manual annotation, reducing human effort and making it scalable.
    

Project Structure
-----------------

*   **Data Cleaning & Preprocessing:**
    
    *   Removing HTML tags, numbers, emojis, and stopwords from the text.
        
    *   Tokenization and feature engineering.
        
*   **Feature Extraction:**
    
    *   Calculating statistics such as character count, word count, sentence count, readability (ARI), sentiment scores, POS tag counts, and topic distributions (via LDA).
        
    *   Extracting user-based features like country, reliability, reputation, and political bias.
        
*   **Feature Selection:**
    
    *   Using Random Forest to determine the top features contributing to misinformation detection.
        
*   **Incremental K-Means Clustering:**
    
    *   Initial clustering on a batch of data.
        
    *   Incremental updates as new data batches arrive, with cluster assignments based on Euclidean distance.
        
    *   Handling concept drift by monitoring silhouette scores and resetting clusters if necessary.
        
*   **Evaluation:**
    
    *   Calculating silhouette and purity scores to assess cluster quality.
        
    *   Analyzing cluster composition and feature importance.
        

How It Works
------------

1\. Data Preparation
--------------------

I start by cleaning and preprocessing the dataset, which includes removing unwanted characters and stopwords, and generating a cleaned\_text column.

2\. Feature Engineering
-----------------------

Using the cleaned text, I extract a comprehensive set of features:

*   **Textual:** Character/word/sentence counts, sentiment scores, ARI, POS tag counts, and topic modeling (LDA).
    
*   **User-specific:** Country, reliability, reputation, and political bias.
    

3\. Feature Selection
---------------------

I use a Random Forest classifier to rank feature importance, then select the top features for clustering.

4\. Incremental K-Means Clustering
----------------------------------

*   The model is first trained on an initial batch.
    
*   As new data arrives, I update the clusters incrementally using MiniBatchKMeans.
    
*   If the silhouette score drops below a threshold, I reset the clusters to handle concept drift.
    

5\. Evaluation
--------------

I use silhouette score to measure cluster cohesion and purity score to assess how well clusters match the underlying credibility labels (if available). Results

*   **Silhouette Score:** Around 0.76 
    
*   **Purity Score:** Up to 0.67
    
*   **Top Features:** Character count, ARI, topic-specific word counts, reputation, sentiment scores, and political bias.
    

References
----------

*    Yashoda Barve, Jatinderkumar R. Saini, "Unsupervised Misinformation Detection Model using Incremental K-Means Algorithm", IJISAE, 2022.
    

Usage
-----

1.  Prepare your dataset in CSV format, ensuring it contains necessary columns as described above.
    
2.  Run the preprocessing and feature extraction scripts.
    
3.  Use the incremental K-Means code to cluster your data.
    
4.  Evaluate the clustering results using silhouette and purity scores.
    

License
-------

This project is for academic and research purposes only. Please refer to the original research paper for citation and further details.

For any questions or suggestions, feel free to open an issue or contact me directly.
