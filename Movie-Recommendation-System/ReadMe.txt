Data used: TMDB movie list dataset from Kaggle 
kaggle link: https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata
You can find the dataset here

We are doing Content based recommendation system
- Recommends movies similar to ones a user has liked based on features (e.g., genre, director, cast).
There are different recommendation methods like:
1. Collaborative filtering
2. Hybrid filtering

We  are using SVM(Support Vector Machine) algorithm for filtering :

A Support Vector Machine (SVM) is a supervised machine learning algorithm used for classification and regression tasks. 
It is particularly powerful for binary classification but can be extended to multiclass problems. 
SVM works by finding the optimal hyperplane that best separates data into different classes in a high-dimensional space.

Here are some of the reasons to consider SVM for this project:
1.Handling High-Dimensional Data
2.SVMs are less prone to overfitting, especially with the right choice of regularization parameters. This makes them useful if your data is sparse or noisy.
3. Since there is lot of textual data it is more convinient to convert the data into vectors to calculate the distance and find the nearest values


To reduce the size of the dataset we have removed some of the columns which are not required for the analysis.

The dataset required preprocessing steps to align it with our requirements.Columns such as 'overview,' 'genres,' 'keywords,' 'cast,' and 'crew' contain lists, with each list consisting of dictionaries that have key-value pairs.
So in this we will try to extract the necessary fields and merge these columns to create a single column named 'tags'.
So the 'tag' column will help you search for the necessary parameters required for the filtering process.
We encountered an issue with the 'tags' column during processing: some words are similar or synonyms, which could lead to confusion for the model.
For instance, words like 'love,' 'loving,' and 'loved' appear in different movie overviews and can be considered similar, but due to tense variations, they are treated as separate words.
To address this, we use CountVectorizer to standardize and effectively handle such cases.

We use the stemming technique in NLP (Natural Language Processing) with NLTK to reduce words to their root or base form, which helps in text normalization.
> Handles Variations in Word Forms
Words like "love," "loving," and "loved" are reduced to their root form, "love." This ensures that different tenses or forms of the same word are treated as a single term.

We have used a package from the library Scikit-learn called CosineSimilarity.
In this project rather than calculating the distance between two vectors we are calculating the angles between them to find the nearest vectors.

Once we are done with all the sorting and necessary steps we will now try to make a webpage where we can perform our requests.
To do that we first need to extract the ML code into file which is a pickle file. It can be done by importing the Pickle library.


I have created a web page API in localhost using Streamlit library 
Streamlit Documentation Link:https://docs.streamlit.io/

In the file app_mrs.py there is code which requires some editing.Below given is the code
response = requests.get('https://api.themoviedb.org/3/movie/{}?api_key=yourkeygenerated'.format(movie_id))

To generate your private API Key you need to create an account in TMDB and go to Settings > API > Generate Key
Once you fill all the credentials your key will be generated and paste that key api_key=here.
This is done to get the posters of the movies so that it will be shown while recommending the movies along with title.

Hope this helps.
