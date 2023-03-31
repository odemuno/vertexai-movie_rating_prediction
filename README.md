# From Datasets to Deployment: How Vertex AI Simplifies ML for Movie Rating Prediction

> YouTube tutorial: https://youtu.be/rwGDN_CNLNA

In today's fast-paced world, businesses of all sizes are looking to harness the power of artificial intelligence to gain a competitive edge. However, managing the entire AI workflow, from datasets to deployment, can be a daunting challenge, especially when teams consist of individuals with varying levels of ML expertise. 

In the [YouTube video](https://youtu.be/rwGDN_CNLNA), I highlight [Google Vertex AI](https://cloud.google.com/vertex-ai) – a platform providing tools for every step of the ML workflow for different model types and varying levels of expertise all in one central place. It enables you to define your prediction task, ingest data, analyze data, transform data, train a model, evaluate the model, and deploy it.

I would illustrate how to use Vertex AI for movie rating prediction. This was a well-documented example by Google Developers: https://codelabs.developers.google.com/moviescore-prediction-vertexai#0

We'll create a movie score prediction model using Vertex AI AutoML and data stored in BigQuery. Then, we will have the deployed model endpoint triggered from Java Cloud Functions. 

# Step 1: Requirements
## Google Cloud Project
In the [Google Cloud Console](https://console.cloud.google.com/getting-started), select or create a Google Cloud project. Then make sure that billing is enabled for your Cloud project. If a billing account is linked, the billing Overview page is displayed. If it is not linked, you would get a message saying “This project has no billing account." [Check if billing is enabled for your project.](https://cloud.google.com/billing/docs/how-to/verify-billing-enabled )

## BigQuery
Next, open [BigQuery](https://console.cloud.google.com/bigquery) and [enable the API](https://console.cloud.google.com/flows/enableapi?apiid=bigquery). This helps complete tasks like running queries, loading data, and even creating and training ML models. 

## Google Cloud Console
Then, you want to activate your [Cloud Shell](https://cloud.google.com/cloud-shell/). Run these commands to confirm that the g-cloud command knows about this project.

```
$ gcloud auth list

$ gcloud config list project
```

# Step 2: Preparing Training Data
Preparing training data is crucial in ensuring the accuracy and effectiveness of machine learning models. Properly labeled and well-structured data can help models learn and generalize better, leading to more accurate predictions and insights. For this short poject, the assumption is that the data is already prepared. It is available on GitHub [(movies.csv)](https://github.com/AbiramiSukumaran/movie-score/blob/main/movies.csv). Some of the features of the data are the movie name, rating, and the genre.

You can also find the dataset in this repo: https://github.com/odemuno/vertexai-movie_rating_prediction/blob/24cd34323530d6d8740a7af5e9e33e1717b913f6/movies.csv#L1

# Step 3: Creating and Loading Dataset
First thing you want to do is clone the repo from the GitHub page linked above. 
```
$ git clone <<repository link>>

$ cd movie-score
```
Then follow these steps as seen in the YouTube video:
- In your BigQuery UI, click on your project ID and then in the section with more details click on create dataset
- Give a name for your dataset. This becomes the dataset ID. 
- For the location type, choose your relevant location. I chose multi-region and U.S. Then click on create dataset.
- In your BigQuery UI, you should see the dataset ID under your project ID. 
Use the bq load command to load your CSV file into a BigQuery table in the Cloud Shell terminal. You should see the loaded file in BigQuery.


Once the dataset is created, you can query the dataset using the bq command or using the BigQuery web UI which gives a bit more visual information.

- In Cloud Shell termainal
```
bq query --use_legacy_sql=false \
SELECT name, rating, genre, runtime FROM bq_movie_dataset.movies_score limit 3;
```

- In BigQuery UI
```
SELECT name, rating, genre, runtime FROM bq_movie_dataset.movies_score limit 3;
```

# Step 4: Using the BigQuery data in Vertex AI AutoML
- Follow instructions in the [YouTube video](https://youtu.be/rwGDN_CNLNA)

# Step 5: Using Java Cloud Function to trigger ML invocation
- Follow instructions in the [YouTube video](https://youtu.be/rwGDN_CNLNA)
- The relevant files are:
    - HelloHttpFunction.java: https://github.com/odemuno/vertexai-movie_rating_prediction/blob/main/HelloHttpFunction.java
    - pom.xml: https://github.com/odemuno/vertexai-movie_rating_prediction/blob/main/pom.xml

