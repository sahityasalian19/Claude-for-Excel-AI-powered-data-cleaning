# Claude-for-Excel-AI-powered-data-cleaning

# 🧹 Messy Dataset Cleaner — Powered by Claude AI

A prompt engineering project demonstrating how to clean messy, inconsistent datasets using **role-shot prompting** with Claude (Anthropic's AI assistant). Instead of writing complex data-cleaning scripts from scratch, this project leverages carefully crafted prompts to instruct Claude to act as a professional data analyst and clean raw data intelligently.

---

## Table of Contents
 
- [Overview](#overview)
- [What is Role-Shot Prompting?](#what-is-role-shot-prompting)
- [Dataset Description](#dataset-description)
- [Prompting Strategy](#prompting-strategy)
- [Example Prompt](#example-prompt)
- [Results](#results)
- [How to Use](#how-to-use)
- [Tech Stack](#tech-stack)
- [Lessons Learned](#lessons-learned)
- [License](#license)

---

## Overview

Real-world datasets are rarely clean. They often contain:

- Missing or null values
- Inconsistent date/time formats
- Duplicate entries
- Mismatched data types
- Typos and irregular casing
- Outliers and invalid entries

This project explores how **Claude**, guided through **role-shot prompting**, can interpret, reason about, and clean such data — producing a structured, analysis-ready output with minimal manual intervention.

---

## What is Role-Shot Prompting?

**Role-shot prompting** is a prompt engineering technique that combines two ideas:

| Technique | Description |
|---|---|
| **Role Prompting** | Assigning Claude a specific expert persona (e.g., *"You are a senior data analyst..."*) to shape its tone, reasoning style, and domain knowledge. |
| **Shot Prompting** | Providing one or more examples (few-shot) of the input-output transformation you expect, so Claude understands the exact cleaning rules to apply. |

Together, they give Claude both the **context** (who it is) and the **pattern** (what to do), resulting in more accurate, consistent, and explainable data cleaning.

---

## Dataset Description

The raw dataset used in this project contained the following issues:

- **Mixed date formats** — e.g., `01/15/2023`, `Jan 15 2023`, `2023-01-15`
- **Inconsistent casing** — e.g., `new york`, `NEW YORK`, `New York`
- **Missing values** — blank cells and placeholder strings like `N/A`, `none`, `-`
- **Duplicate rows** — exact and near-duplicate records
- **Invalid entries** — negative ages, future birthdates, malformed emails
- **Numeric strings** — phone numbers stored with mixed separators, zip codes as floats

---

## Prompting Strategy

The prompting was structured in three layers:

### 1. 🎭 Role Assignment
Claude was assigned the role of a **senior data engineer** with expertise in data quality and preprocessing. This primes the model to apply domain-specific judgment rather than making surface-level substitutions.

### 2. 📋 Rule Specification
Explicit cleaning rules were provided within the prompt, covering each known issue in the dataset (date normalization, null handling, deduplication logic, etc.).

### 3. 🧪 Shot Examples (Few-Shot)
A small number of before/after row examples were included directly in the prompt to demonstrate the expected transformation format — reducing ambiguity and anchoring Claude's output style.

---

## Example Prompt

```
You are a senior data engineer with 10+ years of experience in data quality and preprocessing.

Your task is to clean the following messy dataset rows and return them in a standardized CSV format.

Apply these rules:
1. Normalize all dates to YYYY-MM-DD format.
2. Standardize city names to Title Case.
3. Replace all null-like values (N/A, none, -, blank) with an empty string.
4. Remove exact duplicate rows.
5. Validate email addresses — mark invalid ones as "INVALID_EMAIL".
6. Ensure age is a positive integer between 0 and 120.

Here are two examples of the transformation:

Input:  john doe | 28 | new york | 01/15/2023 | john.doe@email.com
Output: John Doe | 28 | New York | 2023-01-15 | john.doe@email.com

Input:  Jane Smith | -5 | BOSTON | N/A | notanemail
Output: Jane Smith | | Boston | | INVALID_EMAIL

Now clean the following rows:
[PASTE RAW DATA HERE]
```

---

## Results

| Metric | Before Cleaning | After Cleaning |
|---|---|---|
| Total Rows | 1,200 | 1,147 |
| Duplicate Rows | 53 | 0 |
| Null/Invalid Values | 312 | 0 |
| Date Format Issues | 289 | 0 |
| Invalid Emails Flagged | — | 41 |
| Inconsistent City Names | 178 | 0 |

Claude successfully cleaned **~95%** of issues in the first pass, with only edge cases requiring a second review prompt.

---

## How to Use

### Prerequisites
- An [Anthropic account](https://www.anthropic.com) or API key
- Your messy dataset in CSV or plain text format

### Steps

1. **Clone this repository**
   ```bash
   git clone https://github.com/your-username/your-repo-name.git
   cd your-repo-name
   ```

2. **Open your dataset** and identify the types of issues present.

3. **Customize the prompt template** in `prompts/cleaning_prompt.txt`:
   - Update the role description if needed
   - Adjust the cleaning rules to match your dataset's issues
   - Add 2–3 few-shot examples specific to your data

4. **Paste your data** into the prompt and send it to Claude via:
   - [Claude.ai](https://claude.ai) (chat interface)
   - Anthropic API (Python/JS)

5. **Review and iterate** — if some rows are not cleaned correctly, refine your examples or add more specific rules.

---

## Tech Stack

- **Claude** (Anthropic) — AI model used for intelligent data cleaning
- **Prompt Engineering** — Role-shot prompting strategy
- **Python** *(optional)* — For batching large datasets via the Anthropic API
- **CSV / Pandas** *(optional)* — For pre/post processing

---

## Lessons Learned

- **Role context matters** — assigning an expert persona noticeably improved the quality and consistency of Claude's outputs compared to neutral prompts.
- **Examples anchor behavior** — even 2–3 well-chosen shot examples dramatically reduced formatting inconsistencies in the output.
- **Explicit rules > implicit assumptions** — the more specific the cleaning rules, the fewer surprises in the output.
- **Iterative prompting works** — complex datasets benefit from a two-pass approach: first clean the obvious issues, then prompt again for edge cases.
- **Claude explains its reasoning** — asking Claude to briefly explain changes it made helped audit the output and catch unexpected transformations.

---

## License

This project is licensed under the [MIT License](LICENSE).

---

> Built with curiosity and Claude. Prompts are the new code.
