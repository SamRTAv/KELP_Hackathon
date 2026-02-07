# Project Kelp  
**Automated Equity Research & Presentation Generator**

## Overview

Project Kelp is an end-to-end automated pipeline designed to generate professional investment memos and PowerPoint teaser decks for private equity and venture capital analysis.

The system accepts a target company name and executes a multi-stage workflow involving deep web research, financial data extraction, strategic analysis using Large Language Models (LLMs), AI image generation, and programmatic slide creation.

The final output is a structured research report and a fully editable, branded PowerPoint (.pptx) teaser deck suitable for investor presentations.

---

## System Architecture

Project Kelp operates through five sequential modules:

### 1. Data Aggregation (Smart Search)

- Uses **Perplexity API** to identify high-quality, diverse information sources such as:
  - Official company documentation
  - News articles
  - Industry and market reports
- Uses **Firecrawl** to scrape web pages and convert them into clean markdown.
- Uses **pypdf** to extract text from PDF reports.
- Logs all citations and sources to **Google Sheets or CSV** for auditability and traceability.

---

### 2. Strategic Analysis (Gemini 2.5 / Pro)

- Ingests raw scraped data into **Google Gemini**.
- Produces a structured JSON report covering:
  - Investment Thesis
  - Strategic Assessment
  - Financial Health
  - Sector-specific metrics (SaaS, Manufacturing, D2C, etc.)
- Identifies narrative insights suitable for visualization and charting.

---

### 3. Visualization Processing (Groq)

- Parses narrative trend descriptions using **Groq** (LLaMA / GPT-OSS).
- Converts text-based insights into structured JSON objects for:
  - Line charts
  - Bar charts
  - KPI cards
- Ensures chart data is presentation-ready and machine-readable.

---

### 4. Asset Generation (Stable Diffusion)

- Automatically detects the company’s industry sector (e.g., Pharma, Logistics, SaaS).
- Uses **HuggingFace Inference Client** with **Stable Diffusion XL** to generate:
  - Photorealistic
  - Sector-appropriate
  - Investor-grade visual assets
- Images are saved locally and later embedded into slides.

---

### 5. Presentation Assembly (python-pptx)

- Uses **python-pptx** to assemble:
  - Strategic text
  - Financial metrics
  - Native PowerPoint charts
  - AI-generated images
- Outputs a fully branded, editable PowerPoint deck with:
  - Defined color palette
  - Font styles
  - Slide layouts and spacing rules

---

## Prerequisites

### Python Libraries

Ensure the following Python packages are installed:

- requests  
- pandas  
- pypdf  
- gspread  
- oauth2client  
- google-generativeai  
- groq  
- huggingface_hub  
- python-pptx  
- pydantic  

---

### API Keys & Credentials

You must obtain valid API keys for the following services and replace the placeholders in the scripts:

- **Perplexity AI** – Source discovery
- **Firecrawl** – Web scraping and markdown conversion
- **Google Gemini (GenAI)** – Core reasoning and report generation
- **Groq** – Fast JSON structuring for chart data
- **HuggingFace** – Image generation (Stable Diffusion XL)

Optional:
- **Google Service Account** – Required for Google Sheets logging  
  Place the `google_creds.json` file in the project root.

---

## Installation

Clone the repository:

```bash
git clone <repository-url>
cd project-kelp
