Resource: [Attention in transformers, step-by-step | Deep Learning Chapter 6](https://www.youtube.com/watch?v=eMlx5fFNoYc)
- The goal of Transformer model: take in a piece of text and predict what word comes next
	![[Pasted image 20250724163343.png]]
- how directions in this high-dimensional space of all possible embeddings can correspond with semantic meaning.
- Word Embedding: Associate each token with a high-dimensional vector.
	- how directions of in this high-dimensional space of all possible embeddings can correspond with semantic meaning.
	- the aim of transformer: progressively adjust these embeddings so that they don't merely encode an individual word, but instead they bake in some much richer contextual meaning.
- The aim of transformer is to progressively adjust these embeddings, so that they don't merely encode an individual word, but instead they bake in some much, much richer **contextual meaning**.

- The computation you perform to produce a prediction of the next token is entirely a function of the last vector in the sequence.
	- the final vector in the sequence, somehow encoding all of the information from the full context window that's relevant to predicting the next word.
### Single Head of Attention
- The initial embedding for each word is some high dimensional vector that only encodes the meaning of that particular word with no context.
	- They also encode the position of the word
	- The entries of the vector are enough to tell you both what the word is and where it exists in context
- Each token is first embedded into a single vector, but for attention, it is transformed into **3 vectors (Q, K, V) per head**.
### Query Vector
- The Query Vector has a much smaller dimension than the embedding vector, say 128.
- Computing Query:
	- Taking a certain matrix $W_Q$
	- multiplying by the embedding
	![[Pasted image 20250724183118.png]]
	![[Pasted image 20250729184718.png]]




### Key Vector
- Conceptually, you want to think of the keys as potentially answering the queries.
- You think of the keys as matching the queries whenever they closely align with each other.
- Measure how well each key matches each query: 
	- Compute a dot product between each possible key-query pair
		- `Attent to`: The dot products in these two spots would be some large positive numbers
	![[Pasted image 20250730171642.png]]
	- The grid of values: can be any real number from $-\infty$ to $\infty$
	- The score means: how relevant each word is to updating the meaning of every other word
	![[Pasted image 20250730172023.png]]
	- way about to use these words: take a weighted sum along each column
		- weighted by the relevance
		- compute a softmax along each one of these columns to normalize the values
		- to get an **Attention Pattern**
	![[Pasted image 20250730172510.png]]
- The well-known formula:
	$$
\mathrm{Attention}(Q, K, V) = \mathrm{softmax}\!\left(\frac{QK^{T}}{\sqrt{d_k}}\right) V
	$$
	- Q: arrays of Query vectors
	- K: arrays of Key vectors
	- $\sqrt{d_k}$: divide by the square root of the dimension in the key query space, for numerical stability
- The size of attention pattern = the square of the context size
	![[Pasted image 20250801001740.png]]
- Variations to the attention mechanism aimed at making context more scalable:
	- Sparse Attention Mechanisms
	- Blockwise Attention
	- Linformer
	- Reformer
	- Ring attention
	- Longformer
	- Adaptive Attention Span

### Masking
- During the training process, when this model is run on a given text example, all of the weights are slightly adjusted and tuned either reward or punish it, based on how high a probability it assigns to the the true next word in the passage.
- To make the training process more efficient:
	- simultaneously predict every possible next token following each initial subsequence of tokens in this passage
		![[Pasted image 20250801001208.png]]
- You never want to allow **later words** to influence **earlier words**, since otherwise they could give away the answer for what comes next.
	![[Pasted image 20250801001534.png]]
### Value Vector
- Multiply the embedding of the first word by the $W_v$
- Value vector is something that you add to the embedding of the second word.
	- If this word is relevant to adjust the meaning of something else, what exactly should be added to the embedding of that something else in order to reflect this
- How to use Value in the Attention Pattern:
	- You multiply each of the value vectors by the corresponding weight in that column
	- add together all of these rescaled values in the column
		producing the change that you want to add $\Delta \vec{E}$
- Hopefully, what results is a more refined vector, encoding the more contextually rich meaning
	![[Pasted image 20250801004359.png]]
- Apply the same weighted sum across all of the columns, producing a sequence of changes. 
	Adding of those changes to the corresponding embeddings, produces a full sequence of more refined embeddings popping out of the attention block.
	![[Pasted image 20250801005107.png]]
### How many Params
- Query and Key:
	- 12288 columns, matching the embedding dimension
	- 128 rows, matching the dimension of the smaller key query space
		![[Pasted image 20250801005338.png]]
- Value: it's a square matrix
	- both its inputs and outputs live in the very large embedding space
	- 12288 x 12288
- `Low Rank` transformation:
	![[Pasted image 20250801005848.png]]





### Multi-head Transformer
- By running many distinct heads in parallel, you're giving the model the capacity to learn many distinct ways that context changes meaning.
- For every different type of contextual updating that you might imagine, the parameters of these key and query matrices would be different. 
	And the parameters of our value map would be different based on what should be added to the embeddings.
- 









