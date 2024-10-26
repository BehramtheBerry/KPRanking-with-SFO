# Keyphrase Ranking with Submodular Function Optimization (SFO)

This repository contains code for ranking keyphrases using Submodular Function Optimization (SFO) to balance relevance and diversity. It uses publicly available datasets and the `MiniLM` pre-trained sentence transformer model for embedding generation.

![Architecture](https://github.com/user-attachments/assets/1c6d6720-cbc7-41a0-a28c-3cf7b1cb936b)



## Datasets

We have used the following datasets for this project:

1. **Inspec Dataset**: [Link to Inspec Dataset](https://huggingface.co/datasets/memray/inspec/viewer/default/test?row=2)
2. **NUS Dataset**: [Link to NUS Dataset](https://huggingface.co/datasets/memray/nus/viewer/default/test)
3. **SemEval Dataset**: [Link to SemEval Dataset](https://huggingface.co/datasets/memray/semeval/viewer/default/test)

## Pre-trained Model

We use `MiniLM` for sentence embeddings. You can find more information about the model here:

- [MiniLM Model on HuggingFace](https://huggingface.co/sentence-transformers/all-MiniLM-L6-v2)

## Installation

To run this project locally, follow these steps:

1. Clone the repository:

    ```bash
    git clone https://github.com/yourusername/KPRanking-with-SFO.git
    cd KPRanking-with-SFO-main
    ```

2. Create a virtual environment and activate it:

    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    ```

3. Install the dependencies:

    ```bash
    pip install -r requirements.txt
    ```

4. Download the datasets (or the datasets will be automatically fetched via HuggingFace datasets library).

## Measuring Dataset Metrics

If you want to measure the following metrics for your own dataset:

- **GKP**: Average Number of Gold Keyphrases per document (title, abstract, full text)
- **KPL**: Average Keyphrase Length
- **DL**: Average Document Length (in words)

You can use the script `DatasetMetrics.py` provided in this repository. To run this script:

```bash
python DatasetMetrics.py --dataset <dataset_name>
```

## How to Run

To execute the main script, simply run:

```bash
python sfoOnRealDataset.py
```

## Pseudocode for SFO Keyphrase Ranking

The following pseudocode outlines our Submodular Function Optimization (SFO) approach for balancing relevance and diversity in keyphrase selection.

![image](https://github.com/user-attachments/assets/64ef3be6-7296-4d1e-b362-c40db44cc91b)

Here:
- 𝑉 is the set of candidate keyphrases.
- 𝑁 is the desired number of keyphrases.
- 𝛼 is a parameter that adjusts the balance between relevance and diversity.

## Experimental Results

Our model was evaluated on three datasets, comparing F1-Score@5, Intra-List Distance (ILD), Subtopic Recall (SR), and average runtime against three baselines: EmbedRank++, SIFRank, and DPP. The performance of our method in each metric is summarized below.

| Dataset  | Method        | F1-Score@5 | ILD   | SR    | Runtime per Doc (s) |
|----------|---------------|------------|-------|-------|----------------------|
| Inspec   | **SFO**       | **32.46**  | 0.77  | 0.85  | 0.3656              |
|          | EmbedRank++   | 29.88      | 0.73  | 0.78  | 0.1882              |
|          | SIFRank       | 28.49      | 0.77  | 0.84  | 0.6443              |
|          | DPP           | 30.42      | 0.74  | 0.80  | 1.2433              |
| NUS      | **SFO**       | **41.72**  | 0.86  | 0.79  | 2.3251              |
|          | EmbedRank++   | 37.09      | 0.76  | 0.38  | 7.1397              |
|          | SIFRank       | 36.77      | 0.31  | 0.60  | 19.2913             |
|          | DPP           | 36.80      | 0.20  | 0.31  | 1.8312              |
| SemEval  | **SFO**       | **44.43**  | 0.86  | 0.73  | 2.4978              |
|          | EmbedRank++   | 38.40      | 0.74  | 0.38  | 7.4637              |
|          | SIFRank       | 38.82      | 0.29  | 0.46  | 20.6732             |
|          | DPP           | 40.31      | 0.20  | 0.46  | 2.0910              |

These results demonstrate that SFO outperforms the baselines in F1-Score@5 and diversity measures, with competitive runtime efficiency.

