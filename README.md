# RAG-based Author Metadata Extraction
Developed a system that extracts affiliation and contact details of the first and last authors from the enclosed PDF file containing academic paper references and outputs the data into structured Excel files. Leveraged LLMs to interpret complex text and add online search capabilities to cross-reference and validate data against academic databases and institutional websites, ensuring high accuracy.

## Dataset Used
A dataset with 27 pages worth of references in a PDF file was used. <br>
<img src="/reference_screenshot.png" height=300>

## Methodology
### Step 1 : PDF OCR Extraction
1. Extracted scanned text using Tesseract OCR.
2. Cleaned text by normalizing quotes and merging broken lines.
### Step 2: LLM-Based Reference Parsing
1. Passed reference blocks to LLaMA 3 via Ollama to extract: Reference title, First author, Last author
2. Returned structured JSON for reliability.
### Step 3: Multi-Source Online Enrichment
1. **Google Scholar**: Academic affiliation & verified profile
2. **CrossRef API**: DOI inference + affiliation by metadata
3. **DuckDuckGo**: Email + affiliation snippets from the web
4. **LLaMA Fallback**: Infer missing affiliation/email
5. **Local Cache**: Avoid repeated lookups <br>

&nbsp;&nbsp;&nbsp;&nbsp; The most important part of this step is the ranking of the different enrichment methods included, ensuring that results returned from multiple sources (Google Scholar scraping, DuckDuckGo search, and LLM RAG matching) are compared, validated, and prioritized based on accuracy, relevance, and consistency of affiliation and email information.

### Step 4: Final Export
Output 2 Excel files:
1. **OCR_output.xlsx** – raw extracted references <br>
   <img src="/excel1_screenshot.png" height=300>
2. **Verified_output.xlsx** – enriched author data <br>
   <img src="/excel2_screenshot.png" height=300>
