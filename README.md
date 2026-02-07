Project Kelp: Automated Equity Research & Presentation Generator
Overview
Project Kelp is an end-to-end automated pipeline designed to generate professional investment memos and PowerPoint teaser decks for private equity and venture capital analysis. The system accepts a target company name and executes a multi-stage workflow involving deep web research, financial data extraction, strategic analysis using Large Language Models (LLMs), AI image generation, and programmatic slide creation.

System Architecture
The project operates through five distinct modules, processed sequentially:

Data Aggregation (Smart Search):

Utilizes Perplexity API to identify high-quality, diverse sources (official documentation, news, industry reports).

Uses Firecrawl to scrape web content and pypdf to extract text from PDF reports.

Logs citations to Google Sheets or CSV for audit trails.

Strategic Analysis (Gemini 2.5/Pro):

Ingests raw scraped data into Google's Gemini model.

Produces a structured JSON report covering Investment Thesis, Strategic Assessment, Financial Health, and Sector-Specific Metrics (SaaS, Manufacturing, D2C, etc.).

Identifies narrative trends suitable for visualization.

Visualization Processing (Groq):

Parses narrative trend descriptions using Groq (LLaMA/GPT-oss).

Converts textual descriptions into structured JSON objects for specific chart types (Line Charts, Bar Charts, KPI Cards).

Asset Generation (Stable Diffusion):

Detects the industry sector (e.g., Pharma, Logistics, SaaS).

Uses HuggingFace Inference Client (Stable Diffusion XL) to generate photorealistic, sector-appropriate stock imagery for the presentation.

Presentation Assembly (python-pptx):

Compiles all analyzed text, calculated financial metrics, dynamic charts, and generated images.

Renders a branded, edit-ready PowerPoint (.pptx) file with a dedicated design system (colors, fonts, layouts).

Prerequisites
To run this project, the following dependencies and API keys are required.

Python Libraries
Ensure the following Python packages are installed:

requests

pandas

pypdf

gspread

oauth2client

google-generativeai

groq

huggingface_hub

python-pptx

pydantic

API Keys & Credentials
You must obtain valid API keys for the following services and replace the placeholders in the scripts:

Perplexity AI: For source discovery.

Firecrawl: For web scraping and markdown conversion.

Google Gemini (GenAI): For core reasoning and report generation.

Groq: For rapid JSON formatting of chart data.

HuggingFace: For image generation (Stable Diffusion).

Google Service Account (Optional): A google_creds.json file is required if using the Google Sheets logging feature.

Installation
Clone the repository to your local machine.

Install the dependencies using pip:

Bash
pip install requests pandas pypdf gspread oauth2client google-generativeai groq huggingface_hub python-pptx pydantic
Place your google_creds.json file in the root directory (if using Google Sheets).

Configuration
Open the main script files and update the configuration sections:

Target Company: Update the company variable (e.g., company = "KSolves").

API Keys: Replace placeholders (e.g., "YOUR API KEY") with your actual credentials.

Model Selection: The scripts are configured to use specific models (e.g., gemini-2.5-flash, stabilityai/stable-diffusion-xl-base-1.0). Modify these variables if you wish to use different model versions.

Usage
The pipeline is designed to be run sequentially.

1. Data Collection
Executes search and scraping.

Input: Company Name.

Output: input_data{company}.json (Raw text) and Ksolves-OnePager.md.

2. Analysis & Structuring
Passes raw data to Gemini to create the core report.

Input: input_data{company}.json or Markdown file.

Output: layer2_withplot{company}.json (Structured analysis including plot descriptions).

3. Chart Data Extraction
Refines plot descriptions into chart-ready data.

Input: layer2_withplot{company}.json.

Output: Updates layer2_withplot{company}.json with a zplotting key containing chart datasets.

4. Image Generation
Generates visual assets.

Input: Sector definition from the JSON report.

Output: Saved .jpg files in the sector_visuals/ directory.

5. Presentation Generation
Builds the final slide deck.

Input: Fully processed JSON and generated images.

Output: Kelp_Auto_Teaser{company}.pptx.

Output Artifacts
CSV/Google Sheet: A log of all URLs and snippets used for the research.

JSON Report: A deep strategic analysis object containing all financial data and qualitative reasoning.

Sector Images: A folder of AI-generated images specific to the company's industry.

PowerPoint Deck: A 3-slide teaser deck including:

Slide 1: Business Profile & Strategic Overview.

Slide 2: Financial Performance (with native Excel-backed charts and KPI cards).

Slide 3: Investment Highlights (Grid layout).
