# Keyphrase Ranking with Submodular Function Optimization (SFO)

The source code for Keyphrase Ranking with SFO paper accepted in KDBC 2024

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
| Inspec   | SFO       | 19.29  | **0.8277**  | **0.8144**  | **0.3656**              |
|          | EmbedRank++   | **61.85**      | 0.5633  | 0.7326  | 0.1882              |
|          | SIFRank       | 65.00      | 0.3464  | 0.6807  | 0.6443              |
|          | DPP           | 62.43      | 0.2128  | 0.3734  | 1.2433              |
| NUS      | SFO       | 20.98  | 0.8619  | **0.7867**  | **2.3251**              |
|          | EmbedRank++   | **74.18**      | 0.7634  | 0.3836  | 7.1397              |
|          | SIFRank       | 66.53      | 0.3069  | 0.6034  | 19.2913             |
|          | DPP           | 31.95      | 0.1950  | 0.3081  | 1.8312              |
| SemEval  | SFO       | 16.90  | 0.8640  | **0.7345**  | **2.4978**              |
|          | EmbedRank++   | **77.05**      | 0.7408  | 0.3798  | 7.4637              |
|          | SIFRank       | 66.66      | 0.2908  | 0.4615  | 20.6732             |
|          | DPP           | 23.82      | 0.2015  | 0.4618  | 2.0910              |


These results demonstrate that SFO outperforms the baselines in diversity measures with competitive runtime efficiency.

## Citation

If you find this work helpful in your research, please cite our paper:

```bibtex
@misc{umair2024optimizingkeyphraserankingrelevance,
      title={Optimizing Keyphrase Ranking for Relevance and Diversity Using Submodular Function Optimization (SFO)}, 
      author={Muhammad Umair and Syed Jalaluddin Hashmi and Young-Koo Lee},
      year={2024},
      eprint={2410.20080},
      archivePrefix={arXiv},
      primaryClass={cs.IR},
      url={https://arxiv.org/abs/2410.20080}, 
}
```

