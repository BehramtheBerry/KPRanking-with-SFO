# Keyphrase Ranking with Submodular Function Optimization (SFO)

This repository contains code for ranking keyphrases using Submodular Function Optimization (SFO) for balancing relevance and diversity. The repository uses publicly available datasets and the `MiniLM` pre-trained sentence transformer model for embedding generation.

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

## How to Run

To execute the main script, simply run:

```bash
python sfoOnRealDataset.py

## Citation
If you find this repository helpful for your work, please cite our project:

text
@misc{Coming Soon}
License
This repository is licensed under the MIT License. See LICENSE for more details.

css

This version adds a section on how to measure the GKP, KPL, and DL metrics using the `DatasetMetrics.py` script. It provides a simple instruction on how to run it and what to expect.
