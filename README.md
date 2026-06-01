# -Arxiv-paper-summarizer
# 📄 arXiv Paper Summarizer

Automatically fetch research papers from [arXiv](https://arxiv.org/) and generate concise AI-powered summaries using a transformer model — all saved to a clean CSV file.

---

## 🚀 Features

- 🔍 Fetches up to **200 papers** from arXiv on any topic
- 🤖 Summarizes abstracts using **DistilBART** (distilbart-cnn-12-6)
- 📊 Exports results to a structured **CSV file**
- ⚡ Progress bar via `tqdm` for real-time feedback
- 🛠️ Configurable query, result count, and sorting

---

## 📁 Project Structure

```
arxiv-paper-summarizer/
│
├── arxiv_summarizer.ipynb      # Main Jupyter notebook
├── requirements.txt            # Python dependencies
├── .gitignore                  # Files to exclude from Git
├── LICENSE                     # MIT License
└── README.md                   # Project documentation
```

---

## 🧰 Requirements

- Python 3.8+
- Google Colab *(recommended)* or a local Jupyter environment with GPU support

---

## ⚙️ Setup & Usage

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/arxiv-paper-summarizer.git
cd arxiv-paper-summarizer
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Run the notebook

Open `arxiv_summarizer.ipynb` in **Google Colab** or **Jupyter Lab** and run all cells.

### 4. Configure your query

In the **Fetch Papers** cell, change the query and result count:

```python
query = "machine learning"   # 🔁 Change to any topic
max_results = 200            # 🔁 Change as needed
```

### 5. Output

After running, a file named `arxiv_summaries.csv` will be saved with these columns:

| Column | Description |
|---|---|
| `title` | Paper title |
| `authors` | Comma-separated author names |
| `published` | Publication date |
| `pdf` | Direct PDF link |
| `summary_generated` | AI-generated summary |

---

## 🐛 Common Issues

**Only getting ~20 results instead of 200?**

This happens because the default `arxiv.Client()` uses `page_size=10`. The notebook uses the fixed version:

```python
client = arxiv.Client(
    page_size=100,
    delay_seconds=3,
    num_retries=5
)
```

**Slow summarization?**
Enable GPU in Colab: `Runtime → Change runtime type → T4 GPU`

---

## 🧠 Model Used

| Property | Value |
|---|---|
| Model | `sshleifer/distilbart-cnn-12-6` |
| Task | Summarization |
| Framework | HuggingFace Transformers |
| Input limit | 800 characters per abstract |
| Output | 30–120 tokens per summary |

---

## 📦 Dependencies

```
arxiv
transformers==4.41.1
torch
accelerate
sentencepiece
pandas
tqdm
```

---

## 📜 License

This project is licensed under the [MIT License](LICENSE).

---

## 🙌 Acknowledgements

- [arXiv API](https://arxiv.org/help/api/) for open access to research papers
- [HuggingFace Transformers](https://huggingface.co/docs/transformers) for the summarization pipeline
- [sshleifer/distilbart-cnn-12-6](https://huggingface.co/sshleifer/distilbart-cnn-12-6) for the pre-trained model
