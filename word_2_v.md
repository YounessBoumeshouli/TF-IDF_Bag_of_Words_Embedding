import numpy as np
import gensim.downloader as api

# 1. Load Pre-trained Model (The "Brain")
# This maps string "king" -> Array of 50 floats
model = api.load("glove-wiki-gigaword-50")

sentence = "bananas are yellow"

# 2. Step-by-Step Vectorization
word_vectors = []
for word in sentence.split():
    try:
        # Step A: Lookup (Fetch vector from the 'Brain')
        vec = model[word]
        word_vectors.append(vec)
        print(f"Found vector for '{word}': First 3 dims -> {vec[:3]}...")
    except KeyError:
        print(f"Word '{word}' not in vocabulary (OOV). Skipping.")

# 3. Aggregation (Creating the Sentence Embedding)
# We stack them and take the average (Mean Pooling)
if word_vectors:
    sentence_matrix = np.array(word_vectors) # Shape: (3 words, 50 dims)
    sentence_embedding = np.mean(sentence_matrix, axis=0) # Shape: (50 dims)
    print(f"\nFinal Sentence Vector shape: {sentence_embedding.shape}")
else:
    print("Empty vector")