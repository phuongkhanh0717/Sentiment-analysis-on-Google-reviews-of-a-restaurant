# Sentiment-analysis-on-Google-reviews-of-a-restaurant

## Introduction
In this project, we created a deep learning model using Recurrent Neural Networks (RNN) to classify restaurant reviews as either positive or negative. This task is important because it helps restaurant owners and managers better understand their customers' experiences, develop recommendation systems, improve customer satisfaction, and conduct competitive analysis. Our goal is to build an accurate tool for analyzing sentiment in restaurant reviews using RNNs, which can be useful for decision-making and enhancing customer experiences in real-world scenarios.

## Model
We are going to use PyTorch, which provides variations of recurrent neural network modules.
From _Review on methods to fix number of hidden neurons in neural networks. Mathematical Problems in Engineering_, by Sheela and Deepa (2013), the number of neurons can be calculated in a hidden layer is (4*n^2+3)/(n^2-8), where n is the number of input.
### Model Figure
![pretrained GloVe to an RNN-based architecture for sentiment analysis](https://user-images.githubusercontent.com/37010080/234146921-36006957-0201-4892-86c8-6d79b344802e.png)
[Source](https://d2l.ai/chapter_natural-language-processing-applications/sentiment-analysis-rnn.html)

![RNN Architecture](https://user-images.githubusercontent.com/37010080/234147022-3c38ea5b-9780-4d9c-a12c-4f5e870c067b.png)
[Source](https://www.mdpi.com/2076-3417/12/7/3641)
## Data
### Data Source
In this project, we focus our analysis specifically on the reviews of a single restaurant, Sansotei Ramen at Square One (Mississauga, Canada). To collect the review data, we used the following approach:
1.	Targeted Restaurant: We narrowed down our target to Sansotei Ramen at Square One, aiming to analyze their customer reviews since the opening of the restaurant until the present time.
2.	Data Collection: To obtain the review data, we used a web-based tool called ExportComments.com. This tool allowed us to extract all reviews associated with Sansotei Ramen at Square One from Google.
3.	Output: ExportComments.com returned a CSV file containing 804 reviews. The dataset includes information about the author, the date the review was written, the rating (out of 5 stars), the content of the review, and a helpfulness indicator based on the number of people who rated the review as helpful on Google.

## Data Summary
The dataset obtained from ExportComments.com provided valuable insights into the reviews of Sansotei Ramen at Square One. The key data summary points are as follows:
- Total number of reviews: 804
- There are 363 reviews with only rating, no content. We have decided to manually remove them with Excel and classify the rest of reviews as positive if the rating is greater than or equal to 3, and negative if it's less than 3. Based on this classification, there are:
    - 358 positive reviews (81%). An example of positive review:
    
|Author|Date|Rating|Helpful count|Review|
|------|----|------|-------------|------|
|Tiffany Choi|16/06/18|5|1|This cozy restaurant seats about 35 guests, is brightly-lit, and has a moderate noise level. Sansotei hasn't had its grand opening yet, but the servers are very well-trained, and the operations seem to run smoothly. It was organized, with a waitlist for tables, and accurate estimates of the wait time. We received our food soon after ordering, and it was delicious!|

    - 83 negative reviews (19%). An example of positive review. An example of negative review:

|Author|Date|Rating|Helpful count|Review|
|------|----|------|-------------|------|
|Kevin Chow|08/07/18|1|2|Will not come back. Bad service / management and really slow kitchen (you can watch through the window yourself). Longer than usual wait times made worse by bad line management (came Sunday around 2pm). The experience ruined what otherwise was an okay ramen bowl, slightly too salty though. Stick to the ramen places in the east end / downtown, this place isn't up to par with the others. Am dissapointed that there is still no great ramen place in sauga. Problems may be due to new staff, but no management seemed to be present trying to run the business as it should for a new place. Also they don't have the proper soup takeout containers for noodles (isn't this a noodle place?!?)... only had small styrofoam boxes.|

## Data Transformation
To prepare the dataset for training the RNN model, we performed the following data transformation steps:
1.	Labeling: Assign binary labels to the reviews based on the given ratings. If the rating is greater than or equal to 3, it is considered a positive review (label 1), otherwise, it is a negative review (label 0).
2.	Text Preprocessing:
    - Convert all text to lowercase.
    - Tokenize the reviews into words.
    - Remove stopwords (common words like 'the', 'and') and special characters (common like ',', '.', ';', ':').
3.  Embedding: Convert the tokenized words into dense vectors using pre-trained word embeddings. We used GLoVe (Global Vectors for Word Representation), a popular unsupervised learning algorithm, to generate the word embeddings. GLoVe maps words to vectors in a continuous space based on the co-occurrence statistics of the words in a large corpus of text. By using pre-trained word embeddings, we can capture the semantic meaning of the words and improve the performance of our model.
4.	Encoding: Convert the tokenized words into numerical values (word indices) using a word-to-index mapping. This step creates an integer-encoded representation of the reviews.
5.	Padding: Ensure that all sequences (reviews) have the same length by padding shorter sequences with zeros or truncating longer sequences. This creates a fixed-size input for the model.
6.	Dataset Split: Split the preprocessed dataset into training, validation, and testing sets. A common split ratio is 60% for training, 20% for validation, and 20% for testing. This allows us to train the model, fine-tune hyperparameters, and evaluate the model's performance on unseen data.
Once the data is transformed, it can be used to train the RNN model for sentiment classification.
# Ethical Consideration
While developing and deploying our sentiment analysis model, it is crucial to consider the potential ethical issues that may arise due to its use. Here, we discuss some concerns related to the system, the limitations of the model, and the training data:
1.	Misinterpretation of Sentiment: There is a potential ethical concern in our project that the deep learning model may classify the sentiment of a review incorrectly, which could result in an inaccurate representation of the restaurant's performance. This misclassification could potentially harm the restaurant's reputation or misguide users into making decisions based on misleading information.
2.	Limitations of the Model: One of the limitations of our RNN model is that it may encounter difficulties in comprehending intricate language structures, detecting sarcasm, or recognizing industry-specific jargon in the reviews. These limitations could result in inaccurate classifications, which can lead to negative outcomes for businesses or users who rely on the model's output for decision-making purposes.
3.	Bias in Training Data: the training data used for our RNN model may contain inherent biases due to unbalanced ratings, cultural differences, or overrepresentation of certain types of reviews. These biases can lead to unfair assessments by the model, potentially harming the reputation of certain restaurants. It is crucial to ensure that the dataset used for training is diverse and unbiased to avoid perpetuating such biases. 
4.	Privacy Concerns: Although we only focus on the content of the reviews and do not use any personal information for analysis, the use of user-generated content could potentially raise privacy concerns if identifiable information is inadvertently included in the review text.
To address these ethical considerations, it is essential to continuously evaluate the model's performance, actively work on reducing biases in the training data, maintain transparency about the model's limitations, and develop guidelines for responsible use of the sentiment analysis system.

# Author
- Khanh Vo

# Reference
- Sheela, K. G., & Deepa, S. N. (2013). Review on methods to fix number of hidden neurons in neural networks. Mathematical Problems in Engineering, 2013.
