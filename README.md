# Locality Sensitive Hashing for Document Similarity

A repository for finding similar documents using **Locality Sensitive Hashing (LSH)**.
This project involves reading a dataset of **48,505 articles**, applying **shingling and minhashing**, and using **band hashing** to efficiently detect similar documents.

## Project Structure

- **LSH-Document-Similarity.ipynb**: Jupyter Notebook implementing the full pipeline, including data preprocessing, hashing, and similarity detection.
- **Datasets**:
  - `articles.json`: Contains 48,505 articles with their content and metadata.
  - `submissions.csv`: Final output file with nearest neighbors for each document.
- **Report.pdf**: Explanation of the approach, results, and findings.

## Technologies Used

- Python
- Pandas & NumPy
- NLTK (for n-grams processing)
- SciPy (for sparse matrix representation)
- Matplotlib & Seaborn (for visualization)

## Steps to Implement

1. **Read the Data**
   - Load JSON articles.
   - Clean text (remove punctuation, convert to lowercase).

2. **Shingle the Documents**
   - Generate **2-grams (bigrams)** for each article (can experiment with other n-values).
   - Convert n-grams into a binary vector representation.

3. **Convert n-grams to Binary Vectors**
   - Select the top **10,000 most frequent n-grams** (optional optimization).
   - Represent documents as **sparse matrices** using `scipy.sparse.csr_matrix`.

4. **Generate Hash Functions**
   - Create multiple hash functions to map n-grams into buckets.
   - Use different techniques: `hash(value) % num_buckets`, XOR with random integers, etc.

5. **Compute MinHash Signatures**
   - Use a faster algorithm from the lecture notes.
   - Generate a signature matrix for all documents.

6. **Band Hashing**
   - Divide MinHash signatures into bands.
   - Hash each band into buckets to group candidate similar documents.

7. **Tune Parameters**
   - Experiment with different **band sizes** and **hash functions**.
   - Plot the probability of similar articles falling into the same bucket.

8. **Find Nearest Neighbors**
   - Use **Jaccard Similarity** to refine candidate pairs.
   - Store nearest neighbors in `submissions.csv`.

## How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/YOUR_USERNAME/LSH-Document-Similarity.git
   cd LSH-Document-Similarity
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Run the Jupyter Notebook:
   ```bash
   jupyter notebook LSH-Document-Similarity.ipynb
   ```

## Results & Report

- The final output file, `submissions.csv`, contains each article's **nearest neighbors**.
- The **Report.pdf** explains the methodology, optimizations, and results.

## Acknowledgments

- This project follows the **Locality Sensitive Hashing** approach from the lecture materials.
- Thanks to the course instructor for providing the dataset and guidance.
