from sklearn.feature_extraction.text import TfidfVectorizer

corpus = [
    "A generic movie.",
    "A terrible, terrible movie."
]

# 1. Initialize
vectorizer = TfidfVectorizer()

# 2. Fit (Learn Vocab & Calculate IDF stats)
vectorizer.fit(corpus)

print("Step 1: Global Stats (IDF Scores)")
# Lower IDF = Common word (less important). Higher IDF = Rare word (Important).
for word, idf in zip(vectorizer.get_feature_names_out(), vectorizer.idf_):
    print(f"  Word: '{word}' -> IDF: {idf:.4f}")
# 'movie' appears in both, so it has low IDF. 'terrible' appears in only one, so high IDF.

# 3. Transform (Calculate TF * IDF)
tfidf_matrix = vectorizer.transform(corpus)

print("\nStep 2: Final Weighted Scores (TF-IDF)")
print(tfidf_matrix.toarray())
# Notice: In Doc 2, 'terrible' has a high score because it appears twice (high TF) 
# AND is rare in the corpus (high IDF).