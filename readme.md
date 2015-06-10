Note - recommended using k fold cross validation when evaluating cross validation: http://scikit-learn.org/stable/modules/generated/sklearn.cross_validation.StratifiedKFold.html#sklearn.cross_validation.StratifiedKFold

evaluation.py contains scripts for performing evaluation against the metric provided.

When conducting error analysis with KFold - instead of breaking it down into k files, stack the 
tables on top of one another to get one big file of the model trained and tested on different
data.

6/5/2015 - seemt to be getting a lot of false positives - tend to overrate the query results.
This probably makes sense, because the overall rating of query results is high, so any mistake
is probably going to err on the high side. 

TO DO:
Add and test features (see below)
Add comments to your code (so other can undersetand and also so you can understand - your
code borrows a lot from others)
Figure out what CountVectorizer does and see if there would be better alternatives
Adjust cross validation so it always includes a proportionate number of each query
Incorporate porter stemmer code https://www.kaggle.com/duttaroy/crowdflower-search-relevance/porter-stemmer/run/11533
Test out TFIDF
Incorporate SVD transformation to TFIDF output TruncatedSVD(n_components=200, algorithm='randomized', n_iter=5, random_state=None, tol=0.0)
Incorporate stop words below after getting basic stemming working.
stop_words = ['http','www','img','border','0','1','2','3','4','5','6','7','8','9','a','the']
stop_words = text.ENGLISH_STOP_WORDS.union(stop_words)

Feature ideas:
Variance rating in training for that particular query, across all titles and descriptions



Note that for the some of our features rely on the fact that every query in training occurs in testing.
Basically, to use these features, you would perform a preprocessing step to X_test to add these 
variables before you run the model. Also note that cross validation on our training set may become 
tricky when you use these variables since they assume you have at least one example of each query.

One of the queries is harleydavison. It is miscategorized by the algorithm - seems to underestimate 
the relevance of the results, because the titles and descriptions always say "Harley Davidson". Consider
making a feature that converts the title to lower case and removes all spaces - then provides an indicator
whether the query exists in the title. Also consider removing dashes '-' - for example, the "spiderman" query
has results with "Spider-man"

Are there repeated query/title combinations? If so, it seems that any time we encounter a known query/title combination
in test set, we should just assign it the rating seen already. Check to see whether this is the case and also check
the variation in ratings among common query/title combos.