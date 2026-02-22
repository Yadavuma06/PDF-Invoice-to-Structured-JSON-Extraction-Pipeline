📄 PDF Invoice to Structured JSON Extraction Pipeline

**📌 Project Overview**

This project implements a small Python-based pipeline that processes PDF invoices and extracts structured data into JSON format.

The input document contains a table without visible vertical or horizontal lines. The pipeline extracts:

* Invoice metadata (invoice number, dates, totals)

* Line items (description, quantity, unit price, extended price)

* Validated totals

The solution uses rule-based parsing techniques and does not rely on LLMs.

**🛠 Tools & Libraries Used**

 * Python

 * pdfplumber – for PDF text extraction

 * re (Regular Expressions) – for pattern matching and parsing

 * json – for structured output generation

**⚙️ Approach:**

1. PDF Text Extraction
The PDF is processed using pdfplumber to extract raw text from all pages.

2. Metadata Extraction
Regular expressions are used to identify invoice number, invoice date, due date, and invoice total.

3. Line Item Extraction
Since the table does not contain borders, line items are extracted using pattern-based matching:

* Description

* Quantity

* Unit price

* Extended price

4. Data Validation
The calculated total (sum of extended prices) is compared with the invoice total to ensure correctness.

5. JSON Structuring
Extracted metadata and items are combined into a structured JSON output file.

**📂 Output Format:**

The pipeline generates a JSON file with the following structure:
## 📂 Output Format

```json
{
  "metadata": {
    "invoice_number": "373294",
    "invoice_date": "02/25/2025",
    "due_date": "08/10/2025",
    "invoice_total": 24679.54
  },
  "items": [
    {
      "description": "BL050 NVY SAI NVY BLAZER SINGLE BREASTED STUDENT 34",
      "quantity": 2,
      "unit_price": 46.35,
      "extended_price": 92.7
    }
  ]
}
```
**🔎 Observations:**

* The table structure was non-uniform and did not contain visible grid lines.

* Some descriptions were split across multiple rows.

* Totals required validation to ensure extraction accuracy.

* Regex-based filtering was necessary to avoid matching unrelated numeric lines.

**Challenges Faced:**

* Handling inconsistent spacing in the table.

* Avoiding false matches from summary rows.

* Ensuring quantity and price alignment for each item.

* Cleaning noisy text extracted from the PDF.

**🚀 Possible Improvements:**

* Use layout-based PDF parsing for better column alignment.

* Integrate OCR for scanned documents.

* Implement more robust error handling.

* Extend the pipeline to support multiple invoice formats.

**✅ Conclusion:**

This project demonstrates how unstructured PDF invoices can be converted into structured JSON using rule-based parsing techniques. The final output was validated by comparing calculated totals with the invoice total, ensuring accurate extraction.
