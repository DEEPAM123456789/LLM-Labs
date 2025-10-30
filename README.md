# 🧠 Quora Question Pairs — Semantic Similarity Project

This project explores **semantic textual similarity** using **SBERT embeddings**, **cosine similarity**, and **unsupervised visualization (UMAP + HDBSCAN)** on the **Quora Question Pairs (QQP)** dataset.

The primary goal was **to intuitively understand how embedding-based models capture semantic meaning**, rather than building a production-ready app.

---

## 🚀 Project Overview

### **A. Similarity Checker (Main Use)**

1. **Dataset:** Picked 100K samples from **Quora Question Pairs (QQP)** dataset.  
2. **Objective:** Check whether two questions are semantically similar (duplicate or not).  
3. **Embedding Model:**  
   - Used `sentence-transformers/all-MiniLM-L6-v2` (SBERT)  
   - Encoded both `question1` and `question2`  
4. **Similarity Metric:**  
   - Computed **cosine similarity** between the two embeddings  
   - Compared similarity scores with ground truth label (`1 = duplicate`)  
5. **Evaluation:**  
   - Mean similarity (duplicates) ≈ **0.73**  
   - Mean similarity (non-duplicates) ≈ **much lower (~0.4–0.5)**  
   - Base model score improved from **0.55 → 0.73** after fine-tuning on 100K samples  
6. **Threshold Selection:**  
   - Found that a threshold around `0.75` effectively distinguishes duplicates.  
   - `(similarity > 0.75 → semantically similar)`  

✅ **Outcome:** Built a solid intuition for **semantic similarity scoring** using embeddings.

---

### **B. FAQ Search (Optional Adaptation)**

We creatively reused QQP as a **FAQ Retrieval System**:

- Treated all `question2` as the **FAQ corpus**.  
- Given a query (a `question1`), used **FAISS** to find the **most semantically similar question2**.  
- Returned that as *“the most related question.”*

This mimics a **semantic FAQ retriever**, powered by **vector similarity search**.

🧩 *Mechanically identical to real-world RAG / FAQ retrieval systems.*

---

### **C. Visualization (Optional but Insightful)**

To visualize how embeddings cluster semantically:

1. **Selected** 500 balanced pairs (250 duplicates + 250 non-duplicates)  
2. **Generated embeddings** for all unique questions.  
3. **Reduced dimensions** using **UMAP (2D)** for interpretability.  
4. **Clustered** embeddings using **HDBSCAN** to detect semantic clusters.  
5. **Visualization:**
   - **Blue points** → duplicate pairs (semantically close)  
   - **Red/Grey points** → non-duplicates or outliers  
   - Clear **clusters formed** for thematically similar questions (e.g., all “New Year resolutions” together).  

📊 **Techniques Used:**
- `UMAP` (for non-linear dimensionality reduction)
- `HDBSCAN` (for density-based clustering)
- `Matplotlib` (for visualization)

---

## 🧩 Tech Stack

| Category | Tools / Libraries |
|-----------|------------------|
| Language | Python |
| NLP Model | [Sentence-Transformers: all-MiniLM-L6-v2](https://www.sbert.net/) |
| Similarity | Cosine Similarity |
| Clustering | HDBSCAN |
| Dimensionality Reduction | UMAP |
| Visualization | Matplotlib |
| Vector Search (Optional) | FAISS |
| Data Handling | Pandas, NumPy |

---

## 📈 Results Summary

| Metric | Base Model | Fine-Tuned Model |
|---------|-------------|-----------------|
| Mean Similarity (duplicates) | 0.55 | **0.73** |
| Mean Similarity (non-duplicates) | ~0.40 | ~0.45 |
| Threshold | 0.75 | 0.75 |
| Visualization | Clear semantic clusters via UMAP |

✅ **Interpretation:**  
After fine-tuning, the embeddings clearly separated duplicate and non-duplicate pairs in both numeric similarity and visualization space.

---

## 🧪 Learning Outcomes

- Gained strong intuition for **embedding-based similarity**.
- Learned how to **quantify semantic relationships** with cosine similarity.
- Understood **UMAP + HDBSCAN** for unsupervised semantic clustering.
- Practiced **FAISS vector retrieval** for semantic search setups.
- Developed complete understanding of **SBERT pipelines** (encoding → similarity → visualization).


---

## 🧰 Installation

```bash
git clone https://github.com/<your-username>/QQP-Semantic-Similarity.git
cd QQP-Semantic-Similarity

pip install -r requirements.txt
```
