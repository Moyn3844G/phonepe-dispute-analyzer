# PhonePe Transaction Dispute Analyzer

A Python-based transaction dispute analysis tool built in **Google Colab** using **Python and Pandas**. The project helps support and operations teams identify transaction issues, analyze refunds, link complaints and support tickets, classify dispute priority, calculate customer impact, and generate business-readable reports.

## 📌 Project Summary

The **PhonePe Transaction Dispute Analyzer** is designed to help operations teams analyze large volumes of transaction-related issues.

The tool processes transaction, refund, complaint, support ticket, customer, merchant, and status-note data to identify:

- Failed transactions
- Pending and delayed refunds
- Refund SLA breaches
- Customer complaints
- Support ticket issues
- Duplicate transaction suspicions
- High-priority dispute cases
- Customer impact
- Merchant-level dispute patterns
- Payment-mode failure patterns
- City-level transaction issues

The complete solution runs inside **Google Colab** and provides reports along with a lightweight search and filter interface.

---

## 🎯 Business Problem

Support and transaction operations teams often need to manually inspect multiple files to understand customer disputes.

The required information is distributed across transaction records, refund records, complaint logs, and support ticket data.

This can result in:

- Delayed case handling
- Inconsistent prioritization
- Manual errors
- Difficulty identifying refund delays
- Difficulty detecting repeated complaints
- Poor visibility into transaction health

This project provides a centralized analytical workflow to process these datasets and generate actionable information.

---

## 🎯 Project Objectives

The project aims to:

1. Load multiple operational data files.
2. Validate required columns and data quality.
3. Clean and standardize inconsistent data.
4. Analyze transaction status.
5. Analyze refund delays and SLA breaches.
6. Link customer complaints with transactions.
7. Link support tickets with transactions.
8. Detect possible duplicate transactions.
9. Classify transactions into P0, P1, P2, P3, or No Issue.
10. Calculate customer impact scores.
11. Generate recommended actions.
12. Generate AI-ready support prompts.
13. Generate merchant-level summaries.
14. Generate payment-mode-level summaries.
15. Generate city-level summaries.
16. Provide transaction search and filtering functionality.
17. Generate business-readable reports.

---

## 🛠️ Technologies Used

- Python
- Pandas
- Google Colab
- CSV
- Excel / XLSX
- JSON
- TXT
- Colab-compatible GUI / widgets

The project does not require an external database, API, web application, or production deployment infrastructure.

---

## 📂 Input Datasets

The project works with the following data sources:

| File | Format | Purpose |
|---|---|---|
| `transactions.csv` | CSV | Main transaction records |
| `refunds.xlsx` | Excel | Refund processing information |
| `customer_complaints.json` | JSON | Customer complaint records |
| `support_tickets.csv` | CSV | Support ticket and escalation information |
| `customers.csv` | CSV | Customer metadata |
| `merchants.csv` | CSV | Merchant information |
| `status_notes.txt` | TXT | Support notes and issue tags |

---

## 🔗 Core Data Relationships

The datasets are connected primarily using transaction, customer, and merchant identifiers.

### Main relationships

```text
Transactions
     │
     ├── Refunds
     │
     ├── Customer Complaints
     │
     ├── Support Tickets
     │
     ├── Customers
     │
     └── Merchants
```

The transaction ID is used to connect transaction-related records, while customer and merchant IDs support customer-level and merchant-level analysis.

---

## 🧹 Data Validation & Cleaning

The notebook validates and cleans the input data before performing analysis.

The process includes:

- Required column validation
- Missing critical field detection
- Duplicate record detection
- Invalid date handling
- Numeric amount standardization
- Transaction status standardization
- Refund status standardization
- Ticket status standardization
- Complaint status standardization
- Payment mode standardization
- Text cleaning
- Orphan record detection
- Invalid input handling

---

## 💰 Refund Analysis

Refund records are analyzed according to business rules.

The project identifies:

- Refund Completed On Time
- Refund Delay Warning
- Refund SLA Breach
- Refund Failed
- Refund Record Missing
- Partial Refund
- Refund Amount Mismatch

### Refund SLA Rules

