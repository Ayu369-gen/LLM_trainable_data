# LLM_trainable_data

This project provides a robust, notebook-driven pipeline for converting unstructured PDF documents (such as research papers and textbooks) into high-quality, LLM-trainable data in JSONL format. While optimized for Aquaculture and Marine Science, the pipeline is fully adaptable to any subject area by editing the prompt for subject matter expertise.

## Table of Contents

- [Overview](#overview)
- [Process Workflow](#process-workflow)
- [Types of Supported Documents](#types-of-supported-documents)
- [How It Works](#how-it-works)
  - [1. Environment & Dependencies](#1-environment--dependencies)
  - [2. Uploading PDF Files](#2-uploading-pdf-files)
  - [3. PDF to Markdown Conversion](#3-pdf-to-markdown-conversion)
  - [4. Chunking and Cleaning with Llama API](#4-chunking-and-cleaning-with-llama-api)
  - [5. Output: JSONL for LLM Training](#5-output-jsonl-for-llm-training)
- [Training Use Cases](#training-use-cases)
- [Adapting to Other Subjects](#adapting-to-other-subjects)
- [Notebooks](#notebooks)
- [Credits](#credits)

---

## Overview

This repository allows you to generate large-scale, clean, and structured datasets suitable for LLM pretraining, instruction tuning (fine-tuning), full fine-tuning, or continued training.  
The process leverages advanced PDF extraction, text chunking, and the Llama API for domain-specific content cleaning and formatting.

---

## Process Workflow

1. **Upload PDFs:** Research papers or textbooks in PDF format are uploaded to the notebook.
2. **Extract & Convert:** PDFs are converted to markdown using `pymupdf4llm` for accurate text extraction.
3. **Chunk Text:** Extracted text is split into coherent chunks suitable for LLM context windows.
4. **Clean & Filter:** Each chunk is sent to the Llama API with a domain-specific prompt to extract only the relevant, plain text content.
5. **Export JSONL:** Cleaned text is saved line-by-line in JSONL format for downstream LLM training.

---

## Types of Supported Documents

- **Research Papers:** Scientific articles with structured sections (Abstract, Methods, Results, etc.), metadata extraction, and filtering of citations and references.
- **Textbooks:** Less structured, larger documents—chunked primarily by paragraphs or logical breaks.

By changing the prompt, this pipeline can support ANY subject or content domain.

---

## How It Works

### 1. Environment & Dependencies

- All notebooks are designed for Google Colab (no local setup needed).
- Required Python packages are installed automatically:
  - `llama_api_client`
  - `pymupdf4llm` (and its dependencies)
- Google Colab’s file utilities are used for uploads and downloads.

### 2. Uploading PDF Files

- The user uploads one or more PDF files via the Colab file upload widget.
- Only PDF files are processed; others are ignored.

### 3. PDF to Markdown Conversion

- Each PDF is converted to markdown using `pymupdf4llm.to_markdown()`.
- This preserves text integrity and helps avoid formatting issues.

### 4. Chunking and Cleaning with Llama API

- **Chunking:**  
  - Text is split into manageable chunks (default: 4,000 characters), preserving paragraphs or, for research papers, major sections.
- **Cleaning via Llama API:**  
  - Each chunk is sent to the Llama API, with a detailed prompt specifying what to extract, what to remove (headers, citations, bullet points, etc.), and how to format.
  - The API returns only the relevant, continuous, plain text suitable for LLM pretraining/finetuning.
- **Subject Adaptability:**  
  - You can easily modify the prompt in the notebook to target any subject matter or cleaning criteria.

### 5. Output: JSONL for LLM Training

- Cleaned text is saved as one JSON object per line in a `.jsonl` file, e.g.:
  ```json
  {"text": "This is a cleaned paragraph about aquaculture systems."}
  ```
- For research papers, additional metadata (title, authors, etc.) can be included per object.
- Output files are available for download via Colab.

---

## Training Use Cases

- **Pretraining:** Use the generated JSONL files as part of a large-scale pretraining corpus.
- **Finetuning:** Use the data to instruction-tune an LLM for better performance on subject-specific tasks.
- **Full Finetuning:** Replace or supplement the original model’s data with your cleaned corpus for domain adaptation.
- **Continued Training:** Keep training an LLM on fresh, domain-specific data to maintain or improve its knowledge.

---

## Adapting to Other Subjects

To process different domains (e.g., Law, Medicine, Literature, etc.), simply modify the prompt used in the notebooks to specify:
- What content to include
- What content to exclude
- Formatting and cleaning instructions

No code changes are needed beyond updating the prompt for your target domain.

---

## Notebooks

- **Book_clean.ipynb:**  
  For textbooks and unstructured documents.

- **Research_clean.ipynb:**  
  For scientific research papers, with section-aware chunking and optional metadata extraction.

---

## Credits

- **Project Author:** [Ayu369-gen](https://github.com/Ayu369-gen)
- **PDF Extraction:** [PyMuPDF4LLM](https://pypi.org/project/pymupdf4llm/)
- **LLM Processing:** [Llama API](https://llama.com/)
- **Notebook Environment:** Google Colab

---

**For questions, suggestions, or to contribute, open an issue or pull request.**

