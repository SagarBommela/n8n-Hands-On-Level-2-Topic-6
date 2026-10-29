# Topic 6: Multi-Source Data Aggregation, PDF Invoice Extraction & Workflow Synchronization

## 1. Project Overview

This project is part of the **n8n Hands-On Level 2 Intermediate Assessment**.

The goal is to create an n8n workflow that collects customer details from different sources, combines the data, calculates financial details, and sends the results to a mock warehouse API.

The workflow uses three data sources:

- **CRM Data:** Customer details.
- **SQL Data:** Customer transaction details.
- **PDF Invoice:** Customer expense details.

All three sources are combined using Customer ID.

## 2. Objectives

- Get customer details from mock CRM data.
- Get transaction records from mock SQL data.
- Extract expense details from a PDF invoice.
- Convert PDF text into JSON.
- Combine data using Customer ID.
- Calculate revenue, expenses, and profit.
- Send customer records to a mock warehouse API.
- Generate a final workflow summary.

## 3. Tools Used

- n8n Workflow Automation
- JavaScript
- Manual Trigger
- Code Node
- Extract from File Node
- Merge Node
- HTTP Request Node
- Webhook
- Respond to Webhook
- Mock Warehouse API

## 4. Workflow Overview

The workflow contains three branches.

**Branch 1: CRM Data**

`Manual_Trigger → Code_MockCRMData`

Creates sample customer details.

**Branch 2: SQL Data**

`Manual_Trigger → Code_MockSQLData`

Creates sample transaction records.

**Branch 3: PDF Invoice**

`Manual_Trigger → Code_SimulatePDFInvoice → Extract_PDF_Invoice → Transform_ParseInvoiceText`

Creates a sample PDF, extracts the text, and converts expense details into JSON.

**Data Merging**

`Merge_CRM_With_SQL → Merge_With_PDFExpenses`

Combines all three data sources using Customer ID.

**Final Processing**

`Transform_ComputeCustomer360 → HTTP_PostToWarehouse`

Calculates customer financial details and sends the records to the mock warehouse.

## 5. Implementation Steps

### Step 1: Create CRM Data

Used a Code node to create two sample customer records.

Each record contains:

- Customer ID
- Company Name
- Customer Segment

### Step 2: Create SQL Data

Used another Code node to create sample customer transaction data.

The data contains Customer ID and total spending amount.

### Step 3: Create PDF Invoice

Used a Code node to generate a sample PDF invoice containing customer expense details.

### Step 4: Extract PDF Data

Used the Extract from File node to read the PDF content.

Used JavaScript to extract Customer ID and Expense Amount from the PDF text.

### Step 5: Merge Data

Used two Merge nodes.

- First Merge: Combines CRM and SQL data.
- Second Merge: Combines the merged records with PDF expense data.

The records are matched using Customer ID.

### Step 6: Calculate Financial Details

Used a Code node to calculate the net margin.

**Net Margin = Total Revenue - Total Expenses**

Also assigned a customer tier based on revenue.

### Step 7: Send Data to Mock Warehouse

Used an HTTP Request node to send the final customer details to a mock warehouse API.

The API simulates storing customer records in a data warehouse.

## 6. Sample Data

**CRM Data**

| Customer ID | Company Name | Segment |
|---|---|---|
| CUST-1001 | Apex Logistics LLC | Enterprise |
| CUST-1002 | Nexus BioTech | Mid-Market |

**SQL Data**

| Customer ID | Total Spend |
|---|---|
| CUST-1001 | 145200.50 |
| CUST-1002 | 18400.00 |

**PDF Expense Data**

| Customer ID | Expense |
|---|---|
| CUST-1001 | 12500.00 |

## 7. Expected Output

After merging the data, the workflow calculates the following results:

| Customer ID | Revenue | Expense | Net Margin |
|---|---|---|---|
| CUST-1001 | 145200.50 | 12500.00 | 132700.50 |

The final customer record is sent to the mock warehouse API.

**Note:** The sample PDF contains an expense for CUST-1001 only. CUST-1002 will also be included only if the Merge node is configured to keep unmatched CRM records.

## 8. Testing

The following steps are tested:

1. CRM data generation.
2. SQL data generation.
3. PDF invoice creation.
4. PDF text extraction.
5. Expense data conversion into JSON.
6. CRM and SQL data merging.
7. PDF expense merging.
8. Net margin calculation.
9. Mock warehouse API request.

GIT URL:

https://github.com/SagarBommela/n8n-Hands-On-Level-2-Topic-6
Loom Video:

https://www.loom.com/share/96bb9085eb304a9db0de9673c20aaba7