| Condition | Classification |
|---|---|
| Refund completed within 3 days | Refund Completed On Time |
| Refund pending for 4–7 days | Refund Delay Warning |
| Refund pending for more than 7 days | Refund SLA Breach |
| Refund failed | Refund Failed |
| No refund record for failed transaction | Refund Record Missing |
| Refund amount < transaction amount | Partial Refund |
| Refund amount > transaction amount | Refund Amount Mismatch |

---

## 🎫 Complaint & Support Ticket Analysis

Customer complaints are linked to transactions using transaction and customer identifiers.

The project identifies:

- Complaint count per transaction
- Complaint count per customer
- Repeated complaints
- Open complaints
- Unresolved complaints
- Reopened complaints

Support tickets are analyzed for:

- Open tickets
- Pending tickets
- Escalated tickets
- Resolved tickets
- Closed tickets
- Ticket delays
- SLA breaches
- Slow resolutions

---

## 🔍 Duplicate Transaction Detection

The project identifies possible duplicate debit cases using transaction attributes such as:

- Customer
- Merchant
- Transaction amount
- Transaction date/time
- Timestamp proximity
- Transaction status

Suspicious combinations are flagged for further investigation.

---

## 🚦 Dispute Priority Classification

Every transaction receives one of the following priority labels:

```text
P0
P1
P2
P3
No Issue
```

Priority hierarchy:

```text
P0 > P1 > P2 > P3 > No Issue
```

P0, P1, P2, and P3 cases include a business-readable **priority reason**.

### Example Priority Conditions

#### P0

Examples include:

- High transaction amount with refund SLA breach
- Premium customer with repeated complaints
- Duplicate debit suspicion with escalated ticket
- Refund failed with reopened complaint
- More than two complaints for the same transaction

#### P1

Examples include:

- Refund pending for more than 7 days
- Ticket SLA breach
- Angry complaint sentiment
- Multiple unresolved complaints
- Merchant with unusually high dispute count

#### P2

Examples include:

- Refund delay warning
- Ticket delay warning
- Open but non-escalated complaint
- Transaction pending for more than 24 hours

#### P3

Examples include:

- Minor complaint with completed refund
- Resolved ticket with slow resolution
- Reversed transaction with no active complaint

#### No Issue

A successful transaction with no complaint, refund issue, or ticket issue is classified as **No Issue**.

---

## 📊 Customer Impact Score

The project calculates a customer impact score on a scale of:

```text
0 – 100
```

The score considers factors such as:

- Transaction amount
- Customer segment
- Complaint count
- Escalation
- Refund delay
- Reopened complaints
- Duplicate transaction suspicion

The final impact score is capped at **100**.

---

## 🏪 Business Reports

The notebook generates business-readable analytical reports including:

### Transaction Health Summary

- Total transactions
- Successful transactions
- Failed transactions
- Pending transactions
- Disputed cases
- Refund pending cases
- SLA breaches
- Suspected duplicate transactions
- Escalated tickets
- P0/P1 counts
- Success rate
- Dispute rate

### Merchant Analysis

- Total transactions
- Failed transactions
- Dispute count
- Refund pending count
- Complaint count
- Dispute rate
- Top issue merchants

### Payment Mode Analysis

- Total transactions
- Failed transactions
- Failure rate
- Refund pending count
- Dispute count
- Average transaction amount

### City-Level Analysis

- Total transactions
- Failed transactions
- Dispute cases
- Refund SLA breaches
- Complaint count
- Average refund delay

---

## 🖥️ Colab Search & Filter GUI

The project includes a lightweight Colab-compatible interface.

### Transaction Search

Users can enter a transaction ID and view:

- Transaction details
- Refund information
- Complaint information
- Support ticket information
- Priority
- Priority reason
- Recommended action
- Customer impact
- AI-ready support prompt

The interface also handles invalid transaction IDs gracefully.

### Operations Filters

Users can filter cases by:

- Priority
- Refund status
- Payment mode
- City
- Merchant category
- Customer segment
- Ticket status
- Complaint status

---

## 🤖 AI-Ready Support Prompt

For **P0, P1, and P2** cases, the project generates a structured AI-ready support prompt.

The prompt contains relevant case information required by a support executive to prepare a customer-facing response.

