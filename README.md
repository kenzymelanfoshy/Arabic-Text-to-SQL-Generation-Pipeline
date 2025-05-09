# Arabic Text-to-SQL Generation Pipeline 🧠🔁🗃️
![Image](https://github.com/user-attachments/assets/e1ffea37-8a0a-4229-8dbf-cf989cf587e2)

This repository presents an end-to-end pipeline for translating **Arabic natural language questions** into **SQL queries**. It integrates Arabic linguistic preprocessing, semantic embedding, schema linking, and T5 model fine-tuning — specifically designed for schema-aware SQL generation from Arabic input.

## 🚀 Features

- ✅ Arabic text normalization (diacritics, Alef variants, Hamza, etc.)
- ✅ Tokenization using LLaMA-2-7b tokenizer
- ✅ Deep semantic embeddings via CAMeL-BERT
- ✅ Schema linking for contextual awareness
- ✅ Prompt construction with schema + question
- ✅ Fine-tuned T5-small model for SQL generation
- ✅ Evaluation using BLEU & ROUGE scores

---

## 🧱 System Architecture

1. **Arabic Preprocessing**
   - Diacritic removal
   - Alef/Hamza unification
   - Unicode normalization (NFC)

2. **Tokenization**
   - LLaMA-2-7b tokenizer (Hugging Face)
   - Max 512 tokens per input
   - Token IDs saved in `llama_tokenized.jsonl`

3. **Semantic Embeddings**
   - CAMeL-BERT ([CLS] token vector)
   - Saved in `arabic_embeddings.pt`

4. **Schema Linking**
   - Parses database `.sql` files
   - Extracts tables, columns, primary & foreign keys

5. **Prompt Construction**
   - Schema + user query combined
   - Stored in `arabic_sql_with_schema.jsonl`

6. **Model Training**
   - Model: `t5-small`
   - Framework: Hugging Face Transformers
   - Training: 20 epochs, BLEU/ROUGE metrics

---

## 📁 File Overview

| File | Description |
|------|-------------|
| `cleaned_AR_spider.jsonl` | Normalized Arabic questions |
| `llama_tokenized.jsonl` | LLaMA tokenized input IDs |
| `arabic_embeddings.pt` | CAMeL-BERT semantic vectors |
| `arabic_sql_schema_linked.jsonl` | Extracted DB schema |
| `arabic_sql_with_schema.jsonl` | Final training prompts |
| `invalid_lines.jsonl` | Skipped/errored samples |

---

> 📌 Final Model achieves ~0.73 ROUGE-L and steady BLEU gains — indicating effective structure-aware SQL generation.

---

## 🧪 Inference

You can directly generate SQL queries from Arabic input:

```python
# Pseudo-code for inference
input_text = "ما عدد المستخدمين المسجلين بعد 2020؟"
output_sql = model.generate_sql(input_text)
print(output_sql)
