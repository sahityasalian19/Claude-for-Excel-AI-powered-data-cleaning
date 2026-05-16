# Claude-for-Excel-AI-powered-data-cleaning

# 🧹 Messy Dataset Cleaner — Powered by Claude AI

A data analytics project showcasing how AI-assisted prompt engineering can streamline the data cleaning process — using Claude as a smart, instruction-driven data cleaning partner.

---

## Table of Contents

- [Overview](#overview)
- [What is Role-Based Prompting?](#what-is-role-based-prompting)
- [Dataset Description](#dataset-description)
- [Role-Based Prompting Strategy](#role-based-prompting-strategy)
- [Example Prompt](#example-prompt)
- [Ways to Use Claude for Data Cleaning](#ways-to-use-claude-for-data-cleaning)
- [Results](#results)
- [How to Use](#how-to-use)
- [Tech Stack](#tech-stack)
- [Lessons Learned](#lessons-learned)

---

## Overview

Real-world datasets are rarely clean. They often contain:

- Missing or null values
- Inconsistent date/time formats
- Duplicate entries
- Mismatched data types
- Typos and irregular casing
- Outliers and invalid entries

This project explores how **Claude**, guided through **role-based prompting**, can interpret, reason about, and clean such data — producing a structured, analysis-ready output with minimal manual intervention.

---

## What is Role-Based Prompting?

**Role-based prompting** is a prompt engineering technique where you assign Claude a specific expert persona before giving it a task. By telling Claude *who it is*, you shape how it thinks, reasons, and responds — unlocking domain-specific knowledge and judgment that leads to more accurate and context-aware outputs.

Instead of asking Claude to "clean this data," you instruct it to respond *as* a senior data analyst who understands data quality standards, common inconsistencies, and best practices — resulting in far more intelligent and reliable cleaning decisions.

| Without Role Prompting | With Role Prompting |
|---|---|
| Generic, surface-level fixes | Domain-aware, judgement-driven cleaning |
| May miss context-specific issues | Applies industry-standard data quality rules |
| Inconsistent output format | Structured, analysis-ready output |

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

## Role-Based Prompting Strategy

The role-based prompting strategy was structured in three steps:

### 1. Role Assignment
Claude was assigned the role of a **senior data analyst** — responsible for profiling raw data, identifying quality issues, applying domain-specific cleaning rules, and ensuring the dataset is accurate, consistent, and ready for analysis.

### 2. Context & Goal Setting
After defining the role, a clear objective was given — what the data represents, what the expected output format is, and what standards the cleaned data should meet. This gives Claude the *why* behind the task, not just the *what*.

### 3. Instruction Specification
Explicit, rule-based instructions were provided within the prompt, tailored to the specific issues present in the dataset — such as date normalization, null handling, deduplication, and format standardization. The more precise the instructions, the more consistent and reliable Claude's output.

---

## Example Prompt

```
You are a senior data analyst specialized in data quality and preprocessing.
I'm uploading an Excel file that will be used for further analysis like dashboard creation and report creation.

Your job is to:

1. AUDIT: First, identify all data quality issues (nulls, duplicates, wrong formats, outliers, 
   inconsistent values). List them clearly.

2. PLAN: Explain what you'll do to fix each issue and why.

3. CLEAN: Apply the fixes and show me the cleaned data in a New Excel sheet.

Rules:
- Column names must be snake_case
- Dates must be in DD-MM-YYYY format
- Do NOT drop rows with errors — Move them to a separate error sheet.
  Example: If travel date is earlier than booking date, invalid Age values

- You can create flag columns for the below:
  Booking_Date_Flag | Age_flag | Travel_date_flag | Final_Price_INR_Flag |
  Price_Validation_Flag | email_flag | Customer_Rating_flag | Booking_ID_flag | Customer_Name_flag
```

---

## Ways to Use Claude for Data Cleaning

There are two approaches to using Claude for cleaning your messy dataset:

### Method 1: Upload a File via Claude.ai

The simplest way — no setup required.

1. Go to [claude.ai](https://claude.ai) and start a new conversation.
2. Click the **paperclip / attachment icon** and upload your messy dataset file (CSV, Excel, or plain text).
3. Type your role-based prompt directly in the chat, for example:

   > *"You are a senior data analyst specialized in data quality and preprocessing. Audit the uploaded dataset for any data quality issues such as nulls, duplicates, wrong formats, and inconsistent values. Then clean the data by applying fixes and return the output in a new Excel sheet with column names in snake_case and dates in DD-MM-YYYY format. Do not drop any error rows — move them to a separate error sheet instead."*

4. Claude will read the file, apply your cleaning instructions, and return the cleaned data — which you can copy or ask Claude to format as a downloadable CSV.

**Best for:** Quick one-off cleanings, small-to-medium datasets, and exploring prompts interactively.

---

### Method 2: Claude Add-in for Microsoft Excel

Clean your data without ever leaving Excel using the **Claude for Excel** add-in.

1. Install the Claude add-in from the [Microsoft AppSource](https://appsource.microsoft.com) or directly inside Excel via **Insert → Add-ins → Get Add-ins** and search for *Claude*.
2. Open your messy dataset in Excel and activate the Claude panel from the ribbon.
3. Select the cells or columns you want to clean.
4. Type your role-shot prompt in the Claude panel and hit **Run**.
5. Claude processes the selected data and writes the cleaned output directly into your spreadsheet.

**Best for:** Datasets already in Excel, repeatable cleaning workflows, and non-technical users who prefer working within a spreadsheet environment.

---

| | Method 1: Claude.ai (File Upload) | Method 2: Claude for Excel |
|---|---|---|
| Setup required | None | Install Excel add-in |
| Best for | Quick, one-off cleaning | Repeated, in-spreadsheet workflows |
| File types | CSV, Excel, TXT | Excel (.xlsx, .xls) |
| Output | Chat response / copy-paste | Written directly into Excel cells |
| Technical skill needed | Minimal | Minimal |

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


> Built with curiosity and Claude. Prompts are the new code.


