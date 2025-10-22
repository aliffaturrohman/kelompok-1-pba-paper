[![Python Version](https://img.shields.io/badge/python-3.12-blue)](https://www.python.org/)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Build Status](https://img.shields.io/badge/build-passing-brightgreen)]()
[![Coverage](https://img.shields.io/badge/coverage-95%25-brightgreen)]()

# Text Summarization Berita DAMRI

Proyek ini bertujuan untuk melakukan **text summarization otomatis** terhadap berita-berita mengenai Perum DAMRI dari berbagai sumber daring. Proses meliputi tahapan **scraping data**, **preprocessing**, **embedding berbasis MiniLM**, serta pembuatan ringkasan (summary) dengan dua pendekatan:

- **Semantic Similarity** (MiniLM)
- **TF-IDF Extractive Summarization**

---

## Struktur Folder

```

kelompok-1-pba-paper/
│
├─ data/
│   ├─ data_raw/
│   │   └─ Kelompok1_Link Berita_DAMRI - Data.csv
│   └─ data_processed/
│       ├─ scraped_articles.csv
│       ├─ data_extraction_minilm_summary.csv
│       ├─ data_extraction_summary[full].csv
├─ venv/
├─ damri_article.ipynb
├─ requirements.txt
├─ README.md
└─ .gitignore

````

---

## Instalasi

1. **Clone repository**:

```bash
git clone https://github.com/aliffaturrohman/kelompok-1-pba-paper.git
cd kelompok-1-pba-paper
````

2. **Buat virtual environment**:

```bash
python -m venv venv
source venv/bin/activate  # Linux / WSL
# atau
venv\Scripts\activate     # Windows
```

3. **Install dependencies**:

```bash
pip install --upgrade pip
pip install -r requirements.txt
```

---

## Menjalankan Scraping dan Summarization

1. **Pastikan file CSV input tersedia**:

```
data/data_raw/Kelompok1_Link Berita_DAMRI - Data.csv
```

dataset ini memiliki dua kolom:

* `link` : URL berita
* `sumber` : Nama sumber berita

2. **Jalankan notebook `damri_article.ipynb`** langkah demi langkah:

* **Data Loading** : Membaca CSV input
* **Scraping** : Mengambil konten berita menggunakan `trafilatura`
* **Preprocessing** : Membersihkan teks dan tokenisasi kalimat
* **Embedding & Summarization** :

  * Semantic Similarity (MiniLM)
  * TF-IDF Extractive Summarization

3. **Hasil akhir** disimpan di:

```
data/data_processed/data_extraction_minilm_summary.csv
data/data_processed/data_extraction_summary[full].csv
```

---

## Ringkasan Teknis

* **Scraping** : Menggunakan `requests` dan `trafilatura` untuk ekstraksi teks bersih dari HTML.
* **Cleaning** : Menghapus kata umum yang tidak relevan (`Cookies`, `Iklan`, dll.) menggunakan `BeautifulSoup` dan regex.
* **Tokenisasi** : NLTK `sent_tokenize`
* **Semantic Embedding** : `sentence-transformers` MiniLM (`all-MiniLM-L6-v2`)
* **Similarity-Based Summarization** : Menggunakan cosine similarity antar kalimat
* **TF-IDF Summarization** : Mengambil kalimat dengan skor TF-IDF tertinggi

---

## Contoh Penggunaan

```python
from damri_article import summarize_text, tfidf_summarize

# Contoh ringkasan semantic similarity
summary_semantic = summarize_text(sentences_list, model, top_n=3)

# Contoh ringkasan TF-IDF
summary_tfidf = tfidf_summarize(article_text, num_sentences=3)
```

---

## Catatan

* Disarankan menggunakan **Python 3.12+**
* Untuk proyek besar, pastikan **RAM cukup** saat melakukan embedding menggunakan MiniLM
* Semua CSV hasil proses akan **ditimpa** jika dijalankan ulang, jadi backup jika diperlukan

## Tim Pengembang

| Nama | Departemen |
|------|------------|
| Alif Faturrohman | Information Systems |
| Yeremia Maydinata Narana | Information Systems |
| Achmad Fahmi Ainur Ridho | Information Systems |
