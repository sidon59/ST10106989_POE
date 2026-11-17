**Medical Product Reviews: Text Analytics and Sentiment Analysis**

A Python-based text analytics project exploring 5,000 medical product
reviews through exploratory data analysis (EDA), sentiment
classification, and topic modelling.
Scope note: The supplied dataset contains medical product reviews.
It is not a dataset of HelloPeter complaints about a South African
medical aid scheme. The findings describe the product-review dataset
and must not be interpreted as evidence about a medical aid scheme's
claims, benefits, authorisations, or customer service.

**Project objectives**

- Explore the structure, quality, and distribution of the review data.
- Derive sentiment labels from star ratings.
- Examine common words and differences in positive and negative review
  language.
- Train and evaluate a Logistic Regression sentiment classifier.
- Apply Latent Dirichlet Allocation (LDA) to identify broad themes.
- Interpret findings, limitations, and opportunities for further
  analysis.
  
**Dataset**

The dataset contains 5,000 records and 10 columns:

  Column                     Description
  Id                       Review record identifier
ProductId                Product identifier
UserId                   Reviewer identifier
ProfileName              Reviewer profile name
HelpfulnessNumerator     Number of users finding the review helpful
HelpfulnessDenominator   Number of users rating helpfulness
Score                    Star rating from 1 to 5
Time                     Review timestamp
Summary                  Short review heading
Text                     Full review text

**Sentiment labels**

Star ratings are used as a proxy for sentiment:

  Star rating   Derived sentiment
  1--2          Negative
3             Neutral
4--5          Positive

The binary sentiment classifier excludes neutral reviews, leaving
4,440 reviews: 1,241 negative and 3,199 positive.

**Methods and workflow**

1. Data inspection and preparation
   - Inspect dimensions, columns, missing values, and exact
     duplicates.
   - Select review text, summary, and rating fields.
   - Clean text and derive sentiment labels from ratings.
2. Exploratory data analysis
   - Examine star-rating and sentiment distributions.
   - Explore review length and frequent terms.
   - Use word clouds to compare positive and negative vocabulary.
3. Sentiment classification
   - Convert text into numerical features using TF-IDF.
   - Train a Logistic Regression classifier in a scikit-learn
     pipeline.
   - Use a stratified 80/20 train/test split.
   - Tune selected parameters with GridSearchCV, using weighted
     F1-score.
4. Topic modelling
   - Apply five-topic Latent Dirichlet Allocation (LDA).
   - Assign reviews to their dominant topic.
   - Compare the proportion of negative reviews across topics.
     
**Reported results**

Sentiment distribution**

  Sentiment       Reviews   Percentage
  Positive          3,199       63.98%
Negative          1,241       24.82%
Neutral             560       11.20%
Total     5,000     100%

**Sentiment model**

The executed notebook reported these baseline and tuned test results:

  Metric                 Baseline   Tuned model
  Accuracy                   1.00          1.00
Weighted precision         1.00          1.00
Weighted recall            1.00          1.00
Weighted F1-score          1.00          1.00

The tuned model selected:
- max_features: 5,000
- ngram_range: (1, 2)
- C: 1
  
Interpretation caution: Perfect scores are unusually high. The
dataset contains repeated language patterns and only 50 distinct review
summaries. Similar or templated text may occur in both training and test
partitions, making classification easier than it would be on genuinely
new reviews. These results are not proof of real-world performance.
Group-aware validation and testing on an independent dataset are
recommended.

**Topic modelling**

The original five-topic LDA analysis produced these broad, provisional
interpretations:
  Topic           Interpreted                   Reviews       Negative share
theme                                 
  1               Pulse oximeters,                1,200                22.2%
blood-pressure
monitors, and
thermometers                          

  2               Earplugs and                      576                29.2%
face masks                            

  3               First-aid kits                    855                29.0%

  4               Glucose meters                    473                41.6%
and walking aids                      
5               Knee braces and                 1,336                27.1%

**pill organisers**

Topic labels are interpretations of prominent words, not verified
product categories or confirmed defects. Topic 4 had the highest
proportion of negative reviews in this analysis.

**Limitations and next steps**

- Dataset relevance: Product reviews do not directly answer a
  research question about medical aid scheme service complaints.
- Dataset provenance: Add the original dataset source, licence or
  permission information, and access date before publishing or
  submitting the project.
- Rating-derived labels: Star ratings are proxies for sentiment
  and are not equivalent to manually annotated sentiment.
- Repeated text: Repeated sentence patterns and summaries may
  inflate random-split model performance.
- Validation: Evaluate with group-aware splitting and an
  independent test dataset.
- LDA input: The original notebook used TF-IDF features for LDA.
  LDA is generally more appropriate with document-term count features,
  such as those produced by CountVectorizer. Rerun the topic model
  with count-based features before treating the topics as final.
- Topic selection: Compare alternative topic counts and manually
  inspect representative reviews for each topic.
  

The notebook uses Python and common data science libraries, including:
- pandas
- NumPy
- Matplotlib
- Seaborn
- scikit-learn
- NLTK
- WordCloud
- Jupyter Notebook
  
Install the commonly used dependencies:
pip install pandas numpy matplotlib seaborn scikit-learn nltk wordcloud jupyter

**Running the notebook**

1. Clone or download this repository.
2. Place the CSV file in the same directory as the notebook, or update
   the notebook's CSV path.
3. Install the dependencies listed above.
4. Launch Jupyter Notebook:
   jupyter notebook
5. Open Medical_Reviews_Analysis_Executed.ipynb and run the cells.
The notebook expects the dataset file to be named Medical_Reviews.csv
unless its loading path is changed.

**Reproducibility**

The executed analysis used a stratified train/test split with
random_state=42. Keep the notebook and dataset together to reproduce
the analysis. If the dataset changes, rerun all cells and update the
report and results.

**Academic note**
This project was prepared as part of the PDAN8441 Portfolio of
Evidence -- Working with Text. Add the required student details and
complete dataset/source references in the submitted report. Cite
external code, tutorials, or materials used.

**Author**
Ximiyeto Makhubele
