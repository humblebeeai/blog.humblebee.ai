---
date:
  created: 2025-11-29T15:00:00+09:00
  updated: 2025-11-29T16:50:00+09:00
authors:
  - mirsaidl
categories:
  - Tech Blog
tags:
  - Uzbek NLP
  - LLM Training
  - Instruction Datasets
  - Cross-lingual AI
  - Machine Translation
---

# **The State of Uzbek Data for AI**

**A Comprehensive Overview of Open-Source Uzbek Datasets and Their Roles in LLM Development**

## **1\. Introduction**

As artificial intelligence continues to reshape industries worldwide, language remains the foundation of intelligent systems. For Uzbekistan, the future of AI depends on the ability of models to understand, reason, and communicate in **Uzbek**—a rich language with a rapidly digitalizing presence but still limited representation in machine learning datasets.

<!-- more -->

While English, Chinese, and other models benefit from vast open corpora, Uzbek data remains **fragmented and under-structured**. This article provides a detailed exploration of available Uzbek datasets, classifies them by type, and explains how each class contributes to building modern large language models (LLMs) and NLP models. It also presents an **exploratory data analysis (EDA)** of open-source Uzbek data to identify what exists today and what is still missing for true Uzbek AI capability.

## **2\. Why Uzbek Data Matters**

Training a large language model is not only about collecting words \- it is about teaching **language comprehension, task understanding, and reasoning**. Each category of dataset serves a distinct function in that process:

* **Raw text corpora** teaches grammar, structure, and contextual flow.  
* **Instruction datasets** teach models to follow human directions and respond appropriately.  
* **Chain-of-Thought (CoT) data** develop step-by-step reasoning and explainable logic.  
* **Annotated datasets** train and evaluate specific skills such as classification or information extraction.  
* **Evaluation datasets** are used to **measure performance** across language understanding, reasoning, and instruction-following tasks. They provide standardized benchmarks for comparing LLMs.

Understanding how much data exists in each category helps organizations and researchers design the next generation of Uzbek-capable AI systems.

## **3\. Classes of Uzbek Data**

Based on an examination of open repositories such as Hugging Face, Mendeley Data, and academic corpora, Uzbek data can be grouped into **four principal classes**:

