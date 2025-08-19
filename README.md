# Semantic-Product-Search-with-PCA-and-t-SNE-Visualization
Build an AI-powered product search engine using Transformer embeddings, ChromaDB, and visualization with PCA &amp; t-SNE.

# 🛍️ Smart Product Search: How It Works  

Imagine you walk into a store and say to the shopkeeper:  
👉 *“I need a camera for vlogging.”*  

Now, how does our system act like that smart shopkeeper?  

---

## 1️⃣ Transformers: Understanding Context  
We use **Transformer models** (like SentenceTransformer) to process text.  
Unlike older models that looked at words one by one, transformers understand **context**.  

Example:  
- *“Apple” (fruit)* 🍎 ≠ *“Apple” (company)* 💻  
Transformers know the difference because they look at **surrounding words**.  

---

## 2️⃣ Embeddings: Turning Text into Numbers  
Computers can’t understand words directly.  
So, each sentence or product description is converted into a **vector** (a list of numbers) called an **embedding**.  

👉 Think of embeddings as **coordinates on a map**:  
- “Running sneakers” and “Jogging shoes” end up close together.  
- “Headphones” and “Laptop” are far apart.  

This is how the computer “understands” meaning.  

---

## 3️⃣ Vector Database (ChromaDB)  
Once all products are converted into embeddings, we store them in **ChromaDB**.  

💡 Why not a normal database?  
- Normal DBs search by exact **keywords**.  
- ChromaDB searches by **meaning**.  

So even if the query is *“marathon sneakers”*, ChromaDB can match with **Nike Air Zoom** or **Adidas Ultraboost**.  

---


## What Algo runs behind Vetor Database (there are many distance search algorithms - Cosine Similarity is just one of them)

### Cosine Similarity: The Matchmaker 

Now, how does ChromaDB actually decide **which product is closest in meaning**?  

It uses **Cosine Similarity Formula:** 

$$
\text{similarity}(A, B) = \frac{A \cdot B}{||A|| \times ||B||}
$$

Where:  
- **A** = the query embedding (your search as numbers)  
- **B** = a stored product embedding  
- **A · B** = dot product (overlap) between A and B  
- **||A||, ||B||** = lengths of the vectors  

👉 In simple words:  
- If two arrows point in the **same direction**, they mean the same thing.  
- If they point in different directions, they are unrelated.  

**Example:**  

Query = *“running shoes”*  
- Product A: *“marathon sneakers”* → similarity = **0.95** ✅  
- Product B: *“wireless headphones”* → similarity = **0.12** ❌  

So Product A will be ranked higher.  

---

## 4️⃣ PCA vs t-SNE: Visualizing Embeddings  

Embeddings live in **hundreds of dimensions** (far more than humans can imagine).  
To make sense of them, we reduce them into 2D or 3D for visualization.  
That’s where **PCA** and **t-SNE** come in.  

---

### 🔷 PCA (Principal Component Analysis)  
- **What it does**: Finds the main “directions” of variation in the data.  
- This is a technique to reduce the size of embeddings (usually hundreds of dimensions) into just 2 or 3 dimensions so humans can visualize them. PCA keeps the “main patterns” in the data while dropping small details. 
- It’s like compressing a big photo but still being able to see the main picture. 
- Strengths:  
  - Keeps the **global structure** of the data.  
  - Fast and simple.  
- Limitations:  
  - Sometimes spreads apart points that are actually very similar in meaning.  

👉 Example: With PCA, all types of shoes may appear somewhat close,  
but running shoes vs. casual sneakers may not cluster tightly.  

---

### 🔶 t-SNE (t-distributed Stochastic Neighbor Embedding)  
- **What it does**: Focuses on preserving **local neighborhoods**.  
- It ensures that points that were close in high dimensions stay close in 2D.  
- Strengths:  
  - Great at showing **clusters of similar items**.  
  - More human-intuitive: “things that belong together, appear together.”  
- Limitations:  
  - Slower and more computationally heavy.  
  - Sometimes distorts global distances.  

👉 Example: With t-SNE, “running shoes” and “marathon sneakers” will appear very close,  
even if the bigger picture of *all footwear* gets a bit distorted.  

---

### 🧩 How They Work Together  
- **PCA** gives the **big map** — showing how all products are spread out overall.  
- **t-SNE** zooms into **clusters** — showing small groups of very similar items.  

That’s why we often look at **both plots**:  
- PCA → “Where am I in the whole city?” 🗺️  
- t-SNE → “Who are my closest neighbors?” 🏘️  

---

## 5️⃣ The Search Process  

1. User types a query (e.g., *“Best laptop for travel”*).  
2. Transformer converts it into an **embedding**.  
3. ChromaDB compares it with stored product embeddings.  
4. Finds the **closest match**.  
   ✅ *Dell XPS 13 → Lightweight laptop with long battery life.*  

---

## 6️⃣ Why Return Metadata + Description?  
- **Metadata** → Product name (*Dell XPS 13*).  
- **Document** → Product description (*Lightweight laptop with strong performance…*).  

Together, they form a complete human-readable answer.  

---

## 7️⃣ End-to-End Flow  

**User Query → Embedding → ChromaDB → Best Match → Return Metadata + Description**  

---

### 🔑 Summary  
We transformed **text → embeddings → stored in ChromaDB → searched by meaning → returned the best product**.  

And we can even **visualize this “semantic map”** using PCA or t-SNE  
to see how products cluster by meaning.  


Text → Embeddings → Stored in ChromaDB → Searched by Meaning → Best Product Returned ✅
