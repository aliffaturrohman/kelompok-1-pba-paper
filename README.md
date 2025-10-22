[![Python Version](https://img.shields.io/badge/python-3.12-blue)](https://www.python.org/)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Build Status](https://img.shields.io/badge/build-passing-brightgreen)]()
[![Coverage](https://img.shields.io/badge/coverage-95%25-brightgreen)]()

# Text Summarization Berita DAMRI

Proyek ini bertujuan untuk melakukan **text summarization otomatis** terhadap berita-berita mengenai Perum DAMRI dari berbagai sumber daring. Proses meliputi tahapan **scraping data**, **preprocessing**, **embedding berbasis MiniLM**, serta pembuatan ringkasan (summary) dengan dua pendekatan:

- **Semantic Similarity** (MiniLM)
- **TF-IDF Extractive Summarization)


## Workflow Proyek

```mermaid
flowchart LR
    A["Mulai: Input CSV dengan URL Berita DAMRI"] --> B["Load Data CSV dengan Pandas"]
    B --> C["Scraping Konten Web menggunakan Trafilatura & Requests"]
    C --> D["Handle Error & Filter Artikel Valid"]
    D --> E["Preprocessing Teks"]
    E --> E1["Membersihkan HTML & Hapus Noise Cookies, Advertisement, dll."] & E2["Tokenisasi Kalimat dengan NLTK"]
    E2 --> F["Semantic Embedding"] & G["TF-IDF Extractive Summarization"]
    F --> F1["Gunakan MiniLM untuk encode kalimat"]
    F1 --> F2["Hitung cosine similarity antar kalimat"]
    F2 --> F3["Select Top N kalimat untuk summary"]
    G --> G1["Hitung TF-IDF tiap kalimat"]
    G1 --> G2["Pilih Top N kalimat berdasarkan skor TF-IDF"]
    F3 --> H["Output: Summary Semantic Similarity"]
    G2 --> I["Output: Summary TF-IDF"]
    H --> J["Simpan hasil summary ke CSV"]
    I --> J
    J --> K["Selesai"]
````


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
```


## Instalasi

1. **Clone repository**:

```bash
git clone https://github.com/aliffaturrohman/kelompok-1-pba-paper.git
cd kelompok-1-pba-paper
```

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

## Menjalankan Scraping dan Summarization

1. **Pastikan file CSV input tersedia**:

```
data/data_raw/Kelompok1_Link Berita_DAMRI - Data.csv
```

2. **Jalankan notebook `damri_article.ipynb`** langkah demi langkah (Data Loading, Scraping, Preprocessing, Embedding & Summarization).

3. **Hasil akhir** disimpan di:

```
data/data_processed/data_extraction_minilm_summary.csv
data/data_processed/data_extraction_summary[full].csv
```

## Tim Pengembang

| Nama                     | Departemen          |
| ------------------------ | ------------------- |
| Alif Faturrohman         | Information Systems |
| Yeremia Maydinata Narana | Information Systems |
| Achmad Fahmi Ainur Ridho | Information Systems |
