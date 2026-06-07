# FYP_UOW
Analysing Public Perception: Sentiment Analysis of Generative AI Across Social Media Platforms
Author: Mohamed Ahmed-Nur (w1983088)
Degree: BSc (Hons) Computer Science
University: University of Westminster
Submitted: April 2026

Overview
This project analyses public sentiment towards Generative AI across three social media platforms — Reddit, X (Twitter), and YouTube — using multiple sentiment analysis techniques. It addresses the limitation of existing research by adopting a multi-platform, multi-model design rather than relying on a single platform or a single analysis model.
A total of 1,500 posts (500 per platform) from 2023 were collected, cleaned, analysed, and visualised through an interactive Streamlit web application.


🌐 Streamlit App: View the web application

Key Findings

Reddit and X produced consistent sentiment distributions across all three models: ~37–38% positive (lexicon-based) and ~31% positive (RoBERTa), with ~27–28% negative.
YouTube showed significantly higher negative sentiment (~46–47% under RoBERTa, ~41% under TextBlob) and lower positive sentiment, indicating a more emotionally polarised and critical user base.
Model choice matters: VADER, TextBlob, and RoBERTa produced different results on the same data — particularly for YouTube — highlighting the importance of using multiple models.
RoBERTa outperformed lexicon-based models on nuanced text, including sarcasm and contextual language.


Tech Stack
PythonData ManipulationPandas, NumPyNLP & PreprocessingNLTK, WordNetLemmatizer, Stopwords, word_tokenizeSentiment AnalysisVADER (nltk), TextBlob, RoBERTa (Hugging Face Transformers)Deep LearningPyTorch (torch)Data VisualisationMatplotlibWeb ApplicationStreamlitDevelopment EnvironmentsJupyter Notebook, VS CodeDiagram CreationDraw.ioData SourcesKaggle (Reddit & X), YouTube Data API v3

Project Structure
FYP_SENTIMENT_ANALYSIS/
│
├── Data/
│   ├── raw/            # Original datasets (Reddit CSV, X CSV, YouTube API data)
│   ├── cleaned/        # Cleaned and preprocessed datasets per platform
│   └── combined/       # Combined dataset (1,500 rows) used for analysis
│
├── Notebooks/
│   ├── Data_Collection.ipynb     # YouTube API collection + Kaggle loading
│   ├── Data_Cleaning.ipynb       # Preprocessing, analysis, and visualisation
│   └── combined_df.csv           # Final combined dataframe
│
└── streamlit_app/      # Streamlit web application code

Data Collection
PlatformMethodSizeRedditKaggle public dataset500 posts (sampled from 523,017)X (Twitter)Kaggle public dataset500 postsYouTubeYouTube Data API v3500 comments
All data is from 2023 and filtered using AI-related keywords: Generative AI, GenAI, Artificial Intelligence, AI.

Sentiment Analysis Models
1. VADER (Lexicon-Based)

Uses a compound score between -1 and 1
Thresholds: ≥ 0.15 → Positive, ≤ -0.15 → Negative, else Neutral
Fast and efficient but struggles with sarcasm and context

2. TextBlob (Lexicon-Based)

Returns polarity (sentiment) and subjectivity scores
Subjectivity score indicates how opinionated vs objective a post is

3. RoBERTa (Transformer-Based)

Model: cardiffnlp/twitter-roberta-base-sentiment (Hugging Face)
Fine-tuned on Twitter data for sentiment classification
Handles context, negation, and sarcasm more accurately


Data Preprocessing Pipeline
The clean_text() function applies the following steps to all platforms uniformly:

Lowercase normalisation
Contraction expansion (can't → cannot)
Removal of URLs, hashtags, and mentions
Whitespace cleanup
Tokenisation
Stopword removal
Lemmatisation (WordNetLemmatizer)


Installation & Setup
Prerequisites

Python 3.8+
Jupyter Notebook or JupyterLab
A YouTube Data API v3 key (for data collection only)

Install Dependencies
bashpip install pandas numpy nltk textblob transformers torch streamlit matplotlib langdetect google-api-python-client
Download NLTK Data
pythonimport nltk
nltk.download('punkt')
nltk.download('stopwords')
nltk.download('wordnet')
nltk.download('punkt_tab')
Run the Streamlit App Locally
bashstreamlit run app.py

Testing
Black-box testing was used across 10 test cases covering:

Text cleaning (URL removal, hashtag removal, contraction expansion)
Sentiment model classification (positive, negative, neutral, sarcasm)
Streamlit UI functionality

Results: 8/10 passed. Key failures:

T2: Contraction expansion — apostrophe encoding inconsistency caused stopword removal to incorrectly strip word fragments
T6: VADER misclassified clearly positive text as neutral after preprocessing removed intensifying words


Limitations

Sample size of 500 posts per platform limits statistical generalisation
Reddit and X data sourced from Kaggle datasets (unknown sampling bias)
RoBERTa model fine-tuned on Twitter data only — may not fully generalise to Reddit/YouTube
Data limited to 2023 only


Future Work

Replace Kaggle datasets with direct API collection across all platforms
Use platform-specific fine-tuned transformer models
Extend the time period beyond 2023 to capture evolving sentiment
Increase sample size with stratified sampling for greater statistical confidence



Acknowledgements
Special thanks to my supervisor Salma Chahed for her guidance throughout this project, and to YouTube for providing API access for data collection.
