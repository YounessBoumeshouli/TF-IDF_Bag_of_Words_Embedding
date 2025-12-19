from sentence_transformers import SentenceTransformer

# 1. Load Model
model = SentenceTransformer('all-MiniLM-L6-v2')

sentences = ["The bank is closed", "The river bank is muddy"]

# 2. Under the Hood: Tokenization
# BERT doesn't see strings; it sees IDs.
tokenizer = model.tokenizer
for sent in sentences:
    tokens = tokenizer.tokenize(sent)
    print(f"Sentence: '{sent}'")
    print(f"  Tokens: {tokens}") 
    # Notice common words are kept, rare words might be split.

# 3. Encoding (The Forward Pass)
# This handles the contextual lookup and the pooling (averaging) automatically.
embeddings = model.encode(sentences)

print(f"\nFinal Embeddings Shape: {embeddings.shape}")
# (2 sentences, 384 dimensions)
# Even though the sentences share the word "bank", the vectors are totally different
# because BERT factored in the surrounding words ("river" vs "closed").