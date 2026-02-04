# RACT

**Retrieval Augmented Column-Table Learning and Prediction for Multi-Table Schema Matching**

RACT exploits referential context into schema matching by introducing RACT learning and prediction, a self-supervised framework enabling the probabilistic retrieval of candidate tables for source columns to constrain relevant column candidates. The research project implements the following phases:

- **(a.I-II) Retrieval Augmented Columns** using view path traversals from relational schema tables (nodes) and reference constraints (edges) represented as a directed graph.
- **(a.III) Schema-Aware Column Representations** extending classical column serializations (with sentence transformers for matching via semantic similarity) with strong and weak tables of a columns' host table (SerReference).
- **(b) Self-Supervised Column-Table Learning** using Single (b.I), Pairwise (b.II), or Holistic (b.III) schema as input. (b.II-III) use masked loss for simultaneous shared space learning. 
- **(c) Column-Table Prediction** applying the learned models to effectively retrieve table candidates from columns in other schemas. 

## Main Project: RACT.ipynb

Dependencies:
- Python 3.8 or higher with Jupyter Notebook
- Core dependencies: pandas, numpy, SciPy, scikit-learn, NetworkX (graphs), TensorFlow, Keras, Sentence Transformers (Semantic similarity) and FAISS (ANNs)

Notebook Outline:
- 1: Libraries
- 2: Dataset (schema elements, schema matches, referential constraints)
- (A): Retrieval Augmented Columns
- (B): Self-Supervised Column-Table Learning
  - (B.I): Single Model with Prediction (C) and Evaluation (E1-3)
  - (B.II): Pairwise Model with Prediction (C) and Evaluation (E1-3)
  - (B.III): Holistic Model with Prediction (C) and Evaluation (E1-3)
- 3: Impact Study Serialization SerSchema, SerValues, (Reference Magneto: https://dl.acm.org/doi/abs/10.14778/3742728.3742757), SerReference for Blocking and Matching
- 4: ReMatch Target Table Retrieval (Baseline: https://arxiv.org/abs/2403.01567) and Evaluation

Evaluation (E):
1. top-k-table @recall
2. top-k-column @mean Average Precision (mAP)
3. top-k-column @recall 

## Data

The project evaluates curated matching scenarios between the following public schemas:
1. Oracle sample schemas: https://github.com/oracle-samples/db-sample-schemas
2. Classicmodels (MySQL tutorial schema): https://www.mysqltutorial.org/getting-started-with-mysql/mysql-sample-database/
3. TPCH https://www.tpc.org/TPCH/ implemented at scale-factor=1 via DuckDB
4. Sakila (MySQL sample schema): https://dev.mysql.com/doc/Sakila/en/


- `data/dataset.csv` - Schema elements (columns, tables) with metadata.
- `data/joinable_paths.csv` - Referential constraints (foreign-primary key) between tables in a schema.
- `data/joinable_paths_ids.csv` - Mapped to ids of schema elements.
- `data/matches.csv` - Ground truth schema matches for evaluation.

Raw schemas used in experiments can be found at: [THKoeln-ICCT-BigDataAnalytics/DataIntegration](https://github.com/THKoeln-ICCT-BigDataAnalytics/DataIntegration/tree/main/data/raw_schemas)

## Contact

For any questions on set up or implementation, please contact leonard.traeger@umbc.edu :-)
