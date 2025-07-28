#  GitHub Commit Classifier using K-Means Clustering

This project uses **unsupervised machine learning** to automatically categorize GitHub commits into meaningful clusters like `bugfix`, `feature`, `refactor`, `documentation`, etc., by analyzing the textual content of commit messages.

It’s a lightweight but powerful tool to analyze large commit histories and understand contribution trends — useful for productivity analytics, engineering reporting, and smart repo dashboards.

---

## Features

- Pulls commit history from any GitHub repo using the GitHub API
- Preprocesses commit messages with NLP techniques (tokenization, vectorization)
- Applies **K-Means Clustering** to identify natural groupings of commits
- Visualizes cluster distributions using **PCA** or **t-SNE**
- Computes silhouette score and inertia to validate optimal number of clusters
- Supports CSV export of labeled commits

---

## Tech Stack

| Category       | Tools Used                      |
|----------------|---------------------------------|
| Language       | Python                          |
| ML Algorithms  | K-Means Clustering (scikit-learn) |
| NLP            | CountVectorizer / TF-IDF (sklearn) |
| API Access     | GitHub REST API v3              |
| Visualization  | Matplotlib, Seaborn, PCA/t-SNE  |
| Export         | Pandas                          |

---
## Theoretical Background

This project applies **unsupervised machine learning** and **natural language processing (NLP)** to analyze GitHub commit messages and group them into meaningful categories without prior labeling. It leverages real-world development data to uncover latent structures in software version history.

---

### 1. Unsupervised Learning with K-Means

**K-Means Clustering** is a centroid-based algorithm that partitions a dataset into `k` clusters by minimizing the intra-cluster distance. For textual data, each commit message is first converted into a vector space model and then grouped based on semantic similarity.
 

- **Initialization**: Randomly selects `k` centroids
- **Assignment Step**: Assigns each point to the nearest centroid
- **Update Step**: Recomputes centroids as the mean of assigned points
- Repeats until convergence (centroids no longer move significantly)

For this project, `k` is a tunable parameter — optimized using evaluation metrics like **inertia** and **silhouette score**.

---

### 2. Text Preprocessing and Feature Extraction

Since commit messages are short and noisy, effective preprocessing is crucial:

- **Tokenization**: Splits message into meaningful words
- **Stopword Removal**: Eliminates uninformative words like "the", "is", etc.
- **Vectorization**:
  - Uses **TF-IDF (Term Frequency-Inverse Document Frequency)** or **CountVectorizer**
  - Converts text into numerical vectors based on word importance

This transforms a list of strings into a matrix of real-valued feature vectors suitable for K-Means.

---

### 3. Dimensionality Reduction for Visualization

High-dimensional vectors (from TF-IDF) are reduced to 2D for visualization using:

- **PCA (Principal Component Analysis)**: Projects data onto directions of maximum variance
- **t-SNE** (optional): Preserves local structures and visual clusters more clearly

This helps in visualizing clusters in a 2D plot, revealing how different types of commits group together.

---

### 4. Cluster Evaluation

Since there are no labels (unsupervised), we evaluate clustering quality using:

- **Inertia**: Sum of squared distances between samples and their nearest cluster center (lower is better)
- **Silhouette Score**: Measures cohesion and separation of clusters  
  \[
  \text{Silhouette} = \frac{b - a}{\max(a, b)}
  \]
  Where:
  - `a` = intra-cluster distance
  - `b` = nearest-cluster distance

Both metrics help determine a good `k` (number of clusters).

---

###  5. Real-World Data Integration via GitHub API

The commit data is sourced live using the **GitHub REST API**, enabling:

- Dynamic access to commit history from any public repo
- Fresh, diverse textual data across domains and coding styles
- Realistic application of NLP + ML to actual development logs

---

### Why It Matters

- Identifying latent commit patterns helps developers understand project evolution
- Lays the foundation for **auto-tagging**, **release summaries**, and **commit analysis tools**
- Demonstrates a powerful use of **AI in software engineering workflows**
- Fully software-based — no simulation or hardware required

---

## How It Works

1. **Commit Extraction**  
   - Connects to a public GitHub repository using your GitHub token  
   - Fetches latest N commit messages via REST API

2. **Text Preprocessing**
   - Lowercasing, stopword removal
   - Converts messages into numerical feature vectors via `TF-IDF` or `CountVectorizer`

3. **Unsupervised Learning**
   - Applies **K-Means** to cluster commits into unlabeled categories
   - You can experiment with different values of `k` (number of clusters)

4. **Evaluation**
   - Computes **Silhouette Score** and **Inertia** to measure cluster cohesion
   - Optionally reduces features to 2D using **PCA** or **t-SNE** for visualization

5. **Visualization**
   - Scatterplot of clustered commits in 2D space
   - Bar chart of commit count per cluster

---

## Sample Output
### Message Clusters (PCA Projection)
<img width="503" height="658" alt="Screenshot 2025-07-29 at 2 24 16 AM" src="https://github.com/user-attachments/assets/140afaaa-7e82-429c-b444-db9db26dc2be" />
<img width="503" height="435" alt="Screenshot 2025-07-29 at 2 24 26 AM" src="https://github.com/user-attachments/assets/2b2ac383-a78b-4012-887b-de8494569405" />


### Cluster Distribution 


<img width="806" height="550" alt="Screenshot 2025-07-29 at 2 17 53 AM" src="https://github.com/user-attachments/assets/63232711-89af-400e-9972-2d58855527b4" />



---
## Use Cases
- Smart engineering productivity dashboards
- Analyze large open-source repos to find trends
- Training data for supervised commit classifiers
- GitHub Actions integration for auto-tagging commits
## Future Work
- Integrate LDA or DBSCAN for alternate clustering
- Add support for multilingual commit messages
- Train a supervised classifier based on these clusters
- Streamlit dashboard for interactive commit browsing

## Installation & Setup

```bash
git clone https://github.com/yourusername/github-commit-clusterer.git
cd github-commit-clusterer
pip install -r requirements.txt


