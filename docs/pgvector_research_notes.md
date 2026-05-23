# pgvector Research Notes
## 1. Architectural Context: Why pgvector?
Choosing `pgvector` for the Storage Layer (combining both the Structured Data Store and the Vector Database within PostgreSQL) is a highly optimal architectural decision. It significantly reduces the complexity of ETL/ELT pipelines by eliminating the need to synchronize data between a traditional relational database (used for metadata) and a separate, standalone vector database.

## 2. What is pgvector?
`pgvector` is an open-source extension for PostgreSQL. It enables the storage of vectors (often referred to as embeddings generated from Machine Learning / Deep Learning models) and allows you to perform similarity search queries directly inside PostgreSQL using familiar SQL syntax.

An embedding is a vector (list) of floating point numbers. The distance between two vectors measures their relatedness. Small distances suggest high relatedness, and large distances suggest low relatedness.

## 3. Core Components: Data Types & Operators
When data flows in from the Embedding Generation step (in the Processing & AI Layer), it needs to be stored using a specific data type.

### Data Type
* **`vector`**: Defines a fixed number of dimensions for the column. 

### Distance Metrics (Operators)
To find similar vectors (which is essential for the RAG Pipeline), `pgvector` supports primary distance metrics:
<-> - L2 distance
<#> - (negative) inner product
<=> - cosine distance
<+> - L1 distance
<~> - Hamming distance (binary vectors)
<%> - Jaccard distance (binary vectors) 

## 4. Installation - Read in Github
Ensure C++ support in Visual Studio is installed and run **x64 Native Tools Command Prompt for VS [version]** as administrator. Then use `nmake` to build:

```cmd
set "PGROOT=C:\Program Files\PostgreSQL\18"
cd %TEMP%
git clone --branch v0.8.2 [https://github.com/pgvector/pgvector.git](https://github.com/pgvector/pgvector.git)
cd pgvector
nmake /F Makefile.win
nmake /F Makefile.win install