The project avoids including unnecessary sensitive personal information in the generated prompt.

---

## ✅ Recommended Action

Every disputed case receives a business-readable recommended action.

Possible actions include:

- Escalate to Refund Operations
- Escalate to Bank Operations
- Escalate to Merchant Operations
- Escalate to Support Lead
- Immediate Customer Callback
- Send Customer Update
- Investigate Transaction
- Monitor Case

---

## 🐞 Debug & Fix Log

A structured debug log is maintained inside the notebook.

The log records:

- Issue ID
- Code section
- Issue type
- Issue description
- Root cause
- Fix summary
- Testing status
- Remarks

The project includes meaningful fixes covering areas such as:

- File loading
- Missing columns
- Data types
- Duplicate records
- Invalid dates
- Data joins
- Business rules
- Report generation
- User input validation

---

## 🧪 Testing & Edge Cases

The notebook is designed to handle multiple real-world data quality scenarios, including:

- Missing files
- Missing columns
- Missing values
- Duplicate records
- Invalid dates
- Invalid transaction IDs
- Orphan records
- Inconsistent statuses
- Empty or problematic inputs
- High-priority cases
- No-issue cases

The notebook is intended to run from top to bottom after dataset upload without manual code changes.

---

## 📓 Google Colab Notebook

**Google Colab Notebook:**

> Add your final Google Colab shared link here.

Example:

```text
https://colab.research.google.com/drive/YOUR_NOTEBOOK_ID
```

The notebook should be shared as:

**Anyone with the link → Viewer**

---

## 🐙 GitHub Repository

**Repository:**

https://github.com/Moyn3844G/phonepe-dispute-analyzer

---

## 📁 Project Structure

```text
phonepe-dispute-analyzer/
│
├── README.md
├── PhonePe_Transaction_Dispute_Analyzer.ipynb
└── .gitignore
```

Additional generated reports or project files may be created by the notebook as part of its execution.

---

## 🚀 How to Run

### 1. Open the Google Colab notebook

Open the project notebook in Google Colab.

### 2. Upload the required dataset files

Upload the required CSV, Excel, JSON, and TXT files.

### 3. Run the notebook

Run the notebook from top to bottom.

The notebook will:

```text
Load Data
   ↓
Validate Data
   ↓
Clean Data
   ↓
Integrate Datasets
   ↓
Analyze Transactions
   ↓
Analyze Refunds
   ↓
Link Complaints & Tickets
   ↓
Detect Duplicates
   ↓
Calculate Priority
   ↓
Calculate Impact
   ↓
Generate Actions
   ↓
Generate AI Prompts
   ↓
Generate Reports
   ↓
Launch Search / Filter GUI
```

---

## 📌 Assumptions

- Transaction IDs are treated as the primary identifier for transaction-level analysis.
- Customer and merchant IDs are used to connect related operational records.
- Refund SLA rules follow the business rules provided in the project requirements.
- Priority classification follows the defined P0 → P1 → P2 → P3 → No Issue hierarchy.
- Customer impact score is restricted to a maximum of 100.
- AI functionality is limited to generating structured support prompts from analyzed data.

---

## ⚠️ Limitations

- The project is designed to run inside Google Colab.
- It does not use a production database.
- It does not expose a production API.
- It does not deploy a web application.
- AI functionality generates structured prompts rather than directly communicating with customers.
- Generated recommendations are based on the defined business rules and analyzed dataset.

---

## 📚 Project Requirements Coverage

The project covers the major requirements defined in the Product Requirements Document, including:

- Multi-file data loading
- Required column validation
- Data cleaning
- Transaction status analysis
- Refund SLA analysis
- Complaint linking
- Support ticket mapping
- Duplicate transaction detection
- Priority classification
- Customer impact scoring
- Merchant analysis
- Payment-mode analysis
- City-level analysis
- Transaction search
- Operations filters
- Recommended actions
- AI-ready support prompts
- Business reports
- Debug/fix logging
- Colab-based execution

---

## 👨‍💻 Author

**MD Moynuddin Mollick**

GitHub:  
https://github.com/Moyn3844G

---

## 📄 License

This project is created for educational and project evaluation purposes.
