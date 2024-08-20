# DSI_information_retrivial: Two-Stage Document Retrieval System

This repository contains the implementation of a two-stage document retrieval model designed to improve retrieval accuracy and efficiency using the MSMARCO dataset. The approach combines clustering techniques with sequence-to-sequence models to enhance document retrieval performance, particularly in large datasets.

## Overview

This project presents a novel two-stage model approach to document retrieval:

1. **Cluster Predictor Model**: Uses the all-MiniLM-L6-v2 model to cluster documents into semantic groups, significantly reducing the search space.
2. **Refinement Model**: A sequence-to-sequence (seq2seq) model, built on the T5 architecture, that refines the search within the predicted cluster to retrieve the most relevant document.

## Dataset

The model is trained and evaluated using the MSMARCO dataset, which consists of real, anonymized user queries from Bing along with relevant passages:

- **Training Set**: 80,000 query-document pairs
- **Testing Set**: 18,000 pseudo-query-document pairs
- **Evaluation Set**: 2,000 pseudo-query-document pairs

The testing and evaluation sets are sampled from the training set to ensure consistency.

## Methodology

### Preprocessing and Data Augmentation

- **Tokenization**: Queries and documents are tokenized using the all-MiniLM-L6-v2 and T5 tokenizers.
- **Clustering**: Documents are embedded using the all-MiniLM-L6-v2 model and clustered into 2,000 clusters using KMeans.
- **Pseudo-Queries**: Generated using the doc2query/all-t5-base-v1 model, ensuring consistency between the documents seen during training and evaluation.

### Models

#### Cluster Predictor Model

- Embeds queries into dense vectors using the all-MiniLM-L6-v2 model.
- Predicts cluster IDs to assign queries to the most relevant document cluster.

#### Refinement Model

- Built on the T5-small architecture.
- Refines the search within the predicted cluster to generate the doc_id of the most relevant document.

### Inference Process

- **Beam Search**: Utilized during inference to enhance the quality of the generated doc_id sequences.

### Baseline Comparison

- A baseline comparison is provided using the BM25 retrieval model implemented through the Pyserini library.

## Experimental Setup and Results

### Evaluation Metrics

The model is evaluated using the following metrics:

- **Mean Average Precision (MAP)**
- **Set_MAP**
- **Precision at K (P@K)**

### Results

Preliminary experiments showed that the proposed model needs further training to perform competitively with the BM25 baseline. However, the conceptual framework demonstrates potential, especially with sufficient training resources.


### Installation

Clone this repository:

```bash
git clone https://github.com/Feedback02/DSI_information_retrivial.git
