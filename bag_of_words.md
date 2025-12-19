# NLP Under the Hood: Step-by-Step Code Walkthrough

This guide dissects the **execution process** of the four major NLP techniques. Instead of just calling a library function, we break down the steps (Tokenization, Vocabulary Building, Vectorization) to understand *how* the data transforms.

---

## 1. Bag of Words (BoW)
**The Mechanism:** Dictionary Matching & Counting.

### 🛠 The Process
1.  **Tokenization:** Split text into words (tokens).
2.  **Vocabulary Building:** Create a unique ID for every word in the entire dataset.
3.  **Vectorization:** For each sentence, count occurrences of each vocabulary ID.

### 💻 Code & Comments

```python
from sklearn.feature_extraction.text import CountVectorizer
import pandas as pd

# 1. The Input Data
corpus = [
    "The cat sat on the mat.",
    "The dog sat on the log."
]

# 2. Initialize the "Bag" (The Counter)
# binary=False means we count frequency (0, 1, 2...). 
# binary=True would just check presence (0 or 1).
vectorizer = CountVectorizer()

# 3. Step-by-Step Execution
# Fit: Learn the vocabulary (Map words to IDs)
vectorizer.fit(corpus)
vocab = vectorizer.vocabulary_

print(f"Step 1: Vocabulary Built (Word -> ID):")
print(vocab) 
# Output example: {'the': 4, 'cat': 0, 'sat': 3, ...}

# Transform: Turn text into vectors based on that vocabulary
bow_matrix = vectorizer.transform(corpus)

# 4. Visualization
# We convert to DataFrame to see which column belongs to which word
df_bow = pd.DataFrame(bow_matrix.toarray(), columns=vectorizer.get_feature_names_out())

print("\nStep 2: Vectorization (The Counts):")
print(df_bow)
# Notice: 'the' appears 2 times in the first sentence, so its column has value 2.