| Class | Description | Representative Datasets | Primary Use in Model Training |
| ----- | ----- | ----- | ----- |
| **Raw Text Corpora** | Unstructured collections of text (books, news, and web pages). | [*Tahrirchi/uz-crawl*](https://huggingface.co/datasets/tahrirchi/uz-crawl), [*murodbek/uz-books*](https://huggingface.co/datasets/murodbek/uz-books) | Pretraining: builds fundamental Uzbek grammar, syntax, and style. |
| **Instruction Datasets** | Prompt-response examples showing how to follow user instructions. | [*UAzimov/uzbek-instruct-llm*](https://huggingface.co/datasets/UAzimov/uzbek-instruct-llm), [*Behbudiy/alpaca-cleaned-uz*](https://huggingface.co/datasets/behbudiy/alpaca-cleaned-uz), [*Behbudiy/translation-instruction*](https://huggingface.co/datasets/behbudiy/translation-instruction) | Supervised fine-tuning: teaches task execution and conversational behavior. |
| **Chain-of-Thought (CoT) Data** | Multi-step reasoning traces showing how conclusions are reached. | *(No publicly available Uzbek dataset yet)* | Reasoning fine-tuning: trains logical, interpretable problem solving. |
| **Annotated / Task-Specific Data** | Labeled datasets for NLP tasks (e.g., sentiment, NER, semantic similarity). | [*Behbudiy/uzbek-sentiment-analysis*](https://huggingface.co/datasets/behbudiy/uzbek-sentiment-analysis) [*NER for Uzbek (Mendeley)*](https://data.mendeley.com/datasets/xf7pyvhb2v/1) | Evaluation and specialization: supports classification, labeling, or entity recognition. |
| **Evaluation datasets** | Benchmarks used to measure model performance in language understanding, reasoning, and instruction following | *[Tahrirchi/uzlib](https://huggingface.co/datasets/tahrirchi/uzlib), [SimReIUz](https://github.com/UlugbekSalaev/SimRelUz)*  | *Performance assessment* — evaluates comprehension, factual accuracy, fluency, across diverse Uzbek language tasks. |

## **4\. EDA of Open-Source Uzbek Datasets**

In linguistic coverage, Uzbek data is sufficient for language modeling: large corpora-like *uz-crawl* and *uz-books* ensure grammatical and lexical diversity. However, in **reasoning and structured task learning**, the resources are minimal. Models trained purely on existing data can *speak Uzbek* but cannot *reason in Uzbek*—they lack exposure to instructional patterns, logic sequences, and structured decision-making examples.

| Dataset Name | Estimated Total Volume / Rows | Description & Limitation | How it was Collected / Source |
| ----- | ----- | ----- | ----- |
| **murodbek / uz-books** | ≈ 49.93 GB text (≈ 40 000 books)  | Large literary & academic corpus in both Latin and Cyrillic Uzbek. Excellent for pre-training language fluency and style.  | Digitized public-domain Uzbek books from online libraries; cleaned and de-duplicated to plain text. ([Hugging Face](https://huggingface.co/datasets/murodbek/uz-books)) |
| **tahrirchi / uz-crawl** | ≈ 3.41 GB (raw) → ≈ 1.7 GB processed / ≈ 30 M sentences | Web-crawled Uzbek text (news, blogs, forums). Broad topical diversity but some noise and spelling variation. | Automatically crawled and language-filtered; HTML tags removed and duplicates dropped. ([Hugging Face](https://huggingface.co/datasets/tahrirchi/uz-crawl)) |
| **UAzimov / uzbek-instruct-llm** | ≈ 12.6 MB / ≈ 15 000 prompt–response pairs | General instruction dataset (Q\&A / task-following). Good for initial supervised fine-tuning; lacks domain-specific reasoning. | Crowdsourced and translated from English (Alpaca / ShareGPT) prompts; manually cleaned. ([Hugging Face](https://huggingface.co/datasets/UAzimov/uzbek-instruct-llm)) |
| **Behbudiy / alpaca-cleaned-uz** | ≈ 25.1 MB / ≈ 51 760 rows | High-quality Uzbek translation of Stanford Alpaca. Enables general instruction-following. Still general-purpose, not legal or analytical. | Machine-translated and human-post-edited by Behbudiy Lab from the English Alpaca set. ([Hugging Face](https://huggingface.co/datasets/behbudiy/alpaca-cleaned-uz)) |
| **Behbudiy / translation-instruction** | ≈ 13.8 MB / ≈ 20 000 examples | Instruction-style parallel data (English ↔ Uzbek). Useful for bilingual fine-tuning; limited to translation tasks. | Derived from existing parallel corpora reframed as “Translate this sentence into X” prompts. ([Hugging Face](https://huggingface.co/datasets/behbudiy/translation-instruction)) |
| **Behbudiy / uzbek-sentiment-analysis** | ≈ 10 MB / ≈ 10 000 labeled samples | Supervised sentiment dataset (positive / negative / neutral). Good for evaluation but not for reasoning. | Manually labeled reviews and social-media texts from Uzbek online sources. ([Hugging Face](https://huggingface.co/datasets/behbudiy/uzbek-sentiment-analysis)) |
| **UzABSA (Sanatbek / aspect-based-sentiment-analysis-uzbek)** | ≈ 3 500 reviews / ≈ 6 100 sentences ( \~ 3–5 MB ) | Aspect-based sentiment dataset for fine-grained opinion mining (restaurant domain). Useful for NLP benchmarking but small scale. | Collected from Uzbek restaurant reviews; manually annotated for aspect terms and polarities. ([ACL Anthology 2024](https://aclanthology.org/2024.sigul-1.47)) |
| **SimRelUz (Semantic Relatedness)** | ≈ 1 MB / 1 418 word pairs | Semantic similarity and relatedness ratings for Uzbek word pairs. Too small for training but valuable for embedding evaluation. | Word pairs rated (1–5 scale) by 11 native Uzbek speakers for similarity and relatedness. ([arXiv 2205.06072](https://arxiv.org/abs/2205.06072)) |

## **5\. How Each Class Contributes to Model Training**

| Model Stage | Data Type | Objective |
| ----- | ----- | ----- |
| **Pretraining** | Raw text corpora | Establish Uzbek language understanding—grammar, morphology, sentence formation. |
| **Supervised Fine-Tuning** | Instruction datasets | Teach the model to interpret user intent and deliver structured responses. |
| **Reasoning Fine-Tuning** | CoT datasets | Enable step-by-step legal, mathematical, or procedural reasoning. |
| **Evaluation & Domain Adaptation** | Annotated datasets | Benchmark and refine task-specific accuracy (e.g., sentiment, entities, classification). |

Without instruction and CoT data, a model trained solely on text will appear fluent yet behave superficially—unable to follow directives, justify decisions, or apply rules.

## **6\. Key Findings from the EDA**

1. **The Uzbek data ecosystem is text-rich but behavior-poor.**  
   Most datasets contain free text rather than supervised interactions or reasoning traces.  
2. **Instructional data is emerging but not domain-aligned.**  
   Current examples are general rather than specialized (e.g., law, education, healthcare).  
3. **Reasoning (CoT) data remains the largest gap.**  
   No open Uzbek dataset provides reasoning or explanation examples—limiting higher-order understanding.  
4. **Annotated datasets serve auxiliary purposes.**  
   They are useful for evaluation but cannot teach complex cognitive behavior.

## **7\. Implications for Future Uzbek AI Development**

The current landscape demonstrates that Uzbekistan has made progress in **linguistic data availability**, but still lacks **reasoning-oriented, instruction-rich corpora**.

To advance national AI research and productization:

* **Develop domain-specific instruction datasets** (e.g., legal Q\&A, civic information, educational tutoring).  
* **Create Chain-of-Thought datasets** in Uzbek that show intermediate reasoning steps and explanations.  
* **Establish standardized benchmarks** to measure understanding, reasoning, and factual correctness in Uzbek.  
* **Encourage open collaboration** between universities, AI labs, and government agencies to share curated, structured data.

## **8\. Translation Data for Uzbek ↔ English**

### **8.1 What Translation Data Is**

Translation datasets are called **parallel corpora** — collections of sentence pairs (or paragraphs) in two or more languages that express the same meaning.

Each record has the structure:

```json
{
  "source": "Men Toshkentda yashayman.",
  "target": "I live in Tashkent."
}
```

They are used to **train and evaluate neural machine translation (NMT) models** such as MarianMT, M2M100, or NLLB (No Language Left Behind).

In contrast to raw text corpora, which teaches language patterns, **parallel data explicitly teach cross-lingual alignment** — how a sentence in Uzbek corresponds semantically and syntactically to one in English (or another language).

### **8.2 Types of Translation Data**

There are three main categories of translation datasets relevant to Uzbek:

| Type | Description | Example Datasets | Use Cases |
| ----- | ----- | ----- | ----- |
| **Parallel Sentence Corpora** | Sentence-level aligned pairs between Uzbek and other languages (English, Russian, Kazakh). | *OPUS Tatoeba*, *Tilde MODEL Corpus*, *Parallel Uzbek–Kazakh corpus (PMC)* | Training bilingual NMT models (e.g., English ↔ Uzbek). |
| **Instructional Translation Datasets** | Parallel text expressed as instruction–response format (translation as a task). | *Behbudiy/translation-instruction* | Fine-tuning general LLMs to perform translation via instruction tuning (“Translate this sentence into English”). |
| **Multilingual General Corpora** | Large web crawls or mixed datasets that include Uzbek among many other languages (often automatically aligned). | *NLLB (Meta)*, *OPUS GlobalVoices*, *CCAligned*, *WikiMatrix* | Building multilingual or massively multilingual translation systems. |

### 

### 

### **8.3 Overview of Available Uzbek Translation Resources**

| Dataset | Source | Languages | Description / Quality |
| ----- | ----- | ----- | ----- |
| **Behbudiy / translation-instruction** | Hugging Face | Uzbek ↔ English | 20k instruction-form translation pairs. Manually curated and cleaned. Useful for LLM instruction fine-tuning. |
| **OPUS Tatoeba** | University of Helsinki | Uzbek ↔ English (and others) | A multilingual collection of example sentences and translations. Small, clean, conversational. |
| **WikiMatrix** | Facebook AI | Uzbek ↔ English | Sentence-aligned Wikipedia texts. Medium quality; alignment sometimes noisy. |
| **CCAligned / CCMatrix** | Facebook AI | Uzbek ↔ English | Large-scale automatically aligned Common Crawl data. Very noisy, requires filtering. |
| **NLLB Seed Data** | Meta (No Language Left Behind project) | Uzbek ↔ 200+ languages | Used internally by Meta to train NLLB-200 models. Public evaluation set available; raw data not fully open. |
| **Parallel Uzbek–Kazakh Corpus** | Academic dataset (PMC 2024\) | Uzbek ↔ Kazakh | Sentence-level alignment of administrative and news content; suitable for regional cross-lingual transfer. |

### **8.4 How These Datasets Are Used**

#### **a) For Traditional Machine Translation (NMT)**

Parallel Uzbek–English corpora are used to train or fine-tune models like:

* **MarianMT**, **mBART**, **NLLB**, or **M2M100**  
* Objective: learn direct translation mapping via supervised sequence-to-sequence modeling.

#### **b) For Multilingual LLMs and Instruction Fine-Tuning**

Translation pairs can also be reframed as **instruction tasks** to fine-tune multilingual LLMs.

Example format:

```json
{
  "instruction": "Translate the following Uzbek sentence into English.",
  "input": "Bu qonun 2023-yil 15-iyulda qabul qilingan.",
  "output": "This law was adopted on July 15, 2023."
}
```

This method doesn’t just teach the model bilingual equivalence — it also teaches **how to perform translation on request**, integrating translation into the model’s conversational behavior.

#### **c) For Alignment and Multilingual Embeddings**

Some Uzbek–English corpora are used to train **multilingual embedding models** (like LaBSE, LASER3).  
These models learn a *shared vector space* where semantically similar sentences in both languages have nearby representations.  
This is essential for multilingual search, cross-lingual RAG systems, or translation memory tools.

### **8.5 Quality and Coverage Challenges**

Despite progress, Uzbek translation datasets face several limitations:

1. **Data Size** — Most Uzbek↔English corpora are small (tens of thousands of pairs), compared to tens of millions for major languages.  
2. **Domain Imbalance** — Many pairs come from Wikipedia or news sources; there’s limited legal, technical, or colloquial data.  
3. **Alignment Noise** — Automatically aligned datasets (like CCAligned) contain significant mismatches due to inconsistent sentence segmentation.  
4. **Script Variation** — Uzbek appears in both Latin and Cyrillic scripts, complicating alignment and requiring preprocessing.  
5. **Cultural and Legal Context Loss** — Direct translations often omit context critical for Uzbek-specific meaning (e.g., legal or bureaucratic expressions).

### 

### 

### 

### 

### **8.6 Summary of Translation Data Usefulness**

| Model Goal | Data Type Needed | Example Dataset | Why It Helps |
| ----- | ----- | ----- | ----- |
| **Basic bilingual translation** | Parallel corpora | OPUS Tatoeba, WikiMatrix | Teaches direct mapping between Uzbek and English. |
| **LLM instruction fine-tuning** | Instruction-form translation pairs | Behbudiy/translation-instruction | Enables conversational translation tasks (“Translate this text…”). |
| **Cross-lingual retrieval or RAG** | Multilingual embeddings or alignment corpora | LaBSE, NLLB evaluation data | Allows combining Uzbek and English documents in one semantic space. |

### **8.7 Outlook**

To advance translation quality and integrate it with high-level reasoning (e.g., bilingual legal assistants), future projects should:

* Expand **professionally curated bilingual corpora** with domain diversity (law, healthcare, government).  
* Add **reasoning-style translation datasets**, showing how to translate nuanced or context-heavy Uzbek expressions step-by-step.  
* Develop **script normalization tools** to handle Cyrillic↔Latin consistency.  
* Create **translation benchmarks** specific to Central Asian languages for fair evaluation (BLEU, COMET, ChrF++).

With these improvements, Uzbek can move from being a “low-resource language” to a **strategically multilingual language** in global AI.

## **9\. Conclusion**

Uzbek-language AI development has entered a transformative stage.  
In its early years, progress centered on **text collection** — web crawls, literary archives, and digitized books that gave language models their foundational linguistic understanding.  
Today, the next frontier lies not in *more text*, but in **structured and functional data**: resources that teach models not only *how Uzbek sounds*, but *how Uzbek thought and reasoning operate*.

Through this analysis, it is clear that:

* **Raw text corpora** forms a solid linguistic base for pretraining.  
* **Instruction datasets** (like *UAzimov/uzbek-instruct-llm* and *Behbudiy/alpaca-cleaned-uz*) provide the first step toward task-following behavior.  
* **Annotated datasets** add evaluation capabilities for classification and named-entity recognition tasks.  
* **Chain-of-Thought data**—the foundation of reasoning and interpretability—remains a critical missing piece.  
* **Translation datasets** (e.g., *Behbudiy/translation-instruction*, *OPUS Tatoeba*, *WikiMatrix*) are becoming an essential bridge between Uzbek and global languages, enabling multilingual LLMs and cross-lingual retrieval systems.

The strategic direction for the Uzbek AI community is now clear:

* Develop **domain-specific instruction datasets** (especially in law, healthcare, and education).  
* Create **reasoning-rich Chain-of-Thought corpora** that capture Uzbek analytical processes.  
* Expand **translation and alignment data** to ensure interoperability between Uzbek and other major languages.  
* Build **national evaluation benchmarks** that measure reasoning quality, factual accuracy, and multilingual performance.  
* **Establish Uzbek GLUE benchmark** dataset (UzGLUE) to train LLMs in different tasks.

By shifting focus from raw data collection to structured, high-quality, and explainable datasets, Uzbekistan can evolve from a **low-resource language** environment into a **regional AI innovator**—one that promotes ethical, transparent, and locally grounded artificial intelligence aligned with the country’s cultural and linguistic identity.

### **References**

* [UAzimov / uzbek-instruct-llm — Hugging Face](https://huggingface.co/datasets/UAzimov/uzbek-instruct-llm)  
* [Behbudiy / alpaca-cleaned-uz — Hugging Face](https://huggingface.co/datasets/behbudiy/alpaca-cleaned-uz)  
* [Behbudiy / translation-instruction — Hugging Face](https://huggingface.co/datasets/behbudiy/translation-instruction)  
* [Behbudiy / uzbek-sentiment-analysis — Hugging Face](https://huggingface.co/datasets/behbudiy/uzbek-sentiment-analysis)  
* [Tahrirchi / uz-crawl — Hugging Face](https://huggingface.co/datasets/tahrirchi/uz-crawl)  
* [Tahrirchi / uz-books — Hugging Face](https://huggingface.co/datasets/tahrirchi/uz-books)  
* [Parallel Uzbek–Kazakh Corpus — PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC10904177/)  
* [SimRelUz — arXiv](https://arxiv.org/abs/2205.06072)  
* [NER for Uzbek — Mendeley Data](https://data.mendeley.com/datasets/xf7pyvhb2v/1)  
* [OPUS Tatoeba — University of Helsinki](https://opus.nlpl.eu/Tatoeba.php)  
* [WikiMatrix — Facebook AI](https://huggingface.co/datasets/facebook/wikimatrix)
